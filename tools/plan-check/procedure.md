# Procedure: how this skill grades a plan package

## Read order

1. Live mode only: read scope.md first (stop if its Repo line is still a
   placeholder or the issue is outside that repo); then voice-guide.md.
   Eval mode: skip both and fetch nothing.
2. Read the Issue body: write down the one problem it reports.
3. Read Thread highlights and Repo facts: note maintainer requests, claim/
   discuss-first rules, bug-template asks, and any AI-use policy.
4. Read the Repro evidence BEFORE the plan: note environment/versions, the
   exact commands, every control run, the observed output/exit code, and
   where the failure originates. This is the yardstick for diagnosis and test.
5. Read the Candidate plan: note stated cause, in/not-in scope, files,
   approach steps, test plan, unknowns.
6. Read the Plan comment last: note the cause, scope, approach, unknowns,
   and promises it makes.

## Evidence gathering

Use references/evidence-guide.md for where each item lives. Record, per
family, one short fact or quote:
- Diagnosis: the stated cause + each repro observation it must explain.
- Scope: the problem sentence from the issue + every file/step in the plan.
- Executability: first file named + first edit; whether each named
  file/function appears in Repo facts, issue, or repro.
- Test plan: the repro's input command vs the plan's re-run, and the
  expected-after vs observed-before.
- Comms: each maintainer/convention ask, and whether the comment honors it.
Live mode: gather the issue and thread with gh; repro evidence comes from
the student's posted repro comment (house issue: what the drafts quote).
Never read other files in the student's directory.

## Check execution

Run checks in rubric order: bounded-scope, diagnosis-grounded,
executable-by-a-stranger, test-decisive, comment-faithful. Grade each
against its own recorded evidence; do not re-read the whole package unless
a recorded fact is missing. For each, apply the pass condition literally and
test the failure patterns by name: contradicted/ignored repro observation,
symptom-only fix, second unrequested change, unsupported file names, test
that passes before and after, comment that overstates or ignores a
maintainer ask. If the evidence needed is genuinely absent from the package,
grade unclear (never guess pass). Quote one line of evidence per check.
Grade the thing, not the formatting: ignore length, headings, polish.

## Verdict assembly

Apply rubric.md's verdict rule exactly: accept only if all five checks pass;
any fail or unclear gives reject. In the summary and JSON, quote the evidence
of the first failing check in rubric order. Live mode: after the per-check
lines, list voice-guide rules the comment breaks (quote the rule); these
never change the verdict. Note any procedure gap in the summary. End with
the single fenced JSON block, valid and last.
