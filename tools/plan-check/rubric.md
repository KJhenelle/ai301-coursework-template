# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| bounded-scope | The plan's scope statement (in / not-in) and its approach and files-or-areas, read against the issue's stated problem. | Pass if the plan's approach and files touch only what is needed to fix the one problem the issue describes, and anything beyond it (refactors, adjacent bugs, cleanups) is named as not-in rather than done. Fail if the approach or file list includes a second change that the issue and repro evidence do not require, or if the scope has no stated boundary a reviewer could hold the diff to. Unclear only if the issue's problem cannot be identified from the package. | required |
| diagnosis-grounded | The plan's stated cause read against what the repro-evidence block actually shows (observed output, steps, versions), plus the plan's risks/unknowns. | Pass if the stated cause is consistent with every observation in the repro evidence, targets the cause the evidence points at rather than only the symptom, and anything the evidence does not settle is labelled an unknown or assumption. Fail if the cause contradicts or ignores an observation in the repro evidence, patches the symptom while the evidence points at a cause elsewhere, or states an unverified guess as fact. Unclear only if the package has no repro evidence to read the cause against. | required |
| executable-by-a-stranger | The plan's approach and files-or-areas, read against the repo-facts block. | Pass if a contributor who has never seen this issue could name the first file (or specific function/area) to open and the first concrete edit to make from the plan alone, and nothing it names is contradicted by the issue, repro, or repo-facts. A specific path or function that the package simply does not list is NOT a failure: repo-facts never list source files, so do not demand confirmation. Fail if the first step needs knowledge only the author has, relies on vague steps ("fix the handler", "clean up the logic", locations to be "pinned after tracing"), or names files or functions that the package contradicts. Unclear only if the plan names a location whose existence the package actively puts in doubt. | required |
| test-decisive | The plan's test plan read against the repro evidence's steps and observed behavior. | Pass if the test plan re-runs the repro's own inputs and states an expected-after that is observable and differs from the observed-before, so a pass and a fail would look different. Fail if the test plan only says "verify it works", checks something the bug never touched, or would pass identically before and after the change. Unclear only if the repro evidence gives no inputs or observed behavior to compare with. | required |
| comment-faithful | The draft plan comment read against the plan and against the thread highlights and repo conventions (contributing rules, maintainer requests) in the issue context and repo-facts. | Pass if the comment states the same cause, scope, and approach as the plan without adding claims the plan lacks or softening unknowns into certainty, and does not violate anything a maintainer asked for in the thread or the repo's stated conventions (for example claim etiquette or discuss-first rules). If the repo-facts state an AI-use disclosure policy, the comment must contain an explicit disclosure of AI assistance in the form that policy asks for (name the tool or extent only if the policy requires it); a comment with no disclosure at all fails. Fail if the comment contradicts or overstates the plan, or ignores a stated maintainer request or convention. Unclear only if no thread or convention information is in the package and the comment otherwise matches the plan. | required |

## Verdict rule

Accept if all five checks pass. Reject if any check is fail. Unclear
counts as fail: a plan whose soundness cannot be verified from the
package is not ready to build from. No check is preferred, so no check
is exempt. In the output, quote the evidence for the first failing
check in the order listed above.
