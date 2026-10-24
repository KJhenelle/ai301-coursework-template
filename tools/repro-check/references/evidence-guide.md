# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

### Where it lives
* **Eval bundle:** Inside the repro report under the `Environment`, `System Info`, or `Configuration` block; compared directly against the issue context's stated runtime, OS, or dependency versions.
* **Live mode:** In the user's reproduction draft under the environment section, verified against the repository's setup documentation and the issue thread's original bug report.

### What good looks like
The report explicitly lists the exact OS, runtime/compiler version, package versions, and relevant target tool flags. If the testing environment differs in major or minor version from the target described in the issue, the divergence is explicitly stated alongside a justification for why the behavior remains comparable.

## Steps

### Where it lives
* **Eval bundle:** Inside the repro report under `Steps to Reproduce`, `Reproduction Procedure`, or the initial numbered setup commands.
* **Live mode:** In the reproduction comment draft, read directly against the target repository's directory structure and build scripts.

### What good looks like
The steps form an unbroken, ordered sequence starting from a known clean state (e.g., specific commit SHA, empty directory, or default template) to the trigger command. Every command, input argument, file edit, or configuration flag is written out completely, requiring no unstated global installs, undocumented flags, or guesswork to reach the reproduction point.

## Behavior shown

### Where it lives
* **Eval bundle:** Inside the repro report's `Observed Behavior`, `Terminal Output`, `Logs`, or `Artifacts` section, cross-referenced with the error logs, exit codes, or misbehaviors cited in the issue context.
* **Live mode:** In the terminal transcript, error trace, or diff excerpts within the draft comment, evaluated against the symptoms and bug descriptions reported on the GitHub issue thread.

### What good looks like
The captured artifact exhibits the exact failure mode, error string, panic, or faulty output described in the original issue report. Output that fails with a missing module, local syntax typo, permission denial, or build failure unrelated to the target bug is a failure to match behavior.

## Honesty

### Where it lives
* **Eval bundle:** The repro report's `Verdict`, `Conclusion`, or `Result` line compared directly against the raw logs in the artifact section.
* **Live mode:** The summary assertion in the draft comment compared against the attached execution output.

### What good looks like
The stated outcome matches the artifact. If the issue did not manifest, the report explicitly states "Cannot reproduce" and documents the clean run rather than claiming a successful repro. If the bug reproduced partially or required workarounds, the boundaries are stated plainly without overclaiming resolution or root cause certainty.

## Comms

### Where it lives
* **Eval bundle:** The `Claim Comment` and final comment body read against the `repo-facts` block and the original issue prompt.
* **Live mode:** The text of the claim comment or pull request comment read against the target repository's `CONTRIBUTING.md`, issue templates, code of conduct, and mandatory AI-disclosure policies.

### What good looks like
The claim names the targeted behavior, specifies planned next steps, and commits to a reproduction timeline without boilerplate placeholders. All generated text adheres to repository conventions (including template headers and explicit AI-assistance disclosures where required), avoids generic chatbot preamble, and addresses the maintainers directly and concisely.