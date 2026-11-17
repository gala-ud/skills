---
name: self-review
description: Review your own diff as a skeptical reviewer before committing or reporting work as done. Use after finishing a code change and before any commit, pull request, or "done" message; also when the user asks to review, double-check, or sanity-check changes you just made.
license: MIT
metadata:
  author: gala-ud
  version: 0.1.0
---

# Self-review

The author of a change is the person least likely to see its flaws. Before
calling work done, read the diff as someone who did not write it and does not
trust it.

## Process

1. **Get the real diff.** Run `git status` and `git diff` (plus
   `git diff --staged`). Review what changed on disk, not what you remember
   changing.

2. **Re-read the request.** Restate in one sentence what was asked. Everything
   in the diff must serve that sentence.

3. **Go through the checklist** below, file by file.

4. **Run the checks.** Build, tests, linter, and the changed behavior itself.
   Paste the commands and their real results. Never write "tests pass" without
   having run them in this session.

5. **Fix what you find**, then repeat from step 1 for the fixes.

6. **Report** using the format at the end.

## Checklist

**Scope**
- Does every changed line serve the request? Revert drive-by edits, renames
  and reformatting.
- Is anything from the request missing?

**Correctness**
- Empty, null, zero, one, many: what happens at each?
- What happens when the network, the file, or the other service fails?
- Is anything run twice safe to run twice?
- Do changed function signatures match every caller?

**Data**
- Can this lose or corrupt existing data? Does a migration have a way back?
- Is user input validated where it enters the system?

**Leftovers**
- Debug output, commented-out code, TODOs you added, temporary files.
- Secrets, keys, tokens, personal paths.
- New dependencies: is each one needed and did the user agree to it?

**Tests**
- Does a test fail without the change and pass with it?
- Did you change or delete a test to make it pass? If so, justify it or undo it.

**Readability**
- Would a stranger understand each change without this conversation?
- Do comments explain why, not what?

## Rules

- **Evidence over confidence.** A claim that something works needs a command
  and its output, or it is labeled "not verified".
- **Do not weaken checks to pass them.** No skipped tests, loosened
  assertions, or disabled lint rules to get a green run.
- **Say what you did not check** and why.
- **Small leftovers get fixed, not reported.** Report only what needs a
  decision from the user.

## Report format

```markdown
**Changed:** <one sentence>
**Verified:** <command> -> <result>, ...
**Not verified:** <what and why>, or "nothing"
**Needs your decision:** <items>, or "nothing"
```
