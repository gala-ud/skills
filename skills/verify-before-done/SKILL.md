---
name: verify-before-done
description: Before saying a task is done, fixed or working, prove it. List the claims the reply is about to make, run a check for each one on the final state of the code, and report each as verified, failed or not verified with the command and its output. Use at the end of a coding or ops task before reporting completion, and when the user asks "does it work", "did you test it", "are you sure", "verify this" or "prove it". Skip for explanation or planning with nothing to run, and for a read-through of a diff before commit (that is a review, not a run).
license: MIT
metadata:
  author: gala-ud
  version: 0.1.0
---

# Verify before done

"Done, all tests pass" is often written from memory: the tests ran before
the last edit, or a different test ran, or nothing ran. A claim counts only
with a check that would fail if it were false, run after the last change.

## Process

1. **Write down the claims** your final reply would make, as a list.
   Claim 1 is the user's request in their own words. Add every other
   statement that could be false: "existing tests still pass", "it builds",
   "no other callers", "the migration can be rolled back", "docs updated".

2. **Pick a check for each claim**: the strongest one available that would
   fail if the claim were false. From strongest to weakest:
   1. run what the user would run (the command, the request, the page);
   2. a test aimed at the claim;
   3. the full test suite, build or type-check;
   4. a search (for claims such as "no other callers");
   5. reading the code. This one is labelled "read only" in the report.

3. **Show before and after for claim 1**, for a fix and for new behavior
   alike. Run the same command on the code as it was (`git stash`, or run
   it before you edit) and on the final code, and put both in the result:
   "ValueError before, 90 after". If you cannot, write "not run before
   the change".

4. **Run every check on the final state.** An edit made after a check
   cancels every check that edit could affect; run those again.

5. **Read the output, not the exit code.** Count the tests that ran: zero
   tests, the wrong file, or new skips are a failure. Note warnings.

6. **Check next door once**: the wider suite or the callers' tests. A
   failure there is either caused by the change or was there before. Find
   out which by running the same test on the code before the change
   (`git stash`, or the base commit); otherwise write "unconfirmed".

7. **Report** in the format below. The status line is one of these three,
   word for word, with nothing added:
   - **Done**: every claim verified.
   - **Done, with unverified parts**: nothing failed, something not verified.
   - **Not done**: any claim failed.
   A failure confirmed to predate the change does not alter the status. It
   goes on its own line under the table, and the claim it touches is worded
   to exclude it ("no test that passed before fails now").

## Report

```markdown
**Status: Done, with unverified parts**

| # | Claim | Check | Result |
|---|---|---|---|
| 1 | "Login no longer returns 500 on an empty password" | `curl -s -o /dev/null -w '%{http_code}' -d 'user=a&password=' localhost:8000/login` | verified: 500 before, 400 after |
| 2 | Existing tests still pass | `pytest -q` | verified: 212 passed, 3 skipped (the same 3 as before) |
| 3 | Works on Postgres | none | NOT VERIFIED: only SQLite is available here |

**To check what I could not:** `DATABASE_URL=postgres://... pytest tests/test_login.py`
**Failures that were there before:** <test and how you confirmed it, or "none">
```

For a one-line task the report can be one line:
`Verified: <command> -> <the line of output that shows it>`.

## Rules

- **No claim without its row.** "Should work", "this fixes it", "all tests
  pass", "works now" and check marks appear only next to a command run in
  this session and what it printed.
- **Quote, do not paraphrase.** Give the line of output that decides the
  result, such as the suite's own summary line. Never write output you did
  not see. A row whose output shows a failure is not "verified".
- **Rows are claims, not a to-do list.** Something you chose not to build
  is not NOT VERIFIED; say it in a sentence outside the table.
- **Cannot run it? Say so.** No environment, credentials or network, or a
  check that would be destructive: the row reads NOT VERIFIED with the
  reason and the exact command the user can run.
- **Never make a check pass by weakening it**: editing a test to match the
  code, skipping it, mocking the thing under test, catching the error, or
  narrowing the selection until it is green.
- **A failure leads the reply.** Do not bury it in the last row.
- **Nothing destructive or visible to others** (production, real emails,
  payments, deleting data) is run as a check unless the user asked for it.
- **Behavior needs a behavior check.** A type-check or a build does not
  verify that a page renders or an endpoint answers.
- **Long suites.** If the full run takes more than about ten minutes, run
  the targeted tests and report the full suite as not verified.
