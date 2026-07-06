# Visual TreeView — Master Universal Initial Package (MUIP)

**Status:** Living Document — ACTIVE PROJECT INSTANCE (Random Projects). Updates with Folder & File Reference and Folder & File Tree (Item 141).
**Last Updated:** 2026-07-06 — Session 1 activation reflect (Live Folder renamed to Random Projects + Jot subfolder; Sophia wired to `.claude/agents/`).
**Owner:** Sophia (COO)

---

> This is the at-a-glance structural map of the Master Universal Initial Package (MUIP) in its final (post-restructure) starting state.
> Every new project begins here. Phase 0 activates and fills the structure.
> Read `Getting-Started.md` (version root) for the activation sequence.
> Read `Folder & File Tree.md` for the exhaustive file-by-file listing; this view is the graphical orientation map.
> Paste the diagram block below into [mermaid.live](https://mermaid.live) to view it visually.

> **Final structure note (Session 265 end-pass):** Top-level folders 0–6. Retired: Standing Agents, Special Project Agents, Shared Agent Resources (Shared/Cross-Agent is now an on-demand subfolder of the Live Folder). All 9 agents flat in `5. Master Library/1. Soul Folder/`. WorkTree → Live Folder. Mermaid companions pair-named. Only Sophia ships live; every other agent is on-demand from the Soul Folder.

---

```mermaid
graph LR
    v01b["Master Universal Initial Package (MUIP)/"]
    v01b --> DOTCLAUDE[".claude/ — Claude Code config (travels with the package)"]
    v01b --> FG["0. Folder Governance/"]
    v01b --> CEO["1. Sage's CEO Folder/"]
    v01b --> COO["2. Sophia's COO Folder/"]
    v01b --> PO1["3. Phase 0 & 1/ — empty at baseline"]
    v01b --> LIVE["4. Random Projects - Live Folder/ — active (task-tracker, status-board, Jot mini-project)"]
    v01b --> ML["5. Master Library/"]
    v01b --> BT["6. Blank Universal Templates/"]
    v01b --> GS["Getting-Started.md"]
    v01b --> RM["README.md"]

    %% .claude (Claude Code config — travels with the package)
    DOTCLAUDE --> DC_AGENTS["agents/ — sophia-coo.md wired Session 1 (others on-demand)"]
    DOTCLAUDE --> DC_CMD["commands/ — caveman, cohk, surface-transition, validate-pending-list, version-check"]
    DOTCLAUDE --> DC_HOOKS["hooks/ — pre-commit, quick-stats, session-stop, version-gate"]
    DOTCLAUDE --> DC_SKILLS["skills/ — empty at baseline (global skills live in ~/.claude; see Item 152)"]
    DOTCLAUDE --> DC_MAN["MANIFEST.md"]

    %% 0. Folder Governance
    FG --> FG_REF["Folder & File Reference.md"]
    FG --> FG_TREE["Folder & File Tree.md"]
    FG --> FG_VIS["Visual TreeView.md"]

    %% 1. Sage's CEO Folder
    CEO --> CEO_SOUL["0. Sage's CEO Project Soul/"]
    CEO --> CEO_SS["1. Session Summary/"]
    CEO --> CEO_MG["2. Master Guides/"]
    CEO --> CEO_PO["3. Jay's Project Office/"]
    CEO --> CEO_PA["4. Project Artifacts/"]
    CEO --> CEO_SOP["6. SOPs/ (SOPs + pair-named Mermaid companions)"]

    %% 2. Sophia's COO Folder
    COO --> COO_SUITE["0. Sophia's COO Suite/ (sophia-coo.md + SOPs + List-Management Mermaid)"]
    COO --> COO_OPS["1. Operational Files/ — empty at baseline"]
    COO --> COO_AAR["2. AAR/ — empty at baseline"]
    COO --> COO_TLL["3. Teams Lesson Log - TLL/ (+ Lessons-Gotcha-Routing Mermaid)"]

    %% 5. Master Library
    ML --> ML_OPS["0. ML Operations/ (SOPs + 3 index cards)"]
    ML --> ML_SOUL["1. Soul Folder/ — flat 9-agent roster"]
    ML --> ML_DESC["2. Agents - Employees Descriptions/"]
    ML --> ML_RR["3. Research Reports/ (+ 0. Resources Installed)"]

    %% Soul Folder — flat roster
    ML_SOUL --> SF_SHELLS["0. Generic Soul Shells/"]
    ML_SOUL --> SF_BASIC["0a. Basic Built Agents/"]
    ML_SOUL --> SF_COSMO["Cosmo the Skill Creator/"]
    ML_SOUL --> SF_LEXI["Lexi the Librarian/"]
    ML_SOUL --> SF_ROSE["Rose the Researcher/"]
    ML_SOUL --> SF_SOREN["Soren the Security Boss/"]
    ML_SOUL --> SF_FEY["Feynman the Scholar/"]
    ML_SOUL --> SF_NICK["Nick and NinjaTrader/"]
    ML_SOUL --> SF_PETE["Pete and Python/"]
    ML_SOUL --> SF_TODD["Todd and TradingView/"]
    ML_SOUL --> SF_VICKY["Vicky the Videographer/"]

    %% Residency callout
    SOPHIA_LIVE["Only Sophia ships live every session\n(from 2. Sophia's COO Folder).\nAll other agents are on-demand from the Soul Folder."]
    COO_SUITE -.-> SOPHIA_LIVE
    ML_SOUL -.-> SOPHIA_LIVE
```

---

## Quick orientation table

| Folder | What's there at baseline | Phase 0 action |
|--------|--------------------------|----------------|
| `.claude/` | Claude Code config that travels with the package: `agents/`, `commands/` (5), `hooks/` (4), empty `skills/`, MANIFEST.md | Sophia wired into `agents/`; global-vs-travels split resolved at Item 152 (P8) |
| `0. Folder Governance/` | 3 governance docs (Reference, Tree, TreeView) + README | None — reference only |
| `1. Sage's CEO Folder/` | Master Guides, SOPs (+ pair-named Mermaids), soul/session/artifacts subfolders | Soul + session records filled |
| `2. Sophia's COO Folder/` | COO Suite (sophia-coo.md, SOPs, List-Management Mermaid), TLL, operational/AAR shells | Operational files deployed; Sophia wired to `.claude/agents/` |
| `3. Phase 0 & 1/` | README only — empty at baseline | Populated as Phase 0/1 produce records |
| `4. Random Projects - Live Folder/` | Active — task-tracker, status-board, and the Jot mini-project subfolder | Renamed at Session 1; active work lands here |
| `5. Master Library/` | ML Operations, flat 9-agent Soul Folder, agent descriptions, Research Reports | On-demand agent pulls; resources cataloged |
| `6. Blank Universal Templates/` | 24 blank templates + README | Templates pulled and deployed |

---

*Regenerated from disk Session 265 (P7 end-pass). At-a-glance map of folders 0–6 with the flat 9-agent Soul Folder and retired folders removed. For the exhaustive file listing, see `Folder & File Tree.md`; for purpose/decision context, see `Folder & File Reference.md`.*
