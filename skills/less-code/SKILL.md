---
name: less-code
description: Solve a coding task with the least code that fully meets the request, or audit a diff or module for code that can be deleted, without cutting input validation, error handling, security checks or tests. Use when the user asks for a minimal, lean or simple solution, says a change is over-engineered or bloated, asks whether code can be simpler or what can be deleted, or wants a diff trimmed before merge. Skip for code golf or fewest-characters requests, performance optimization, formatting or naming clean-up, and refactors whose goal is structure rather than size.
license: MIT
metadata:
  author: gala-ud
  version: 0.1.0
---

# Less code

Agents over-build: a dependency where the platform has the feature, an
abstraction with one caller, options nobody asked for. But "less" chased as
a number is gamed by packing lines and deleting checks. The aim is fewer
things that exist, not fewer characters.

## Process: writing code

1. **List the behaviors asked for**, one line each. Nothing off this list
   gets built.

2. **Read the code the change touches and search the codebase** for a
   function, component or helper that already does part of the job.

3. **Go down this ladder and stop at the first rung that works:**
   1. Nothing: existing behavior or configuration already covers it.
   2. Something already in the codebase.
   3. The standard library or a platform feature (native HTML element,
      database constraint, framework built-in).
   4. A dependency that is already installed.
   5. New code, in an existing file, sized to the list from step 1.
   Add a dependency only for security-sensitive work (cryptography, token
   parsing, HTML sanitizing) or when rung 5 would exceed about 50 lines.

4. **Write it without**: an interface, base class, factory or wrapper that
   has one implementation or one caller; parameters, flags or config
   options nobody asked for; handling for inputs the callers cannot
   produce; comments that restate the code.

5. **End the reply with `Left out:`**, one line per thing you chose not to
   build that a reader might expect, or "nothing".

## Process: auditing a diff or module

1. Read all of it and the code that calls it.
2. Put each candidate for deletion in one class:
   - **Unused**: nothing references it.
   - **Duplicate**: an equivalent already exists; give its `file:line`.
   - **Replaceable**: the standard library, platform or an installed
     dependency does it; name the replacement.
   - **Speculative**: an option, layer or hook with a single use.
   - **Noise**: comments restating code, dead branches, leftover debugging.
3. **Search before calling anything unused**: by name across the whole
   repository, including string lookups (`getattr`, registries, config,
   templates, routes), exports and tests. Say what you searched.
4. For a Replaceable or Duplicate item, check that the replacement gives
   the same result for the existing call sites, and state any difference.
5. Report in the format below. Change nothing unless asked. Asked to apply:
   one row at a time, running the tests after each, or saying you cannot.

## Protected

Never cut these to save lines, in either mode: validation of external
input; authentication and authorization checks; escaping and parameter
binding; error handling around I/O, network and parsing; failure logging;
tests; accessibility attributes; migrations and rollbacks. If one looks
redundant, put it under **Ask first** with the reason; do not delete it.

## Audit output

```markdown
## Deletion audit: <target>
Read: <files>. Reference search: <how>

| # | Location | What | Class | Evidence | Lines |
|---|---|---|---|---|---|
| 1 | `sync/backoff.py:1-40` | `Backoff` class | Unused | name appears only in its own file | -40 |
| 2 | `sync/http.py:12-30` | hand-written URL join | Replaceable: `urllib.parse.urljoin` | same result at the 3 call sites | -17 |

Total: -57 of 380 lines
**Ask first:** <public API or protected items that look removable, and why>
**Keep:** <at most 3 things that look like bloat but are needed, and why>
```
"Lines" is the net change after the replacement.

## Rules

- **A cut counts only when a thing stops existing**: a function, branch,
  parameter, file or dependency. Joining statements, shortening names,
  dense one-liners, removing comments that explain why, and moving code to
  another file are not savings; do not do them.
- **Behavior on the step-1 list never changes**, including error messages
  and status codes that callers or tests rely on.
- **No drive-by deletions.** When writing code, do not remove unrelated
  code you happen to see; mention it in one line under `Left out:`.
- **Exported or public names** go under Ask first, never straight into
  the table: you cannot see outside callers.
- The user's instruction to keep or add something wins over this skill.
