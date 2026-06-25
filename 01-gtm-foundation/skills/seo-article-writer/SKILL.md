---
name: seo-article-writer
description: Plan and write an on-brand, SEO/AEO-optimized article for {{PRODUCT}}. Loads the brand/product/market foundation, follows the writing rules, fills the article template, and runs a quality check before delivering. Use when the user asks to write a blog post, comparison, alternatives page, or guide.
---

# SEO article writer

Writes a complete, on-brand article that follows your foundation and the writing rules, optimized for both classic search and AI search (GEO/AEO).

## Files to read before starting (always)

Load these first, every time. Never rely on memory of the product.

- `../../foundation/brand/voice-and-tone.md`
- `../../foundation/brand/messaging-pillars.md`
- `../../foundation/brand/terminology.md`
- `../../foundation/product/overview.md`
- `../../foundation/strategy/content-house.md`
- `../../modules/content-writing/writing-rules.md`
- `../../modules/content-writing/templates/article.md`

For comparison / alternatives / landscape content, also load:

- `../../foundation/market/competitors/approved.md` (the gate)
- the relevant `../../foundation/market/competitors/direct/<name>.md` fact pack(s)
- `../../modules/competitive-analysis/comparison-framework.md`

For product-capability claims, also load `../../foundation/product/features.md`.

## Workflow

### Step 1 — Brief

Confirm with the user (or infer and state your assumptions):
- Topic and `article_type` (explainer / comparison / alternatives / guide / landscape).
- **Primary keyword** (one). If unknown, propose 2-3 candidates and pick with the user. For volume/difficulty, see `../../../03-seo-and-backlinks/docs/ahrefs-setup.md`.
- Which **content stream** and **pillar** it maps to (from `content-house.md`). If it fits none, flag it as off-strategy before writing.

### Step 2 — Research (only if needed)

If the topic touches competitors or claims you can't source from the foundation:
- For competitors, use the `competitor-researcher` skill first so facts come from a fact pack, not the open web.
- For external claims, web-search and record dated source URLs. Never invent numbers.

### Step 3 — Outline

Produce an outline using `templates/article.md`: title, summary, question-based H2s, comparison section (if any), FAQ, next step. Map H2s to reader questions. Get a quick nod from the user before drafting (optional but recommended for long pieces).

### Step 4 — Draft

Write the full article into the template. Apply:
- The voice archetype and formatting rules.
- Answer-first sections (first sentence of each = a standalone, quotable answer).
- The SEO/AEO hooks from `writing-rules.md` (primary keyword placement, question headings, internal links, schema recommendation).
- For comparisons: the 3-competitor rule + the fork + honesty rules.

### Step 5 — Quality check

Run the full checklist in `writing-rules.md`. Fix anything that fails. Specifically verify:
- No buzzwords from the blocklist, no em dashes, sentence-case headings.
- Primary keyword in title + first 100 words + one H2.
- If landscape: 3+ approved competitors named.
- Every factual/competitor claim is sourced.
- FAQ present; one clear next step.

### Step 6 — Deliver

Save to your articles folder (e.g. `outputs/blog/<slug>.md`) with frontmatter filled. Tell the user: file path, primary keyword, the schema you recommend, and any claim you couldn't source (flag explicitly).

## What this skill does NOT do

- Does not invent product facts. If a fact isn't in `foundation/`, ask or research, then add it to the right foundation file.
- Does not store opinion in competitor fact packs (opinion is written here, in the article).
- Does not publish to any live site (that's a separate step you control).
