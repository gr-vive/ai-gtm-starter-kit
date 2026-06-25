---
description: The canonical, approved competitor list. Single source of truth for which competitors may appear in content.
load-when: Before any comparison or landscape content.
applies-to: Comparison, alternatives, and landscape pieces.
---

# Approved competitors

> **How to fill this in.** This table is the single source of truth for which competitors content may name. Other files point here rather than listing competitors inline (inline copies drift; pointers don't). Only competitors on this list get fact packs and appear in published content. Replace the examples.

## Why a single list

- Prevents content from naming a half-researched or off-list competitor.
- Lets you enforce the **3-competitor rule** (landscape content names at least 3 of these).
- One place to add/remove a player as the market shifts.

## Direct competitors

| Name | Domain | Camp / fork side | Fact pack | Notes |
|---|---|---|---|---|
| _CompetitorA_ | _competitora.com_ | _e.g. invoice-based_ | `direct/competitora.md` | _one-line why they're a competitor_ |
| _CompetitorB_ | _competitorb.com_ | _e.g. real-time_ | `direct/competitorb.md` | |
| _CompetitorC_ | _competitorc.com_ | _e.g. subscription-first_ | `direct/competitorc.md` | |

## Adjacent / indirect (name only when relevant)

| Name | Domain | Why adjacent |
|---|---|---|
| _AdjacentX_ | _adjacentx.com_ | _solves a neighboring problem_ |

## Rules

- A competitor must be in the **Direct** table above before content may compare against it in depth.
- To add one: confirm it's intentional, build a fact pack with the `competitor-researcher` skill, then add the row here.
- Detailed facts live in `direct/<name>.md`. This file is only the index + the gate.
