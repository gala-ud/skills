---
name: landing-copy
description: Write or rewrite landing page copy from the facts the user supplies - one reader, one promise, one call to action, and proof taken only from those facts, with missing proof marked as a gap instead of invented. Use when the user asks for landing page, homepage, product page or launch page copy, for a hero headline and subheadline, or to make existing page copy clearer or more convincing. Skip for blog posts, emails, ads and social posts, for keyword research, and for the page's design or code.
license: MIT
metadata:
  author: gala-ud
  version: 0.1.0
---

# Landing copy

Generated landing pages sound alike and lie alike: "trusted by 10,000+
teams", a five-star quote from nobody, "save 10 hours a week". The page
converts only if a reader believes it, so every claim has to be one the
owner can back.

## Process

1. **List the facts** from the user's material: what the product is, who
   it is for, what they use today instead, outcomes with numbers, proof
   (customers, quotes, data), price, and the action wanted. If the product,
   the reader or the action is missing, ask for it in one message and stop.

2. **Pick one reader and one promise**: the outcome that reader wants, in
   words they would use. Write them down first:
   `Reader: ... | Promise: ... | Action: ...`

3. **Write the page in this order**, each part labeled:
   - **Hero**: a headline of at most 10 words that states the outcome or
     says plainly what the product is; a subheadline of 1-2 sentences (who
     it is for, what it does, how it differs); one button, verb first.
   - **Problem**: the reader's situation today, 2-3 sentences.
   - **How it works**: at most 3 steps, or features written as "feature,
     so you can outcome".
   - **Proof**: only what the facts contain.
   - **Questions**: 3-5 real objections (price, effort, risk, switching).
   - **Final call to action**: the same action as the hero button.

4. **Mark every gap.** Where the page needs proof you were not given,
   write `[NEEDED: a customer quote about setup time]` in that spot.

5. **Check the draft.**
   - Every number, name, quote, price and integration is in the facts.
   - The headline fails the swap test if a competitor could use it
     unchanged: rewrite it with something only this product can say.
   - One action throughout. No "best", "#1", "fastest" without proof. No
     "revolutionary", "seamless", "unlock", "supercharge", "game-changing".

6. **Deliver** the copy, then `Facts used`, then `Needed` (every gap, with
   where it goes), then at most 2 alternative headlines.

## Rules

- **Never invent** a statistic, testimonial, customer, logo, rating,
  guarantee, integration, price, discount or deadline, a promise to
  signups ("early access", "no spam"), or a detail of the reader's day
  that the facts do not state. Not as an example, not as a placeholder
  that looks real.
- **A fact is used at the strength given.** "Two beta users cut invoicing
  time" does not become "customers cut invoicing time". Round nothing.
- **Absolute and regulated claims** ("guaranteed", "100% secure", health or
  income claims) appear only if supplied, and are listed under `Needed` as
  "confirm you can state this".
- **Rewriting existing copy:** keep its facts, cut its filler, and list
  each claim in the original that the user's material does not support
  under `Needed` instead of silently keeping or dropping it.
- **Plain words, second person**, the reader's vocabulary, most sentences
  under 20 words. Default length 250-400 words unless the user sets one.
- **One primary action.** At most one lower-commitment link beside it
  ("See how it works").
- **Write in the language of the user's material.**
- The user's brand voice and wording instructions override these defaults,
  except for the rule against inventing.
