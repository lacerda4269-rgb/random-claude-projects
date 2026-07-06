# 3. Research Reports — Master Library

**Owner:** Lexi (Librarian) places; Rose (Researcher) authors the reports.
**Purpose:** The research record for every resource the team has evaluated — what was researched, when, and what was found.

---

## How this folder is organized

There are two homes for a research report. Where a report lives depends on one question: **is the resource installed?**

### `0. Resources Installed/` — installed resources (canonical home)

When a resource has been installed and is in active use, its research report lives here. This folder sorts first and is the canonical home for installed-resource reports. It also holds two install-config records subfolders:

- `Built - CLI Folder/` — install records for installed CLI tools.
- `Built - MCP Folder/` — config records for installed MCP servers.

### Category folders — not-installed resources

Every named category folder holds an inner `Research Reports/` folder containing the reports of resources that were researched but **not** installed:

- `Skills`
- `Hooks`
- `Command Line Interface (CLI)`
- `Model Context Protocol (MCP)`
- `Claude - Plugins`
- `Workflow Patterns`
- `Reference & Ecosystem`
- `Alternative Tools & Notable Ecosystem`
- `Jay's Shelf`
- `Universal Research Reports`

The model in one line: **installed → report lives in `0. Resources Installed`; not-installed → report stays in its category.**

---

## The `-removed` suffix convention

A report filename ending in `-removed.md` (for example, `report-mcp-youtube-removed.md`) means the resource was **installed and then retired**. The report is kept as a historical record — it documents something that was once part of the stack. Because it was installed, a `-removed` report lives in `0. Resources Installed/`, not in a category folder.

---

*Research record. Cleared, cataloged items live in their numbered ML folders; this tree holds the research behind them.*
