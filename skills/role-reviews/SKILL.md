---
name: role-reviews
description: Review a change (diff, pull request, branch) or a plan from five roles in turn (product, design, engineering, QA, security), each asking its own questions, and merge the results into one ship decision with located findings. Use when the user asks for a full, team-style, cross-functional or multi-perspective review, a go/no-go or pre-merge check of a feature, or wants a plan or spec challenged from several angles before building. Skip for a narrow request (find the bug in one function, a security-only audit, a style or naming review), for a quick check of your own diff before committing, and when the user asks to fix the code rather than review it.
license: MIT
metadata:
  author: gala-ud
  version: 0.1.0
---

# Role reviews

Five roles find five kinds of problem, but only if each asks its own
questions; otherwise one remark comes back five times in different voices.
This is one read-only pass that ends in one decision.

## Process

1. **Get the material.** For a change: the full diff and the files it
   touches. For a plan: the whole document. Read the request, ticket or
   spec the work answers; if there is none, state in one line what you
   take its goal to be. List what you could not see or run.

2. **Go through the roles in this order.** A role with no surface in the
   material is "n/a" with the reason (Design on a migration script).
   - **Product**: Does this solve the stated problem for the stated user?
     What is in it that nobody asked for, and what was asked for and is
     absent? What existing behavior or default changes for current users?
   - **Design**: Walk the flow a user takes through whatever they see:
     screens, CLI output, error text, emails. Are the empty, loading and
     error states handled? Does each message say what happened and what to
     do next? Does it match the patterns already in the product?
   - **Engineering**: What happens on empty, huge, duplicate and concurrent
     input, and when a dependency fails? Can it be rolled back, data
     included? Does it follow how the codebase already does this?
   - **QA**: What shows that it works? Would each new test fail without
     the change? Which reachable paths have no test? Which neighboring
     behavior could it break? Name the three cases most worth running.
   - **Security**: What new input crosses a trust boundary? Is every new
     action checked for who may do it and on whose data? What reaches
     logs, responses or third parties? Any secrets or new dependencies?
   For a plan, each role asks the same questions of what the plan says
   will exist, and QA asks how each step will be verified.

3. **Write findings.** Each has a location (`file:line`, or the plan
   section), what goes wrong and for whom, and a fix. Severity is **Block**
   (data loss, a security hole, the stated goal not met, or something that
   cannot be undone after release), **Fix** (wrong in a case that will
   happen) or **Note** (optional). Report every Block. Beyond those, at
   most three findings per role, the most severe first; name the rest in
   the "Also" line.

4. **Remove overlap.** Report each problem once, under the role whose
   question exposes it: a missing permission check is Security, a missing
   test is QA, a confusing error is Design, an unrequested feature Product.

5. **Verify.** Reopen every cited location and delete any finding the text
   there does not support.

6. **Decide by rule**: any Block gives "Do not ship"; otherwise any Fix
   gives "Fix first"; otherwise "Ship". For a plan the same three read "Do
   not build", "Fix first" and "Build". Reply in the format below.

## Output

```markdown
## Review: <change or plan>
Goal: <one line, "assumed" if no ticket or spec>
Material: <what was read; "author: this session" if you wrote it>

**Decision: Do not ship** - <the finding that decides it>. Not judged: <roles, or "none">

| Role | Verdict | Reason |
|---|---|---|
| Product | Pass | Matches the ticket; no extras |
| Design | n/a | No user-facing surface |
| Engineering | Fix | Retry loop has no upper bound |
| QA | Not judged | Tests exist but could not be run |
| Security | Block | Export endpoint skips the owner check |

### Findings
1. **Block - Security** `api/export.py:42`: any signed-in user can export
   another account's invoices. Fix: load it via `current_user.accounts`.

**Also:** <findings beyond the limit, a few words each; omit if none>
**Not checked:** <files, callers, environments or runs you did not see>
```

## Rules

- **Verdicts**: Block, Fix, Pass, n/a or Not judged. A role's verdict is
  its worst finding. Pass means the material answered the role's questions;
  when it cannot answer them, the verdict is Not judged, never Pass.
- **No theater**: no first-person role-play, scores, praise section or
  summary of what the change does.
- **Read-only.** Do not edit code or rewrite the plan unless asked. Asked
  to "fix it": apply the listed Block and Fix items and nothing else.
- **Your own work**: if you wrote the change in this session, say so in the
  Material line and review the diff on disk, not your memory of it.
- The user's own role list or gates replace these defaults.
