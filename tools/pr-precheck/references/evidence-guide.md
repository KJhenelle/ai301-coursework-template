# Evidence guide: where evidence lives in a PR package

Eval mode: use ONLY the bundle text. Sections are `## Repo facts`, `## Issue`, `## Thread highlights`, `## Plan context` (the plan's scope in / not-in, files, approach, test plan, and its repro evidence), and `## Candidate PR` (`### Title`, `### Description`, `### Commits`, `### Diff`, `### Test evidence`).
Live mode: the plan is plan.md (with its deviation notes); the diff is `git diff <default-branch>...HEAD` plus `git log` and `git status`; the draft title and description are pr_draft.md; the evidence is test_evidence.md; the issue is `gh issue view <url> --comments`; the repo's asks are `.github/PULL_REQUEST_TEMPLATE.md` and CONTRIBUTING.md. Anything not in these is not evidence.

## Plan fidelity (harness category: silent-drift)

- Where it lives: the plan's scope (in / not-in), files, approach, and deviation notes, against the diff's changed-file list and hunks; the description's "what changed" claims against the diff.
- What good looks like: every changed file and behavior change is inside the plan's boundary or explained by a deviation note, the plan's central change is in the diff, and the description claims exactly what the diff does. Drift in either direction is a fail: the diff does more than the plan (an extra feature, a refactor, a touched not-in area) with no note; the diff does less (a planned file or case missing) with no note; or the description says "per the plan" or "also covers X" where the diff contradicts it. A noted deviation consistent with the diff is honest, not drift.

## Test evidence (harness category: not-tested)

- Where it lives: the test-evidence section, read against the plan's test plan and the repro's inputs and observed-before output; the repo's own suite command and its outcome.
- What good looks like: the repro's own command (or a named test on the changed path) shown before and after with different, observable output matching the plan's expected-after, plus the repo's own checks run with their outcome visible (a pass count, or an honest failure and its reason). Not decisive: "tests pass" with nothing named, output from a path the diff does not touch, an after with no before, or the repo's checks never run.

## Diff quality (harness category: unreviewable)

- Where it lives: the unified diff and the commit list (live: also `git status` for untracked or stray files).
- What good looks like: every hunk is the change, visible at a glance. Debris tells: debug prints or leftover logging, commented-out blocks, dead code, formatting-only churn or whitespace rewrites, unrelated drive-by edits, lockfile or generated-file noise, committed working notes (plan.md, pr_draft.md, test_evidence.md), build artifacts, `.DS_Store`. Judge the hunk content, not the count.

## Standards and comms (harness category: standards-wall)

- Where it lives: the repo-facts block's PR-template asks and contribution policy (live: the template file and CONTRIBUTING.md), the thread highlights for maintainer direction, and the description plus diff where the repo's asks are honored. The AI-use policy lives in the same repo-facts or CONTRIBUTING lines and is answered by the description's disclosure section.
- What good looks like: every template section has real, specific content; each asked-for artifact (changelog or whatsnew entry, test, docs line, closing-issue reference like `Fixes #N`) is actually in the diff or description; the AI disclosure is explicit and in the form the policy asks; any maintainer direction (discuss first, use this approach) is engaged. Bad: blank, placeholder, or boilerplate sections, an unticked or missing checklist, a stated entry absent from the diff, no disclosure under a stated policy, or an ignored maintainer ask. (Whether the description's claims match the diff is plan fidelity, above.)
