---
name: plan-first
description: Write a short step-by-step implementation plan and get it accepted before changing code. Use once what to build is clear, for any change that touches more than one source file, needs more than about three distinct edits, adds a dependency, or changes a data schema or public interface; also when the user asks to plan, outline an approach, or "think before coding". Skip for small single-purpose edits confined to one file (typos, version bumps, one-function fixes), even if a lockfile changes too. If scope is still open, use idea-to-spec first.
license: MIT
metadata:
  author: gala-ud
  version: 0.2.0
---

# Plan first

Code written without a plan gets rewritten. A plan costs a minute to read and
is the cheapest place to catch a wrong approach.

## Process

1. **Read before planning.** Open the files the change will touch and one
   level of what calls them. Find how the project already solves similar
   problems and follow that pattern. Note the test and build commands. Say
   what you have not read yet.

2. **State the goal in one sentence** and list what is explicitly out of
   scope. If a spec exists, link it instead of restating it.

3. **Write the plan** using the template below.

4. **Show the plan and wait.** Start coding only after the user accepts it.
   If the user has said to proceed without asking, show the plan and continue,
   except for held steps (see the rules).

5. **Follow the plan.** If reality disagrees with it, stop, say what changed,
   and update the plan before continuing. Do not silently improvise.

## Template

```markdown
## Goal
One sentence. Out of scope: ...

## Approach
2-4 sentences: the chosen approach and the main alternative you rejected,
with the reason.

## Steps
1. <verb> <what> in `<file>`. Check: <command or observation>
2. ...

## Risks
- <what could go wrong> -> <how you will notice> -> <fallback>

## Not sure about
- Up to three questions that would change the plan, each with your default.
```

## Rules for steps

- **Each step leaves the project working.** Build and tests pass after every
  step, so work can stop at any point.
- **Each step has a check**: a command to run or a behavior to observe. A step
  without a check is not finished when the code is written.
- **Order by risk.** Do the step most likely to fail or to invalidate the plan
  first, even if it is not first logically.
- **Data before code.** Schema changes and migrations come before the code
  that depends on them, and each migration states how to roll back.
- **Hold what cannot be undone.** Mark as **Held** any step that deletes data,
  drops a column or table, or breaks something another team or system reads.
  A held step waits for an explicit yes, even when the user said to proceed.
- **3 to 8 steps.** Fewer means the steps are too large to check; more means
  the task should be split into two plans.
- **Name files.** "Update the auth logic" is not a step. "Add token refresh to
  `src/auth/session.ts`" is.

## What not to put in a plan

- Code. A plan with code in it has already skipped the planning.
- Steps for things nobody asked for: refactors, renames, extra abstractions.
  Mention one under "Not sure about" only if skipping it would hurt the result.
- Questions whose answer would not change a step. Decide those yourself.
- Time estimates.
