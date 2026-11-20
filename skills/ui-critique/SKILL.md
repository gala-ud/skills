---
name: ui-critique
description: Review a user interface (HTML and CSS, a component, a screenshot or a running page) and return a short, ranked critique in which every finding names the element, the measured problem and a concrete fix. Use when the user asks to critique, review, audit or polish a UI, page, screen, form or component, asks why it looks off, amateur, generic or AI-generated, or wants design feedback before shipping. Skip when the user asks to build or redesign the UI from scratch, for review of program logic, and for copy-only edits.
license: MIT
metadata:
  author: gala-ud
  version: 0.1.0
---

# UI critique

Design feedback fails in two ways: taste with no evidence ("feels
cluttered") and a forty-item dump nobody acts on. A useful critique is a
few findings, each one measured, located and fixable.

## Process

1. **Name the screen's main task** and who does it, from the code or the
   request. If it is unclear, state your assumption in one line. Judge
   everything against that task.

2. **Read all of it first**: markup, styles, every state the code defines.
   From a screenshot you cannot see states or exact values: say so.

3. **Measure, in this order.** If you can run code, compute with it.
   - **Main action**: is it the strongest element? Count the buttons that
     share the primary style. Does its label say what happens?
   - **Contrast**: the WCAG ratio of each text and background pair, from
     the actual colors. Body text needs 4.5:1; text of 24 px or more, or
     19 px bold, needs 3:1.
   - **Type**: count distinct font sizes and weights. More than 6 sizes on
     one screen, body text under 16 px or lines over 75 characters.
   - **Spacing**: list the distinct margin, padding and gap values. Values
     off a 4 px step, or near-duplicates (14, 15, 16), are one finding.
   - **Forms and targets**: inputs with no `<label>`, a placeholder used as
     the label, targets under 44 x 44 px, errors shown by color alone.
   - **States**: focus removed with no replacement, missing hover,
     disabled, loading, empty or error states.
   - **Small screens**: fixed widths, no viewport meta tag, overflow at
     360 px.
   - **Generic look**: gradient text, everything centered, three identical
     cards with emoji icons, the same large radius and shadow everywhere.

4. **Rank.** Blocker: someone cannot read it, reach it or finish the task.
   Major: it slows or misleads them. Minor: polish. One row is one cause;
   the same cause in several places is one row with a count. Report the 7
   most severe at most and name the rest in the "Also" line.

5. **Verify.** Re-open every cited line and recompute every number. Delete
   any finding you cannot point at.

## Output

```markdown
## Critique: <screen>
Task assumed: <who does what here>
Checked: <files, or "screenshot only: values are estimates">

| # | Severity | Where | Problem (measured) | Fix |
|---|---|---|---|---|
| 1 | Blocker | `.hint`, `signup.css:41` | #9aa0a6 on #ffffff is 2.6:1, needs 4.5:1 | `color: #5f6368` (6.0:1) |

**Also:** <findings beyond the 7, a few words each, or omit the line>
**Works well:** <one or two specific things to keep>
**Generic look:** <the patterns from step 3 that apply, or "none">
**Not checked:** <states, breakpoints or content you could not see>
```

## Rules

- **Every finding has a location and a measurement**, or names the thing
  that is missing. No "feels", "pops", "clean", "modern" or "cluttered".
- **A fix is a value or a code change.** A contrast fix states the new
  ratio and keeps the original hue where it can.
- **Never state a number you did not compute** from values in the source.
  From a screenshot, write "approx.".
- **Taste is not a finding.** A color or font you would not have chosen,
  but that passes every check, stays out.
- **Do not pad, do not cram.** Three real findings are three rows; two
  different problems are never merged into one row to fit the limit. If
  there are no blockers, say "No blockers found".
- **Generic-look patterns go in their own line**, and into the table only
  when one of them hurts the main task.
- **Do not edit the files** unless asked. Asked to "fix it": apply the
  listed fixes and nothing else.
- The user's brand or design-system constraints override these defaults.
