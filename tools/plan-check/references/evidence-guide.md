# Evidence guide: where evidence lives in a plan package

Eval mode: use ONLY the bundle text. Sections are `## Repo facts`, `## Issue`
(body), `## Thread highlights`, `## Repro evidence`, `## Candidate plan`
(`### Diagnosis`, `### Scope`, `### Files`, `### Approach`, `### Test plan`,
sometimes risks/unknowns) and `## Candidate plan comment`.
Live mode: the plan is the student's plan.md and the comment is the draft
comment file; the issue is read with `gh issue view <url> --comments`; repro
evidence is the student's own posted repro comment on that issue (on the house
issue: the repro-pack text quoted inside the drafts). Anything not in the
drafts or the thread is not evidence.

## Diagnosis and grounding

- Where it lives: the plan's `Diagnosis` section (the stated cause) and its
  risks/unknowns. The behavior the cause must explain is in the Repro evidence
  block: environment/versions, numbered steps, control runs, exit codes, and
  the "Actual" paragraph.
- What good looks like: every observation in the repro (including controls,
  such as "works without the flag" or "works on version X") is explained by
  the stated cause, and the fix targets the place where the repro says the
  failure originates (e.g. the traceback or `--debug` line). Bad: the cause
  dismisses a repro observation as "a red herring", points at code the repro
  shows is never reached, or only suppresses the symptom. Anything the repro
  does not settle must be worded as an assumption or unknown.

## Scope

- Where it lives: the plan's `Scope` section (in / not-in), `Files`, and
  `Approach`, compared against the Issue body's single stated problem.
- What good looks like: one problem, one change; every listed file and
  approach step is needed for that problem, and extras (refactors, renames,
  migrations, docs rewrites, adjacent bugs) appear only under not-in. Bad: the
  Files/Approach contain a second change the issue never asked for, or the
  scope has no not-in boundary to hold the diff to. Judge Files/Approach, not
  just the Scope wording: a clean Scope paragraph over a sprawling Approach
  fails.

## Executability

- Where it lives: `Files` and `Approach`, checked against the Repo facts block
  and the Issue/Repro text (file paths, function names, commands shown there).
- What good looks like: a stranger can say "open file X, change Y to Z" for
  step one, and every named file/function appears in Repo facts, the issue, or
  the repro output. Bad: "fix the handler", steps that need author-only
  knowledge, or named files/functions that nothing in the package supports.
  If Repo facts are too thin to confirm a named location, that is unclear,
  not pass.

## Test plan

- Where it lives: the plan's `Test plan`, read against the Repro evidence's
  steps, commands, and observed output.
- What good looks like: it re-runs the repro's own inputs (same command,
  same environment/version that failed) and states an expected-after that is
  observable (specific output, exit code, test name) and different from the
  observed-before. Bad: "verify it works", a test on a path the bug never
  touched, or a check that passes both before and after the change.

## Honesty

- Where it lives: risks/unknowns and any deviation notes in the plan; the
  confidence of wording in Diagnosis and in the plan comment.
- How to tell: honest plans mark unverified claims ("I believe", "unknown
  until I read X", "assumption") and name what could change the approach.
  False confidence states a guess as fact ("the root cause is...") with no
  repro observation behind it, or the comment drops an unknown the plan
  carries. Mid-build deviations belong in plan.md and then the thread, not
  only in the diff.

## Comms

- Where it lives: the Candidate plan comment, read against Thread highlights
  (maintainer requests, who owns/claims, direction suggested) and the Repo
  facts lines on bug-report template, CONTRIBUTING rules, and AI-use policy.
- What good looks like: the comment states the same cause, scope, and approach
  as the plan, keeps its unknowns, and honors anything the thread or repo
  asks (e.g. discuss before PR, wait for maintainer go-ahead, follow a stated
  approach, disclose AI use if the policy requires it). Bad: boilerplate that
  could be pasted on any issue, claims the plan does not make, promises a PR
  where maintainers asked to discuss first, or ignores a maintainer's stated
  direction.
