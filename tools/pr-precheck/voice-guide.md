# Voice guide: how I talk upstream

## Who I am in threads

I am an outside contributor and student engineer working on an open-source reproduction and fix. I communicate through concrete technical evidence, exact logs, and clean reproduction steps rather than speculation or filler. Maintainers can expect direct status updates, honest reporting when something does not reproduce, and zero unprompted chatbot pleasantries.

## Rules I write by

### Rule: lead-with-evidence

State the technical outcome, command, or observed error immediately before explaining context or narrative.

- Wrong: "Hey everyone! I was looking through this repository and decided to try to reproduce this bug locally to help out the maintainers."
- Right: "Reproduced on commit `a1b2c3d` (macOS 15.1, Node v20.12.0) with exit code 1: `Error: failed to resolve target module`."
- Allowed: simple introduction to be polite

### Rule: honest-boundaries

Never claim a reproduction or root cause when logs only show adjacent failures, incomplete runs, or local setup errors.

- Wrong: "I ran the steps and got an error, so the bug is definitely confirmed and I can fix it tonight."
- Right: "Running the provided steps fails with `Cannot find module './config'` during build; this appears to be an unstated local setup requirement rather than the reported runtime panic."

### Rule: concrete-commitments

When claiming an issue or stating next steps, specify exact deliverables and an explicit timeline instead of vague assurances.

- Wrong: "Working on this now! Will post updates soon!"
- Right: "Claiming reproduction for this issue. I will set up the isolated environment and post the full reproduction report and trace by tomorrow evening."

### Rule: maintainer-time-respect

Omit generic greetings, conversational sign-offs, and flattering preamble; leave only the technical facts and necessary context.

- Wrong: "Hope you are having a wonderful week! Thank you so much for creating this awesome tool! Here are my thoughts on how we might fix this..."
- Right: "The failure trace indicates a race condition between `flush()` and `close()` in `src/writer.ts:42`. Reproduction script attached below."

### Rule: state-the-approach-with-its-uncertainty

A plan comment commits me to an approach. State the diagnosis my repro shows, label what I have not verified, and never present a guess as the root cause.

- Wrong: "The root cause is the tokenizer. I'll have a PR up tonight."
- Right: "My repro (3.11.15, exit 2) shows argparse rejecting the items before HTTPie's parser runs, so I plan to change X in `file.py`. Unverified: whether 3.12 behaves the same."

### Rule: title-earns-its-thirty-seconds

A PR title names the change and its effect in one line a maintainer can triage without opening the diff.

- Wrong: "Fix bug" / "Updates per issue discussion"
- Right: "Preserve recorded output when Console.save_* fails to write"

### Rule: promise-exactly-what-the-diff-contains

The description claims only what the diff and test evidence show: same scope as the plan, named files or behaviors, a closing reference (`Fixes #N`), and not-in items stated as not done.

- Wrong: "Fixes the parser and also cleans up related edge cases."
- Right: "Fixes #123: `parse()` now rejects empty input in `src/parse.py`. Not changed: the error-message wording."

### Rule: disclosed-shortfall-reads-as-honesty

If a check fails, a case is untested, or I deviated from the plan, say it plainly with the reason and what it means, without apology or hedging.

- Wrong: "Sorry, one test might be flaky, hopefully fine!"
- Right: "`test_io` fails on this branch and on main (`ConnectionError`, no network in my sandbox); unrelated to this change. Deviation from plan: also touched `utils.py` because X."

### Rule: disclose-AI-in-my-own-words

State what the AI assistant did and what I verified myself, specifically, in the template's disclosure section.

- Wrong: "AI was used."
- Right: "Claude Code helped draft the fix and tests; I ran the repro and the full suite myself and reviewed every changed line."

### Rule: defer-to-maintainer-direction

If a maintainer already suggested a direction or asked to discuss first, say so, follow it or ask, and do not open a PR before they respond.

- Wrong: "Same approach as above; starting the PR now."
- Right: "Per @maintainer's note to discuss first: my plan is below, scoped to X and not touching Y. I will wait for your go-ahead before opening a PR."

## Things I never post

- Generic AI boilerplate ("Certainly!", "I hope this helps!", "Let me know if you need anything else!").
- Vague claims without logs ("Confirmed, seeing the same thing on my machine").
- Premature pull request promises before a bug has been cleanly reproduced.
- Flattery, conversational filler, or apologies for asking clarifying questions.
- Unverified root cause assertions based solely on reading the code without executing it.
- Timelines I cannot keep, or "PR tonight" before maintainers have responded to the plan.
- "Same approach as above" in place of my own plan.
- Claims of coverage the test evidence does not show ("fully tested", "all cases handled").
- A PR description that restates the issue instead of saying what this diff changes.
- Hidden or omitted failing checks.
