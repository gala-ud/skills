---
name: next-step-first
description: Shape replies so the next concrete action comes first, followed by short numbered steps, with one decision at a time and nothing to scroll past. Use when the user asks for action-first, scannable or step-by-step replies or says "just tell me what to do"; says they get lost, overwhelmed or lose focus in long answers; is doing the task while reading; or asks "what do I do next?" in the middle of a multi-step task. Once requested, stays on for the conversation until the user says to stop. Skip when the user asks for a detailed explanation, comparison, essay or document, and for the content of files, code and commit messages.
license: MIT
metadata:
  author: gala-ud
  version: 0.1.0
---

# Next step first

A reply that explains before it instructs makes the reader hold it all in
their head until the action appears. Put the action first.

## Process

1. **Find the next action**: the one thing the user can do right now
   without deciding anything else first: a command, a click, a line to
   change. If your tools let you do it yourself, do it and report it.

2. **Write it as line 1**: `**Now:** <verb> <exact thing>`, with the exact
   command, path or menu name. No greeting, no restated question.

3. **If the action depends on a choice, make the choice.** Recommend one
   option in line 1. Name at most one alternative first action on an
   `**Or:**` line with its condition. `**Or:**` is always line 2, directly
   under `**Now:**` and above `**Then:**`. If you cannot choose without a
   fact only the user has, line 1 is that one question, with the default
   you will assume.

4. **List the remaining steps** under `**Then:**`, numbered. Each step
   starts with a verb, fits in two lines, and is finished before the user
   reads on. A step with more than two commands becomes two steps; never
   drop a command to make a step fit. More than 7 steps: show the current
   phase in full, later phases in one line ("After that: deploy, verify").

5. **Put the warning before the action it guards.** The reader acts while
   reading, so a warning after the command arrives too late. A step that
   deletes, empties, overwrites, resets, force-pushes, pays or sends opens
   with one bold sentence saying what is lost, then the action (the one
   exception to "starts with a verb"). Routine clean-ups count too:
   `3. **This deletes the table for good - back up first.** Run ...`
   A warning is never a step of its own and never sits in a later step. In
   the `**Now:**` line it goes right after the label.

6. **Add at most one `**Why:**` line**, two sentences at most, when the
   user would not trust the action without it. More only when asked.

7. **In later replies of the same task, open with one state line**:
   `Done: ... | Left: N steps`, then `**Now:**`. If something failed, the
   state line says what failed, in plain words.

8. **Check the draft, then stop.** Is `**Or:**` on line 2? Does each step
   that deletes, empties, overwrites or sends open with its bold warning?
   Is anything else bold? Unbold it. No recap, no offers, no other options.

## Template

```markdown
Done: ... | Left: N steps        (later replies only)
**Now:** <one action, exact>
**Or:** <alternative> if <condition>        (optional)
**Then:**
1. <verb> ...
2. ...
**Why:** <one or two sentences>        (optional)
```

## Example

User: "git push got rejected, says non-fast-forward. what do i do"

```markdown
**Now:** Run `git pull --rebase origin main`.
**Or:** Run `git pull origin main` if your team merges instead of rebasing.
**Then:**
1. If it reports conflicts: fix each listed file, then run `git add <file>`
   and `git rebase --continue`.
2. **No `--force` - it deletes the other person's commits.** Run
   `git push origin main`.
**Why:** Someone pushed to `main` after your last pull. Rebasing puts your
commits on top of theirs.
```

## Rules

- **Never cut a warning, prerequisite or exact value** (command, number,
  name) to keep a reply short. Shorten by cutting explanation.
- **One question per reply at most**, and only if the answer changes the
  next action. State the default you will use.
- **No time estimates** unless you measured the time or a source states it.
- **A question that wants a fact** ("which port does Postgres use?"):
  answer in line 1 and skip the template.
- **Bold only for the four labels and for warnings.** Button, menu and
  file names go in "quotes", commands in code formatting.
- **If the user asks for more detail**, give it, then return to this format.
- **Never mention the user's attention, focus or any diagnosis.** Use the
  format without commenting on it.
- The user's explicit formatting instructions override this template.
