# Plan: #67 Review creation does not verify profile ownership

Issue: https://github.com/codepath/pathreview-ai301-fa26-howard/issues/67
Repro baseline: main @ 99673c7, my posted repro comment on the issue.

## Repro evidence (quoted from my posted repro comment)

- As user 2, `POST /reviews {"profile_id": "45c08a39-7464-412a-8556-203d7961bf11"}` (a profile owned by user 1, `user_id: b3c1a9c7-...`) returned `HTTP 200` with `"status": "pending"`. Repeated via Swagger: a second review (`5d4371ef-...`) on user 1's profile.
- Expected: 404, as `get_review` returns not-found for another user's review.
- Failing test: `test_create_review_rejects_profile_not_owned_by_user` in `tests/unit/test_review_service.py` fails with `DID NOT RAISE HTTPException`.
- Environment: macOS 26.6.2, Python 3.12.2, fastapi 0.159.1, SQLAlchemy 2.1.6.
- Related observation: a `profile_id` that does not exist returns 500 "Failed to create review".
- Not tested: whether user 1 can see the review user 2 created; whether `process_review` ingests the other user's profile data.

## Diagnosis

`create_review()` in `core/services/review_service.py` accepts `user_id` but never uses it. It builds `Review(profile_id=profile_id, ...)` straight from the request and commits. The route `create_review_endpoint` in `api/routes/reviews.py` does pass `current_user.id`, so the missing check is in the service, not the route. This explains the 200 on a profile owned by someone else, and the failing unit test (nothing raises). `get_review()` and `list_reviews()` already scope through `Profile.user_id`, which is why only creation is affected.

The cause is confirmed by reading the code and by the repro. After building the fix (commit 68efb02), the live repro returns 404 instead of 200 and the unit test passes (see evidence.md).

## Scope

In scope: one change, an ownership check inside `create_review()`: look up the profile by `Profile.id == profile_id` and `Profile.user_id == user_id`; if no row matches, raise `HTTPException(404)` before any `Review` is created.

Not in scope: changes to `get_review`/`list_reviews`; `process_review` or the ingestion pipeline; any route change in `api/routes/reviews.py`; a distinct error for "profile exists but belongs to someone else" (a single 404 avoids leaking which profile IDs exist); the frontend; unrelated files (for example the uncommitted `frontend/package-lock.json` change in my clone, which stays out of the branch).

## Files / areas

- `core/services/review_service.py`: `create_review()` (only function edited; `select`, `and_`, `Profile` are already imported there).
- `tests/unit/test_review_service.py`: add `test_create_review_rejects_profile_not_owned_by_user` (404, no `db.add`), and adjust the existing create-success test only if it breaks (see risks).

## Approach

1. In `create_review()`, before building `Review`, run `select(Profile).where(and_(Profile.id == profile_id, Profile.user_id == user_id))` and take `scalars().first()`.
2. If the result is `None`, raise `HTTPException(status_code=404, detail="Profile not found")`. The route already re-raises `HTTPException`, so no route edit is needed.
3. Otherwise continue unchanged (create the pending `Review`, commit, refresh, return).
4. Add the failing-first unit test, confirm it fails on main and passes after the change.
5. Run `make lint`, `make format`, `make typecheck`, `make test-unit`, and the integration and frontend checks CONTRIBUTING lists (all five CI jobs must be green).

## Test plan

Re-run my unit 6 repro steps against the built change:
- Unit: `pytest tests/unit/test_review_service.py -k rejects_profile_not_owned -q`. Before: fails with `DID NOT RAISE HTTPException`. Expected after: passes (404 raised, `db.add` not called).
- Live: same request as the repro, user 2's token with user 1's profile id `POST /reviews {"profile_id": "<user 1 profile id>"}`. Before: HTTP 200, status pending, new review row. Expected after: HTTP 404 `{"detail": "Profile not found"}` and no new review row.
- Control: user 1 posting their own profile id still returns 200 with status pending.
- Side effect to check: nonexistent `profile_id` returns 404 instead of 500 (same check covers it; I will only state it if I observe it).

## Risks and unknowns

- Unknown: `core/` imports no fastapi anywhere today, so raising `HTTPException` from the service is a layering choice. The alternative is returning `None` and raising 404 in the route. I am choosing the service-raise because the failing test from my repro expects an `HTTPException` from `create_review`; I will switch if the maintainer prefers.
- Unknown: the existing create-success unit test mocks `db.execute` loosely, so the new lookup may need that mock adjusted. I will change only that test's setup if it breaks.
- Unknown (not tested in repro): whether `process_review` ran against the other user's profile. The fix prevents creation, so it should not run, but I have not observed it either way.
- Risk: a legitimate caller passing a valid own-profile id must keep working; covered by the control above.

## Deviations

- Build (commit 68efb02): adding the lookup broke six existing `create_review` unit tests, because the shared `mock_db_session.execute` returns a coroutine. I added a `profile_found` fixture in `tests/unit/test_review_service.py` and used it in only those six tests, instead of editing the shared fixture (which could flip the strict-xfail tests). Production change is unchanged from the plan; the posted comment's intent is unchanged.
- Result: `pytest tests/unit/test_review_service.py` gives 7 passed, 13 xfailed (before the fix: the new test failed with DID NOT RAISE); the full unit suite gives 376 passed, 53 xfailed. The live repro goes from 200 to 404 (see plan-and-implement.md Evidence). No integration tests exist in the repo yet; the frontend check was not run locally.
