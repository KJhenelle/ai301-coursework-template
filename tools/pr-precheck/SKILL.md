---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer exactly one question about exactly one PR package: **is this ready to submit?** A PR package is a candidate pull request (title, description, commits, diff, test evidence) read against the plan it claims to implement and the issue that plan belongs to. Grade one package per run. Never answer a different question (is the code good, is the issue worth taking, should the maintainers merge it), never grade a second package in the same run, and never answer from gut feel: execute the components in this directory.

## Inputs and modes

Run in exactly one of two modes.

**Live mode** (the student's own submission, checked before it goes out). Inputs, all read from the working copy on the student's branch unless noted:
- the plan: `plan.md`, including its deviation notes (house-chain students: the house plan instead);
- the diff: everything the branch changes relative to the repo's default branch, produced by `git diff main...HEAD` (three dots; substitute the default branch name if it is not `main`), plus `git log main..HEAD --oneline` for the commits and `git status` to see untracked or uncommitted files;
- the draft PR title and description: `pr_draft.md` (first line is the title, the rest is the description);
- the test evidence: `test_evidence.md` (house-chain students: the house repro pack's steps are the repro the evidence is read against);
- the issue: read with `gh issue view <url> --comments`, plus the repo's `.github/PULL_REQUEST_TEMPLATE.md` and `CONTRIBUTING.md` for the template asks and stated policy (including any AI-use policy).
Live mode reads only these. Do not read other files in the student's directory.

**Eval mode** (a package bundle is the whole world). Every fact comes from the bundle text (repo facts, issue, thread highlights, plan context, candidate PR title, description, commits, diff, test evidence). Fetch nothing, read nothing else, and ignore scope.md and voice-guide.md entirely. Always grade the complete package: every check, full verdict rule.

If the user's request names a bundle or says eval, use eval mode; if it names an issue URL and the student's files, use live mode.

## The scope seam (live mode only)

In live mode, read scope.md before anything else, before the diff, the plan, or the issue. Take the repo from its `Repo:` line. If that line still carries a bracketed placeholder (for example `<ORG>/<PATH-REVIEW-REPO>`), stop without grading: say that the scope is unfilled, tell the student to fill the `Repo:` line in scope.md with their section's Path Review repo (the install step of this unit's activity page names it; otherwise ask the instructor), and emit no verdict. Never guess a scope. If the issue or the PR targets any repo other than the scoped one, refuse to grade it and say why. Apply the house rules scope.md states (PR from your own fork's branch, one PR per issue, template always used) as part of the standards check. In eval mode, ignore scope.md entirely.

## The voice seam (live mode only)

After scope passes, read voice-guide.md. Hold the outgoing PR text (the title and the description, and only those) against each rule in it. After the per-check summary, list every rule the draft breaks, quoting the rule's name and the offending phrase. The voice guide never changes the verdict by itself: only a rubric check that reads it can, and rubric.md has none. Voice is personal and carries no gold labels. In eval mode, ignore voice-guide.md entirely.

## Component reads

Read these four files, in this order, before grading, and treat them as the tool:
- rubric.md defines the checks and the verdict rule. Grade exactly its checks, no more, none invented.
- references/evidence-guide.md maps where each evidence family lives in a package (live and eval) and what good looks like.
- procedure.md is executed as written: read order, evidence gathering, check execution, verdict assembly.
- This file is the frame around them.
When procedure.md is silent on a step, report the gap in the summary and do the most literal thing the rubric allows; never improvise a new check or step. If rubric.md or procedure.md has no written content (only a template or comments), refuse to grade: say which file is empty and emit no verdict.

## Verdict and output

The verdict space is binary: `accept` (ready to submit) or `reject` (hold). There is no third verdict, no "accept with reservations", no score; reservations go into check evidence lines. Assemble the verdict only with rubric.md's verdict rule via procedure.md.

Reply with a short readable per-check summary (one line per check: grade and the deciding fact), then, in live mode, the voice-guide findings, then end with a single fenced JSON block, valid, last, with nothing after it. The schema is fixed and must not be altered, extended, or reordered:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

The `item` is the bundle id in eval mode and the PR URL (or the branch name if no PR exists yet) in live mode. List every rubric check, in rubric order, using its exact name.

## Grading discipline

- **Evidence first.** Grade no check without naming the fact or quote that decided it. "Looks fine" is not evidence.
- **Grade the thing, not the polish.** A terse complete PR can be ready, and a beautiful confident one can be hiding drift. Read the artifact (the diff, the output) against the plan, the issue, and the stated standards, never the formatting or length.
- **The rubric decides, not the run.** If a check passes by its stated condition but feels wrong, it still passes; if it fails by its condition, it fails. Do not soften or harden a check on instinct.
- **The procedure decides how, not the run.** Follow procedure.md as written and report its gaps.
- **Honest outcome.** A PR that honestly discloses a shortfall (a deviation note, a failing check with its reason) can be ready; do not equate "less than everything" with "hold".
- **Unclear defaults to fail.** Treat `unclear` as rubric.md's verdict rule directs; where that rule is silent, an unverifiable claim is a failing one. A PR you cannot verify from the package is not ready to submit.
