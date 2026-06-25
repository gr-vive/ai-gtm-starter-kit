# SEO + GEO/AEO optimization

How to make a page rank in classic search **and** get cited by AI search engines. For an AI product, the second matters as much as the first: your buyers increasingly ask ChatGPT, Perplexity, Claude, and Google AI Overviews "what's the best tool for X" before they ever open Google.

Definitions:
- **SEO** — ranking in the classic blue-link results.
- **GEO** (Generative Engine Optimization) / **AEO** (Answer Engine Optimization) — getting quoted and cited by AI answer engines.

The good news: the same fundamentals serve both. AI engines mostly cite pages that are clear, well-structured, trustworthy, and crawlable.

## The non-negotiables (do these on every page)

### 1. Answer-first structure

- A **summary / TL;DR** at the top that directly answers the page's core question in 2-4 sentences. AI engines lift this almost verbatim.
- Each section's **first sentence** is a standalone, quotable answer. Then explain.
- **Question-based headings** (H2/H3) that match how people actually ask, in search boxes and to AI.

### 2. Structured data (schema)

Add JSON-LD so machines understand the page:
- `Article` (or `BlogPosting`) on every article.
- `FAQPage` on the FAQ section (huge for AEO; engines quote Q&A pairs).
- `Organization` + `Person` (with `sameAs` links) so your brand is a recognized entity.
- `Product` / comparison markup on comparison pages where applicable.

### 3. Crawlability for AI bots

- A clean `robots.txt` that doesn't accidentally block AI crawlers (GPTBot, ClaudeBot, PerplexityBot, Google-Extended) unless you intend to.
- Server-rendered content. If your page needs JavaScript to show its text, many AI crawlers won't see it. Render the words in HTML.
- A correct sitemap, fast load (Core Web Vitals), and HTTPS.

### 4. An `llms.txt` (emerging standard)

A plain-text file at your domain root that points AI systems at your most important pages and explains your site. Cheap to add, increasingly read by AI tools. Generate one from your sitemap + key pages.

### 5. E-E-A-T signals

Experience, Expertise, Authoritativeness, Trust. Concretely:
- Named authors with real bios and `sameAs` profile links.
- Dated content and "last updated" stamps.
- Sources/citations for claims (also makes the AI trust you).
- A clear about/contact page and consistent brand entity across the web.

## On-page checklist (per article)

- [ ] One **primary keyword**, in the title, first 100 words, and one H2 (no stuffing).
- [ ] Summary/TL;DR that answers the title up top.
- [ ] Question-based H2/H3s; answer-first sections.
- [ ] FAQ section with `FAQPage` schema.
- [ ] `Article` schema with author + dates.
- [ ] Internal links to related pages with **descriptive anchors** (not "click here").
- [ ] Meta title + meta description written to earn the click (this is your SERP ad).
- [ ] Text rendered in HTML (not JS-only).
- [ ] Sources for every factual claim.

## What ranks for AI product categories specifically

The highest-intent, highest-converting pages for an AI startup:

1. **Comparison pages** — "{{PRODUCT}} vs CompetitorA." The reader is in-market.
2. **"Alternatives to X" pages** — capture demand searching for a competitor.
3. **"Best [category] tools" landscape pages** — name 3+ competitors honestly (the 3-competitor rule from Part 1).
4. **Integration pages** — "{{PRODUCT}} + [popular tool in your stack]."
5. **Mechanism explainers** — "how X actually works," which both readers and AI engines reward for clarity.

Write these with Part 1's `seo-article-writer`; it bakes in the structure above.

## Internal linking

- Link new articles **up** to your core landing/hub pages and **across** to siblings on the same topic.
- Use varied, descriptive anchor text. Over-using one exact-match anchor everywhere reads as manipulation; vary it.
- Avoid orphan pages (no internal links pointing in). Every page should be reachable.

## Measuring it

- **Google Search Console** for classic-search impressions, clicks, position, and CTR. Low-CTR / high-impression pages = rewrite the title + meta.
- For **AI visibility**, track whether your brand gets mentioned/cited in AI answers for your target prompts. Tools are emerging (some SEO suites now report "AI overview" presence and brand mentions in AI responses); at minimum, manually ask the AI engines your target questions and see if you appear.

## Tools

- **Ahrefs** (or similar) for keyword research, rank tracking, and the backlink work in `backlink-methodology.md`. See `ahrefs-setup.md`.
- **Google Search Console** (free) for your own performance data.
- A schema generator/validator (Google's Rich Results Test) to check your JSON-LD.
