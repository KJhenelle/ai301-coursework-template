# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

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

## Things I never post

- Generic AI boilerplate ("Certainly!", "I hope this helps!", "Let me know if you need anything else!").
- Vague claims without logs ("Confirmed, seeing the same thing on my machine").
- Premature pull request promises before a bug has been cleanly reproduced.
- Flattery, conversational filler, or apologies for asking clarifying questions.
- Unverified root cause assertions based solely on reading the code without executing it.