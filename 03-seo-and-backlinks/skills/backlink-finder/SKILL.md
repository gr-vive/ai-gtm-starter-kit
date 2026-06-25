---
name: backlink-finder
description: Find and rank backlink opportunities for {{DOMAIN}} using the link-intersect method over competitors' referring domains (via Ahrefs), then route each survivor to an action. Produces a prioritized, routed opportunity list. Use when the user wants to find where to earn backlinks.
---

# Backlink finder

Runs the link-intersect backlink method end to end and produces a ranked, routed opportunity list. Full method: `../../docs/backlink-methodology.md`. Ahrefs connection + endpoints: `../../docs/ahrefs-setup.md`.

## Files to read before starting

- `../../docs/backlink-methodology.md` — the method (the canonical description of every step).
- `../../config/competitors.json` — your domain + competitor universe.
- `../../config/filters.json` — the selection gate (tune here, not in prose).
- `../../config/routing.json` — what action each site type gets.
- Cross-check the competitor list against `../../../01-gtm-foundation/foundation/market/competitors/approved.md` and reconcile any drift.

## Prerequisites

- Ahrefs connected (MCP or API). If not, walk the user through `../../docs/ahrefs-setup.md` first.
- `config/competitors.json` filled with your domain and 5+ competitor domains.

## Workflow

### Step 1 — Load config
Read all three config files. Confirm the self domain and competitor list with the user. Warn if competitors here don't match the approved list in Part 1.

### Step 2 — Fetch (cost-disciplined)
For each competitor, call `site-explorer-referring-domains` (filter `is_spam=false`, `dofollow_links>0`, traffic floor; select `domain, domain_rating, traffic_domain, dofollow_links`). For the self domain, pull the full referring-domain set (the exclusion list). **Use cache**: skip competitors already fetched unless the user forces a refresh. Tell the user the estimated row/credit cost before a large pull.

### Step 3 — Pool + intersect
Union all competitor referring domains. Compute `overlap_count` per domain = number of distinct competitors linking to it.

### Step 4 — Subtract
Remove every domain already in the self exclusion set.

### Step 5 — Filter
Apply every rule in `filters.json`: spam flag + spam-pattern regex, dofollow-capable, `min_domain_rating`, `min_traffic_domain`, `platform_denylist`, `category_denylist`, and the overlap rule (`>=2`, or `1` if topically relevant).

### Step 6 — Classify
For each survivor, read the linking page(s) via `site-explorer-all-backlinks` (`url_from, title, anchor, snippet`) and tag the link type from `filters.link_type_targets`. `other` → held for manual review.

### Step 7 — Score + rank
```
score = 0.35*overlap + 0.20*norm(DR) + 0.15*norm(traffic)
      + 0.20*topical_relevance + 0.10*linktype_actionability
```
Normalize DR and traffic across the candidate set. Sort descending.

### Step 8 — Route
Apply `routing.json`: assign each survivor exactly one action (`email_outreach`, `report_newsletter`, `report_directory`, `exclude` with a reason, or `needs_review`). Use the `known_sites` map as a cache; classify unknown domains by probing the signal pages (`/advertise`, `/write-for-us`, `/submit`, etc.) and the site's topic.

### Step 9 — Deliver
Write a ranked report (Markdown or CSV) grouped by action:
- **Email outreach** — domain, DR, overlap, link type, suggested pitch angle.
- **Newsletters to consider** — with their advertise/sponsor page.
- **Directories to self-list** — with their submit page.
- **Excluded** — with the reason (so the user can override).
- **Needs review** — ambiguous, for a human glance.

Report the cost spent and what was served from cache.

## What this skill does NOT do

- Does **not** send any outreach email. Drafting/sending is a separate, later step the user explicitly opts into, only after reviewing the list.
- Does not re-fetch cached competitors without an explicit forced refresh.
- Does not pitch sites classified `other` or `exclude`.
