# Build Requests

**Owner:** Cosmo (Skill Creator)
**Purpose:** Cosmo's Sage-authorized build queue — every authorized build brief lives here until completed.

---

## What This Folder Is

This is **Cosmo's approved work queue — not an open drop-box.** Build briefs arrive here only after Sage has authorized them. Cosmo works from this folder; he does not accept build requests dropped here directly by other agents.

---

## How a Build Gets Here (intake flow)

Build requests follow the same gated path as research requests — **agent → Sage → builder, never agent → builder direct:**

1. **Request** — An agent (or Jay) submits a build need to **Sage**, not to Cosmo directly.
2. **Sage's gate** — Sage applies the CEO relevance check (aligned, needed, in scope?) **and the ML-first check**: does this already exist, cleared, in the Master Library / Deployable Arsenal roll-up? No rebuilding what the arsenal already holds.
3. **Authorize** — If it passes both, Sage places an authorized **build brief** (template below) in this folder. That placement *is* the build authorization.
4. **Build** — Cosmo triages and builds from the brief. He acknowledges on pickup and runs his own full synthesis check (reuse / combine / leanest path) — Sage's ML-first gate screens for duplicates; it does **not** replace Cosmo's synthesis review. Anything ambiguous, or that touches an external/deployable resource → Cosmo escalates to Sage first, before building.

> **On-demand activation:** Sage activates Cosmo into `.claude/agents/` when authorizing the build, and spins him down after.

---

## When a Build Is Complete

The brief moves to `Completed Requests — Done/`; the built artifact moves to its deployment destination (active project folder, or through the ML clearance pipeline for anything external/deployable).

---

## Boundaries

- This queue and its files are Cosmo's own. Cosmo never writes Sophia-owned files (Pending Changes, Session Summary, Gotcha, TLL). If his output must land in a Sophia-owned file, Sophia writes it.
- No build begins without a Sage-authorized brief in this folder. A request that skips the Sage gate is not a valid build request. *(This includes Cosmo-flagged candidates: when Cosmo spots a build opportunity, it still routes through Sage — the brief originates with Sage regardless of who saw it first.)*

**Blank version:** Empty at baseline.

---

## Build-Brief Template

Copy the block below; Sage fills every field before placing the brief in the queue.

```
# Build Brief — [resource name]

**Requested by:** [agent / Jay / Cosmo-flagged]
**Authorized by:** Sage — [date / session]
**Build type:** Skill | Hook | CLI | MCP | Plugin
**Tri-form note (HR21):** [assessed for command / skill / hook forms? which apply? — "N/A — single form" is valid]
**What's needed:** [one-line description of the capability]
**Use case / why:** [the problem it solves; why now]
**ML-first check:** [result — "not in ML/Registry, clear to build" | "exists: [name] → use that instead" | "partial overlap: [note]"]
**External/deployable resource?:** Yes → clearance pipeline (Sage → Rose → Soren → Lexi) before/with build | No → in-lane build
**Urgency:** [now / this phase / backlog]
**Notes / constraints:** [optional — scope limits, dependencies, target destination]

---
Authorized brief. Cosmo builds from this and runs his own synthesis check on pickup;
escalates to Sage before building if anything is ambiguous or resource-touching.
```

---

*Cosmo's authorized queue. Sage authorizes in; built items out.*
