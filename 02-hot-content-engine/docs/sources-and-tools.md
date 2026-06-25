# Sources and tools

Every source the engine can pull from, the recommended tool to do it, cost, where it can run, and the gotchas learned the hard way. Start with the free ones; add paid sources only when you see the value.

## At a glance

| Source | Tool / API | Cost | Runs in cloud? | Config file |
|---|---|---|---|---|
| News (RSS) | any RSS parser | free | yes | `config/feeds.json` |
| Hacker News | Algolia HN API | free | yes | `config/keywords.json` |
| Twitter / X | a 3rd-party X data API | paid | yes | `config/twitter-sources.json` |
| LinkedIn | a 3rd-party LinkedIn data API | paid | yes | `config/linkedin-sources.json` |
| Email | IMAP on a dedicated inbox | free | laptop only | `config/email-sources.json` |
| Telegram | Telethon (your own session) | free | laptop only | `config/telegram-channels.json` |

## News (RSS) — start here

The cheapest, highest-signal source. Subscribe to the official blogs of the AI labs, the major tech outlets, and the niche newsletters in your space.

- **Tool**: any RSS/Atom parser.
- **Paywalled outlets** (e.g. some business press) don't expose full RSS. Trick: use **Google News RSS** for their domain to at least catch headlines and links.
- **Freshness**: trust the article's `pubDate`; it's accurate (unlike social, which uses arrival time).
- Fill `config/feeds.json` with feed URLs grouped by topic.

## Hacker News — free, high-signal for technical audiences

- **Tool**: the **Algolia HN Search API** (`hn.algolia.com/api/v1/search`). No key.
- Two passes: (1) your keyword clusters from `config/keywords.json`, (2) a "big news" sweep of high-points front-page items.
- Great for finding what technical founders are actually arguing about.

## Twitter / X — where AI discourse happens first

- **Tool**: a third-party X data API (several exist; pick one with a per-call price you can live with). The official X API is expensive for this use.
- Two query types: `from:` batches of the accounts you track (labs, founders, builders, VCs), and viral keyword search with a minimum-likes floor.
- **Gotcha**: some providers return 0 results when you pass `-filter:retweets`; exclude retweets client-side instead.
- Fill `config/twitter-sources.json` with handles + keyword queries. Run **once a day** (it's paid).

## LinkedIn — founder and operator takes

- **Tool**: a third-party LinkedIn data API. Cheaper providers exist than the big scraping platforms; pick one that does profile + company-page posts and keyword search.
- **Gotcha**: many providers cap concurrency (e.g. 5 simultaneous requests) and silently return empty above it. Use a small concurrency pool.
- Track founder/operator profiles + a few company pages. Fill `config/linkedin-sources.json`.

## Email — the earliest "be first" signal

Vendor announcement emails and newsletters often land before anything hits RSS.

- **Setup**: create a **dedicated** inbox (not your personal one). Subscribe it to AI newsletters and vendor announcement lists. Enable IMAP and create an **app password** (provider → Security → App passwords).
- **Tool**: read it over IMAP. Auto-filter onboarding/transactional mail.
- Runs on your laptop (personal creds), writes a small JSON the cloud job ingests. Fill `config/email-sources.json` with the senders/lists you care about.

## Telegram — niche + regional channels

- **Tool**: **Telethon** with **your own user session** (not a bot — bots can't read most channels).
- Runs on your laptop. For an unattended cloud run you can mint a **StringSession** once and store it as a secret, but logging a personal account in from a datacenter IP can trip a security challenge, so laptop is the safe default.
- Fill `config/telegram-channels.json` with channel usernames.

## A note on Reddit

Reddit is better handled as its own thing (keyword monitoring + reply drafting) than folded into this engine. If you want it, run a separate small scan. Public Reddit JSON and read-only MCP tools exist for browsing; for keyword search across subreddits you'll want a data provider.

## Output: Google Sheets

The ranked board lives in a Google Sheet.

- Create a **service account** in Google Cloud, download its JSON key, and **share the Sheet with the service-account email as Editor**.
- Put the key path + Sheet ID in `.env`.
- The collector writes a ranked tab; you triage the Status column; it syncs back.

## Security

- All keys go in `.env` (gitignored). Never commit them.
- The dedicated email inbox and Telegram session are personal creds, keep them off public CI unless you understand the risk.
