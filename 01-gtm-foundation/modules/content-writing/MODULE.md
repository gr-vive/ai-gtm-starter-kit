# Content-writing module

Task-specific guidance and templates for producing written content. Loaded by the `seo-article-writer` skill (and useful to read before any writing task).

## What this module provides

- **`writing-rules.md`** — the rules an article must follow: structure, formatting, SEO/AEO hooks, the quality checklist.
- **`templates/article.md`** — the skeleton an article is filled into (frontmatter + section order).

## Which skill consumes this module

- `../../skills/seo-article-writer/SKILL.md` reads `writing-rules.md` and the relevant template before drafting.

## Foundation dependencies

Before writing, the skill always loads these from `foundation/`:

- `brand/voice-and-tone.md`
- `brand/messaging-pillars.md`
- `brand/terminology.md`
- `product/overview.md`
- `strategy/content-house.md`

And, for comparison content, `market/competitors/` + `../competitive-analysis/comparison-framework.md`.

## What is NOT in this module

- Brand voice (lives in `foundation/brand/`).
- Product facts (live in `foundation/product/`).
- The competitor comparison framework (lives in `../competitive-analysis/`).
