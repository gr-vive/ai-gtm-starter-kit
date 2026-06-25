# Scoring

How the engine decides which ideas are worth your attention. Every **new** item gets one AI scoring call; the result ranks it on the Ideas board.

## The formula

A simple weighted blend. Tune the weights to your taste.

```
priority = 0.55 * relevance + 0.45 * hotness

hotness  = 0.55 * insight + 0.20 * engagement + 0.25 * recency
```

- **relevance** (0-100): how much this matters to *your* ICP and content streams. The AI judges this against your Part 1 foundation.
- **insight** (0-100): is there a real idea here, or is it a recycled listicle? Sharp takes score high; SEO filler scores low.
- **engagement**: likes/points/comments, normalized. **Kept at low weight on purpose** (see below).
- **recency**: newer is hotter; decay over a few days.

### Tiers

- **P0**: priority ≥ 70 — post about this now.
- **P1**: priority ≥ 45 — strong candidate.
- **P2**: everything else kept.
- Below a **relevance floor** (e.g. 40): dismissed (kept in the ledger for dedup, hidden from the board).

## Two opinions baked in

1. **Author credibility boosts insight.** A founder/CEO/VP/operator's take outranks an influencer's or a course-seller's. Feed the author's headline/bio to the model and let it weight credibility. This is why connectors capture `author_headline`.
2. **Engagement floor is deliberately low.** A founder's sharp take with 12 likes beats a 5,000-like listicle. You're hunting for *ideas to react to*, not for what's already viral. High engagement is a weak signal of insight.

## The scoring prompt (template)

Point the prompt at your Part 1 foundation so "relevance" means relevance to *you*.

```
You score content ideas for {{COMPANY}}'s marketing.

Our ICP and what we care about:
<paste or reference 01-gtm-foundation/foundation/market/icp.md>

Our content streams (the themes we publish under):
<paste or reference 01-gtm-foundation/foundation/strategy/content-house.md>

Score this item. Return JSON only:
{
  "relevance": 0-100,   // to OUR ICP and streams, not generic "is this AI news"
  "insight":   0-100,   // real idea vs recycled filler; reward sharp founder takes
  "content_type": "insight | news-reaction | viral-repost",
  "angle": "one sentence: the angle WE would take on this"
}

Author: {{author}} — {{author_headline}}
Title: {{title}}
Text: {{text}}
Engagement: {{engagement}}

Weight a credible author (founder/operator/VP) higher on insight.
Do not reward high engagement on its own.
```

## Cost discipline

- Score **only new items** (the dedup ledger makes this automatic). Never re-score the whole ledger.
- Use a small/fast model for scoring; save the bigger model for drafting.
- Run scoring in a small concurrency pool (e.g. 5 at a time) to stay under rate limits.

## Tuning notes

Keep a running `docs/filter-notes.md` of your own as you tune: which items the model over/under-rated, and the example "good posts" that define what you want. Re-reading your own notes (and a few exemplar posts) before adjusting weights beats guessing.
