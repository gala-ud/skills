---
name: idea-to-spec
description: Turn a rough product or feature idea, or a messy set of requirements, into a one-page written spec with explicit scope before any planning or coding. Use when the user describes something to build and the scope, users or behavior are still open ("I want an app that...", "we need some kind of..."), when requirements are vague or contradictory, or when asked to write a spec, PRD, or requirements. Skip when the request already names the concrete change to make ("add a dark mode toggle to settings"); use plan-first for those.
license: MIT
metadata:
  author: gala-ud
  version: 0.2.0
---

# Idea to spec

A one-line idea hides most of its decisions. Put them on one page before anyone
plans or writes code. The spec is for a solo developer or a small team: short
enough to read in two minutes, concrete enough to say no to things.

## Process

1. **Read the existing project** if there is one. The spec must fit the stack,
   data model and conventions already in place.

2. **Restate the idea in one sentence**: who does what, and why it matters to
   them.

3. **Write the full spec in your first reply**, using the template below. Do
   not open with a round of questions. Where you lack an answer, choose a
   sensible default, write it into the spec, and list it under "Open
   questions" so the user can overrule it. A draft to correct is faster for
   the user than a questionnaire.

4. **Ask first only if a missing answer would change most of the spec** (for
   example, you cannot tell who the user is or what is being built). Then ask
   at most three questions, together, each with your proposed default.

5. **Stop and show it.** Do not plan or code until the user accepts the spec
   or edits it. After acceptance, continue with plan-first if it is installed.

## Template

```markdown
# <Name>

## Problem
Who has it, what they do today, why that is not good enough. 2-4 sentences.

## Version 1 does
- 3-7 bullets, each a thing a user can do and observe.

## Version 1 does not
- Things a reader would reasonably expect but will not get yet.

## Key flows
1. The main path, step by step, from the user's side.
2. One important failure or edge path.

## Data
What is stored, who owns it, what must never be lost.

## Constraints
Platform, stack, deadline, performance, privacy, cost.

## Done when
Checks a person can run by hand to confirm version 1 works.

## Open questions
Defaults you chose that the user may want to change, most important first.
```

## Rules

- **Cut scope before adding detail.** If "Version 1 does" has more than seven
  bullets, move the weakest ones to "does not".
- **"Version 1 does not" is mandatory** and holds at least three items. When
  the user floats an extra ("maybe it should also email them?"), put it here
  with one line on why it waits.
- **Describe behavior, not implementation.** No table names, endpoints or
  libraries unless the user stated them or the existing project fixes them.
- **Every "Done when" item is checkable** by a person in under a minute.
  "Works well" is not a check; "a second device shows the new note within 5
  seconds" is.
- **At most five open questions**, each phrased as the default you chose.
- **One page.** If the spec grows past about 60 lines, the idea is two ideas.
  Say so and propose a split.
- Save the spec as `docs/spec-<name>.md` unless the project keeps specs
  elsewhere.
