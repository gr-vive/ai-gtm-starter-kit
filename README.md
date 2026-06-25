# AI GTM Starter Kit

A template repository for anyone starting **go-to-market (GTM) marketing for an AI product** with AI assistance (Claude Code, Cursor, or any LLM agent).

It is not a finished marketing site or a tool you run. It is a **structured way of working**: a set of folders, documents, config files, and reusable AI "skills" that turn a vague "we need marketing" into a repeatable system you and an AI assistant can execute together.

Everything here is generic. There are no API keys, no company data, and no proprietary content. Placeholder tokens like `{{COMPANY}}`, `{{PRODUCT}}`, and `{{DOMAIN}}` mark the spots you fill in for your own product.

## Who this is for

- Founders and early marketers at an AI startup who want a content and SEO engine but don't have a marketing team.
- People who "vibe-code" with an AI assistant and want their marketing work to be as structured as their code.
- Anyone who has read scattered advice about GTM, content, and SEO and wants one opinionated, working scaffold.

You do **not** need to be a developer. Most of this repo is markdown you edit in plain English. The few config files are JSON you can fill in with an AI assistant's help.

## What's inside

The kit is three independent parts. Use one, two, or all three.

| Part | Folder | What it gives you |
|---|---|---|
| **1. GTM Foundation** | [`01-gtm-foundation/`](01-gtm-foundation/) | A single source of truth for your brand voice, product facts, market, and competitors, plus reusable AI skills that read it to write on-brand content. This is the backbone everything else pulls from. |
| **2. Hot-Content Engine** | [`02-hot-content-engine/`](02-hot-content-engine/) | A system for collecting trending AI/industry content from many sources, scoring each idea with AI for relevance, and turning the best ones into ready-to-post LinkedIn / X / Reddit drafts. |
| **3. SEO & Backlinks** | [`03-seo-and-backlinks/`](03-seo-and-backlinks/) | How to optimize your content for both classic search and AI search (GEO/AEO), plus a backlink-finder skill that uses Ahrefs to find exactly which sites to pitch for links. |

## How the three parts connect

```
        01-gtm-foundation  (who you are, what you sell, who you compete with)
                 │
     ┌───────────┴────────────┐
     ▼                        ▼
02-hot-content-engine    03-seo-and-backlinks
(what to post about)     (how to rank + get linked)
     │                        │
     └──────────┬─────────────┘
                ▼
        on-brand content that ranks, gets cited by AI,
        and earns backlinks
```

The Foundation is the spine. The Hot-Content Engine feeds it ideas. SEO & Backlinks make the output discoverable.

## Quick start

1. **Read [`GETTING-STARTED.md`](GETTING-STARTED.md)** — a step-by-step walk-through written for non-developers.
2. Open this repo in your AI coding assistant (Claude Code recommended) so it can read [`CLAUDE.md`](CLAUDE.md).
3. Fill in [`01-gtm-foundation/foundation/`](01-gtm-foundation/) with your product facts. Start with `brand/messaging-pillars.md` and `product/overview.md`.
4. Pick the part you need next and follow its `README.md`.

## How to use this as a template

- On GitHub, click **"Use this template"** to create your own copy (or fork it).
- Do a global find-and-replace of the placeholder tokens (see [`GETTING-STARTED.md`](GETTING-STARTED.md#placeholder-tokens)).
- Delete the parts you don't need. Each top-level folder is self-contained.

## Philosophy

Three rules carried over from the production systems this kit is distilled from:

1. **Documents are the source of truth, not the AI's memory.** Your AI assistant should re-read your foundation files every time, never rely on what it "remembers" about your product.
2. **One concept per file.** No 40-page "brand bible." Small, atomic files that a skill can load exactly when needed.
3. **Separate facts from opinion.** Competitor *facts* live in one place; your *positioning against* them is written fresh each time. This keeps content honest and easy to update.

## License

MIT. Use it, fork it, sell the output. See [`LICENSE`](LICENSE).
