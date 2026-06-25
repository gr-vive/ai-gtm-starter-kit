# Backlink methodology

How to find exactly where to earn backlinks, with minimal wasted effort. Backlinks remain one of the strongest off-page ranking signals; the trick is choosing targets that are actually receptive instead of emailing the whole internet.

## The core idea: link intersect, not a flat gap

A naive "list everyone who links to a competitor" is mostly junk: CMS footprints, social profiles, job posts, SEO spam. The signal that matters is **overlap**.

> A domain that links to **two or more** of your competitors already references multiple players in your category. It is far more likely to accept you too.

So you rank by overlap first, then by authority, topical fit, and how pitch-able the link is.

## The pipeline

```
[0] Config        your domain + competitors + filters
        |
[1] Fetch         Ahrefs → referring domains per competitor (+ your own)
        |
[2] Pool+Intersect  overlap_count = # distinct competitors linking to each domain
        |
[3] Subtract      drop domains that already link to you
        |
[4] Filter        spam / platform / category denylists + DR & traffic floors + overlap floor
        |
[5] Classify      read the linking page → link type (listicle / resource / media / ...)
        |
[6] Score+Rank    weighted score → prioritized opportunity list   ← THE DELIVERABLE
        |
[7] Route         each survivor → one action (pitch / self-list / buy slot / skip)
        |
[8] (optional) Enrich → contact email, then draft + send outreach
```

Steps 0-7 are the analysis. Step 8 (actually sending email) is deliberately the **last** thing you wire up, and only after you've reviewed the opportunity list. Outreach from a cold domain can hurt; review first.

## Step detail

### [1] Fetch
For each competitor, pull **referring domains** from Ahrefs with a server-side filter (`is_spam=false`, `dofollow_links>0`, a traffic floor), selecting `domain, domain_rating, traffic_domain, dofollow_links`. For your own domain, pull the full referring-domain set, that's your exclusion list. (Endpoints in `ahrefs-setup.md`.)

### [2] Pool + intersect
Union all competitor referring domains. For each unique domain, `overlap_count` = how many distinct competitors link to it. This is the primary ranking signal.

### [3] Subtract
Remove any domain already linking to you. Never pitch a site that already links to you.

### [4] Filter — the selection gate
A domain survives only if it passes every rule in `config/filters.json`:
- not already linking to you (step 3)
- `is_spam = false`, and doesn't match the spam-pattern regex (PBN `.shop`/`.agency` footprints, "buybacklinks"-style domains)
- dofollow-capable
- `domain_rating >= 20` (tune)
- `traffic_domain >= 100` (tune)
- not in `platform_denylist` (Substack, Medium, GitHub, social, generic CMS hosts, wikis, etc. — these are hosted pages/profiles, not editorial opportunities)
- not in `category_denylist` (job boards, podcast-hosting platforms)
- `overlap_count >= 2`, OR overlap 1 **and** topically relevant (matches your `topical_keywords`)

### [5] Classify link type
For each survivor, read the actual linking page(s) (`url_from, title, anchor, snippet`) and tag the opportunity type from `filters.link_type_targets`:
- **listicle** ("best X / top tools / alternatives to") → ask to be added
- **resource page** ("tools we use") → ask to be included
- **editorial media** → pitch a contributor piece or expert quote
- **newsletter** (covered a competitor) → brief the author / consider a sponsor slot
- **directory** (SaaS/startup database) → claim or request a listing
- **dev blog** → offer a technical guest post / integration note
- **podcast** → pitch a guest spot

Anything that classifies as `other` is held for manual review, never auto-pitched.

### [6] Score + rank — the deliverable
```
score = 0.35*overlap + 0.20*norm(DR) + 0.15*norm(traffic)
      + 0.20*topical_relevance + 0.10*linktype_actionability
```
Output: a ranked opportunity list (CSV / Markdown / Sheet). This is what you review.

### [7] Route the action
Use `config/routing.json` to send each survivor to exactly one action: direct **email outreach**, **buy a newsletter slot**, **self-list in a directory** (no email), or **exclude** (commercial blogs that won't link to a competitor, events, wrong vertical, tier-1 press too expensive, foreign-market, incidental noise). Ambiguous ones go to `needs_review` for a human glance.

## Cost discipline

Ahrefs charges per row returned. A first run on ~5 competitors costs a few thousand units; a full sweep of ~25 competitors at a sane row limit is still modest. **Cache** your own referring-domain set and per-competitor pulls between runs; only re-fetch new competitors or on a forced refresh. Don't re-pull everything every time.

## What "we can contribute" means

Only propose places where a contribution is *real*: a roundup missing you, a resource page you fit, a media outlet that covered a competitor, a directory you can list in, a dev blog open to guest posts, a podcast that hosts founders. If there's no honest way to contribute, exclude it.
