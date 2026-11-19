---
name: natural-writing
description: Rewrite existing prose so it reads as written by a person - cut stock AI phrasing, filler and inflated tone while keeping every claim, number, name and quote unchanged. Use when the user asks to make a text sound natural or human, less robotic, less like AI or ChatGPT, or to strip fluff and "AI-isms" from a draft such as an email, post, README, article or cover letter. Works in the language of the text. Skip for writing new text from scratch, translation, summarizing or cutting to a length target, grammar-only or typo-only proofreading where wording must stay, and code or code comments.
license: MIT
metadata:
  author: gala-ud
  version: 0.1.0
---

# Natural writing

Readers stop trusting a text when it sounds generated: stock phrases,
inflated importance and tidy rhythm suggest nobody checked the words. The
repair is editing, not disguise: say each thing plainly, once, and leave
every fact where it was.

## Process

1. **Read the whole text.** Note its language, audience and register. Edit
   in the text's language and keep its register: a formal letter stays
   formal.

2. **List the load.** Before editing, list for yourself everything that must
   survive: claims, numbers with units, dates, names, quotes, links,
   warnings, conditions ("only if", "except") and hedges that carry real
   uncertainty ("may", "in early tests").

3. **Mark the patterns** from the table below. One instance is not a
   problem. Act when a pattern repeats or several cluster in one paragraph.

4. **Edit sentence by sentence.** For each marked sentence choose one: cut
   it (carries no load), state it plainly (carries load under padding), or
   leave it. Sentences that are already plain stay word for word.

5. **Check the load.** Compare the step 2 list with the rewrite, item by
   item. Each item is present at the same strength: not dropped, not
   rounded, not more or less certain. Restore whatever fails.

6. **Re-read for what you introduced.** A removed dash becomes a semicolon
   habit, a removed triad becomes a pair in every sentence. Fix those.

7. **Deliver the rewritten text first**, with no introduction. Add `Notes:`
   after it only for two things: a phrase left vague because the fix needs
   a fact only the author has, and a place where meaning may have shifted.
   One line each, `"<phrase>": <what is missing or what shifted>`, five
   lines at most. No list of cuts, no advice on improving the text.

## Patterns

| Pattern | Repair |
|---|---|
| Wrappers and cheer: "In today's fast-paced world", "In conclusion", "we're thrilled", "We can't wait to see ..." | Delete. Start at the first claim, stop after the last. |
| Inflated significance: "pivotal", "game-changing", "a testament to", "plays a crucial role" | Say what the thing does. If nothing is left, cut the sentence. |
| Staged contrast: "It's not just X, it's Y" | State Y. Keep the contrast only if a reader really believes X. |
| Reflex triads: three adjectives, three benefits | Keep the items that are true and distinct, however many that is. |
| Stock words: "delve", "leverage", "seamless", "robust", "landscape", "unlock" | The plain word: "use", "works with", "field". |
| Vague authority: "experts say", "studies show" | Keep the claim, ask for the source in Notes. Never supply one. |
| Trailing commentary: ", highlighting the importance of ..." | Cut it, or make it a sentence if it carries a claim. |
| Signposts and hedge stacks: "It's important to note that", "it could be argued that perhaps" | Drop signposts. Keep one hedge where uncertainty is real. |
| Uniform rhythm: equal-length sentences, a punchline ending each paragraph | Split or merge where the content asks. Drop the punchline. |
| Decoration: scattered bold, emoji bullets, headings on a short text, a dash in every sentence | Plain paragraphs. Formatting only where a reader navigates. |

## Example

Before:

> In today's fast-moving digital landscape, we're thrilled to announce
> Relay 2.0 - a game-changing update that doesn't just improve sync, it
> reimagines it. Sync is now up to 40% faster on files over 1 GB,
> delivering a seamless, robust and intuitive experience. Studies show
> most users abandon a sync that takes over a minute. It's important to
> note that offline mode may lose edits made within 5 seconds of
> disconnecting, underscoring our commitment to transparency.

After:

> Relay 2.0 is out. Sync is now up to 40% faster on files over 1 GB.
> Studies show most users abandon a sync that takes over a minute. Offline
> mode may lose edits made within 5 seconds of disconnecting.
>
> Notes:
> - "Studies show": name the study or cut the sentence.

## Rules

- **Never add.** No new facts, examples, numbers, sources, anecdotes,
  opinions or feelings, and no deliberate typos or slang. A human-sounding
  detail the author did not supply is a fabrication.
- **Never drop or change** a claim, number, unit, date, name, warning or
  condition. If cutting filler would remove one, keep the sentence.
- **Leave untouched:** quotations, titles, code, commands, URLs, legal or
  regulatory wording, and defined terms.
- **Keep the author's voice.** Their unusual word choices, jokes and first
  person stay. If the user gives a sample of their own writing, match its
  sentence length and vocabulary.
- **The rewrite is never longer than the original.**
- **Promise nothing about AI-detector scores**; say so in one line if asked.
- The user's instructions on tone, length and what to keep override the
  pattern table.
