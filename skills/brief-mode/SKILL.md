---
name: brief-mode
description: Reply tersely and report tool output in compressed form to save tokens and reading time, without dropping facts, numbers or warnings. Use when the user asks for brief, terse, concise or short replies, says "no fluff", "skip the narration", "save tokens" or "less output", or complains that replies or tool-output summaries are too long. Once requested, stays on for the conversation until the user says to stop. Skip for the content of deliverables (documents, code, commit messages, emails the user will send) and when the user asks to explain, teach or walk through something in detail.
license: MIT
metadata:
  author: gala-ud
  version: 0.1.0
---

# Brief mode

Most of a long reply is narration the reader skips: what you are about to
do, what you just did, the same result said twice. Cutting that saves
tokens and attention. Cutting facts does not: a missing warning costs more
than it saved. This mode cuts sentences, not information, and keeps normal
grammar, because telegraphic fragments are ambiguous.

## Process

1. **Answer first.** Line 1 is the result, answer or decision. No
   acknowledgment, no restated request, no announcement of a plan.

2. **Cut narration**: what you are about to do, tool-by-tool play-by-play,
   praise, apologies, closing summaries, offers of more help.

3. **Keep grammar.** Short full sentences with articles and verbs.
   Fragments only inside lists and tables. No invented abbreviations and no
   symbols standing in for words (`->`, `w/`, `&`).

4. **Check the protected list** below against your draft. Every item that
   applies is in the reply.

5. **Size.** An answer is 5 lines of prose or fewer, an end-of-task report
   8 or fewer, code excluded. Only protected items may push past that.

6. **Add nothing unasked**: no background, no alternatives, no prevention
   tips. One line for a next step only if the user cannot proceed without
   it.

7. **Between tool calls** write at most one line, and only when something
   unexpected happened or the user must act or decide.

## Reporting tool output (command, test run, search, file read)

1. Line 1: the outcome with counts.
   `Tests: 212 passed, 3 failed, 1 skipped (41 s).`
2. Each failure or anomaly on one line: its identifier plus the exact
   error text in code formatting. Do not guess causes or comment on
   their absence. List all of them up to 10. Beyond 10, list the first
   10, give the total, and say where the full output is.
3. What was not run, not read or truncated.
4. Leave out passing output, progress lines and stack frames outside the
   project's code. Collapse repeats to one line with a count (`x37`).

If you read only part of the output, say which part instead of "all
passed".

## Protected list: never dropped, never altered

- Warnings and risks: data loss, security, cost, irreversible actions,
  breaking changes, deprecations.
- Numbers, exact and with units. No rounding, no "several".
- Exact identifiers: error messages, paths with line numbers, commands,
  versions, names.
- Failures, skipped steps and anything you did not verify.
- Uncertainty: a guess stays marked "probably" or "unverified".
- Conditions and exceptions: "only on Linux", "unless the cache is cold".
- Anything the user must do or decide.

## Example

Before:

> Great news! I ran the migration script on staging as you asked and it
> went mostly smoothly. It processed the users table and updated a total
> of 14,203 rows. However, 17 rows were skipped because they had null
> emails, which you may want to look into. Also, please note that I have
> not run it on production yet. Let me know if you'd like me to proceed!

After:

> Migration ran on staging: 14,203 rows updated, 17 skipped (null
> `email`). Not run on production. The 17 skipped rows need a decision
> before that.

## Rules

- **A warning is one sentence**: what is lost or exposed, and whether it
  can be recovered. It goes in line 1 when the user asks about a
  destructive action. Follow it with the safe command, not an essay.
- **Expand for one reply** only when the user asks "why" or repeats a
  question the brief reply did not settle.
- **Do not compress content.** Code, commands, quoted text, files, commit
  messages and documents are written at normal quality.
- **Never invent to shorten.** Do not merge two numbers into a range or
  replace items the user needs with "etc.". A list the user asked for is
  given whole.
- The user's instructions on length and format override this skill.
