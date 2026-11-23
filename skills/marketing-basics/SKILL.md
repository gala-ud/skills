---
name: marketing-basics
description: Review an existing landing page as a marketer would: work out the product's positioning, list what is wrong with the copy with a rewrite for each finding, and run an on-page SEO check, using only facts the user supplied. Use when a founder or marketer asks for a positioning statement, asks to review, critique or audit a landing page, homepage or its copy, asks what to fix on it, or asks for a basic SEO check of a page they provide. Skip for writing a full page of new copy from scratch or from notes (that is the job of landing-copy), for ads, emails, social posts or blog articles, for keyword research, ranking or backlink analysis that needs SEO tools, for visual design critique, and for plain grammar or tone edits.
license: MIT
metadata:
  author: gala-ud
  version: 0.1.0
---

# Marketing basics

Most weak landing pages have a positioning problem, not a wording problem:
the page never says what the product replaces or for whom. Rewrites then
fix the wording by inventing proof. So: positioning first, copy judged
against it, and no made-up facts.

## Process

Do only the parts the user asked for: a positioning request gets steps 1-2,
an SEO request gets steps 1 and 5, a page review gets all five.

1. **List the facts you were given** under four heads: what the product
   does, who buys it, what they use today instead, and proof (numbers,
   named customers, quotes, guarantees). Where a head is empty, write your
   best reading and mark it `Assumed`. Do not stop to ask; collect up to
   three questions for the end of the reply.
2. **Work out positioning in this order**, one line each:
   1. Alternatives: what the buyer does today, including "nothing" or a
      spreadsheet. Not a list of every competitor.
   2. Difference: what the product has that those alternatives lack.
   3. Value: what that difference gets the buyer. Ask "so what?" until
      the answer is a result, not a feature.
   4. Best-fit buyer: who cares most about that value. Narrow beats broad.
   5. Category: the existing category that makes the value obvious.
   Then write the statement: `For <buyer> who <situation>, <product> is a
   <category> that <value>. Unlike <alternative>, it <difference>.`
3. **Review the copy against the statement.** Check, in this order: the
   headline says what the product is and for whom; the first screen has
   one primary action; claims are specific; sections lead with the buyer's
   result, not the feature; proof sits next to the claim it supports.
   Report at most seven findings, most damaging first.
4. **Give a rewrite with every finding**, built only from the listed facts.
   Where the rewrite needs a number, customer name, quote or guarantee
   that was not supplied, write `[NEED: <what>]` in its place.
5. **Check on-page SEO from the supplied page only.** Mark each line
   `ok`, `fix` (with the fix) or `cannot see`: title present, 60
   characters or fewer, names the product's main term; meta description
   present, 155 characters or fewer; exactly one h1; heading levels not
   skipped; images have alt text; link text describes its target; the
   main term appears in the first 100 words; no `noindex`. If the user
   gave plain text, not HTML, check only the main term and replace the
   other lines with `Head and markup: cannot see (plain text supplied)`.

## Output

```markdown
## Facts
Does: ... | Buyer: ... | Today they use: ... | Proof: ...

## Positioning
(the five lines, then the statement)

## Copy findings
1. "<quoted text>" - <problem in one sentence>
   Rewrite: "<new text>"

## SEO check
- Title: fix - 71 characters; cut to "<new title>"
- Meta description: cannot see

## Not checked
Rankings, search volume, backlinks, page speed, competitor pages.

## Questions
1. <question> (I assumed: ...)
```

Omit the sections for parts you did not do. "Not checked" appears whenever
the SEO check does.

## Rules

- **Never invent proof.** No statistics, percentages, customer names,
  testimonials, awards, user counts, guarantees or prices that the user did
  not supply. This holds in rewrites, examples and titles alike.
- **Never drop what protects the reader or the company**: disclaimers,
  price and renewal terms, limits ("up to", "results vary"), legal and
  safety notices stay in every rewrite, with their meaning unchanged.
- **Flag unsupported claims on the page** ("#1", "10x faster", "trusted by
  thousands") as a finding. Do not repeat, strengthen or quietly delete
  them; the rewrite uses `[NEED: source for ...]` or a claim the facts
  support.
- **Say what the product does, not a result nobody measured.** "Sends the
  reminder for you" is a fact; "ends late payments" is a claim and needs
  `[NEED: evidence ...]`. This holds for the positioning statement too.
- **Predict nothing.** No promised rankings, traffic or conversion lift.
- **Quote before you criticize.** Every copy finding starts with the exact
  words it is about.
- **No praise section and no closing offer.** End with the last section.
