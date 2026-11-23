---
name: diagram-kit
description: Draw a step-by-step process or a message sequence from a description as one self-contained HTML file with inline SVG, on a fixed grid and in a fixed visual style, so that every diagram in a project looks like part of one set. Use when the user asks to draw, diagram, sketch or visualize a flow, process, pipeline of steps, or a sequence of messages between participants that they describe in words, or to restyle such a diagram to match the set. Skip when the user names another format (Mermaid, PlantUML, Graphviz, ASCII, draw.io), for system or architecture maps where many components connect to many, for org charts and other hierarchies, for data charts, and when the content must first be worked out by reading a codebase.
license: MIT
metadata:
  author: gala-ud
  version: 0.1.0
---

# Diagram kit

Hand-placed SVG spills text out of boxes, runs arrows through them, and
never looks the same twice. Here every coordinate comes from a grid formula.

## Process

1. **List the content**: steps or participants, arrows, branches. Draw only
   what the description states. Where something needed is unstated, draw
   the likeliest reading and name it in the caption after "Assumed:".
2. **Pick the layout**: steps in order are a **flow** (steps 3-6);
   messages between participants over time are a **sequence** (step 7).
3. **Flow: nodes are steps, not systems.** Name each by what happens
   ("Write user"), with the system on the second line ("Postgres"). An
   arrow means "then", never "sends data to".
4. **Flow: put the main path in column 0**, top to bottom from row 0: the
   steps that happen when everything succeeds, in order, at most 10. A
   longer path becomes two files; the second starts by repeating the last
   step of the first.
5. **Flow: put each branch in column 1**, in the row of the step it
   leaves: one node naming the outcome. A branch that returns to an
   earlier step or rejoins the main path is still one node, and its
   second line says where it leads ("back to form"). Never draw an arrow
   that points up or skips a cell. One branch node per step.
6. **Place nodes in cells.** Cell (column c, row r): x = 24 + 256c,
   y = 40 + 136r, width 160, height 56; cx = x + 80, cy = y + 28.
   `viewBox="0 0 W H"`, W = 256 x columns - 48, H = 136 x rows - 16.
   One line of text sits at cy and holds 18 characters. Two lines are
   `<tspan x=cx>` at cy - 9 and cy + 9, the second with class `small` (20
   characters). Reword to fit without abbreviating; never widen a node.
   Flow arrows have two shapes and no others:
   - down to the next step: `M 104 y+56 V y+136`, no label
   - right to a branch node: `M 184 cy H 280`, with a `small` label of at
     most 11 characters at (232, cy - 12) giving the condition.
7. **Sequence.** Participants are the row-0 cells, at most 5. Lifeline per
   participant: `<path class="group" d="M cx 96 V H-24"/>`. A message is
   `M cx_from m H cx_to`: the first at m = 144, each next one 40 lower,
   its `small` label at (mid-x, m - 12), at most 34 characters between
   neighbours. A reply is its own message. An alternative ("if expired")
   is a `group` rect from 32 left of its leftmost lifeline to 32 right of
   its rightmost, from 44 above its first message to 16 below its last,
   labelled `small left` at (rect x + 8, rect y + 12). The first message
   inside a frame and the first after one sit 64 below the previous
   message; where one frame directly follows another, 88. H = last m + 48.
8. **Write the file** from the skeleton with its style block unchanged,
   then recompute every coordinate and count the characters of every label.

## Skeleton

```html
<!doctype html>
<html lang="en"><head><meta charset="utf-8"><title>TITLE</title>
<style>
:root{--bg:#ffffff;--ink:#1f2328;--muted:#59636e;--line:#818b98;--fill:#f6f8fa;--accent:#0969da;--accent-fill:#ddf4ff}
@media (prefers-color-scheme:dark){:root{--bg:#0d1117;--ink:#f0f6fc;--muted:#9198a1;--line:#656c76;--fill:#151b23;--accent:#4493f8;--accent-fill:#10233e}}
body{margin:24px;background:var(--bg);color:var(--ink);font:14px/1.4 system-ui,sans-serif}
svg{max-width:100%;height:auto} h1{font-size:18px;margin:0 0 16px} p{font-size:12px;color:var(--muted);max-width:720px}
svg text{fill:var(--ink);font-size:14px;text-anchor:middle;dominant-baseline:central} svg .small{fill:var(--muted);font-size:12px} svg text.left{text-anchor:start}
.node rect{fill:var(--fill);stroke:var(--line)} .focus rect{fill:var(--accent-fill);stroke:var(--accent)}
.node.outside rect{fill:none;stroke-dasharray:4 4} .group{fill:none;stroke:var(--line);stroke-dasharray:2 4}
.edge{fill:none;stroke:var(--line);stroke-width:1.5;marker-end:url(#arrow)}
.edge.async{stroke-dasharray:6 4} .head{fill:var(--line)}
</style></head><body><h1>TITLE</h1>
<svg viewBox="0 0 464 256" width="464" role="img" aria-labelledby="t d"><title id="t">TITLE</title><desc id="d">One sentence saying what the diagram shows.</desc>
<defs><marker id="arrow" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto"><path class="head" d="M0 0L10 5L0 10z"/></marker></defs>
<g class="node"><rect x="24" y="40" width="160" height="56" rx="8"/><text x="104" y="68">Submit form</text></g>
<path class="edge" d="M104 96V176"/>
<g class="node"><rect x="24" y="176" width="160" height="56" rx="8"/><text><tspan x="104" y="195">Validate data</tspan><tspan x="104" y="213" class="small">API</tspan></text></g>
<path class="edge" d="M184 204H280"/><text class="small" x="232" y="192">invalid</text>
<g class="node"><rect x="280" y="176" width="160" height="56" rx="8"/><text><tspan x="360" y="195">Error 422</tspan><tspan x="360" y="213" class="small">back to form</tspan></text></g>
</svg><p>Caption: how to read it. Legend. Assumed: ...</p></body></html>
```

## Rules

- **Classes mean one thing each.** `node outside`: a third-party service
  the description names by brand or calls external, or a step it carries
  out; never the user's own app, database, queue or worker. `edge async`:
  only the arrow into a step that a worker, scheduler or background job
  runs later, or a message the description calls asynchronous. Putting a
  job on a queue is an ordinary step with a solid arrow.
  `node focus`: the one node the user names as the subject; none if they
  name none. `group`: a lifeline or an alternative frame. The caption
  names each class the diagram uses and its meaning, then the assumptions.
- **Self-contained and static**: no external fonts, scripts, images or
  stylesheets, no JavaScript, no gradients, shadows, icons, emoji or colors
  outside the tokens. It must read correctly in grayscale.
- **One style per project.** Copy the style block of the project's
  existing diagram if there is one. Brand colors change token values in
  `:root` only, with text contrast 4.5:1 or better in both schemes.
