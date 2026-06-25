# Part 2 — Hot-Content Engine

A system that watches AI/industry news and opinion leaders across many sources, scores every item with AI for how relevant and "hot" it is, gives you a **ranked ideas board**, and turns the best ideas into ready-to-post **LinkedIn / X / Reddit** drafts.

It solves the blank-page problem: you never again wonder "what should I post about today." The engine surfaces the sharpest, most timely angles, pre-scored, with a draft already written.

This part is **documented as an approach**, not shipped as runnable code. The docs explain exactly what each piece does and which tools to use, so you (with an AI assistant) can build it in your stack of choice in an afternoon. The `config/` files are real templates you fill in.

## The pipeline

```
sources (RSS · Hacker News · Telegram · Email · X · LinkedIn)
   → dedup ledger      (a CSV or sheet — no database needed)
   → AI prioritize     (relevance + insight + author credibility → priority + tier)
   → ranked Ideas board (you triage: pick / dismiss)
   → drafter           (top ideas → LinkedIn / X / Reddit posts)
```

Each stage is independent. You can start with just RSS + one AI scoring pass and grow from there.

## What's in this folder

| File | What it covers |
|---|---|
| [`ARCHITECTURE.md`](ARCHITECTURE.md) | The full data flow, the dedup ledger, and how to schedule it for free. |
| [`docs/sources-and-tools.md`](docs/sources-and-tools.md) | Every source, the exact tool/API to use, cost notes, and gotchas. |
| [`docs/scoring.md`](docs/scoring.md) | The AI scoring formula and the prompt that drives it. |
| [`docs/turning-ideas-into-posts.md`](docs/turning-ideas-into-posts.md) | How to turn a ranked idea into a platform-native post. |
| [`config/*.json`](config/) | Template source lists + keyword clusters. Fill these with your own. |
| [`.env.example`](.env.example) | The keys this part can use (all optional, add sources incrementally). |

## Minimum viable version

You don't need all six sources to start. The cheapest useful setup:

1. **RSS** (free) — 10-30 feeds relevant to your space.
2. **One AI scoring pass** — score each new item for relevance to your ICP (see `docs/scoring.md`).
3. **A Google Sheet or CSV** as the ranked board.

Add Hacker News (free), then paid social sources (X, LinkedIn), then a dedicated newsletter inbox, as you see value.

## How it connects to the rest of the kit

- Scoring relevance is judged against your **ICP** and **content streams** from Part 1 (`01-gtm-foundation/foundation/market/icp.md`, `strategy/content-house.md`). Point the scoring prompt at them.
- Drafted posts should follow your **voice** (`01-gtm-foundation/foundation/brand/voice-and-tone.md`).
- Ideas worth a full article get handed to Part 1's `seo-article-writer`.
