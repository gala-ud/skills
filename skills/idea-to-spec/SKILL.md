---
name: idea-to-spec
description: Turn a rough product or feature idea into a short written spec with explicit scope before any planning or coding. Use when the user describes something to build in a sentence or two ("I want an app that...", "add a feature for..."), when requirements are vague or contradictory, or when asked to write a spec, PRD, or requirements.
license: MIT
metadata:
  author: gala-ud
  version: 0.1.0
---

# Idea to spec

A one-line idea hides most of its decisions. Surface them on one page before
anyone plans or writes code. The spec is for a solo developer or a small team:
short enough to read in two minutes, concrete enough to say no to things.

## Process

1. **Restate the idea in one sentence**: who does what, and why it matters to
   them. If you cannot, ask until you can.

2. **Ask only what you cannot decide yourself.** At most five questions, asked
   together, each with your proposed default so the user can answer "defaults
   are fine". Ask about:
   - who the user is and what they do today instead
   - the one thing version 1 must do well
   - hard constraints: platform, stack, deadline, budget, data that must be kept
   Do not ask about things the codebase or the conversation already answers.

3. **Read the existing project** if there is one. The spec must fit the stack,
   data model and conventions already in place.

4. **Write the spec** using the template below. Fill every section. Write
   "none" rather than deleting a section.

5. **Stop and show it.** Do not start planning or coding until the user accepts
   the spec or edits it.

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
Decisions still unmade, each with a proposed default.
```

## Rules

- **Cut scope before adding detail.** If "Version 1 does" has more than seven
  bullets, move the weakest ones to "does not".
- **"Version 1 does not" is mandatory** and must contain at least three items.
  It is the section that prevents the most rework.
- **Describe behavior, not implementation.** No table names, endpoints or
  libraries unless the user stated them as constraints.
- **Every "Done when" item must be checkable** by a person in under a minute.
  "Works well" is not a check; "a second device shows the new note within 5
  seconds" is.
- **One page.** If the spec grows past about 60 lines, the idea is two ideas.
  Say so and propose a split.
- Save the spec as `docs/spec-<name>.md` unless the project keeps specs
  elsewhere.
