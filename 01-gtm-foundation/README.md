# Part 1 — GTM Foundation

The backbone of the kit. This is **one place that holds the truth about your product**, and a set of AI skills that read it to produce on-brand content.

The problem it solves: when you ask an AI to "write a blog post about our product," it makes things up, drifts off-brand, and contradicts what you said last week. The fix is to give the AI a small set of authoritative files to read first, every time.

## The two-layer architecture

```
01-gtm-foundation/
├── foundation/        # Layer 1 — always loaded. The facts.
│   ├── brand/         # how you sound + what you stand for
│   │   ├── voice-and-tone.md
│   │   ├── messaging-pillars.md
│   │   └── terminology.md
│   ├── product/       # what you sell
│   │   ├── overview.md
│   │   └── features.md
│   ├── market/        # the landscape
│   │   ├── icp.md
│   │   ├── positioning.md
│   │   └── competitors/
│   │       ├── approved.md
│   │       └── direct/_TEMPLATE.md
│   └── strategy/
│       └── content-house.md   # your "big idea" every piece reinforces
│
├── modules/           # Layer 2 — loaded per task. The how-to.
│   ├── content-writing/
│   │   ├── MODULE.md
│   │   ├── writing-rules.md
│   │   └── templates/article.md
│   └── competitive-analysis/
│       └── comparison-framework.md
│
└── skills/            # reusable AI workflows that read the above
    ├── seo-article-writer/SKILL.md
    └── competitor-researcher/SKILL.md
```

**Foundation** = atomic, single-concept files, always read first. **Modules** = task-specific guidance a skill loads when it needs it.

## Why split it this way

- **Atomicity.** One concept per file. Voice is separate from terminology is separate from positioning. Small files are easier to keep accurate and cheaper for an AI to load.
- **No duplication.** Each fact lives in exactly one file. Skills point at it. If you change your one-line positioning, you change it once.
- **Facts vs opinion.** Competitor *facts* live in `market/competitors/`. Your *take* on a competitor is written fresh inside each article (by the writer skill), never baked into the fact file. This keeps your competitor research honest and reusable.

## How to fill it in

Order matters. Start at the top of this list and work down. Each file has instructions and a fill-in template at the top.

1. `foundation/brand/messaging-pillars.md`
2. `foundation/product/overview.md`
3. `foundation/market/icp.md`
4. `foundation/market/positioning.md`
5. `foundation/brand/voice-and-tone.md`
6. `foundation/brand/terminology.md`
7. `foundation/product/features.md`
8. `foundation/strategy/content-house.md`
9. `foundation/market/competitors/approved.md` (then one fact pack per competitor)

Fastest way: open a file, then ask your AI assistant to interview you and fill it in.

## The skills

| Skill | What it does |
|---|---|
| [`seo-article-writer`](skills/seo-article-writer/SKILL.md) | Plans and writes an on-brand article: loads your foundation, follows the writing rules, fills the article template, runs a quality check. |
| [`competitor-researcher`](skills/competitor-researcher/SKILL.md) | Builds an objective, opinion-free fact pack for a competitor into `market/competitors/direct/<name>.md`. |

To run a skill in Claude Code, ask: *"Use the seo-article-writer skill to write an article about X."* The skill's `SKILL.md` is the full instruction set.
