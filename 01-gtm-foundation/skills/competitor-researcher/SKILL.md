---
name: competitor-researcher
description: Create or refresh an objective, opinion-free fact pack for an approved competitor at foundation/market/competitors/direct/<name>.md. Produces facts only (overview, ICP, pricing, customer evidence, technical dimensions) with sourced URLs and dates. Use when adding a new competitor or refreshing an existing one.
---

# Competitor researcher

Builds and maintains structured competitor fact packs. Fact packs contain **only objective facts**, no positioning, no "where we differ", no "when to choose us". That editorial layer is produced separately by `seo-article-writer` when writing comparisons.

Separation of concerns:
- **This skill**: facts about the competitor (what they are, what they do, how they price).
- **seo-article-writer**: your editorial take, written fresh in each article.

## Files to read before starting

- `./_TEMPLATE.md` is the schema — actually it lives at `../../foundation/market/competitors/direct/_TEMPLATE.md`. Every output conforms to it.
- `../../foundation/market/competitors/approved.md` — the approved list (the gate).
- The existing fact pack (if refreshing): `../../foundation/market/competitors/direct/<name>.md`.

Do **not** read your own brand/product files. This skill is product-agnostic; the fact pack describes only the competitor.

## Two modes

### Create

No fact pack exists yet. Build a new `direct/<name>.md` from the template.
- First confirm the competitor is on `approved.md`. If not, tell the user adding one requires intent + research + updating `approved.md`, and confirm before proceeding.

### Refresh

A fact pack exists. Check its `Last updated` date. If within 3 months and no specific change was flagged, confirm with the user before re-researching. Otherwise update stale sections (most likely: pricing, funding/acquisitions, notable customers, known limitations) and bump the date.

## Research workflow

1. **Read the existing file** (if any). In create mode, strip any opinion left from before; keep sourced facts.
2. **Web research**, prioritizing: product page, pricing page, docs, blog/changelog, G2/Capterra reviews, press/funding news.
3. **Fill the schema** from `_TEMPLATE.md`. Every section present. Discipline:
   - Record URL + access date for every claim.
   - Never invent numbers. If a figure isn't public, say so and leave it blank.
   - Paraphrase; never copy their marketing language.
   - "Why customers choose them" and "Known limitations" come from verifiable reviews, attributed. If sources are sparse, say so.
   - Pricing needs a dated source per figure.
4. **Validate** — every section non-empty or explicitly "not publicly available"; technical dimensions filled; claims sourced; `Last updated` = this month.
5. **Write** the file to `../../foundation/market/competitors/direct/<name>.md`. In refresh mode, rewrite the whole file (don't patch) to avoid drift.
6. **Confirm** to the user: file path, last-updated date, which sections changed, any data that couldn't be sourced.

## What this skill does NOT do

- No editorial / positioning content (that's `seo-article-writer`).
- Does not write to articles or any outputs folder.
- Does not add your product's framing to the fact pack.
- Does not edit `approved.md` automatically (update its index row manually when adding a competitor).
