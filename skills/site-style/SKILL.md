---
name: site-style
description: Build or extend a website so that every page looks like one site, by setting a small set of design tokens once (type scale, spacing scale, color roles, radius) and styling everything through them, then checking that no raw values slipped in. Use when the user asks to build a landing page, marketing site, docs site or other multi-page site, to add a page or section to an existing site, or says the pages look inconsistent. Skip for a tweak to a single component, for apps that already use a component library or design system the user names, and for critique with no building.
license: MIT
metadata:
  author: gala-ud
  version: 0.1.0
---

# Site style

A generated site drifts: each page gets its own blue, its own heading size
and its own gap, and by the third page nothing matches. Consistency comes
from a small set of named values, written once and used everywhere.

## Process

1. **Look for an existing style source**: a tokens file, CSS custom
   properties, a Tailwind theme, or the values the current pages already
   use. Extend what is there. Never start a second system beside it.

2. **If there is none, define tokens in one place** (`:root` in one
   stylesheet, or the framework's theme):
   - **Type**: one font family, system stack unless the user names fonts.
     At most 6 sizes (default 14, 16, 20, 24, 32, 48 px), 2 weights, one
     line height for text and one for headings.
   - **Space**: one scale: 4, 8, 12, 16, 24, 32, 48, 64, 96.
   - **Color by role, not by name**: `--bg`, `--surface`, `--text`,
     `--text-muted`, `--border`, `--accent`, `--on-accent`. One accent.
   - **Shape**: at most 2 radii and 1 shadow, one content width.

3. **If the site has raw values and no tokens**, derive the tokens from the
   values already in use (most frequent wins), replace the raw values with
   them, and change nothing else about how the pages look.

4. **Fix the page rules once**: container width, one vertical padding for
   sections, which size each heading level uses, and at most 2 button
   variants. Write them as classes, not per page.

5. **Build with tokens only.** Outside the token definitions: no hex or
   rgb colors, no font-size literals, no spacing literals except 0 and
   1 px borders. A value you need and do not have becomes a token first.

6. **Check before delivering.**
   - Search the styles for raw values outside the token block
     (`#[0-9a-fA-F]{3,8}`, `rgb(`, `\d+px`, `\d*\.?\d+rem`) and replace them.
   - Count distinct font sizes: 6 or fewer.
   - Compute contrast for `--text`, `--text-muted` and `--on-accent` on
     their backgrounds: 4.5:1 or better. If you can run code, use it.
   - No fixed widths that break at 360 px; one `<h1>` per page; every
     page links the same stylesheet.

7. **Deliver** the files and the style contract below.

## Style contract (end of the reply)

```markdown
**Tokens:** `<file>`, <n> sizes, <n> colors, added: <new tokens or "none">
**Page rules:** <container, section padding, button variants>
**Raw values left:** <none, or each one with its reason>
**To add a page:** link `<stylesheet>`, use `<the classes>`
```

## Rules

- **One source of truth.** Tokens live in one file; pages never redefine
  them. A dark theme only reassigns the role tokens.
- **A seventh size, a second accent or a third radius replaces an existing
  one**; it is not added.
- **No decoration the tokens do not define**: no gradients, glows or emoji
  icons unless the user asks.
- **Use the user's content.** Missing text or images are marked
  `[PLACEHOLDER: ...]`; never invent testimonials, statistics or logos.
- **Semantic HTML**: landmarks, heading order, `alt` text, labels on
  inputs, a visible focus style built from `--accent`.
- **Nothing keeps a browser default color or font**: links, buttons, inputs
  and tables are styled from the tokens as well.
- **Tailwind or similar**: put the tokens in the theme and avoid arbitrary
  values such as `text-[13px]`.
- **Adding to an existing site**: reuse its classes before writing new
  ones, and say which tokens you added.
- The user's brand values replace the defaults; the limits still hold.
