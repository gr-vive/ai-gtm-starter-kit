# Architecture

How the hot-content engine fits together. The design goal is **cheap, simple, and stateless-enough to run on a free cron**.

## Data flow

```
[collect]  each connector fetches recent items from its source
              → normalizes to a common shape
              → upserts into the dedup ledger (skip if seen before)
[score]    every NEW item gets one AI scoring call
              → relevance, insight, content_type, angle  → priority + tier
[publish]  write a ranked, deduped view to the Ideas board (Google Sheet / CSV)
[draft]    on demand: take top ideas → AI writes platform posts
```

Stages are loosely coupled. `collect` can run every 15 minutes; `draft` runs only when you ask.

## The normalized item shape

Every connector outputs the same fields, so scoring and dedup don't care where an item came from:

```
{
  "dedup_key": "stable hash of url or title+source",
  "source": "rss | hackernews | telegram | email | twitter | linkedin",
  "title": "...",
  "text": "the post / summary / first paragraphs",
  "url": "...",
  "author": "name or handle",
  "author_headline": "their bio/title, if available — used for credibility",
  "engagement": 0,            // likes/points/comments if available
  "published_at": "ISO timestamp"
}
```

## The dedup ledger (no database)

State lives in **one CSV file** (or a Google Sheet tab). Each row is an item keyed by `dedup_key`. On every collect:

- New `dedup_key` → insert, mark for scoring.
- Seen `dedup_key` → skip (and never resurface a `dismissed` idea).

This is deliberately boring. A CSV in the repo (or a Sheet) is enough for thousands of items, needs no hosting, and is trivially inspectable. Add a real database only if you outgrow it.

## The Ideas board

A Google Sheet is the human interface. One tab, ranked by priority, with the full post text inline so you can read without clicking. You set a **Status** column (`picked` / `dismissed`) and that round-trips back to the ledger so dismissed ideas never come back.

- Use a service account to write to the Sheet (see `.env.example` and `docs/sources-and-tools.md`).
- Columns: Date · Tier · Priority · Source · Type · Title · Text · URL · Author · Engagement · Relevance · Angle · Status.

## Scheduling for free

Run it on **GitHub Actions cron** (free for public repos, generous free minutes for private). A sensible split:

| Job | Cadence | What it runs |
|---|---|---|
| fast lane | every 15 min | free sources only (RSS + Hacker News) — catches breaking items |
| daily | once a day | all sources incl. paid (X, LinkedIn) + email + Telegram |
| digest | daily / weekly | one AI-curated summary message to Slack (optional) |

Serialize the collect jobs with a shared concurrency group so two runs never write the ledger at once.

### Sources that can't run in the cloud

Some sources use **personal sessions** (Telegram via your own account, a personal email inbox). Those run on your laptop, write a small JSON file, and the cloud job ingests that file. Everything else (RSS, HN, X via API, LinkedIn via API) runs fine in CI. See `docs/sources-and-tools.md` for which is which.

## Cost shape

- RSS + Hacker News: free.
- AI scoring: a few cents per run (one small call per new item; only new items are scored).
- X / LinkedIn data APIs: paid per call — run those once a day, not every 15 minutes.
- Google Sheet + GitHub Actions: free.

The expensive mistake is re-scoring everything every run. Only score new items; the ledger makes that automatic.
