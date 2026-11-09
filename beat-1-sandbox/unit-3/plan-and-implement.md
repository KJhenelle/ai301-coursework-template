# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

KJhenelle

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/67#issuecomment-6731461488

> Plan for #67, based on my repro above (main @ 99673c7: user 2's `POST /reviews` on user 1's profile returned 200 and created a pending review).
>
> Cause (confirmed by reading the code and by my repro; the fix itself is not built or verified yet): `create_review()` in `core/services/review_service.py` accepts `user_id` but never uses it, so the review is built straight from the request's `profile_id`. The route already passes `current_user.id`, so the missing check is in the service. `get_review()` and `list_reviews()` already scope through `Profile.user_id`.
>
> Change (one bounded edit): in `create_review()`, look up the profile with `Profile.id == profile_id` and `Profile.user_id == user_id`; if nothing matches, raise `HTTPException(404, "Profile not found")` before any `Review` is created. One 404 for both "missing" and "not yours" so profile IDs are not leaked. No route change needed, since the route already re-raises `HTTPException`.
>
> Not touching: `get_review`/`list_reviews`, `process_review`/ingestion, the frontend.
>
> Test plan: `pytest tests/unit/test_review_service.py -k rejects_profile_not_owned -q` fails on main with `DID NOT RAISE HTTPException` and should pass after. Live: re-run my repro request as user 2 (expected 404 instead of 200, no new review row), and user 1 on their own profile still gets 200.
>
> Unknowns: `core/` imports no fastapi today, so raising `HTTPException` from the service is a layering choice. I can return `None` and raise the 404 in the route instead if you prefer. I have not tested whether `process_review` ran against the other user's profile; the fix should prevent it, but I have not observed it. The existing create-success unit test may need its `db.execute` mock adjusted.
>
> I'll make a PR from `fix/67-create-review-ownership-check` for your review.

---

## Your branch

**Branch**

fix/67-create-review-ownership-check (https://github.com/KJhenelle/pathreview-ai301-fa26-howard/tree/fix/67-create-review-ownership-check, commit 68efb02)

**Evidence**

Re-run of my unit 2 repro (issue #67) against the built change. Same three requests before and after, through the real code path (uvicorn + Postgres), using `repro.sh`; run on port 8001 because an older uvicorn was bound to 8000. Unit test: before, `test_create_review_rejects_profile_not_owned_by_user` FAILED (1 failed, 6 passed, 13 xfailed); after, 7 passed, 13 xfailed; full unit suite 376 passed, 53 xfailed.

Run on port 8001 (an older uvicorn was bound to 8000 and was avoided).

## Before
```
BEFORE: main @ 99673c7
user1 profile: 5ce7a193-835c-4e77-b98f-11b17e906d95
--- user2 -> user1's profile (the bug)
{"id":"080b0a25-3a29-44b4-b01d-a8df7d66b6a0","profile_id":"5ce7a193-835c-4e77-b98f-11b17e906d95","status":"pending","sections":null,"overall_score":null,"error_message":null,"created_at":"2026-11-09T08:38:36.924143Z","updated_at":"2026-11-09T08:38:36.924144Z"}
HTTP 200
--- control: user1 -> own profile
{"id":"829731ec-35ed-42ec-af5c-606a9e0b6221","profile_id":"5ce7a193-835c-4e77-b98f-11b17e906d95","status":"pending","sections":null,"overall_score":null,"error_message":null,"created_at":"2026-11-09T08:38:36.941537Z","updated_at":"2026-11-09T08:38:36.941537Z"}
HTTP 200
--- nonexistent profile_id, as user2
{"detail":"Failed to create review"}
HTTP 500
```

## After
```
AFTER: fix/67-create-review-ownership-check @ 68efb02
user1 profile: 48b0226e-e96a-4028-b3a7-61656f6ae0cc
--- user2 -> user1's profile (the bug)
{"detail":"Profile not found"}
HTTP 404
--- control: user1 -> own profile
{"id":"3ff0c97e-1be0-40ec-873c-1a44eb96cf3b","profile_id":"48b0226e-e96a-4028-b3a7-61656f6ae0cc","status":"pending","sections":null,"overall_score":null,"error_message":null,"created_at":"2026-11-09T08:38:51.487035Z","updated_at":"2026-11-09T08:38:51.487037Z"}
HTTP 200
--- nonexistent profile_id, as user2
{"detail":"Profile not found"}
HTTP 404
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Full runs, in order: 15/20, 17/20, 17/20, 18/20. The last (18/20, category floor held) is the agreement line in the committed `eval-run.txt`. Partial `--only` runs in between: 6/7 after the first rubric revision, 1/3, 4/5.

**Package analysis**

pkg-20 (thread-convention, ghostty). Gold: reject. On the first full run my rubric graded it accept, because every check passed: the plan follows mitchellh's recompute-only-on-capacity-change direction and the comment repeats it. What it missed is that the repo-facts block states a strict AI policy ("All AI usage in any form must be disclosed") and the comment contains no disclosure. My `comment-faithful` check only mentioned claim etiquette and discuss-first rules, so a missing disclosure was invisible to it. I added the disclosure requirement, and pkg-20 now grades reject on `comment-faithful`.

**Check rationale**

```
| comment-faithful | The draft plan comment read against the plan and against the thread highlights and repo conventions (contributing rules, maintainer requests) in the issue context and repo-facts. | Pass if the comment states the same cause, scope, and approach as the plan without adding claims the plan lacks or softening unknowns into certainty, and does not violate anything a maintainer asked for in the thread or the repo's stated conventions (for example claim etiquette or discuss-first rules). If the repo-facts state an AI-use disclosure policy, the comment must contain an explicit disclosure of AI assistance in the form that policy asks for (name the tool or extent only if the policy requires it); a comment with no disclosure at all fails. Fail if the comment contradicts or overstates the plan, or ignores a stated maintainer request or convention. Unclear only if no thread or convention information is in the package and the comment otherwise matches the plan. | required |
```

The last sentence ("If the repo-facts state an AI-use disclosure policy ...") is my revision. I added it after pkg-20 graded accept against a reject gold label, and then softened it to "in the form that policy asks for (name the tool or extent only if the policy requires it)" because pkg-03's policy does not require naming a tool and my first wording rejected pkg-03, whose gold label is accept.

**Trade-offs**

The `executable-by-a-stranger` check gives something up. It originally required every named file to appear in the repo-facts block, but repo-facts never list source files, so pkg-03, pkg-09 and pkg-13 graded unclear and rejected against accept gold labels. I loosened it so a specific path or function the package merely does not list passes, while vague steps or locations "to be pinned after tracing" still fail. The cost is that a plausible but invented path now passes this check. I re-ran with `--only` including canaries pkg-04 (thread-convention) and pkg-06 (scope-creep), and both stayed correct, and the full runs kept all five categories matched. I accept that it misses pkg-14: gold is accept, but its plan leaves the functions unnamed and states a mechanism as fact, so my rubric rejects it on `diagnosis-grounded` and `executable-by-a-stranger`. pkg-02 and pkg-09 flip between runs, so 18/20 has little margin.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
