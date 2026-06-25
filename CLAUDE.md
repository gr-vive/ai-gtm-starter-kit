# CLAUDE.md — AI GTM Starter Kit

This file guides AI assistants (Claude Code, Claude via API, other agents) working in this repository. Humans should read `README.md` and `GETTING-STARTED.md` first.

This is a **template repo**. The person using it is adapting it for their own AI product. Treat placeholder tokens (`{{COMPANY}}`, `{{PRODUCT}}`, `{{DOMAIN}}`, `{{CATEGORY}}`, `{{ICP}}`) as values the user will fill in. Never invent real product facts. If a foundation file is still a template, ask the user for the facts rather than guessing.

## Session start

1. **Health check** — note which parts are set up:
   - Is `01-gtm-foundation/foundation/` filled in, or still placeholder text?
   - Does a `.env` exist for the part the user wants to work in (Part 2 or Part 3)?
2. **Present a short menu** and ask what the user wants to do:
   - Fill in or update brand / product / market foundation → edit `01-gtm-foundation/foundation/*`
   - Write an on-brand article → use the `seo-article-writer` skill
   - Research a competitor → use the `competitor-researcher` skill
   - Set up the content-collection engine → `02-hot-content-engine/README.md`
   - Find backlink opportunities → use the `backlink-finder` skill (`03-seo-and-backlinks/`)
   - Optimize a page for SEO/GEO → `03-seo-and-backlinks/docs/seo-optimization.md`
   - Something else → ask clarifying questions first.

## Repository architecture

Three independent parts. Each can be used or deleted on its own.

```
ai-gtm-starter-kit/
├── 01-gtm-foundation/      # source of truth + content skills
│   ├── foundation/         # Layer 1. Universal. Loaded always.
│   │   ├── brand/          # voice, messaging pillars, terminology
│   │   ├── product/        # overview, features
│   │   ├── market/         # ICP, positioning, competitors/
│   │   └── strategy/       # content-house (the big idea)
│   ├── modules/            # Layer 2. Task-specific. Loaded per task.
│   │   ├── content-writing/
│   │   └── competitive-analysis/
│   └── skills/             # reusable Claude skills
│
├── 02-hot-content-engine/  # collect → score → draft posts
│   ├── config/             # source lists + keyword clusters (templates)
│   └── docs/               # how each source works, scoring, drafting
│
└── 03-seo-and-backlinks/   # rank + get cited + earn links
    ├── docs/               # SEO/GEO, backlink method, Ahrefs setup
    ├── config/             # competitor + filter + routing templates
    └── skills/             # backlink-finder skill
```

### Foundation vs modules

- **`foundation/`** holds atomic, single-concept files loaded always. Brand voice, product facts, positioning.
- **`modules/`** holds task-specific content that becomes input for a skill. Each module has a `MODULE.md` explaining what it provides and which skill consumes it.

### Two governance rules (carry these forward)

- **Atomicity**: every file in `foundation/` describes exactly one concept. No mixed "brand bible" files. If you need to describe two concepts, make two files.
- **No duplication**: content lives in exactly one place. Skills read the canonical file via relative paths; they never keep copies. If two files say the same thing, that's a bug.

## Non-negotiable content rules

These are good defaults for AI-product GTM. The user can change them, but keep them unless told otherwise.

- **Write in English** (or the user's chosen content language), consistently.
- **Sentence case for headings.** Never Title Case.
- **No em dashes.** Use periods or semicolons.
- **No buzzwords**: seamless, revolutionary, game-changing, cutting-edge, innovative, best-in-class, world-class, next-generation, paradigm shift.
- **Question-based headings where natural** — this helps AI search engines (AEO) quote you.
- **Never write false dichotomies.** Not "build it yourself vs {{PRODUCT}}." The real market has more options.
- **Position on differentiation, not superiority.** "{{PRODUCT}} is purpose-built for X," not "{{PRODUCT}} is the best."
- **Never make monopoly claims** ("the only," "the first") without a verifiable source.
- **The 3-competitor rule** (landscape content): when the reader is asking "what are my options," name at least 3 real competitors. Showing fewer creates a false choice. In a head-to-head ("X vs Y"), cover only the two named.

## Source of truth

The foundation files in this repo are canonical. Never use cached knowledge about the user's product. If a fact isn't in the files, ask or research, then write it into the right foundation file so it's there next time.

## Skills

Skills live under `01-gtm-foundation/skills/` and `03-seo-and-backlinks/skills/`. Each is a `SKILL.md` with frontmatter (`name`, `description`) and a workflow. They read foundation/module files via relative paths. To use one, follow its instructions step by step. If you edit a `SKILL.md`, changes apply on the next invocation.

## Safety

- Never expose or commit API keys, tokens, or credentials. Use `.env` (gitignored).
- Never commit `.env` files or any real customer data.
- Confirm before destructive operations.
- This is a template the user will share publicly. Keep it free of any real company's private information.
