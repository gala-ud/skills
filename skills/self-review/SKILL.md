---
name: self-review
description: Before you commit, open a pull request, or say work is done, review your own diff as a skeptical reviewer. Use after finishing any code change beyond a typo, comment or version bump, and when the user asks to double-check or sanity-check changes you just made in this session. Not for reviewing other people's code or pull requests.
license: MIT
metadata:
  author: gala-ud
  version: 0.2.0
---

# Self-review

The author of a change is the person least likely to see its flaws. Before
calling work done, read the diff as someone who did not write it and does not
trust it.

## Process

1. **Get the real diff.** Run `git status` and `git diff` (plus
   `git diff --staged`). Review what changed on disk, not what you remember
   changing. Untracked files count.

2. **Re-read the request.** Restate in one sentence what was asked. Everything
   in the diff must serve that sentence.

3. **Go through the checklist** below, file by file.

4. **Run the checks.** Build, tests, linter, and the changed behavior itself.
   Never write "tests pass" without having run them in this session.

5. **Fix what you find**, then repeat from step 1 for the fixes. If you cannot
   fix something now, it goes under "Open problems" in the report.

6. **Report** using the format at the end.

## Checklist

**Scope**
- Does every changed line serve the request? Revert drive-by edits, renames,
  config changes and reformatting.
- Is anything from the request missing?

**Correctness**
- Empty, null, zero, negative, one, many: what happens at each?
- What happens when the network, the file, or the other service fails?
- Is anything run twice safe to run twice?
- Do changed names and signatures match every caller, including files outside
  the diff? Search for them.

**Data**
- Can this lose or corrupt existing data? Does a migration have a way back?
- Is user input validated where it enters the system?

**Leftovers**
- Debug output, commented-out code, TODOs you added, temporary files.
- Secrets, keys, tokens, personal paths.
- New dependencies: is each one needed and did the user agree to it?

**Tests**
- Would each new test fail without the change? A test that passes either way
  proves nothing.
- Did you change, skip or delete a test to make it pass? Restore it.

## Rules

- **Evidence over confidence.** A claim that something works needs a command
  and its output, or it is listed as not verified.
- **Do not weaken checks to pass them.** No skipped tests, loosened
  assertions, or disabled lint rules to get a green run.
- **A known defect is not "not verified".** Bugs you found and did not fix go
  under "Open problems", stated as defects, worst first.
- **Not ready means say so first.** If open problems remain, the report opens
  with "Not ready to commit" and the reason.
- **Small leftovers get fixed, not reported.** Ask the user only about choices
  that change behavior.

## Report format

```markdown
**Changed:** <one sentence>
**Fixed in review:** <what you found and fixed>, or "nothing"
**Open problems:** <defects still in the diff, worst first>, or "none"
**Verified:** <command> -> <result>, ...
**Not verified:** <what you could not check and why>, or "nothing"
**Needs your decision:** <choices only the user can make>, or "nothing"
```
