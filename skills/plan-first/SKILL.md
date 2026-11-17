---
name: plan-first
description: Write a short step-by-step implementation plan and get it accepted before changing code. Use for any change that touches more than one file, adds a dependency, changes a data schema or public interface, or will take more than a few minutes; also when the user asks to plan, outline an approach, or "think before coding". Skip for one-line fixes and typos.
license: MIT
metadata:
  author: gala-ud
  version: 0.1.0
---

# Plan first

Code written without a plan gets rewritten. A plan costs a minute to read and
is the cheapest place to catch a wrong approach.

## Process

1. **Read before planning.** Open the files the change will touch and one
   level of what calls them. Find how the project already solves similar
   problems and follow that pattern. Note the test and build commands.

2. **State the goal in one sentence** and list what is explicitly out of
   scope. If a spec exists, link it instead of restating it.

3. **Write the plan** using the template below.

4. **Show the plan and wait.** Start coding only after the user accepts it.
   If the user has said to proceed without asking, show the plan and continue.

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
- Questions that would change the plan, each with your default.
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
- **3 to 8 steps.** Fewer means the steps are too large to check; more means
  the task should be split into two plans.
- **Name files.** "Update the auth logic" is not a step. "Add token refresh to
  `src/auth/session.ts`" is.

## What not to put in a plan

- Code. A plan with code in it has already skipped the planning.
- Steps for things nobody asked for: refactors, renames, extra abstractions.
  List them under "Not sure about" if they seem worthwhile.
- Time estimates.
