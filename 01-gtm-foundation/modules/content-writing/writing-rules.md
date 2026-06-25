# Writing rules

The rules every article follows. The `seo-article-writer` skill enforces these. Read alongside `foundation/brand/voice-and-tone.md` (voice) and `../../03-seo-and-backlinks/docs/seo-optimization.md` (the deeper SEO/GEO playbook).

## Structure

1. **Title** — sentence case, includes the primary keyword naturally, promises a specific answer.
2. **Executive summary / TL;DR** — 2-4 sentences up top that answer the title's question directly. AI search engines quote this; impatient readers need it.
3. **Body** — question-based H2s where natural. One idea per section. Lead each section with the answer, then explain.
4. **Honest comparison** (if relevant) — follow the 3-competitor rule and `../competitive-analysis/comparison-framework.md`.
5. **FAQ** — 3-6 real questions as H3s with direct answers. Strong for AEO (AI engines lift these verbatim).
6. **One clear next step** — a single, relevant call to action. Not a wall of links.

## Formatting (from `foundation/brand/voice-and-tone.md`)

- Sentence case headings. No em dashes. No buzzwords (see the blocklist).
- Short paragraphs (1-3 sentences). Use lists and tables where they aid scanning.
- Code or config in proper fenced blocks.
- Currency as `$N`; estimates with a tilde.

## SEO / AEO hooks (the minimum)

- **One primary keyword**, used in the title, the first 100 words, and one H2. Don't stuff.
- **Answer-first**: each section's first sentence should stand alone as a quotable answer.
- **Question headings**: phrase H2/H3s as the questions a reader would type or ask an AI.
- **Internal links**: link to your own related pages with descriptive anchors (not "click here").
- **Structured data**: recommend FAQ / Article schema for the page (see SEO docs).

Full playbook: `../../03-seo-and-backlinks/docs/seo-optimization.md`.

## Competitive integrity

- Position on differentiation, not superiority.
- No false dichotomies ("build vs us"). The real market has more options.
- Acknowledge where an alternative genuinely fits.
- No "the only / the first" claims without a dated source.
- Only name competitors from `foundation/market/competitors/approved.md`.

## Quality checklist (run before delivering)

**Brand**
- [ ] Loaded `voice-and-tone.md` + `terminology.md`
- [ ] Tone matches the voice archetype
- [ ] Correct product terminology
- [ ] No blocklisted buzzwords

**Research**
- [ ] Claims have dated sources
- [ ] If landscape content: 3+ approved competitors named
- [ ] No false dichotomies

**Formatting**
- [ ] Sentence case headings, no em dashes
- [ ] Executive summary present
- [ ] Question-based headings where natural
- [ ] FAQ section present

**SEO/AEO**
- [ ] Primary keyword in title + first 100 words + one H2
- [ ] Answer-first sections
- [ ] Internal links with descriptive anchors
- [ ] Schema recommended
