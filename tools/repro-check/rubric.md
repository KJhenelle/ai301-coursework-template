# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `env-recorded` | Repro report's environment block or explicit config section | Operating system, tool/runtime version, and relevant dependencies are explicitly recorded so another engineer can configure a matching sandbox. | preferred |
| `steps-followable` | Repro report's reproduction sequence read against the target repo | A reader can execute or follow the listed steps without having to guess missing repository-specific scripts, undocumented arguments, or custom paths. Standard development practices (e.g., standard builds, dependency installation, or default CLI invocations documented in the repo) do not need to be re-explained command-by-command. | required |
| `behavior-matches` | Repro report output/artifacts compared against the target issue description | The observed outcome demonstrates the core defect, error path, or bug symptom described in the issue (or cleanly confirms a cannot-reproduce result), allowing for benign environment or formatting variances. | required |
| `claim-specific` | The claim comment's text and intended scope | The comment explicitly names the exact issue/behavior targeted, commits to clear forward-looking next steps or a promised reproduction path, and stays bounded to that single defect. | required |
| `outcome-honest` | Repro report's final verdict and conclusion section | The reported outcome accurately reflects what the artifacts show without overclaiming success or masking inconclusive evidence. | required |
| `policy-compliant` | The entire package read against repo policies in `repo-facts` or repository guidelines | The package complies with all stated repository policies, issue templates, and contributor rules; if the repository mandates an explicit disclosure of AI tool usage, that disclosure must be present. | required |

## Verdict rule
Accept (`ready`) if and only if every `required` check passes (`P`). Any failure (`F`) or indeterminate assessment (`?` / `unclear`) on a required check triggers an immediate reject (`hold`). A failure on a `preferred` check does not block the package from passing, provided all required checks pass.
<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->
