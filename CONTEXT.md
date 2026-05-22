# Matt Pocock Skills

A collection of agent skills (slash commands and behaviors) loaded by Claude Code. Skills are organized into buckets and consumed by per-repo configuration emitted by `/setup-matt-pocock-skills`.

## Language

**Issue tracker**:
The tool that hosts a repo's issues — GitHub Issues, Linear, a local `.scratch/` markdown convention, or similar. Skills like `to-issues`, `to-frd`, `triage`, and `qa` read from and write to it.
_Avoid_: backlog manager, backlog backend, issue host

**Issue**:
A single tracked unit of work inside an **Issue tracker** — a bug, task, FRD, or slice produced by `to-issues`.
_Avoid_: ticket (use only when quoting external systems that call them tickets)

**FRD** (Feature Requirements Document):
A feature-level work brief — 1–3 pages, single-feature scope, work-order shape. Produced by `to-frd`. Carries enough detail (problem, solution, user stories, implementation decisions, testing decisions, out of scope) that an implementing agent can pick it up and start coding without further clarification.
_Avoid_: PRD (reserve PRD for product-level documents — see below)

**PRD** (Product Requirements Document):
A product- or initiative-level strategic document — multi-page, covers problem, target users, goals, success metrics, feature breakdown, constraints, risks, rollout. Produced by `prd-interview`. Not directly implementable; decomposes into FRDs for implementation. Lives durably in `docs/prd/`.

**Triage role**:
A canonical state-machine label applied to an **Issue** during triage (e.g. `needs-triage`, `ready-for-afk`). Each role maps to a real label string in the **Issue tracker** via `docs/agents/triage-labels.md`.

## Relationships

- An **Issue tracker** holds many **Issues**
- An **Issue** carries one **Triage role** at a time

## Flagged ambiguities

- "backlog" was previously used to mean both the *tool* hosting issues and the *body of work* inside it — resolved: the tool is the **Issue tracker**; "backlog" is no longer used as a domain term.
- "backlog backend" / "backlog manager" — resolved: collapsed into **Issue tracker**.
