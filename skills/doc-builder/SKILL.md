---
name: doc-builder
description: Turn raw notes, meeting minutes, logs or scattered material into a structured report or document, built outline first, then section by section, then checked against the notes for invented facts, changed numbers and inconsistencies. Use when the user hands over notes or source material and asks for a report, write-up, summary document, status update, proposal, postmortem, design doc or brief built from them. Skip when the user asks to edit or polish an already written document, to write from scratch with no source material, to research a topic on the web, or only to convert a file between formats.
license: MIT
metadata:
  author: gala-ud
  version: 0.1.0
---

# Doc builder

A document written from notes goes wrong quietly: a gap gets filled with a
plausible number, a "maybe" becomes a fact, the summary says 14 and the table
says 12. The notes are the only source, and the reader cannot see them, so
the document has to be traceable to them line by line.

## Process

1. **Read all the material and list what it holds**: every fact, number,
   date, name, decision, warning, objection and open question, with where it
   came from. Note where two sources disagree.

2. **Name the reader and the purpose in one line**: who reads this and what
   they decide or do afterwards. If the user did not say, assume and state
   it; do not ask. Ask one question only if the notes fit two different
   documents and you cannot tell which is wanted.

3. **Outline, answer first.** Write the headings and one sentence per
   section stating its point. The first section gives the conclusion or the
   decision asked for; background comes after. Give every listed item a
   section or put it under "Left out". A section the reader needs but the
   notes cannot fill stays in as a heading with a `[MISSING: ...]` line. If
   the user asked to approve the outline, show it and wait; otherwise go on.

4. **Write the sections.** Each opens with its point. Copy numbers, names,
   dates and units exactly as the notes give them. Keep each hedge and its
   owner: "Dana thinks", "unconfirmed", "about". Write the summary last,
   from the finished sections, and place it first.

5. **Fact pass.** Go through the draft and trace every number, name, date,
   quotation and claim back to the notes. What you cannot trace, delete or
   replace with `[MISSING: what is needed]`.

6. **Consistency pass.**
   - The same thing has the same name and the same number everywhere,
     including the summary, tables and headings.
   - Recompute every total, difference and percentage. A count in the text
     ("three risks") matches the number of items listed.
   - A value you derived is marked "(calculated)".
   - Where the notes disagree, the document shows both values with their
     sources as `[CONFLICT: ...]`. Do not pick one.

7. **Deliver** the document, then the build notes below.

## Build notes (after the document, every time)

```markdown
---
**Build notes** (not part of the document)
- Reader and purpose: <one line; mark "assumed" if it was>
- Missing: <each [MISSING] marker and who could fill it, or "nothing">
- Conflicts in the notes: <each [CONFLICT] marker, or "none">
- Calculated by me: <derived values and their inputs, or "nothing">
- Suggested by me: <estimates, ratings or next steps of your own, or "nothing">
- Left out: <notes not used, with the reason, or "nothing">
```

## Rules

- **Never invent.** No fact, number, name, date, quotation, source or
  citation that is not in the notes, even one you know to be true. Outside
  background is a `[MISSING]` line unless the user asks you to research;
  then every added fact carries its source.
- **Never drop** a warning, a risk, a caveat, an objection, an open question
  or a number that bears on the decision. If one does not fit the outline,
  the outline is wrong.
- **Never strengthen or weaken.** "Might" stays "might"; one person's view
  stays that person's view; a plan is not reported as done.
- **Your judgment is not a note.** Calculate only sums, differences and
  shares of the notes' own figures. An estimate that needs an assumption, a
  rating, a recommendation or a next step of your own goes in the build
  notes under "Suggested by me", never in the document.
- **Markers stay visible.** `[MISSING]` and `[CONFLICT]` appear in the body
  where the reader meets the gap, and again in the build notes.
- **No padding.** No section that restates another, no closing section that
  repeats the summary, no introduction about what the document will do.
- **Structure follows the reader's question**, not a template: use only
  headings this material fills or the reader needs.
- **Fix the form, keep the content.** Spell out an abbreviation only when
  the notes define it; otherwise keep it as written.
- **Plain Markdown** in the language of the request, unless the user names
  another format or language. The user's own template or section list
  replaces the outline in step 3; every other step still applies.
