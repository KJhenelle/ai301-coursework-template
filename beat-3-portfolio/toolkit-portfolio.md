# Toolkit Portfolio

Path: `beat-3-portfolio/toolkit-portfolio.md`

This file is Assignment 6, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. It has been waiting here since you created the repo in unit 1;
unit 9 is when you write it.

**Only this page is read.** Your `tools/` folders and your installed skill folders are never
opened, so every piece of evidence you want seen has to live inline here: an output excerpt,
a before/after pair, a dated commit reference.

**Write every sentence yourself.** AI may gather diffs, dates and excerpts for you; it does
not draft entries.

**Keep every section header below under its exact name** — Featured Tools, Inventory, The
Arc, and Limitations and What's Next. Feature three or four tools, each in the entry shape
shown below; give every other tool one inventory line.

**Some lines below are labelled, and the label is how they are read.** Three places on this
page use a `Label: your words` shape — the arc's beats, the tool-limits list, and nothing
else. Keep those labels exactly as written, one per line, and never delete a labelled line:
where you have nothing to put after a label, write `none` and move on. A deleted label reads
as a deleted answer.

**Before you finish**, replace every `[bracketed prompt]` with your own words, then delete
the unused `[Tool name]` entry stub, its copy-me sentence, and the prompt sentences under
each header. A leftover bracketed prompt reads as unfilled.

**Student:** Jhenelle Walters

## Featured Tools

I chose issue-scout because it streamlined finding issues to work on and let me prescreen each one, so problems with scope or the repo's rules would not surface later. I chose voice-guard because it let me write my PRs and comments in a way that is genuine to me and does not come across as overly flat, so I could spend more time on my code instead of worrying about whether I had phrased something correctly. I chose pr-precheck because it let me verify my PR up front, so I would not have to rewrite it multiple times.

**issue-scout**

**What it is, and the judgment hole I wrote:** issue-scout searches all of GitHub with `gh search issues`, ranks the results cheaply from the fields the search returns, and grades the top five against a written rubric. The judgment is mine in two files. `search-strategy.md` holds three queries traced to my fit profile (Python first, front-end JavaScript second, nothing in Java or Go). `rubric.md` holds the checks, for example `maintainer_active` condition 3: "every non-maintainer comment older than 7 days has a maintainer reply", and the verdict rule: "Accept if and only if every `required` check passes."

**How it evolved, dated:** issue-scout changed a lot from its first iteration. On 2026-11-11, after my first scan, I made it more lenient about what counts as an accepted issue by loosening the allowance for scope, and stricter on other checks, such as maintainer_active and unclaimed. In scan 1, `unclaimed` accepted student-performance-predictor #7 although the owner had approved a claim ("OK WORK") 25 days earlier, so it now fails on a claim of any age. `maintainer_active` passed Payhub #4 on one commit 80 days old while two strangers' proposals went unanswered, so it now needs a recent non-bot commit, an outside PR merged or issue closed within 60 days, and replies to old outside comments. I also moved the `--comments 0` and date filters into the queries themselves, because the 100-result limit had returned only the newest issues and every Python result was dropped (267 merged results became 74). I replaced `scope_bounded` with `scope-feasible` because the old check rejected honest work: nomnom #214 failed it over an unsettled design edge.

**Evidence:** The scan of 2026-11-10 graded Payhub #4 with the old rubric:

`maintainer_active: pass (author and maintainer's commit Aug 22 is within 90 days)`

Under the fixed rubric the same check separated two real repos. Paradise #32854 passed (commits and a merged PR within days, replies the same day) and nomnom #214 failed (latest commit 2026-09-18, outside comments with no reply). The fixed scout then accepted avogadrolibs #2095 with a "moderate" difficulty note, which became my pull request #3370.

**voice-guard**

**What it is, and the judgment hole I wrote:** voice-guard is a hook that checks the body of every `gh issue comment` and `gh pr create` against my voice guide before it goes out, and stops the command if a rule is broken. The judgment is the guide, `voice-guide.md`. One of its rules, concrete-commitments: "When claiming an issue or stating next steps, specify exact deliverables and an explicit timeline instead of vague assurances." Another, from the Upstream section I added: "A question is a single question a maintainer can answer in a sentence, and it states what I already tried and found."

**How it evolved, dated:** voice-guard barely changed. The one change came when I wanted it to use more familiar language, because its initial run was very formal. In unit 10 (2026-11-11) I added the Upstream section with the claim, question and ping rules and installed the hook that enforces them.

**Evidence:** From `guard-log.md`, my claim draft for #2095 on 2026-11-11:

`19:15 stop: rule broken: "A question is a single question a maintainer can answer in a sentence, and it states what I already tried and found."`

`19:31 stop: rule broken: "A claim names the concrete first step I will take and a date I can keep..."` (I had written "ASAP" instead of a date)

`19:37 pass`

I replaced "ASAP" with "by Friday" and cut the question, and the hook let the real post through at 19:38. On 2026-11-19 it also stopped a PR description whose disclosure did not say what I verified myself.

**pr-precheck (with the ship-gate)**

**What it is, and the judgment hole I wrote:** pr-precheck grades a pull request package (the draft title and description, the diff, the plan, and the issue) against five checks: plan-fidelity, test-evidence, diff-reviewability, template-and-standards and ai-disclosure. The ship-gate is its second half: a hook that runs pr-precheck plus the commands in my `ship-manifest.md` (`git clang-format origin/master --diff`, `cmake --build build`, `ctest --test-dir build`) before `gh pr create` is allowed. The judgment is the rubric and the manifest. For example plan-fidelity requires that "the description claims nothing the diff does not deliver", and any single failed or unclear check rejects the PR.

