# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**Kjhenelle1**

[Your GitHub username, exactly as it appears on your profile — no `@`, no profile URL. Your
comments upstream are identified by this name.]

---

## Posted upstream

**[Claim comment](https://github.com/codepath/pathreview-ai301-fa26-howard/issues/67#issuecomment-6349267657)**

Hi I'd like to claim #67: create_review() does not verify that profile_id belongs to the authenticated user.

From reading core/services/review_service.py, create_review() accepts user_id but never uses it, while get_review() and list_reviews() filter through Profile.user_id. This is from reading the code only. I have not run it, so it is unconfirmed.

Next steps:

Set up the sandbox from the repo's docs and record the environment (OS, Python version, dependencies).
Send POST /reviews as user A with a profile_id owned by user B, and capture the response and the resulting database state.
Post the full reproduction report, with exact commands and output, or a documented cannot-reproduce, by Sunday, Oct 25.
I will propose a fix only after the report is posted.

**[Reproduction comment](https://github.com/codepath/pathreview-ai301-fa26-howard/issues/67#issuecomment-6352250586)**

Reproduced on main @ 99673c7: POST /reviews returns 200 and creates a review on a profile owned by a different user.

Environment

macOS 26.6.2, Python 3.12.2
fastapi 0.159.1, pydantic 2.14.1, SQLAlchemy 2.1.6, uvicorn 0.54.0
Backend run with uvicorn api.main:app --port 8000, seeded via make setup
Requests sent through Swagger UI (/docs) and curl

Steps:
Start the backend on main @ 99673c7.
Log in as user1@example.com (POST /auth/login) and user2@example.com. Keep both tokens.
As user 1, POST /profiles. The response has id: 45c08a39-7464-412a-8556-203d7961bf11 and user_id: b3c1a9c7-23db-4819-8628-2c90b6e8c5d5 (user 1).
As user 2 (token sub = 98c9712f-..., a different user), send:

```
POST /reviews
{"profile_id": "45c08a39-7464-412a-8556-203d7961bf11"}
```
Observed

```json
HTTP 200
{"id": "e3498634-d804-48cb-8a0a-1f5e38292afa",
 "profile_id": "45c08a39-7464-412a-8556-203d7961bf11",
 "status": "pending", ...}
```
I repeated the request through Swagger and got the same result. That response was review 5d4371ef-7cc7-4fa5-a1a4-7040d22405ba, again on user 1's profile, created with user 2's token.

Expected: a 404, matching get_review, which returns "not found" for a review that isn't the caller's.

Cause (read from code, not yet confirmed by a fix): create_review() in core/services/review_service.py takes user_id but never uses it. It builds Review(profile_id=...) straight from the request. get_review() and list_reviews() both filter on Profile.user_id.

Failing test: test_create_review_rejects_profile_not_owned_by_user in tests/unit/test_review_service.py fails with DID NOT RAISE HTTPException.

```
pytest tests/unit/test_review_service.py -k rejects_profile_not_owned -q
```
Not tested:

Whether user 1 can see the review user 2 created. I did not call GET /reviews as user 1.
Whether process_review runs against the other user's profile and ingests its data. I only observed the pending response.
Related, separate finding: a profile_id that doesn't exist returns 500 "Failed to create review", not a 404. I hit this by sending a user ID in the profile_id field. The same ownership check would fix it.

Next: I will open a PR that makes create_review look up the profile by id and user_id, raise a 404 on no match, and include the test above.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**
categories: clear-accept 7/8  disclosure 0/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 3/4
agreement: 17/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in disclosure)

categories: clear-accept 5/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4
agreement: 17/20 scored items  (bar: 18/20: below the bar)

categories: clear-accept 8/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4
agreement: 20/20 scored items  (bar: 18/20: PASS)

categories: clear-accept 7/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 2/3  wrong-target 4/4
agreement: 18/20 scored items  (bar: 18/20: PASS)

categories: clear-accept 8/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 2/3  wrong-target 3/4
agreement: 18/20 scored items  (bar: 18/20: PASS)

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

**Package analysis**

pkg-6 graded accept env-recorded fails, but it's preferred. The report records no OS, driver or minikube version. A preferred check never changes the verdict, so that failure was ignored.
steps-followable probably passed. The issue says minikube start --driver vmware on Windows. The report says minikube start with no driver. the pass condition forgives "standard… default CLI invocations," which covers a bare minikube start. But omitting the driver on a Windows-specific bug isn't a default. behavior-matches passed. The log shows the repeating route ADD … retrying loop, which looks like the issue's symptom.

**Check rationale**

| `behavior-matches` | Repro report output/artifacts compared against the target issue description | The observed outcome demonstrates the core defect, error path, or bug symptom described in the issue (or cleanly confirms a cannot-reproduce result), allowing for benign environment or formatting variances. | required | 
It reads this way because the check has to judge the behavior the report shows, not the report's format. The pass condition asks whether the observed outcome demonstrates the issue's own defect, and the "benign environment or formatting variances" clause stops me failing a good report over a different OS or output layout. I rejected a stricter wording that required the report's environment to match the issue's exactly, because that would fail honest reproductions on a slightly different setup.


**Trade-offs**

The final run (the one in `eval-run.txt`) disagrees on pkg-06 (gold reject, graded accept)
and pkg-16 (gold reject, graded accept). Between the previous run and this one I did not
change the rubric, yet pkg-12 flipped from reject (failed `steps-followable`) to accept,
matching its gold label, and pkg-16 flipped from reject to accept, against its gold label.
So `steps-followable` and `behavior-matches` are borderline checks: on arguable packages
the same wording can grade either way from run to run. I accept that, because both
errors this run are accepts of packages that should be held (a wrong-target miss, 3/4),
and I did not loosen anything to chase the score. pkg-06 is the case I expect the rubric
to keep missing: a bare `minikube start` where the issue names `--driver vmware` passes
the "default CLI invocations" allowance.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
