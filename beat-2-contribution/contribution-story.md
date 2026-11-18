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
**Pull Request:** [OpenChemistry/avogadrolibs#3370](https://github.com/OpenChemistry/avogadrolibs/pull/3370)

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

**Unit 11: ship-gate and a gate manifest on the force-arrow branch**

I wrote `ship-manifest.md` for avogadrolibs (clang-format on the diff against `origin/master`, `cmake --build build`, full `ctest`) and ran the ship-gate on `force-arrow-settings`. The first run passed all five checks, but its notes caught three things in my description: a Developer's Certificate of Origin section that said "this repository's PR template" when the repo has no template, `Fixes #2095` on a PR that leaves arrow head size undone, and a "Before (master)" label for a screenshot from the downloaded continuous build. I fixed all three, reran, and it passed again (suite 573 s), then let it through to the PR command. What fought me was the hook: it checks the folder the session started in, so opening the PR from my coursework folder was stopped twice, and I had to run it from a Claude session started inside the avogadrolibs clone. The full suite also makes every gate run about 8 to 10 minutes, so each edit to the description costs one.

**Unit 12: PR monitor and a playbook written from avogadrolibs' own review times**

I installed the PR monitor and wrote a playbook with a first-response threshold of 3 days, 7 days after approval, 5 days for a stalled review, one nudge, and walk-away cases, using a count of five merged outside-contributor PRs (typical first response under 2 days, one at 11 days). My first draft of the playbook had a 3-day staleness threshold next to "no nudge for a month", which would have let the monitor call a PR stale and then forbid the nudge, and I rewrote it so every threshold leads to the one nudge. The monitor read PR #3370 (approved, 22 checks passing, mergeable, no changes requested) and drafted a wait until 2026-11-24, citing my 7-day rule, plus an optional "thanks for testing it" that assumed the maintainer had tested the change, which the thread does not say. I did not post the optional thanks and nothing from the draft went on the PR. It fell short because my PR had no review to answer, so I only exercised the wait path, not a reply or a nudge, and the monitor said NO PR YET when I first ran `--state` from my coursework folder instead of the avogadrolibs clone.

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

Issue #2095 is a feature request, not a bug. In Avogadro 2 you can switch on the Force display type to draw an arrow on each atom for the force acting on it, but you cannot change how those arrows look. Every other display type lets you change its settings, and Force does not. The issue asks for arrow color, length, width and head size.

**Expected Behavior**

Selecting Force should show a settings panel, like the other display types, where I can set the arrow color, length and width, and the arrows should redraw straight away. The values should be remembered, and the defaults should look the same as the arrows do today. Head size is the fourth setting in the issue. I said in my claim comment that I would do it in a follow-up, so it is not part of this change.

**Current Behavior**

With Force ticked, green arrows are drawn at the length of the raw force vector. The "Force Settings" panel is empty, and Force has no "..." button, unlike Ball and Stick, Cartoons, Close Contacts, Crystal Lattice and Labels. Nothing in the app changes the arrow color, length or width. I saw this in the continuous build with `raman.cjson` (the Reproduction Process section has the steps).

**Affected Components**

- `avogadro/qtplugins/force/force.h` and `force.cpp`: the `Force` scene plugin. `Force::process()` draws each arrow from `pos1` to `pos1 + forceVector` and never sets a color or size, and the plugin has no settings widget. These are the only files I changed.
- `avogadro/qtgui/sceneplugin.h`: `setupWidget()` and `hasSetupWidget()` are the hooks the app uses to fill the settings dock.
- `avogadro/rendering/arrowgeometry.h`: it already has `setColor` and `setRadiusScale`, so no rendering change was needed.
- `avogadro/qtplugins/crystal/crystalscene.cpp`: the existing example of a scene plugin with saved settings (`QSettings`, a lazily built widget, slots that redraw). The maintainer pointed to it in the issue, and I copied its pattern.

**Toolkit**

- Tool: Claude Code in the avogadrolibs clone, in explain-and-review mode, reading `force.cpp`, `sceneplugin.h`, `arrowgeometry.h` and `crystalscene.cpp` with me; repro-check graded the claim and the reproduction.
- What it produced: an account of how a scene plugin gets a settings dock, the finding that `ArrowGeometry` already supports color and width, and an accepted repro report.
- Difficulties: I did not know C++ or Qt, so each term (`private slots`, `QSettings`, `setupWidget`) had to be explained before I could follow the files. It also said once that Crystal pre-fills its color button, which was wrong, and I had to check that against the file.
- What changed: I read the file I am copying before relying on any claim about it, and I wrote the Affected Components from the code, not from the issue's description.

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

Done since (2026-11-16):

7. Re-checked the arrows in the app I built from `f62ee3ae`, before and after, and recorded the result in the PR description (see Testing Strategy).
8. Opened the PR against `OpenChemistry/avogadrolibs` `master` (#3370) with `Refs #2095` and an AI-assistance disclosure.

Not done:

9. An automated test under `tests/qtplugins/`. A draft `forcetest.cpp` exists but does not compile, is not registered and is not in the PR.

Test plan, with the observable result expected after the change:

- Fresh settings (no `force/*` keys): the dock shows Arrow length 1.00, Arrow width 1.00 and a green color button, and the arrows look the same as on master.
- Set Arrow length to 2.00: every arrow doubles in length and the redraw happens immediately. Set it back to 1.00 and they match master again.
- Set Arrow width to 0.50: arrows get thinner, and short arrows stay thin because the width scales each arrow's own radius.
- Pick another color: all arrows change to it.
- Close and reopen the app: the three values and the color are restored from `QSettings`.
- Automated test (step 7): fails on master and passes on the branch, for whichever of the above it can check. If it can't be done for the widget, the PR description will say why.
- The repo's existing suite (155 tests, all passing on master) still passes. Result on `f62ee3ae`: 155 of 155 passed, finished 2026-11-16 00:05 EST.

Unverified (2026-11-16): the dock on fresh settings and restart persistence were not observed, and there is no automated test for the widget.

Deviations: the automated test (step 9) was not added, and the PR says so. The PR uses `Refs #2095` instead of the planned `Fixes #2095`, because arrow head size is left for a follow-up.

**Toolkit**

- Tool: plan-check, run in live mode on `plan.md` and a draft plan comment (`plan-comment.md`, not posted) against issue #2095.
- What it produced: a verdict of accept with all five checks passing (bounded-scope, diagnosis-grounded, executable-by-a-stranger, test-decisive, comment-faithful). Before that, it held the plan and told me to add an observed-before with the app build named, an observable expected-after in the test plan, and an "Unverified" line with a date, and to either record my local-build check or drop it from the comment.
- Difficulties: #2095 is an enhancement, so there was no bug to trace and the "cause" had to be stated as what was missing. I also wrote the plan after most of the code, so the Implementation Plan had to separate what was done from what was left. The build I observed "before" in was easy to describe loosely, and the check would not pass it until the About-dialog version was named.
- What changed: I added the observed-before with the app version, a test plan with expected results, and a dated Unverified line to `plan.md`. I dropped my unverified "works in a local build" claim from the comment, and corrected "155 of 155 on that commit" to say the suite passed on master before my change, since I had not run it on my commit.

---

## Testing Strategy

I re-ran the reproduction steps (raman.cjson, Force display type on) against an app I built from commit `f62ee3ae`, and ran the repo's own checks.

- **Before:** in the downloaded continuous build, the Force Settings dock is empty and the arrows are green with no way to change them.
- **After:** the dock has Arrow length, Arrow width and Arrow color. At length 1.00, width 1.00 and an orange color the arrows are orange; at length 2.00, width 0.50 and cyan they are thinner, cyan and longer. They redraw as soon as a control changes.
- **Repo checks on `f62ee3ae`:** `git clang-format origin/master --diff` made no changes, `cmake --build build` succeeded, and `ctest --test-dir build --output-on-failure` gave `100% tests passed out of 155`. The ship-gate reran all three (suite 573 s) and passed.
- **Not observed:** the dock on fresh settings (the 1.00 screenshot already had a non-default color) and restart persistence of the saved values. The before and after are different builds, so they show what a user sees, not a controlled comparison.
- **No automated test.** The widget is built from Qt controls, my draft `forcetest.cpp` does not compile, and it is not in the PR. The PR says so and asks for a pattern.

**Toolkit**

- Tool: the ship-gate with my `ship-manifest.md`, plus the app itself for the before and after.
- What it produced: pass on formatting, build and the 155-test suite, and a test-evidence check that passed with the unobserved items disclosed.
- Difficulties: the suite takes about 10 minutes per run, and the About dialog's version is set at configure time, so it cannot show that a build includes my change. I confirmed the build by the "Arrow color:" label instead, after an older screenshot showed "Line color:".
- What changed: I stopped using that older screenshot, retook the after screenshots, and wrote the unobserved checks into the evidence rather than claiming them.

---

## Implementation Notes

**2026-11-12 to 2026-11-13: writing the change**

I wrote the code myself, in `force.h` and `force.cpp`, copying the shape of `crystalscene.cpp`. I do not know C++, so Claude explained each piece (what `private slots` means, why the header and the `.cpp` are separate files, what `QSettings` does) and reviewed what I wrote, and I typed every line. The first version had a pile of typos and wrong guesses: `Qwidget` and `m_SetupWidget` spelled differently in two places, `arrows->setColor();(m_color);`, calls to `setLength` and `setArrowSize` on `ArrowGeometry` that do not exist (only `setColor` and `setRadiusScale` do), a missing `QFormLayout` include, and a helper `colorButton()` I never declared, which I deleted. I set the width default to 0.5 first, then changed it to 1.0 because that is what `ArrowGeometry` already draws, so the defaults match today's rendering. I also changed the label "Line color:", copied from Crystal, to "Arrow color:". I committed on 2026-11-13 on `force-arrow-settings` after `git clang-format origin/master` fixed some whitespace and one long line.

**2026-11-14 to 2026-11-15: building so I could see it**

The first build gave me a test suite but no window, because `avogadrolibs` has no app in it; the window comes from `avogadroapp`. So I built three things. The libraries with static plugins in `build/` (for tests), the libraries as shared plugins in `build-app/`, installed to `$HOME/avogadro-dev`, and then `avogadroapp` against that install. Each step failed once: no `cmake`, no GoogleTest, then Spglib and JKQTPlotter needing to be turned off (`USE_SPGLIB`, `USE_PLOTTER`, `USE_LIBMSYM`, `USE_LIBARCHIVE` set to OFF), then the install failing on `../fragments/polymers` until I cloned the `fragments`, `molecules` and `crystals` repos next to it, and avogadroapp needing `-DBUILD_SHARED_LIBS=ON`. At one point I asked whether the first build had been pointless if I could not see my work; it was not, it is the one the tests run on. A VM or container would have hidden these problems, not removed them.

**2026-11-15: checking it in the app, and what I decided**

The dock showed Arrow length, Arrow width and Arrow color, and changing them redrew the arrows at once. Two things confused me. A short arrow stayed thin when I lowered the width: the radius is 0.02 times each arrow's own length times the width setting, so the width scales with the arrow, which is how `ArrowGeometry` works. And the unchecked boxes looked different in my build from the continuous build, which I put down to the Qt version (I did not confirm that). I checked that the saved values reached the settings file (`force.length` and so on in the macOS plist), but I did not watch them restore after a restart on fresh settings, so I left that out of the evidence. I also decided to scale the force vector by the length setting, not to change the arrow geometry, so the arrow still shows the relative size of the force at any length.

**2026-11-15 to 2026-11-16: the test I did not finish**

I started `tests/qtplugins/forcetest.cpp` from the BallAndStick test, to check that a setting is saved and the display redraws, not that the force is right, since I only wanted to test my own change. It does not compile: the class name is lowercase, a semicolon is missing, `buildMolecule();` is left over, and it calls `setLength`, which is a private slot, so a test cannot call it directly and would have to go through the spin box. It is not registered in `tests/qtplugins/CMakeLists.txt` and it is not in the commit. I chose to open the PR without a test and say so, and ask for a pattern.

**2026-11-16: checks and PR**

`git clang-format origin/master --diff` was clean, `cmake --build build` succeeded and `ctest` passed 155 of 155 (finished 00:05 EST). I ran `plan-check` three times on `plan.md` and `plan-comment.md`: the first rejected the plan for having no observed-before, a vague test plan and a "works in a local build" claim the plan did not back, and the next two accepted after I fixed those. One thing I got wrong: I attributed the "before" to a build I compiled, when it came from the continuous build, and Claude caught it when the version numbers did not match. I fixed the wording. I opened PR #3370 after the ship-gate passed.

**2026-11-17: review**

ghutchis approved with "LGTM, thanks" and asked for nothing. I have not yet replied on the issue thread, and my "this weekend" update there is now out of date.

**Toolkit**

- Tool: Claude Code in the avogadrolibs clone, in explain-and-review mode only (my `CLAUDE.local.md` rules), with the ship-gate and plan-check around it.
- What it produced: explanations of the C++ and Qt pieces, line-by-line review of my edits, the build and install recipe, and the dated record above.
- Difficulties: reviews found my typos one round at a time, and the local build took several failed tries before it worked. It also made two wrong claims that I had to catch: that Crystal pre-fills its color button (it does not), and that the "before" came from a build I compiled.
- What changed: I check claims against the file I am copying before I rely on them, and I name which build every observation came from.

---

## Pull Request

**PR Link:** https://github.com/OpenChemistry/avogadrolibs/pull/3370

**PR Description:** "Add arrow length, width and color settings to the Force display type", from `KJhenelle:force-arrow-settings` to `master`. It changes `force.h` and `force.cpp` only: a settings widget with arrow length, width and color, saved with `QSettings` and applied in `process()`, with defaults equal to the old rendering. It says what is not in the PR (arrow head size), shows the before and after, lists the clang-format, build and 155-test results, says no automated test is included and why, and has an AI-assistance section. It uses `Refs #2095`, not `Fixes`, because head size is left for a follow-up.

**Maintainer Feedback:**

- 2026-11-17: ghutchis (maintainer) reviewed: "Thanks. Code looks good - I'll wait until I can test it personally before I approve. (Should work fine, but some GUI testing is needed.)" Later the same day he approved: "LGTM, thanks". No changes were requested.
- 2026-11-17: I made no code changes and have not replied on the thread; nothing was asked of me. CI on the PR shows 22 checks passing and 6 skipped, and the PR is mergeable.

**Status:** Awaiting review (approved by the maintainer on 2026-11-17, waiting for him to merge).

**Toolkit**

- Tool: pr-precheck inside the ship-gate, run in live mode on the branch and `pr_draft.md`, then the PR opened from a Claude session inside the clone.
- What it produced: two passes on five checks (plan-fidelity, test-evidence, diff-reviewability, template-and-standards, ai-disclosure). The first run's notes led to three fixes in the description.
- Difficulties: the gate hook checks the folder the session started in, so it stopped the PR command from my coursework folder; it also only lets the PR through for 30 minutes without changes. It cannot check that screenshots are attached.
- What changed: I removed the false template/DCO line, switched to `Refs #2095`, and named the continuous build as the source of the "before".

---

## Learnings and Reflections

**Technical Skills Gained**

I learned how a C++/Qt scene plugin gets a settings dock: a `setupWidget()` override that builds the widget once, `private slots` that update a member, call `emit drawablesChanged()` to redraw, and save to `QSettings`, with the saved values loaded in the constructor. I learned that `avogadrolibs` has no window of its own, so seeing my change meant building `avogadroapp` against an installed copy of the libraries, and that the library version in the About dialog is set when CMake configures, so it cannot prove a build includes my change. I also learned how this repo checks work: `git clang-format origin/master --diff`, a CMake/Ninja build, and a 155-test `ctest` run that takes about 10 minutes. Last, I learned the Developer's Certificate of Origin: a `Signed-off-by:` line on every commit, which the DCO bot checks, and which my first commit lacked.

**Challenges Overcome**

The build was the hardest part: no `cmake`, no GoogleTest, Spglib and JKQTPlotter that had to be turned off, an install that failed until I cloned the `fragments`, `molecules` and `crystals` repos beside it, and `avogadroapp` needing `-DBUILD_SHARED_LIBS=ON`. I fixed each failure one at a time, and the Implementation Notes record them. Writing C++ without knowing it was the second: my first version had mismatched names, a call to `setLength` and `setArrowSize` on `ArrowGeometry` that do not exist, and a helper I never declared, and I fixed them by reading `arrowgeometry.h` and getting my edits reviewed. Third was getting my evidence right. I attributed the "before" to a build I compiled when it came from the continuous build, I almost used an old screenshot that showed "Line color:" instead of "Arrow color:", and my first commit failed the DCO check, so I amended it with `git commit -s` and force-pushed. I did not manage to write a working automated test. `forcetest.cpp` does not compile, so the PR says there is no test.

**What I'd Do Differently Next Time**

I would read the repo's PR requirements before I commit, including how the DCO bot works, so my first commit is signed and I do not need an amend and a force-push on an open PR. I would write the plan and the evidence as I work, not afterwards, because I wrote `plan.md` after most of the code and had to separate what was done from what was left. I would record which build every screenshot comes from at the moment I take it. I would also get a small test working earlier, or ask the maintainer for a pattern before I wrote the change, so the PR does not have to say there is no test.

---

## Resources Used

- `avogadro/qtplugins/crystal/crystalscene.cpp` in avogadrolibs: the pattern I copied for the settings widget and `QSettings`.
- Issue #2095, https://github.com/OpenChemistry/avogadrolibs/issues/2095: the maintainer's comment naming `force.cpp` and `crystalscene.cpp` told me where to start.
- `.github/workflows/build_mac.yml` in avogadrolibs: the source-build steps, since the build guide linked from `AGENTS.md` (https://two.avogadro.cc/develop/build.html) returned a 404.
- `CONTRIBUTING.md` and `AGENTS.md` in avogadrolibs: the AI policy (levels 0 and 1), the `master` branch, and the full-name rule for commits.
- ghutchis, the maintainer: he reviewed and approved the PR within a day.
