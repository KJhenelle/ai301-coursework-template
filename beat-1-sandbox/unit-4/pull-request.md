# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-howard/pull/96

**My pr-precheck verdict on the draft**

accept. All five checks passed (plan-fidelity, test-evidence, diff-reviewability, template-and-standards, ai-disclosure); no voice-guide findings.

**Branch**

fix/67-create-review-ownership-check

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

20/20, then 20/20. The first full run already passed, so nothing was revised; the second full run was made only to save `eval-run.txt`. (eval-run.txt agreement line: `agreement: 20/20 scored items  (bar: 18/20: PASS)`.)

**Package analysis**

pkg-01 (pandas-dev/pandas#66657, standards-wall). Gold: reject. My rubric: reject. It failed `template-and-standards` with the evidence "Template requires 'closes #xxxx' and a whatsnew entry for bug fixes; the description has no issue reference and the diff has no whatsnew change." The fix itself has decisive ASAN evidence (test-evidence passed), so the package is held only because the repo's stated template asks are visibly ignored, which is what that check reads. My rubric also failed `plan-fidelity` on it (the description claims a bulk-copy-path check the diff does not deliver); the gold note does not name that, but the verdict still agrees.

**Check rationale**

> | template-and-standards | The repo-facts block's stated PR-template asks and contribution rules (live: `.github/PULL_REQUEST_TEMPLATE.md` and CONTRIBUTING.md), read against the description and the diff; plus explicit maintainer direction in the thread. | Pass if every section or ask the repo states for a PR is honored with real content (not blank, placeholder, or boilerplate), including any item the template asks for that lives in the diff (a changelog, whatsnew, test, or docs entry; a closing-issue reference), and nothing a maintainer asked for in the thread is ignored. Fail if a stated template section or checklist is visibly ignored or left as boilerplate, or a stated required file entry is absent from the diff, or a maintainer's explicit direction is ignored. Unclear only if the package states no template or policy and the description otherwise names the issue. | required |

It reads this way because the repo's template is the standard a PR is held to, and the check
has to be something another reader could apply and get my answer. The pass condition
names what to look at (template sections, and the entries the template asks for in the
diff, such as a changelog or a closing-issue reference) and what counts as failing
(blank, placeholder or boilerplate content, or a maintainer's direction ignored). It
judges content, not how the description is formatted. I kept AI disclosure out of this row
and gave it its own `ai-disclosure` check, so a missing disclosure shows up on its own
line and a PR that satisfies the template can still be held for it. Folding the two
together would have let a well-filled template hide a missing disclosure. The last
sentence sets `unclear` only for a package that states no template or policy, so a PR is
not held for a rule that does not exist.

**Trade-offs**

The rubric reads template asks and file entries literally. A PR in a repo with no stated
template or AI policy has nothing to fail on there, so it passes `template-and-standards`
whatever the description says. All five checks are required and `unclear` counts as fail,
so a package whose evidence is merely missing is held and not accepted. I accept that cost,
because holding a good PR once is cheaper than posting one a reviewer can't verify. I made
no revision after the first full run (20/20), so no canary re-runs were needed, and the
second full run was made only to save `eval-run.txt`.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
