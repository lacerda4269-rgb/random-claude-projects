# .claude Folder Manifest — Master Universal Initial Package

**Status:** Baseline template — version-neutral starting state
**Note:** This folder is the MUIP (Master Universal Initial Package) template set. Files here are templates carried by the package — they do not execute in the template context; they activate once the package is copied into a live project.

---

## hooks/ — Standard MUIP set (universal only; project-specific hooks sorted at AAR)

| File | Trigger | Type | Purpose |
|------|---------|------|---------|
| version-gate-hook.json | git commit | Blocking | `**Version:**` header must match highest log entry (GL38) |
| pre-commit-checklist-hook.json | git commit | Advisory | 7-item pre-commit reminder checklist |
| quick-stats-validation-hook.json | git commit (sophia-pending-changes.md staged) | Blocking | Quick Stats numbers must match actual row counts |
| session-stop-hook.json | Stop event | Advisory | Session close + compact wrap-up checklists |

## commands/ — Standard MUIP set (universal only; project-specific commands sorted at AAR)

| File | Trigger | Purpose |
|------|---------|---------|
| caveman.md | /caveman | Token-efficient communication mode |
| cohk.md | /cohk | CloseOut-HouseKeeping 20-step navigator |
| surface-transition.md | /surface-transition | Cross-surface context handoff |
| validate-pending-list.md | /validate-pending-list | On-demand Quick Stats audit (companion to Hook 7) |
| version-check.md | /version-check | On-demand version header audit (companion to Hook 6) |

## skills/ — One bundled universal skill at baseline

Most universal skills live **global** at `~/.claude/skills/` (camofox-browser, find-skills, graphify, humanizer, hyperframes, playwright-cli, rag-anything) and their engines/binaries at `C:\ClaudeTools` — the template **references** them, it does not carry copies (Item 152, ratified S264 — global-canonical). The one exception bundled in this package's `skills/`:

| Skill | Purpose |
|-------|---------|
| fresh-eyes | Zero-prior-context review — spawns fresh sub-agents to rate a target (file/folder/tree) 0-10 against a supplied rubric, free of anchoring. Carried in the template so it is available on every project from the start. |

Beyond `fresh-eyes`, this folder holds only Cosmo-built, project-spawned skills before they're promoted to global at AAR.

---

## Tailoring Notes — Review when deploying a new project from this template

1. **Project-specific commands** (e.g., `[project-specific command].md`) do NOT travel in this template — they live in the live project's own `.claude/commands/` and are sorted at AAR (universal → here; project → the project)
2. **Project-specific hooks** (e.g., `[project-specific hook].json`) are added at project setup — they do not travel in this template
3. **Agent SOT copies** go in `agents/` at project setup — pull from MUIP soul files; do NOT copy from another project's `.claude/agents/`
4. **settings.json** is built up per-project over time; start from the project's own permission needs
5. **Item 152 — RESOLVED (S264): global-canonical.** Universal skills/tools live global (`~/.claude/skills/` + `C:\ClaudeTools`); the template references them via this manifest rather than carrying copies. playwright-cli relocated to global S264 (it had been the lone template-carried skill).

---

---

## Change Log

| Date | Change |
|------|--------|
