# Resource Report: InsForge

**URL:** https://github.com/InsForge/insforge
**Date Researched:** 2026-05-03
**Researched by:** Rose | Security pre-check: Soren (FLAG → Jay's Shelf) | Filed by: Sage
**Already in Master Library?** No — new item

---

## What It Is
InsForge is an AI-powered development platform that integrates with Claude Code via MCP (Model Context Protocol), providing LLM-assisted coding workflows and project intelligence. The platform's MCP server connects to a running InsForge instance, which routes requests through InsForge's cloud infrastructure. The "coding help" framing understates the scope: InsForge functions as a full LLM gateway with admin-level access to the development environment.

## What It Does
Provides AI-assisted coding assistance, code review, and project intelligence through an MCP integration layer. Claude Code connects to InsForge's MCP server; the platform handles routing and coordination with its LLM backend. Cloud-hosted execution means code context and project files flow through InsForge's servers during use.

## Relevance to This Project
Jay flagged this as a "coding help" resource. The underlying concept has merit — an MCP-integrated AI development layer could augment Claude Code's native capabilities. However, the cloud data routing and admin-level MCP scope introduce concerns that are not resolvable without a self-hosted deployment path.

---

## Why It's On the Shelf — Security Flag Summary

**This section explains why InsForge reached Jay's Shelf instead of the Full Database. Jay likes the concept and directed it here so the thread is not lost.**

**Soren Re-review: 2026-06-08 — VERDICT UPDATED: ARCHIVED/FLAG-CLOSED**
The GitHub repo is now ARCHIVED (confirmed by Rose freshness sweep, 2026-06-08). The three conditions Jay set for this item to come off the shelf — self-hosted deployment path, documented data flows, narrowed MCP scope — are no longer resolvable via this vehicle. Active development has stopped; no maintainer is present to address the flags. This is not VOID: the repo exists, is readable, and the code could theoretically be audited. But the clearance path is permanently closed unless a replacement tool emerges that independently meets the three conditions. The concept (MCP-integrated AI dev layer augmenting Claude Code) remains valid and is preserved. The vehicle is dead. Verdict changes from FLAG to ARCHIVED/FLAG-CLOSED.

**Original Soren concerns (FLAG verdict, 2026-05-03):**

1. **Admin-level MCP access** — InsForge's MCP server operates with admin-level privilege scope. This is broader than necessary for a coding assistance tool and creates a wide attack surface on the development environment. A principled MCP scope for coding assistance should be read/limited-write, not admin.

2. **LLM gateway credential path unclear** — How API credentials flow through the platform is not documented. It is not clear where keys are stored, how they are transmitted, or what InsForge's LLM gateway does with them.

3. **Cloud data flows undocumented** — Code, project context, and potentially environment information transmit to InsForge's servers. Their data handling, retention, and privacy policies are not publicly documented at the level required for use in any production or sensitive project.

**What would need to change for this to come off the shelf:**
- Self-hosted deployment option available and functional (code and context stay local)
- Data handling and retention policy publicly documented
- MCP privilege scope narrowed or clearly justified with a stated rationale
- Credential flow transparent and secure

**The concept Jay kept:** An MCP-integrated AI development layer that goes beyond Claude Code's native capabilities — project-wide intelligence, LLM-assisted code review, coordinated context. The direction is interesting. The execution needs a self-hosted path before this team can use it.

---

## Master Library Assessment
- **Proposed Section:** 9 — Jay's Shelf
- **Proposed Tier:** 3
- **Rationale:** Concept held by Jay for future evaluation. Not cleared for deployment. Revisit when self-hosted path is available and data flows are documented.
- **⚠️ June 2026 Update:** The GitHub repository (https://github.com/InsForge/insforge) is now **ARCHIVED** — read-only, no further development. The repo has 11,575 stars but is no longer maintained. This significantly reduces the likelihood that the three conditions for coming off the shelf (self-hosted deployment, documented data flows, narrowed MCP scope) will ever be met by this project. The concept remains valid; the execution vehicle is effectively dead.

## Recommendation
File to Section 9 — Jay's Shelf, Tier 3. **Updated June 2026:** The GitHub repo is now archived — no further development expected. The three conditions for deployment are now unlikely to be met by this project. Jay's direction was to keep the concept; the concept (MCP-integrated AI dev layer with project-wide intelligence) remains valid. The vehicle is gone. If the concept resurfaces in a different project or tool, it should be evaluated fresh at that time.

---
*Report by Rose + Sage | Session 106 | 2026-05-03*

---

## C&P Summary

InsForge is an AI-powered development platform that integrates with Claude Code via MCP, providing LLM-assisted coding workflows routed through InsForge's cloud infrastructure. Soren flagged three concerns: admin-level MCP privilege scope (broader than needed), unclear LLM gateway credential path, and undocumented cloud data flows to InsForge servers. Verdict: FLAG — not cleared for standard ML deployment. Jay liked the concept and directed it to Jay's Shelf with an expanded explanation so the thread is not lost. **As of June 2026: the GitHub repo is ARCHIVED — 11,575 stars, no further development.** The three conditions for coming off the shelf are now unlikely to be met. The concept (MCP-integrated AI dev layer that augments Claude Code) remains valid and worth holding; the vehicle is effectively dead. If a similar tool surfaces that meets the three conditions, evaluate it fresh.

---

## Report Version Log

| Version | Date | What Changed |
|---------|------|--------------|
