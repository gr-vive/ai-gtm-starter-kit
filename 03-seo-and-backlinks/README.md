# Part 3 — SEO & Backlinks

Two jobs that decide whether anyone finds your content:

1. **On-page SEO + GEO/AEO** — making each page rank in Google *and* get cited by AI search (ChatGPT, Perplexity, Claude, Google AI Overviews).
2. **Backlinks** — earning links from other sites, which is still the strongest off-page ranking signal, done with a precise, low-waste method instead of spray-and-pray outreach.

## What's in this folder

| File | What it covers |
|---|---|
| [`docs/seo-optimization.md`](docs/seo-optimization.md) | The on-page + GEO/AEO playbook: how to structure a page so both Google and AI engines pick it. |
| [`docs/backlink-methodology.md`](docs/backlink-methodology.md) | The **link-intersect** method: find sites that link to several of your competitors but not you, the warmest possible targets. |
| [`docs/ahrefs-setup.md`](docs/ahrefs-setup.md) | How to connect Ahrefs (MCP server or API) and which endpoints to use, with cost discipline. |
| [`skills/backlink-finder/SKILL.md`](skills/backlink-finder/SKILL.md) | An AI skill that runs the backlink method end to end and produces a ranked, routed opportunity list. |
| [`config/competitors.json`](config/competitors.json) | Your competitor domains (the universe to intersect). |
| [`config/filters.json`](config/filters.json) | The selection gate: what makes a link target worth pitching. |
| [`config/routing.json`](config/routing.json) | What action each kind of site gets (pitch / self-list / buy a slot / skip). |

## The core idea behind the backlink method

Don't list everyone who links to one competitor (mostly junk). Find the domains that link to **two or more** of your competitors. Those sites already reference multiple players in your category, so they're far more likely to add you too. Rank by that overlap, then by authority and topical fit. This is the single biggest lever for not wasting outreach effort.

## How it connects to the rest of the kit

- The articles you optimize here are written by Part 1's `seo-article-writer`.
- Your competitor list comes from Part 1's `foundation/market/competitors/approved.md`, keep `config/competitors.json` in sync with it.
- Keyword research (via Ahrefs) feeds the article briefs in Part 1.

## Order of operations

1. Connect Ahrefs (`docs/ahrefs-setup.md`).
2. Fill `config/competitors.json` from your approved competitor list.
3. Run the `backlink-finder` skill → get a ranked opportunity list.
4. For content you publish, apply `docs/seo-optimization.md` before it goes live.
