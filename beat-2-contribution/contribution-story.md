# Contribution: Customisation of force vectors

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Jhenelle
**GitHub Username:** KJhenelle
**Issue:** [Customisation of force vectors (OpenChemistry/avogadrolibs#2095)](https://github.com/OpenChemistry/avogadrolibs/issues/2095)
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 9: issue-scout with a fit-profile search strategy, fixed after scan 1**

I turned my issue-select skill into issue-scout, with a search strategy of `gh search issues` queries and ranking rules, and ran one scan. It fell short in three ways: my 100-result limit returned only the newest issues, so every Python result was dropped and all five graded issues were JavaScript; `unclaimed` accepted an issue whose owner had approved a claim 25 days earlier; and `maintainer_active` passed a repo on one 80-day-old commit while two strangers' proposals sat unanswered. I moved the `--comments 0` and date filters into the queries (267 merged results became 74), made `unclaimed` fail on any claim of any age, and made `maintainer_active` require recent maintainer activity plus replies to outside comments. I then graded two Issue Selection picks with the fixed rubric: `maintainer_active` passed Paradise #32854 (commits and a merged PR within days, replies the same day) and failed nomnom #214 (latest commit 2026-09-18, outside comments with no reply), so it separated an active repo from a quiet one. I still haven't re-run the full scan, so I don't know whether it is too strict for small student repos, and the scout still has no check for repos that require maintainer assignment before a PR.

**Unit 10: a voice guard in front of every comment I post upstream**

I added an Upstream section to my voice guide (claim, question and ping rules) and installed a hook that checks every `gh issue comment` against it before it goes out. It stopped my claim draft twice: once because my question didn't say what I had already tried, and once when I wrote "ASAP" instead of a date, which my own claim rule forbids. It also blocked a post when I chained a second command after it, because it read `claim-draft.md;` as the file name, so I now run the post as one plain command. For the repo I wrote a `CLAUDE.local.md` (42 lines) after reading `CONTRIBUTING.md` and the repo's own `AGENTS.md`: it imports the maintainers' guide, records the AI policy (I write every line myself; Claude explains and reviews), and holds the force plugin, `crystalscene.cpp` as the pattern, and `ArrowGeometry`'s existing `setColor` and `setRadiusScale`. It fell short because `CONTRIBUTING.md` still says to branch from `dev` when the default branch is `master`, so I wrote the correction into the file, and I kept it out of my PR with `.git/info/exclude`.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

My scan in unit 9 surfaced Paradise #32854, which my scout accepted, and nomnom #214, which it rejected. This week I swapped my scope check for the scope-feasible row and the difficulty note, then graded six issues with the patched rubric: Paradise #32854 (now reject, see below), nomnom #214 (reject: no issue closed or outside PR merged in 60 days), GTNH #23476 (accept, but its AI policy bans AI co-authored commits and wants only bugs I have hit in-game), cartography #882 (reject only because `maintainer_active` was unclear), PILOS #1522 (reject for the same reason, plus a design discussion with no replies in 12 months) and avogadrolibs #2095. The scout **accepted** #2095: no assignee or PR, the maintainer ghutchis commits daily and replies within hours to days, the issue is labeled good first issue, and he already named the files to change on 2026-09-06 (`force.cpp`, adapting colors from `crystalscene.cpp`). Its difficulty note is moderate: the location is named, but it is C++/Qt, which is outside my Python strength, and the maintainer has not said which options he wants beyond color, length and thickness. I chose it because the AI policy is clear (levels 0 and 1 are fine, code must be written by a human, and I will write the change myself), the maintainer is responsive, and my deadline is the 16th. I hope to learn how a real C++/Qt codebase is built and how a maintainer reviews a rendering change.

**Why I dropped Paradise #32854.** My first pick in unit 9 was Paradise #32854, the `*hug` emote that says "hugs herselves". It looked ideal: my scout accepted it, it was labeled Good First Issue, had no comments or assignee, and the fix was one string in `human_emote.dm`. When I re-graded it this week and read the repo's other docs, I found the Generative AI section of its `CODE_OF_CONDUCT.md`: "The use of generative AI tools is not permitted on the ParadiseSS13 repository. This includes pull request code, code review, and filing issues," with a ban for repeat offenses. My whole workflow in this course is AI-assisted (the scout, the repro and claim checks, drafting), so I could not contribute there honestly. I considered writing the fix and every comment by hand, but I would still have been using AI tools on the repository's issue and review work, and I did not want to hide that from the maintainers, so I dropped it and chose again.

The scout fell short in two places on a real search. Last week it accepted Paradise #32854 because it read only `CONTRIBUTING.md`; the generative-AI ban is in `CODE_OF_CONDUCT.md`, so this week's re-grade rejects it and I dropped it. And `maintainer_active` returned unclear on two otherwise healthy repos because the five most recently updated items were bot pull requests with no outside comments to test reply speed. I logged both in `scan-notes.md` but have not fixed either yet; the fix I would make is to read every document `CONTRIBUTING.md` links to and to sample the most recent outside-authored items.

My claim comment: https://github.com/OpenChemistry/avogadrolibs/issues/2095#issuecomment-6810860294

**Toolkit**

- Tool: issue-scout (my search strategy and rubric), run through Claude Code in direct mode on each issue URL, with the scope-feasible patch applied.
- What it produced: six graded issues with read-outs in `scan-output.md`; it accepted avogadrolibs #2095 with a moderate difficulty note, and corrected last week's Paradise accept to a reject.
- Difficulties: `policy_allowed` missed Paradise's ban because the scout read only `CONTRIBUTING.md`; `maintainer_active` condition 3 came back unclear on cartography #882 and PILOS #1522 because the sample was bot-only.
- What changed: I replaced the `scope_bounded` row with `scope-feasible` and added the difficulty note, and logged both misses in `scan-notes.md`. Still to do: make `policy_allowed` read every linked doc, and change the `maintainer_active` sample.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

- OS: macOS 27.0.1 (build 26A434), Apple M2.
- App: Avogadro 2.1.0-20261111-g4d21680, the macOS Apple Silicon continuous build from https://github.com/OpenChemistry/avogadrolibs/releases/download/continuous/Avogadro2-continuous-arm64.dmg, downloaded on 2026-11-11 and dragged into Applications. The window title shows the version.
- Sample file: `raman.cjson` from https://github.com/OpenChemistry/avogadrodata/blob/master/data/cjson/raman.cjson (formaldehyde, CH2O, with vibrational mode data).
- I have not built from source yet, so this run uses the released binary, not my own build of `master`.
- Challenges: the repo's `CONTRIBUTING.md` tells you to start from a `dev` branch, but the default branch is `master`, and the build guide linked from `AGENTS.md` (https://two.avogadro.cc/develop/build.html) returned a 404. I used the continuous build for the repro and read `.github/workflows/build_mac.yml` for the source build steps instead.

**Steps to Reproduce**

1. Open Avogadro 2 (the continuous build above).
2. Choose File > Open and open `raman.cjson`. The Files list shows `raman.cjson (CH2O)`.
3. Open the Vibrational Modes window and select a mode (I used mode 9, 1,527.14 cm^-1).
4. In the Display Types panel, tick **Force**. Green arrows are drawn on the atoms.
5. Look beside each entry in Display Types, and at the "Force Settings" panel below it.
6. Observed: Ball and Stick, Cartoons, Close Contacts, Crystal Lattice and Labels each have a "..." button. Force (and Dipole Moment) have none, and the "Force Settings" panel is empty, so there is no way to change the arrow color, length or thickness.

**Reproduction Evidence**

- **Commit showing reproduction:** none (this run used the released binary, not a build from my fork).
- **Screenshots/logs:** screenshot of the main window with Force ticked, green force arrows on CH2O, "..." buttons on the other display types, none beside Force, and an empty "Force Settings" panel; a second screenshot of the Vibrational Modes window with mode 9 selected. Window title: `raman.cjson - Avogadro 2.1.0-20261111-g4d21680`.
- **My findings:** The issue's description matches what I see. The arrows are drawn by `Force::process()` in `avogadro/qtplugins/force/force.cpp`, which calls `ArrowGeometry::addSingleArrow` and has no settings widget, while `crystalscene.cpp` shows the pattern the maintainer pointed to (a `setupWidget()` override plus values saved with `QSettings`). Not verified: where the maintainer wants the controls (the empty "Force Settings" panel or a "..." menu); behavior on Windows or Linux; behavior on my own build of `master`.

**Toolkit**

- Tool: repro-check, run through Claude Code in live mode on `claim-draft.md` and `repro-draft.md` together, against issue #2095.
- What it produced: an accept, all six checks passing. It graded the posted claim (names the force-arrow settings, a first step, a Friday date) and the repro (environment recorded, steps followable, behavior matches the issue, honest about what is not verified, repo AI policy respected).
- Difficulties: its first run on the claim alone flagged nothing wrong, but my voice guard, a separate check, stopped two earlier drafts (a question with no "what I tried", and "ASAP" instead of a date). repro-check also cannot tell whether the screenshots exist; it graded my written description of them.
- What changed: I replaced "ASAP" with "by Friday" and cut the question from the claim. For the repro I wrote down explicitly what I did not verify (my own build, other operating systems) so the report claims only what I saw.

---

## Solution Approach

**Analysis**

Issue #2095 is an enhancement, not a bug, so there is no faulty behavior to trace. What is missing is any way to change how force arrows look.

- `avogadro/qtplugins/force/force.h` and `force.cpp`: the `Force` scene plugin had no settings and no `setupWidget()`, so the app's "Force Settings" dock had nothing to show.
- `Force::process()` drew every arrow from the raw force vector, `pos1 + forceVector`, with the arrow geometry's built-in color and size.
- `avogadro/qtgui/sceneplugin.h`: `setupWidget()` and `hasSetupWidget()` are the hooks the app uses to fill that dock.
- `avogadro/rendering/arrowgeometry.h`: `ArrowGeometry` already has `setColor(const Vector3ub&)` and `setRadiusScale(float)`, so no rendering change is needed. Its defaults are color (0, 255, 0) and radius scale 1.0.
- `avogadro/qtplugins/crystal/crystalscene.cpp`: the existing pattern for a scene plugin with saved settings (`QSettings` in the constructor, a lazily built setup widget, slots that save and redraw). The maintainer pointed to it in the issue, and I followed it.

**Observed before the change**

Seen in the continuous build of Avogadro 2 (version 2.1.0-20261111-g4d21680, macOS), not a build I compiled. With the Force display type enabled, its "Force Settings" dock is empty, and the arrows are green at a length equal to the raw force vector. Nothing in the app changes their color, length or width. In the code this is the missing `setupWidget()` and the fixed `pos1 + forceVector` in `process()`.

The "after" checks below are made in the app I compiled: avogadroapp built against avogadrolibs from my commit `f62ee3ae` on top of library master `dd911a8b`. The About dialog's library version is set when CMake configures, so it may still read `gdd911a8b`; the commit I built is the one named here. This app is a different build from the continuous build, so the before and after show what a user sees, not a controlled comparison of my change alone.

**Proposed Solution**

Will change, in `force.h` and `force.cpp` only:

- Add a settings widget with arrow length, arrow width and arrow color.
- Save each value with `QSettings` under `force/length`, `force/arrowWidth` and `force/color`, and load them in the constructor.
- Apply them in `process()`: scale each force vector by the length, and call `setColor` and `setRadiusScale` once on the arrows.
- Defaults are length 1.0, width 1.0 and green, the same as today's rendering, so existing users see no change until they touch a setting.

Will not change:

- Arrow head size. I said in my claim comment that it is a follow-up PR.
- `ArrowGeometry` or any other rendering code.
- Any other plugin, including the `crystalscene` files I copied the pattern from.

**Implementation Plan**

This was written after most of the code, so the list records what I did and what is left.

Done (commit f62ee3ae on branch `force-arrow-settings`):

1. In `force.h`, add the `setupWidget()` and `hasSetupWidget()` overrides, private slots `setColor`, `setLength` and `setArrowWidth`, and members for the widget pointer, length, width and color.
2. In `force.cpp`, initialise `m_setupWidget` to `nullptr` and load the three saved values in the constructor.
3. Write the three slots. Each updates its member, emits `drawablesChanged()` to redraw, and saves to `QSettings`.
4. Write `setupWidget()`: two spin boxes and a `ColorButton` in a form layout.
5. Update `process()` to apply the color, width and length.
6. Run `git clang-format origin/master --diff` (no differences) and the full suite on commit `f62ee3ae`: 155 of 155 tests passed, finished 2026-11-16 00:05 EST.

Left:

7. Add a test under `tests/qtplugins/` and register it in `tests/qtplugins/CMakeLists.txt`. It must fail without the fix and pass with it. A draft `forcetest.cpp` exists but is not registered or verified.
8. Re-check the arrows in the app, before and after, and record the output in the PR description.
9. Open the PR against `OpenChemistry/avogadrolibs` `master` with `Fixes #2095` and an AI-assistance disclosure.

Test plan, with the observable result expected after the change:

- Fresh settings (no `force/*` keys): the dock shows Arrow length 1.00, Arrow width 1.00 and a green color button, and the arrows look the same as on master.
- Set Arrow length to 2.00: every arrow doubles in length and the redraw happens immediately. Set it back to 1.00 and they match master again.
- Set Arrow width to 0.50: arrows get thinner, and short arrows stay thin because the width scales each arrow's own radius.
- Pick another color: all arrows change to it.
- Close and reopen the app: the three values and the color are restored from `QSettings`.
- Automated test (step 7): fails on master and passes on the branch, for whichever of the above it can check. If it can't be done for the widget, the PR description will say why.
- The repo's existing suite (155 tests, all passing on master) still passes. Result on `f62ee3ae`: 155 of 155 passed, finished 2026-11-16 00:05 EST.

Unverified so far (2026-11-16): the built change has not been re-run against the app checks above since the commit. There is no automated test for the widget yet.

Deviations: none so far.

**Toolkit**

- Tool: plan-check, run in live mode on `plan.md` and a draft plan comment (`plan-comment.md`, not posted) against issue #2095.
- What it produced: a verdict of accept with all five checks passing (bounded-scope, diagnosis-grounded, executable-by-a-stranger, test-decisive, comment-faithful). Before that, it held the plan and told me to add an observed-before with the app build named, an observable expected-after in the test plan, and an "Unverified" line with a date, and to either record my local-build check or drop it from the comment.
- Difficulties: #2095 is an enhancement, so there was no bug to trace and the "cause" had to be stated as what was missing. I also wrote the plan after most of the code, so the Implementation Plan had to separate what was done from what was left. The build I observed "before" in was easy to describe loosely, and the check would not pass it until the About-dialog version was named.
- What changed: I added the observed-before with the app version, a test plan with expected results, and a dated Unverified line to `plan.md`. I dropped my unverified "works in a local build" claim from the comment, and corrected "155 of 155 on that commit" to say the suite passed on master before my change, since I had not run it on my commit.

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
