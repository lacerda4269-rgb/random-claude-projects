# Folder & File Tree

**Version:** 0
**Status:** Living Document — updates with Folder & File Reference and Visual TreeView
**Last Updated:** 2026-06-23 — Sterilization pass (re-rooted to canonical package name; regenerated against fresh disk; phantom rows removed; description count corrected to 11)
**Owner:** Sophia (COO)

---

> This is the literal nested text tree of every folder and file in the Master Universal Initial Package at current (final, sterilized) state.
> Updated whenever Folder & File Reference.md and Visual TreeView.md are updated.
> Read alongside `Folder & File Reference.md` for purpose and decision context.
> Read alongside `Visual TreeView.md` for the graphical view.

> **Final structure note:** Top-level folders 0–6. Retired: `Standing Agents - Employees`, `Special Project Agents - Employees`, `Shared Agent Resources` (the Shared/Cross-Agent layer is now an on-demand subfolder documented in the Live Folder README). All 9 agents live flat in `5. Master Library/1. Soul Folder/`. `Named Project - WorkTree` → `Named Project - Live Folder`. Mermaid companions renamed numbered → pair-based (`<Name>-Mermaid.md`). Tracker template `progress-tracker` → `task-tracker` (canonical); `progress` → `status-board`.

---

```
Master Universal Initial Package/
├── README.md
├── Getting-Started.md
├── .mcp.json
├── .claude/
│   ├── MANIFEST.md
│   ├── agents/                          (empty at baseline — Sophia SOT copy added at Phase 0)
│   ├── commands/
│   │   ├── caveman.md
│   │   ├── cohk.md
│   │   ├── surface-transition.md
│   │   ├── validate-pending-list.md
│   │   └── version-check.md
│   ├── hooks/
│   │   ├── pre-commit-checklist-hook.json
│   │   ├── quick-stats-validation-hook.json
│   │   ├── session-stop-hook.json
│   │   └── version-gate-hook.json
│   └── skills/                          (empty at baseline — universal skills live global)
│
├── 0. Folder Governance/
│   ├── README.md
│   ├── Folder & File Reference.md
│   ├── Folder & File Tree.md
│   └── Visual TreeView.md
│
├── 1. Sage's CEO Folder/
│   ├── README.md
│   ├── 0. Sage's CEO Project Soul/
│   │   ├── README.md
│   │   ├── ME - Jay.md
│   │   └── Sage-project-soul.md
│   ├── 1. Session Summary/
│   │   └── README.md
│   ├── 2. Master Guides/
│   │   ├── README.md
│   │   ├── Hard Rules — Master List.md
│   │   ├── Master Guide - Sage's Version (SOP).md
│   │   └── Master Guide - Jay's Version (SOP).md
│   ├── 3. Jay's Project Office/
│   │   └── README.md
│   ├── 4. Project Artifacts/
│   │   └── README.md
│   └── 6. SOPs/
│       ├── README.md
│       ├── Agent-Creation-Pipeline-SOP.md
│       ├── Agent-Creation-Pipeline-Mermaid.md
│       ├── CloseOut-HouseKeeping-SOP.md
│       ├── CloseOut-HouseKeeping-Mermaid.md
│       ├── Compact-Wrap-Up-SOP.md
│       ├── CrossTalk-FireDrill-SOP.md
│       ├── CrossTalk-FireDrill-Mermaid.md
│       ├── Every-SOP-Built.md
│       ├── Every-SOP-Built-Jay.md
│       ├── Post-Compact-Return-SOP.md
│       ├── Promotion-Pipeline-SOP.md
│       ├── Session-Close-SOP.md
│       ├── Session-Close-and-Compact-Wrap-Up-Mermaid.md
│       ├── Session-Start-SOP.md
│       ├── Session-Start-and-Post-Compact-Mermaid.md
│       ├── Army-vs-Company-Chain-of-Command-Mermaid.md
│       └── Company-Growth-Jay-to-Holding-LLC-Mermaid.md
│
├── 2. Sophia's COO Folder/
│   ├── README.md
│   ├── 0. Sophia's COO Suite/
│   │   ├── README.md
│   │   ├── sophia-coo.md
│   │   ├── Sophia-COO-SOP.md
│   │   ├── Sophia-COO-SOP-Jay.md
│   │   ├── Sophia-List-Management-SOP.md
│   │   ├── Sophia-List-Management-SOP-Jay.md
│   │   ├── Sophia-List-Management-Mermaid.md
│   │   ├── internal-build-record.md
│   │   └── internal-build-record-Jay.md
│   ├── 1. Operational Files/
│   │   └── README.md
│   ├── 2. AAR/
│   │   └── README.md
│   └── 3. Teams Lesson Log - TLL/
│       ├── README.md
│       └── Lessons-Gotcha-Routing-Mermaid.md
│
├── 3. Phase 0 & 1/
│   └── README.md
│
├── 4. Named Project - Live Folder/
│   └── README.md
│
├── 5. Master Library/
│   ├── README.md
│   ├── 0. ML Operations/
│   │   ├── README.md
│   │   ├── 0. Master Library SOP - Lexi.md
│   │   ├── 1. Master Library SOP - Jay's version.md
│   │   ├── 2. Master Library - Research Report Request (Blank).md
│   │   ├── 3. Master Library Index — Full Database.md
│   │   ├── 4. ML Index Card — Quick Reference.md
│   │   └── 5. ML Index Card — C&P Summary.md
│   ├── 1. Soul Folder/
│   │   ├── README.md
│   │   ├── 0. Generic Soul Shells/          (soul shell .txt templates + README)
│   │   ├── 0a. Basic Built Agents/
│   │   │   └── README.md
│   │   ├── Cosmo the Skill Creator/
│   │   │   ├── README.md
│   │   │   ├── cosmo-skill-creator.md
│   │   │   ├── Cosmo-Skill-Creator-SOP.md
│   │   │   ├── Cosmo-Skill-Creator-SOP-Jay.md
│   │   │   ├── Cosmo-Skill-Creator-Mermaid.md
│   │   │   └── Build Requests/
│   │   │       ├── README.md
│   │   │       └── Completed Requests — Done/
│   │   │           └── README.md
│   │   ├── Lexi the Librarian/
│   │   │   ├── README.md
│   │   │   ├── lexi-librarian.md
│   │   │   ├── Lexi-Librarian-SOP.md
│   │   │   └── Lexi-Librarian-SOP-Jay.md
│   │   ├── Rose the Researcher/
│   │   │   ├── README.md
│   │   │   ├── rose-researcher.md
│   │   │   ├── Rose-Researcher-SOP.md
│   │   │   ├── Rose-Researcher-SOP-Jay.md
│   │   │   ├── Rose-Researcher-Mermaid.md
│   │   │   ├── rose-report-format-standard.md
│   │   │   └── cli-tool-intake-checklist.md
│   │   ├── Soren the Security Boss/
│   │   │   ├── README.md
│   │   │   ├── soren-security-manager.md
│   │   │   ├── Soren-Security-Manager-SOP.md
│   │   │   ├── Soren-Security-Manager-SOP-Jay.md
│   │   │   ├── Prompt-Injection-Protocol.md
│   │   │   └── Web-Only-Pre-Approved-Tools.md
│   │   ├── Feynman the Scholar/
│   │   │   ├── README.md
│   │   │   ├── feynman-scholar.md
│   │   │   ├── Feynman-Scholar-SOP.md
│   │   │   ├── Feynman-Scholar-SOP-Jay.md
│   │   │   ├── Feynman-Session-Management-SOP.md
│   │   │   ├── Feynman-Session-Management-SOP-Jay.md
│   │   │   └── Feynman-Course-Workflow-Mermaid.md
│   │   ├── Nick and NinjaTrader/
│   │   │   ├── README.md
│   │   │   ├── nick-ninjatrader.md
│   │   │   ├── Nick-NinjaTrader-SOP.md
│   │   │   └── Nick-NinjaTrader-SOP-Jay.md
│   │   ├── Pete and Python/
│   │   │   ├── README.md
│   │   │   ├── pete-python.md
│   │   │   ├── Pete-Python-SOP.md
│   │   │   └── Pete-Python-SOP-Jay.md
│   │   ├── Todd and TradingView/
│   │   │   ├── README.md
│   │   │   ├── todd-tradingview.md
│   │   │   ├── Todd-TradingView-SOP.md
│   │   │   └── Todd-TradingView-SOP-Jay.md
│   │   └── Vicky the Videographer/
│   │       ├── README.md
│   │       ├── vicky-videographer.md
│   │       ├── Vicky-Videographer-SOP.md
│   │       ├── Vicky-Videographer-SOP-Jay.md
│   │       ├── Vicky-Videographer-Tool-Deployment-SOP.md
│   │       └── Vicky-Videographer-Tool-Deployment-SOP-Jay.md
│   ├── 2. Agents - Employees Descriptions/
│   │   ├── README.md
│   │   └── [11 description profiles: cosmo, feynman, lexi, nick, pete, rose,
│   │       sage, sophia, soren, todd, victoria]
│   └── 3. Research Reports/
│       ├── README.md
│       ├── 0. Resources Installed/
│       │   ├── install-master-list.md
│       │   ├── [20 report-*.md install/deployment records]
│       │   ├── Built - CLI Folder/        (4 install records + README)
│       │   └── Built - MCP Folder/        (3 config records + README)
│       ├── Skills/Research Reports/
│       ├── Command Line Interface (CLI)/Research Reports/
│       ├── Model Context Protocol (MCP)/Research Reports/
│       ├── Claude - Plugins/Research Reports/
│       ├── Hooks/Research Reports/
│       ├── Reference & Ecosystem/Research Reports/
│       ├── Alternative Tools & Notable Ecosystem/Research Reports/
│       ├── Jay's Shelf/Research Reports/
│       ├── Universal Research Reports/Research Reports/
│       └── Workflow Patterns/Research Reports/
│
└── 6. Blank Universal Templates/
    ├── 0. README.md
    ├── [lead]-pending-changes (Blank Template).md
    ├── activation-brief (Blank Template).md
    ├── alignment-sweep-gap-log (Blank Template).md
    ├── CLAUDE (Blank Template).md
    ├── discovery (Blank Template).md
    ├── Gotcha (Blank Template).md
    ├── lessons-template (Blank Template).md
    ├── plan (Blank Template).md
    ├── Project Resources Log (Blank Template).md
    ├── project-file-index (Blank Template).md
    ├── project-navigation-map (Blank Template).md
    ├── Project-Soul (Blank Template).md
    ├── research (Blank Template).md
    ├── Session Summary (Blank Template).md
    ├── Session Summary Index (Blank Template).md
    ├── sophia-completed-changes (Blank Template).md
    ├── sophia-pending-changes (Blank Template).md
    ├── status-board (Blank Template).md
    ├── task-tracker (Blank Template).md
    ├── Team-Lessons-Log (Blank Template).md
    ├── technical-manual-python-template (Blank Template).md
    ├── technical-manual-template (Blank Template).md
    ├── title-role-sweep-tracker (Blank Template).md
    └── user-guide-template (Blank Template).md
```

---

*Regenerated from disk (sterilization pass). 24 blank templates in folder 6; 9 flat agents in the Soul Folder; folders 0–6 with retired folders gone. Mermaid companions are pair-named. The Research Reports category subfolders each hold a `Research Reports/` subfolder with per-item write-ups (contents abbreviated above for the category-level view; full per-item list lives in the ML Full Database index).*

---

## Change Log

| Version | Date | Change |
|---------|------|--------|
