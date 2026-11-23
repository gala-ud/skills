---
name: design-direction
description: Propose two or three clearly different visual directions for a product (typography, color, layout), each argued from the product and its audience and shown side by side in one HTML specimen, then help the user pick one and turn it into design tokens. Use when a new product, site or app has no visual style yet, or the user asks for design options, concepts, a look and feel, a visual identity, or says they do not know how it should look. Skip when a design system, brand guide or styled UI already exists (extend that instead), when the user asks to critique or fix an existing interface, and when the user has already named the style and only wants it built.
license: MIT
metadata:
  author: gala-ud
  version: 0.1.0
---

# Design direction

Asked for design options, an agent tends to deliver one default three times
with a different accent color. A choice is real only when the options differ
in kind, are argued from the product, and can be seen side by side.

## Process

1. **Write the brief in four lines**: product, audience, the one thing a
   user comes to do, where it is seen (phone, desktop, both). Take them from
   the request and the repository. A line you cannot infer becomes a stated
   assumption, not a question; ask only if the product itself is unknown.

2. **Pin down the adjectives.** For each style word the user gave ("modern",
   "premium"), write what it means here in terms someone could check on
   screen. Then write one line on how products in this category usually look.

3. **Write three directions** (two if the user asked for two). Direction A
   stays closest to the category's usual look, the last one departs from it
   furthest, and all of them must be options you would defend. Each has a
   name of two or three words that is not a style label such as "Minimal";
   an idea sentence that starts from the audience or the task; one or two
   type families, each with a fallback stack ending in a generic family,
   their roles, and h1 and body sizes; hex values for seven color roles; the
   layout's organizing principle; the shape; and the one thing it makes harder.

4. **Check that they differ in kind.** Fill the comparison table below. Any
   two directions must differ in at least three of its four rows and may not
   share a font family or an accent hue. Rewrite a direction that fails.

5. **Compute contrast** (WCAG ratio) for text on bg, text-muted on bg and
   on-accent on accent. Each must reach 4.5:1; change the color until it
   does. Run code if you can; otherwise work the formula by hand.

6. **Build the specimen**: one self-contained file, `design-directions.html`,
   with one panel per direction, side by side and stacked below 900 px. Every
   panel shows the same content, word for word: the product name, a headline
   and one sentence that restate the user's description, a primary button,
   a secondary link, one card or list row of the kind this product really
   shows, and the seven swatches with their hex values. Each panel arranges
   that content by its own layout principle and shape, so the panels differ
   in structure and not only in color. The file loads nothing: no font
   links, images or scripts.

7. **Recommend and stop.** Reply in the format below and ask the user to
   choose. Build no product screens before they do.

8. **After the choice**, output the chosen direction as CSS custom properties
   under the seven role names plus font, size and radius tokens. If the user
   mixes in one element from another direction, apply it and repeat step 5.

## Reply format

```markdown
**Brief:** <product> for <audience>; main task: <task>; seen on <where>.
Assumed: <assumptions, or "nothing">
**Your words:** <each style word and what it means on screen; omit if none>
**Category default:** <one line>

### A. <Name>
<Idea sentence.>
- Type: <families, roles, sizes>
- Color: bg #… / surface #… / text #… / text-muted #… / border #… / accent #… / on-accent #…
- Layout: <principle, width, alignment>
- Shape: <radius, borders or shadows>. Costs: <one thing>

| | A | B | C |
|---|---|---|---|
| Type class (serif, sans, mono, display) | | | |
| Background (light, dark, colored) | | | |
| Layout principle | | | |
| Shape (sharp, soft, round) | | | |
| Contrast: text / muted / on-accent | 12.6 / 5.1 / 4.8 | | |

**Specimen:** `design-directions.html`. Shown by fallback until loaded: <fonts>
**I would pick** <letter>, because <reason from the brief>. Pick <other> if <condition>. Which one?
```

## Rules

- **Every choice has a reason from the brief** and an exact value: "read on
  a phone in a kitchen, so 18 px body text", not "clean and modern".
- **Real, free fonts**: only system fonts or open-license families you are
  sure exist. The specimen cannot load them; list those shown by fallback.
- **No gradients, glows or emoji** unless the idea sentence calls for them.
- **Sample copy restates what the user said**; anything else is
  `[PLACEHOLDER: ...]`. Never invent testimonials, statistics or logos.
- **Fixed brand elements stay fixed.** If the user gives a color, font or
  logo, every direction keeps it and varies the rest; the table rows it
  fixes do not count against step 4.
