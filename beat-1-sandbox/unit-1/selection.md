# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

[The individual Path Review issue page. A link to the repository or the issue list
does not satisfy this field.]
https://github.com/codepath/pathreview-ai301-fa26-howard/issues/67

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/67",
  "checks": [
    {
      "name": "unclaimed",
      "grade": "pass",
      "evidence": "Issue has no assignees, 0 comments, and no branches or pull requests listed under Development."
    },
    {
      "name": "policy_allowed",
      "grade": "pass",
      "evidence": "README directs contributors to docs/CONTRIBUTING.md, which welcomes fork-based contributions; neither it nor the PR template requires internal-maintainer-only PRs, a CLA, or an AI-use disclosure."
    },
    {
      "name": "repo_in_use",
      "grade": "pass",
      "evidence": "Repository metadata says archived: false; the repo describes itself as the Fall 2026 student copy, and main has a commit dated 2026-09-16."
    },
    {
      "name": "maintainer_active",
      "grade": "pass",
      "evidence": "Default-branch commit history shows activity on 2026-09-16, within 90 days of 2026-10-08."
    },
    {
      "name": "scope_bounded",
      "grade": "pass",
      "evidence": "The issue identifies a specific defect in POST /reviews: create_review() does not verify that the supplied profile belongs to the authenticated user."
    },
    {
      "name": "beginner_friendly",
      "grade": "fail",
      "evidence": "Labels are bug and tier-2 (Intermediate difficulty); there are 0 comments and no beginner label or maintainer invitation."
    }
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

Run 1: 12/20
Run 2: 15/20
Run 3: 17/20

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

issue-01
Rubric decision: reject
Gold label: accept
Reasoning: In Run 3, issue-01 was evaluated as reject because it failed the scope_bounded check. The pass condition in rubric.md strictly expected isolated bug fixes or localized feature changes and penalized the task as ambiguous, whereas the gold label accepts it as a well-bounded documentation task with a clear home and scope in an active repository.

**Check rationale**

| unclaimed | Issue body, assignees list, and comment thread. | Issue has 0 active assignees, no open linked PR attempting a fix, and no unabandoned claim comment within the last 14 days. | required |
Reasoning: This check establishes concrete, quantitative criteria to prevent duplicate effort and race conditions. Instead of relying on subjective notions like "unclaimed," it sets a hard boundary of 0 assignees, checks for open linked pull requests, and allows issues with stale claim comments older than 14 days without activity to be safely re-evaluated by a new contributor.

**Trade-offs**

The 14-day abandoned comment window risks duplicate work if an existing contributor is actively developing a solution locally without posting weekly status comments on GitHub. Additionally, the strict 90-day maintainer activity window in maintainer_active trades off well-scoped newcomer issues on stable, low-churn utility repositories that do not push commits every quarter.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
The issue involves a GUI/sidebar click-event debounce or duplicate execution bug in Python. It aligns with my background in software debugging and allows me to isolate the rewrite trigger and reproduce the multiple-application glitch locally within the weekly timeframe without configuring complex external dependencies.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
The verdict verified that the repository has recent default-branch commits, contains no blocking AI contribution policies, has zero assignees, and has no open pull requests attempting a fix. In addition to the automated checks, I weighed that the issue was filed directly by a repository collaborator (RazinShaikh), giving strong confidence that a clean fix will receive prompt review and be merged.
3. The anticipated difficulty in claiming it.]
Minimal difficulty. The issue currently has 0 assignees, 0 comments, and no open linked PRs. Writing a focused claim comment in Unit 2 that outlines local reproduction steps will secure the issue cleanly according to course guidelines.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
