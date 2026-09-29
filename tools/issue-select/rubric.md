# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| unclaimed | Issue body, assignees list, and comment thread. | Issue has 0 assignees, no open linked PR attempting a fix, and no unabandoned claim comment within the last 14 days. | required |
| policy_allowed | Repo facts, contributing documentation, and issue body. | The repository or contributing docs do not ban AI-generated contributions/tools, do not restrict PRs to internal maintainers only, and have no mandatory CLA roadblocks. | required |
| repo_in_use | Repo facts: repository status, archiving flag, and commit history. | Repository is not archived, not deprecated, and has at least 1 commit to the default branch within the last 180 days (releases not required). | required |
| maintainer_active | Repo facts: commit history and comment timestamps. | At least 1 commit to default branch or maintainer response within the last 90 days. | required |
| scope_bounded | Issue body and comment discussion. | The issue is a concrete, bounded bug fix, localized feature, or documentation task with an agreed direction; it is NOT an umbrella/tracking megaissue, an open-ended feature wish lacking specification, or subject to unresolved multi-year design debate. | required |
| beginner_friendly | Issue labels and issue comments. | Issue is labeled `good first issue`, `beginner-friendly`, `easy`, `help wanted`, or a maintainer explicitly invites newcomers. | preferred |
## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

Accept if and only if every `required` check passes. If any `required` check fails or is unclear, the verdict is reject (unclear counts as fail). The `preferred` check (`beginner_friendly`) never alters the binary verdict; it is strictly used to rank accepted issues.