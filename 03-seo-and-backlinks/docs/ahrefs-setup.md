# Connecting Ahrefs

The backlink method and keyword research both run on Ahrefs data. There are two ways to connect it; the MCP server is the easiest for an AI-assistant workflow.

## Option A — Ahrefs MCP server (recommended)

An MCP (Model Context Protocol) server exposes Ahrefs as tools your AI assistant can call directly, no glue code.

1. You need an Ahrefs plan that includes API access (the API is a paid add-on / higher tier).
2. Add the Ahrefs MCP connector to your AI client. In Claude (claude.ai) this is **Settings → Connectors → Add custom connector**; in Claude Code it's an `mcp` server entry. Authenticate with your Ahrefs account/token when prompted.
3. Once connected, the assistant can call the Ahrefs tools by name. They appear as `site-explorer-*`, `keywords-explorer-*`, `rank-tracker-*`, etc.

> Note on values: Ahrefs returns monetary values in **USD cents**. Divide by 100 to display dollars.

## Option B — Ahrefs API v3 directly

If you'd rather call the REST API from a script:
- Base: the Ahrefs API v3 endpoints.
- Auth: your API token (store it in `.env` as `AHREFS_API_KEY`, never commit it).
- You build the HTTP calls yourself. More control, more plumbing.

## The endpoints the backlink method uses

| Purpose | Endpoint (MCP tool name) |
|---|---|
| Referring domains for a competitor (and your own exclusion set) | `site-explorer-referring-domains` |
| The actual linking pages (to classify link type) | `site-explorer-all-backlinks` |
| Domain authority of a candidate | `site-explorer-domain-rating` |
| Backlink overview stats | `site-explorer-backlinks-stats` |

Typical referring-domains query: server-side filter `is_spam=false`, `dofollow_links>0`, `traffic_domain>50`; select `domain, domain_rating, traffic_domain, dofollow_links`; order by `traffic_domain` desc.

## The endpoints keyword research uses (feeds Part 1 article briefs)

| Purpose | Endpoint (MCP tool name) |
|---|---|
| Volume / difficulty for a keyword | `keywords-explorer-overview` |
| Related + matching terms | `keywords-explorer-related-terms`, `keywords-explorer-matching-terms` |
| Where your pages rank | `rank-tracker-overview` |
| Your own organic keywords / top pages | `site-explorer-organic-keywords`, `site-explorer-top-pages` |

## Cost discipline (important)

Ahrefs bills per row/credit. Two rules:

1. **Fetch once per article keyword.** When the article writer needs volume/difficulty, call `keywords-explorer-overview` once for the confirmed primary keyword and store the result. Never silently re-fetch existing rows.
2. **Cache competitor pulls.** For the backlink method, cache each competitor's referring domains and your own exclusion set between runs. Re-fetch only new competitors or on an explicit forced refresh.

## If you don't have Ahrefs

- Some metrics have free alternatives (Google Search Console gives you your own rankings/clicks for free).
- The link-intersect *method* works with any backlink data source (Moz, Semrush, free-tier tools); the skill and configs are tool-agnostic, just swap where the referring-domain data comes from.
- For a one-off, a free Ahrefs "Domain Rating" checker plus manual competitor research can bootstrap a first list, just slower.
