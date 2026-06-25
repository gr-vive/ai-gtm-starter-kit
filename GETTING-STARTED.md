# Getting started

A step-by-step guide for using this kit, written for people who are **not** professional developers. If a step mentions a terminal command, you can paste it to your AI assistant and ask it to run and explain it.

## 1. Get your own copy

- On GitHub: click **"Use this template" → Create a new repository**. This gives you a clean copy with no history.
- Or clone it locally and re-init git:
  ```bash
  git clone <this-repo-url> my-ai-gtm
  cd my-ai-gtm
  rm -rf .git && git init
  ```

## 2. Open it with an AI assistant

This kit is designed to be driven by an AI coding agent. The recommended one is **Claude Code**, because the included skills (`SKILL.md` files) and the `CLAUDE.md` guide are written for it. Cursor, Windsurf, or plain Claude/ChatGPT in a chat window also work, you just paste files in manually.

When you open the repo in Claude Code, it automatically reads [`CLAUDE.md`](CLAUDE.md), which tells it how the repo is organized and what the rules are.

## 3. Fill in your foundation (do this first)

Everything else reads from `01-gtm-foundation/foundation/`. Spend your first session here. Recommended order:

1. `foundation/brand/messaging-pillars.md` — what your product is, in one line and three pillars.
2. `foundation/product/overview.md` — what it does and why it's different.
3. `foundation/market/icp.md` — who you sell to.
4. `foundation/market/positioning.md` — how you sit in the market.
5. `foundation/brand/voice-and-tone.md` — how you sound.
6. `foundation/market/competitors/approved.md` — your competitor list.

Tip: open each file, read the instructions at the top, then **ask your AI assistant to interview you** and fill it in. Example prompt:

> Read `01-gtm-foundation/foundation/brand/messaging-pillars.md`. Ask me 5 questions, then fill the file in based on my answers. Keep it factual, no buzzwords.

## 4. Placeholder tokens

The templates use tokens you replace with your own details:

| Token | Replace with | Example |
|---|---|---|
| `{{COMPANY}}` | Your company name | Acme |
| `{{PRODUCT}}` | Your product name | Acme Bill |
| `{{DOMAIN}}` | Your website domain | acme.com |
| `{{CATEGORY}}` | Your product category | AI billing infrastructure |
| `{{ICP}}` | Your ideal customer | AI startup founders |

Find-and-replace them across the repo once your basics are set. Your AI assistant can do this in one pass:

> Replace every `{{COMPANY}}` with "Acme", `{{PRODUCT}}` with "Acme Bill", and `{{DOMAIN}}` with "acme.com" across the whole repo.

## 5. Pick your next part

- Want a steady stream of post ideas? → [`02-hot-content-engine/`](02-hot-content-engine/)
- Want to rank in Google and get cited by ChatGPT/Perplexity? → [`03-seo-and-backlinks/`](03-seo-and-backlinks/)

Each has its own `README.md` with setup steps.

## 6. Keys and secrets

Some parts use third-party APIs (an LLM, social data providers, Ahrefs, Google Sheets). **Never put real keys in any file that gets committed.**

- Copy `.env.example` → `.env` and put values there.
- `.env` is already in [`.gitignore`](.gitignore).
- See each part's `.env.example` for the exact keys it needs.

## 7. Working rhythm

A healthy loop with this kit:

1. **Collect** ideas (Part 2) or pick a target keyword (Part 3).
2. **Write** with a Foundation skill so it's on-brand (Part 1).
3. **Optimize** for SEO/GEO before publishing (Part 3).
4. **Distribute** as social posts (Part 2's drafter).
5. **Earn links** to the best pieces (Part 3's backlink finder).

You don't need all five every day. Start with one, get comfortable, add the next.
