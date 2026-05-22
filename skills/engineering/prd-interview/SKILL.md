---
name: prd-interview
description: Interactive interview that drives the user through writing a product-level PRD — problem, target users, goals and non-goals, success metrics, feature breakdown, constraints, risks, rollout. One question at a time, recommends an answer at every step, writes the PRD to a markdown file incrementally so the user can react to the doc as it grows. Use when the user wants to author a PRD from scratch, plan a new initiative or product, draft a strategic spec, or asks to "interview me on a PRD" or "draft a PRD together". For single-feature work briefs, use `to-frd` instead.
---

<what-to-do>

Run an interview that produces a product-level PRD. Walk the user through sections in dependency order, ask one focused question at a time, and recommend an answer for each. Write the PRD to a markdown file incrementally as each section lands so the user always has something concrete to react to.

If the user did not pass a path, ask once where to save the PRD (default suggestion: `docs/prd/<slug>.md`, slug derived from the working title), then remember it for the rest of the session.

Capture a working title and one-paragraph problem statement from the user's very first turn — including the initial prompt. Write a minimal stub (H1 + Problem header) on first save. No frontmatter, no TOC, no status field.

Re-read the file from disk before every write. The user will be editing in parallel; preserve their changes. Never overwrite — append new sections, or edit a specific section in place when asked.

</what-to-do>

<supporting-info>

## Scope of this skill

A **PRD** here means a product- or initiative-level strategic document: 1–3 dense pages that frame why the work exists, who it's for, and what success looks like. It is not directly implementable — it later decomposes into feature-level briefs (FRDs) that get coded.

If the user is describing a single feature ("add a mute toggle", "fix the login flow"), redirect: that's `to-frd` territory, not this skill.

If the user already has a partial PRD on disk, treat it as input — read it, summarise what's there, and continue from the first incomplete section rather than starting over.

## Interview structure

Walk these sections in order. Dependencies are real — Goals depend on Users and Problem; Metrics depend on Goals; Feature Breakdown depends on all of the above. The user can jump sections, but flag the dependency they're skipping ("OK, doing rollout — note that Success Metrics is still empty, which the rollout gates will want to reference").

1. **Working title** — one line; can change later
2. **Problem** — from the user's perspective, one paragraph
3. **Context** — why now; business/market/technical background; relevant prior work
4. **Target Users** — who this is for, with enough detail that later decisions can reference them
5. **Goals** — 1–3 numbered goals; what success looks like
6. **Non-Goals** — what this PRD is explicitly NOT trying to do
7. **Success Metrics** — measurable, time-bound; one or two per goal
8. **Feature Breakdown** — numbered list of slices that together deliver the goals; each slice should be roughly the scope of one FRD
9. **Constraints** — technical, regulatory, time, team, budget, dependencies
10. **Risks and Open Questions** — what could derail; what's still unknown
11. **Rollout** — phases, gates, audience for each phase, success criteria

## Conversational rhythm

- **One question at a time.** Wait for the answer before asking the next.
- **Recommend an answer with every question.** "My read is X — does that hold?" beats "What do you think?" — give the user something to react to, not a blank page.
- **Push back on vague language.** "Users" — which segment? "Better" — by what measure? Propose a precise alternative; don't just complain about the fuzziness.
- **Stress-test with concrete scenarios.** When the user states a goal or constraint, invent a scenario that probes its edge. "If we hit 10x the user base in week one, does this rollout plan still hold?"
- **Don't fabricate user stories, metrics, or constraints.** Extract them or co-author. If you suggest one, mark it as a suggestion until the user confirms it.
- **Force ownership clarity.** For each goal, ask: who decides if this met its target?
- **Stop when good enough.** A PRD shipped at 80% beats a perfect one that never lands. At the end of each major section, offer to freeze the doc.

### Specific moves to keep using

- "Who is this for?" — push past "users" to a specific segment
- "What changes for that user when this ships?" — forces behavioural specificity
- "What's the smallest version that proves the goal?" — forces scoping
- "If we built only feature N, would it be a useful product?" — tests slice viability
- "What would make us cancel this six months in?" — surfaces non-goals and risks together
- "If two of these goals conflict at implementation time, which wins?" — forces priority

## Domain awareness (opportunistic)

Before starting the interview, check for:

- `CONTEXT.md` at the repo root (or `CONTEXT-MAP.md` for multi-context repos) — read the glossary; use its vocabulary; sharpen conflicting terms against it
- `docs/adr/` — skim ADR titles so you know what's been architecturally decided
- The codebase itself — a 2-minute skim to ground recommendations in the actual system

If none of these exist (greenfield project, or no repo at all), skip silently. Do not invent infrastructure that isn't there.

If the user uses a term that conflicts with `CONTEXT.md`, surface the conflict immediately: "Your glossary defines 'account' as the Customer entity, but you're using it for the User session — which is it for this PRD?"

## File format

```markdown
# <Working title>

## Problem
…

## Context
…

(remaining sections appended as they land)
```

No frontmatter. No TOC. No status field — the issue tracker handles state if used. Empty sections render as `## Heading\n\n_TBD_\n` so the structure stays visible while the doc is in progress.

## End of session

When the user signals "done" (or the Rollout section lands):

1. Re-read the file; check every section has substance (no orphan `_TBD_` lines unless the user accepts them).
2. Summarise what the PRD covers in 2–3 sentences.
3. Offer: "This PRD breaks into roughly N features. Want me to start an FRD interview for one of them, or stop here?" — do not auto-decompose.

A PRD's natural home is `docs/prd/`, where it lives durably as a reference. If the project uses an issue tracker, also offer to open a tracking issue that links back to the doc — but the doc remains the source of truth, not the ticket.

## Out of scope

- Producing feature-level work briefs (use `to-frd`)
- Implementation planning beyond Feature Breakdown
- Writing code, ADRs, or `CONTEXT.md` during the session (offer these as follow-ups)
- Decomposing the PRD into FRDs without explicit confirmation
- Publishing/formatting for a specific platform beyond plain markdown

</supporting-info>
