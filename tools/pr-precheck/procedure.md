# Procedure: how this tool grades a PR package

## Read order

1. Live mode only: read scope.md first (stop without grading if the Repo line is still a placeholder or the issue or PR is outside that repo), then voice-guide.md. Eval mode: skip both and fetch nothing.
2. Read the repo facts (live: the PR template, CONTRIBUTING.md, and any AI policy) and the issue body and thread highlights. Note: the one problem the issue reports, each template section or ask, any required file entry (changelog, whatsnew, tests, closing-issue line), the AI-use policy, and any maintainer direction.
3. Read the plan BEFORE the diff, including its deviation notes (live: plan.md; eval: the plan-context block). Note: the scope in / not-in, the listed files, the approach, the test plan (expected-after), and every deviation note. This is the yardstick: the diff is judged against it, so read it first.
4. Read the diff and commit list. Note: every changed file and what each hunk does, and any hunk that is not part of the plan's change. Live: `git diff main...HEAD`, `git log main..HEAD --oneline`, and `git status`.
5. Read the description (title first, then body), against both the plan and the diff. Note: each claim about what changed, each template section and its content, and the disclosure.
6. Read the test evidence last. Note: commands and test names, observed-before, observed-after, and whether the repo's own checks or suite were run and with what outcome.

## Evidence gathering

Use references/evidence-guide.md for where each item lives. Record one short fact or quote per family:
- Plan fidelity: the plan's boundary (in / not-in), the list of changed files, any file or hunk outside the boundary and not in a deviation note, any piece of the plan's change missing from the diff, and any description claim the diff contradicts.
- Test evidence: the plan's expected-after, the repro's input command, the evidence's before and after output, and the repo-suite command with its outcome (counts or an honest failure reason).
- Diff quality: each debris tell found (debug prints, commented-out or dead code, formatting-only changes, drive-by edits, working-note files, artifacts) with its file; or "none".
- Standards and comms: each template section or ask with the description text that meets it or the gap; each required file entry and whether it is in the diff; the AI policy and the disclosure sentence; each maintainer direction and whether the PR honors it.

## Check execution

Run the checks in rubric order: plan-fidelity, test-evidence, diff-reviewability, template-and-standards, ai-disclosure. Grade each against its own recorded evidence; re-read the package only when a recorded fact is missing. Apply each pass condition literally and test its failure patterns by name: out-of-scope hunk, missing planned change, description overclaim, an un-noted deviation; "tests pass" with nothing named, evidence on an unchanged path, no before, repo checks never run; debris or unrelated hunks; blank or boilerplate template section, absent required entry, ignored maintainer direction; missing or empty disclosure. A deviation honestly noted and matching the diff re-ties a mismatch; a failing check honestly reported with its reason is evidence, a hidden one is not. If the evidence a check needs is genuinely absent from the package, grade it unclear (never guess pass). Quote one line of evidence per check. Grade the thing, not the formatting: ignore length, headings, and polish.

## Verdict assembly

Apply rubric.md's verdict rule exactly: accept only if all five checks pass; any fail or unclear gives reject. Quote in the summary the evidence of the first failing check in rubric order as the deciding fact. Live mode: after the per-check lines, list each voice-guide rule the title or description breaks (name the rule and quote the phrase); these never change the verdict. Note any procedure gap in the summary. End with the single fenced JSON block, valid and last, nothing after it.
