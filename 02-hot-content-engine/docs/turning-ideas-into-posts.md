# Turning ideas into posts

Once the board has ranked ideas, the drafter turns the best ones into platform-native posts. The goal is posts that read like a sharp human wrote them, not "AI content."

## The drafting flow

1. Take the top N `picked` (or high-priority) ideas from the board.
2. For each, generate one draft **per target platform** (LinkedIn / X / Reddit), each native to that platform.
3. Write them to a "Drafts" tab or file for you to review, edit, and post.

Posting itself stays manual (or goes through a scheduler like Buffer). The engine drafts; a human approves.

## A layered drafting model

Don't ask the AI for "a LinkedIn post about this link." Build the post in layers so it has a spine:

1. **Pain** — which ICP pain does this idea touch? (from `01-gtm-foundation/foundation/market/icp.md`)
2. **Take** — your one-sentence opinion on the news (the `angle` from scoring is a starting point).
3. **Archetype** — the post shape: hot take, teardown, contrarian, "here's what most people miss," personal story.
4. **Bridge** — connect to your product's worldview *without* a hard pitch (most posts shouldn't pitch at all).

## Platform rules

| Platform | Length | Voice | Don'ts |
|---|---|---|---|
| **LinkedIn** | 1 idea, ~3-8 short lines, line breaks | first person, operator-to-operator | no hashtag soup, no "Agree?" bait, no link in the first line (kills reach — put it in a comment) |
| **X** | punchy, often a 2-3 post thread | terse, confident | no hashtags, no thread-bait ("🧵👇" sparingly) |
| **Reddit** | genuinely helpful, context-first | a real person in that subreddit | no promo unless the subreddit allows it; read the subreddit's rules first; disclose any affiliation |

**Reddit especially**: each subreddit has its own culture and self-promotion rules. A post that works in one gets you banned in another. Check the rules before drafting, and default to "be helpful, mention nothing" unless promotion is explicitly allowed.

## The drafting prompt (template)

```
Write a {{platform}} post from this idea.

Our voice:
<reference 01-gtm-foundation/foundation/brand/voice-and-tone.md>

The idea:
  Title: {{title}}
  Source: {{url}}
  Our angle: {{angle}}
  ICP pain it touches: {{pain}}

Rules:
- Native to {{platform}} (see the platform rules doc).
- One clear idea. Lead with the hook, not the context.
- Apply our voice; obey the word blocklist.
- Do NOT hard-pitch the product. At most, end with a light bridge to our worldview.
- {{platform-specific don'ts}}

Return the post text only.
```

## From post to article

If an idea is too big for a post, it's an article. Hand it to Part 1's `seo-article-writer` skill with the angle and source, and it'll produce a full on-brand, SEO-optimized piece.

## Keep it human

Run drafts through a quick "does this sound like a person?" pass. Cut: opening throat-clearing ("In today's fast-paced world"), the blocklisted buzzwords, and any sentence that could appear under any company's logo. The point of capturing *founder takes* upstream is to sound like one downstream.
