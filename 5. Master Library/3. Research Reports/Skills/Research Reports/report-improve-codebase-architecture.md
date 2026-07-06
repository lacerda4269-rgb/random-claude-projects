# Resource Report: improve-codebase-architecture (mattpocock/skills)

**URL:** https://github.com/mattpocock/skills/blob/main/skills/engineering/improve-codebase-architecture/SKILL.md
**Date Researched:** 2026-06-08
**Researched by:** Rose | Security pre-check: Soren | Report by: Rose
**Already in Master Library?** No — new item (parent repo mattpocock/skills not yet in ML)

---

## What It Is

improve-codebase-architecture is a Claude Code skill from Matt Pocock's skills repository — a curated collection described as "Skills for Real Engineers, straight from my .claude directory." The skill runs a structured architectural review of a codebase and produces an interactive HTML report identifying where the architecture is too shallow, too tightly coupled, or poorly testable. It uses a specific vocabulary (modules, interfaces, depth, seams, adapters, leverage, locality) applied consistently throughout, and is explicitly informed by two project artifacts: CONTEXT.md (domain vocabulary) and docs/adr/ (architecture decision records). Parent repo: 121,116 stars, MIT licensed, actively maintained (pushed 2026-06-07).

---

## What It Does

- Explores the codebase organically using the Agent tool in Explore mode — identifies friction, shallow modules, tightly coupled components, and hard-to-test interfaces
- Applies a "deletion test" to suspected shallow modules: would deleting it concentrate complexity, or just move it?
- Generates a self-contained HTML report in the OS temp directory — each candidate gets a card with problem, solution, benefits (expressed as locality and leverage gains), before/after diagram, and a recommendation strength badge (Strong / Worth exploring / Speculative)
- Uses Tailwind CDN for layout and Mermaid CDN for relationship diagrams; hand-crafted divs/SVG for editorial visuals
- Ends with a "Top recommendation" section: which candidate to tackle first and why
- Enters a grilling loop with the user once a candidate is selected — walks the design tree: constraints, dependencies, interface shape, what tests survive
- Side effects of the grilling loop: updates CONTEXT.md with new terms, offers to file ADRs for rejected candidates (when the rejection reason is load-bearing), links to companion skills (grill-with-docs, INTERFACE-DESIGN.md)
- Only produces interface proposals after grilling — never upfront

---

## Relevance to This Project *(as of research date — context may not carry to future projects)*

This skill is directly applicable to any code-heavy phase where the codebase starts accumulating technical debt or where AI navigability becomes a concern. The emphasis on deep vs. shallow modules and seam discipline is exactly the kind of architectural rigor that prevents the agent team from building a tangled system at scale. The ADR integration is also relevant — Sophia's documentation discipline maps well to maintaining the ADR record this skill expects. The HTML report output makes architectural findings visible and reviewable without requiring Jay to read dense code analysis text.

---

## Builder Footprint

- **Integration type:** Skill-composable — lives in a SKILL.md file; installs by reference from the mattpocock/skills repo; invoked via Claude Code's native skill system
- **Extension points:** CONTEXT.md (domain vocabulary fed to the skill), docs/adr/ (decision records the skill respects), companion skills (LANGUAGE.md, HTML-REPORT.md, ADR-FORMAT.md, CONTEXT-FORMAT.md, INTERFACE-DESIGN.md) — all modular and optional
- **Build complexity signal:** Low to Moderate — skill install is simple; full value requires maintaining CONTEXT.md and an ADR directory; the HTML report requires a browser to view
- **Known conflicts:** None identified with existing ML items

---

## Master Library Assessment

- **Proposed Section:** 3 — Skills
- **Proposed Tier:** 2
- **Rationale:** High-quality skill from a high-trust source (121k stars, Matt Pocock, MIT). Tier 2 because it is code-phase specific — not needed until a codebase exists to review. When the trading system build phase begins, this skill is the structured answer to "how do we keep the architecture clean as the codebase grows."

---

## Soren Security Pre-check

- **Verdict:** CLEARED
- **Checked:** License (MIT — permissive, confirmed for parent repo mattpocock/skills), stars (121,116 for parent repo), forks (10,615), last pushed (2026-06-07 — active, pushed one day before research), language (Shell, skill files are Markdown), maintainer (mattpocock — Matt Pocock, verified public identity, TypeScript educator and widely trusted tool author), skill content (read-only codebase analysis, no code execution, no network calls, no writes outside OS temp directory), no known CVEs, no supply chain concerns
- **Notes:**
  1. The skill writes one HTML file to the OS temp directory only — no persistent writes to the codebase. Contained and clean.
  2. The Agent tool (Explore mode) reads the codebase locally — no network egress, data stays in the local environment.
  3. No suspicious patterns, obfuscated content, or undisclosed behaviors in the SKILL.md file.
  4. Companion skill files in the same repo (HTML-REPORT.md, LANGUAGE.md, ADR-FORMAT.md, etc.) are not covered by this report — each requires individual review before adoption.

*Reviewed by Soren | 2026-06-08*

---

## Recommendation

Add to Section 3 (Skills), Tier 2. CLEARED — no conditions. Install via the mattpocock/skills repo when the trading system codebase reaches a stage where architectural review is warranted. Cosmo is the natural owner of this skill when it is deployed.

---

## C&P Summary

improve-codebase-architecture is a Claude Code skill from Matt Pocock's skills library (121,000 stars, MIT) that performs a structured architectural review of a codebase and produces an interactive HTML report. It identifies where the code is too shallow (a lot of complexity with little payoff), too tightly coupled (changing one thing requires changing many), or hard to test — and proposes specific improvements with before/after diagrams and a recommendation strength rating. Once you pick a candidate improvement, it walks you through the design with questions before proposing any actual changes. It does not modify any code on its own. For this team, it is the structured answer to keeping the trading system codebase clean and AI-navigable as it grows.

---

*Report by Rose | Session 230 | 2026-06-08*