**How it evolved, dated:** pr-precheck's rubric barely changed after I wrote it on 2026-11-10 (commit ad1a43f): the installed copy is identical to the one in my repo. The reason is that the five checks already caught real problems. What moved was the PR, and I added the gate around it on 2026-11-16 by writing the manifest for avogadrolibs.

**Evidence:** Two gate runs on my branch `force-arrow-settings` on 2026-11-16 (the template-and-standards line):

`15:22 pass: ... CONTRIBUTING's why/implementation/how-to-test are present with 'Fixes #2095' ...`

`15:42 pass: ... CONTRIBUTING's why/implementation/how-to-test present with 'Refs #2095' and not-in list ...`

Both runs passed, but the first run's notes led me to three fixes: a false "this repository's PR template" line, `Fixes #2095` on a PR that leaves arrow head size undone, and a "Before (master)" label on a screenshot from the continuous build. The rerun passed, and I opened PR #3370 at 16:05.

## Inventory

- **repro-check:** grades a claim comment and a reproduction report against the issue. It accepted my #2095 claim and repro on all six checks, and it cannot tell whether my screenshots exist, only that I described them.
- **plan-check:** grades a plan and its plan comment before I post. It held my plan until I named the app version I observed "before" in, added a test plan with expected results, and dated what was unverified; it then accepted with all five checks passing.
- **PR-monitor with its playbook:** reads an open PR and drafts one move from my playbook's thresholds (3 days to first response, 7 days after approval, 5 days for a stalled review, one nudge). On #3370 it drafted a wait; I have not yet exercised its reply or nudge paths.

## The Arc

**Beat 1**
Date: 2026-11-10 to 2026-11-11 (unit 9)
Friction: My first scan returned only JavaScript because the 100-result limit kept the newest issues, and its accepts included an issue with an approved claim 25 days old (student-performance-predictor #7) and a repo with one 80-day-old commit (Payhub #4). I saw it when I read why each accepted issue had passed.
Change: I moved the filters into the queries, made `unclaimed` fail on a claim of any age, tightened `maintainer_active`, and replaced `scope_bounded` with `scope-feasible`.
Result: The fixed rubric passed Paradise #32854 and failed nomnom #214 on activity, and the scout accepted avogadrolibs #2095, which became PR #3370. A later re-grade found it had missed Paradise's AI ban in `docs/CODE_OF_CONDUCT.md`, so it still has a gap.

**Beat 2**
Date: 2026-11-11 (unit 10)
Friction: I was about to post a claim to a real maintainer with no check on my own wording.
Change: I added an Upstream section to my voice guide and installed a hook that checks each `gh issue comment` against it.
Result: It stopped my claim draft twice (a question with no "what I tried", and "ASAP" instead of a date), and the corrected claim posted on #2095 at 19:38. It also blocked one post where I had chained a second command after the file name.

**Beat 3**
Date: 2026-11-16 (unit 11)
Friction: My PR description contained three errors I had not noticed: a false PR-template line, `Fixes #2095` where `Refs #2095` was true, and a mislabeled "before" screenshot.
Change: I wrote `ship-manifest.md` and ran the ship-gate; its notes pointed to all three, and I fixed them.
Result: The rerun passed (suite 573 s) and the PR opened at 16:05. The maintainer approved it on 2026-11-17 with "LGTM, thanks" and asked for nothing.

**Beat 4**
Date: 2026-11-18 (unit 12)
Friction: My first playbook draft had a 3-day staleness threshold next to "no nudge for a month", so the monitor could have called a PR stale and then forbidden the nudge.
Change: I rewrote the playbook so every threshold leads to the one nudge, using a count of five merged outside-contributor PRs for the numbers.
Result: The monitor read #3370 (approved, 22 checks passing, mergeable) and drafted a wait until 2026-11-24 rather than a nudge. I posted nothing from it. My PR had no review to answer, so the reply and nudge paths remain untested.

## Limitations and What's Next

My toolkit has been tested on one contribution in one repo, so each tool has one real case behind it, not a range. The scout still has not been re-run as a full scan on the fixed rubric, so I do not know if it is too strict for small student repos. The monitor has only run its wait path. My PR has no automated test, because the draft test does not compile, and the PR says so.

Next I would make `policy_allowed` read every doc that `CONTRIBUTING.md` links to and search the whole docs folder for "AI", "LLM" and "generative". I would change the `maintainer_active` sample to the five most recent outside-authored issues and PRs, add a check for repos that require maintainer assignment before a PR, and run the monitor on a PR that has a review to answer.

**Tool limits.** One line per featured tool, in the same order as the entries above, naming
where that tool still stops or what it still gets wrong. A small honest limit is full credit;
"none really" is not a limit. If a tool genuinely has none you can name, write `none` after
its label rather than deleting the line.

issue-scout: `policy_allowed` reads only `CONTRIBUTING.md`, so it missed Paradise's AI ban in a linked doc, and `maintainer_active` returns unclear when the sampled items have no outside comments to test.
voice-guard: it checks a post against my rules but not whether the claim is true, and it read `claim-draft.md;` as the file name when I chained a second command, so I post as one plain command.
pr-precheck: it cannot check that screenshots are attached, the hook checks the folder the session started in, and each gate run costs the full test suite (about 8 to 10 minutes).
