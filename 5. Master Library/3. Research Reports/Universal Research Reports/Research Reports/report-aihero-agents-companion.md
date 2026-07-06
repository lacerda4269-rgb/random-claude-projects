# aihero.dev "Complete Guide to AGENTS.md" — Companion Research Report for Sage

**Report Type:** Fact-finding — companion to Item 5 resource report; for Sage's comparative analysis
**Researcher:** Rose
**Date:** 2026-05-03
**Requested by:** Jay (Item 5, Session 106 batch)
**For:** Sage — comparative analysis: good/bad/ugly vs. our agent handling; bloat concern

---

**C&P Summary:** AIHero.dev is Matt Pocock's AI engineering education platform — Matt is a well-known developer educator (Total TypeScript, 210K+ Twitter followers, Vercel developer advocate background) with 54,000+ newsletter subscribers. This specific guide covers how to write AGENTS.md files — the configuration files that tell AI coding agents how to behave in a project. The guide argues strongly for keeping these files small and focused, using progressive disclosure rather than cramming everything into one file, and warns that large files waste the agent's instruction budget and become stale quickly. The guide is NOT about agent soul/persona design specifically — it covers operational config files. But the same principles apply to any file that loads into context on every session. Our soul files, CLAUDE.md, and agent behavioral rules all consume context window budget. The guide's warnings about bloat, stale content, and instruction budget limits are directly applicable to how we design and maintain those files.

---

## Source Credibility

- **Matt Pocock** — creator of Total TypeScript (industry-standard TypeScript course), former Vercel developer advocate, XState core team member
- 210,300+ Twitter followers; 54,000+ newsletter subscribers — **Verified**
- Endorsed by Guillermo Rauch (Vercel CEO): "Matt is one of the best developer educators in the world" — **Verified**
- Active open-source presence at github.com/ai-hero-dev

---

## Full Content for Sage's Comparative Analysis

### What the guide is about

AGENTS.md is the operational configuration layer — not a persona/identity file. It tells agents what to do in a specific codebase (commands, testing, conventions). This is distinct from a soul file, which defines who an agent is. That distinction matters for our comparison.

---

### Key Concepts and Recommendations

**1. The Instruction Budget Is Real and Finite**

The guide cites research indicating frontier LLMs follow approximately 150-200 instructions with reasonable consistency. Every instruction added beyond that degrades reliability on earlier instructions. The constraint is not theoretical — it is a hard limit on how much behavioral guidance any file can usefully carry. This applies to any file that loads on every session: soul files, CLAUDE.md, agent behavioral rules.

**2. "As Small as Possible"**

The explicit recommendation: "The ideal AGENTS.md file should be as small as possible." Not "appropriately sized." As small as possible. Every line must earn its place.

**Minimum necessary content for a root AGENTS.md:**
- One-sentence project description
- Package manager (if non-npm)
- Non-standard build/typecheck commands
- Everything else belongs elsewhere.

**3. Stale Content Is Actively Harmful**

Outdated documentation does not just fail to help — it actively misdirects agents. "If documentation references moved files, agents confidently search wrong locations." For soul files, the equivalent is: outdated behavioral rules, superseded processes, or obsolete role definitions that were never removed. They do not sit quietly — they compete with current instructions for attention.

**4. Progressive Disclosure Over Front-Loading**

Rather than putting everything in one file, create a pointer system. The root file contains breadcrumbs; agents navigate to detailed guidance when needed. Applied to our system: soul files should contain identity and principles; operational details (SOPs, runbooks, skills) should live elsewhere and be referenced rather than embedded.

**5. Describe Capabilities, Not Structures**

The guide warns specifically against documenting file paths and structures that change frequently. The stable layer is what an agent can do and what it values — not where specific files live. Soul files are naturally well-suited to this: they document identity, personality, and principles — all stable. Where bloat creeps in is when procedural rules, project-specific details, or frequently-changing operational notes get embedded in what should be identity documents.

**6. Bloat Causes Identified:**
- Reactive rule accumulation: adding instructions every time something goes wrong, without removing obsolete ones
- Auto-generated content: comprehensiveness over restraint
- No audit cadence: files grow but are never trimmed
- Treating the file as a knowledge base instead of a behavioral anchor

**7. The "Balls of Mud" Warning**

The guide uses this phrase explicitly for files that accumulate without governance: "natural accumulation occurs as developers add rules reactively." Without deliberate trimming, any behavioral config file becomes unmaintainable.

---

### What the guide does NOT cover

- Agent identity or persona design (soul files in our sense)
- Multi-agent team structures
- Session management or memory persistence
- The distinction between who an agent is vs. how an agent works

---

### Sage's Comparative Frame — Findings for Analysis

*Rose's observations for Sage to use in the comparative analysis:*

**Where our system likely diverges from the guide's recommendations:**

1. **File length** — CLAUDE.md (global soul) and individual agent souls are significantly longer than the 200-400 word / under-50-line community standard. This is partly by design (stateless system requires more briefing content per session), but the instruction budget concern still applies.

2. **Behavioral Rules as SOPs-within-the-soul** — CLAUDE.md contains a "Behavioral Rules — Full" section with detailed procedural content (loop prevention, two-round rule, session management mechanics, etc.). By the community standard, these operational procedures belong in SOPs/skills — not in the soul file. The soul should establish the principle; the SOP should define the steps.

3. **Merged identity + operations design** — Our souls mix identity content (who the agent is, what they value) with operational content (what they should do in specific situations). The community and SoulSpec recommend separating these. We don't have to adopt that architecture, but we should consciously evaluate it.

**Where our system is aligned with the guide:**

1. We already have the concept of separating soul files from SOPs — SOPs are separate documents; souls carry identity.
2. CLAUDE.md contains an explicit "Soul Discipline" section: "every line earns its place."
3. We have a review trigger (every project AAR) — the community recommends quarterly cadence.
4. We use role-based references instead of absolute paths (matches "describe capabilities, not structures").
5. We distinguish between CLAUDE.md (identity) and project CLAUDE.md (operational loader) — this is architecturally sound.

**The key nuance for stateless systems:**

The community standard assumes persistent agent memory between sessions. Our agents are stateless — each session starts fresh. This means our soul files must carry more operational detail than a persistent-memory agent would need, because there is no learned behavior to fall back on. The "200-400 word" guideline applies to persistent agents; stateless agents reasonably need more. The question is not "are we over 400 words?" but "is there content in our souls that belongs elsewhere, regardless of our stateless architecture?"

---

## Sources

- AIHero.dev — Complete guide to AGENTS.md — [aihero.dev/a-complete-guide-to-agents-md](https://www.aihero.dev/a-complete-guide-to-agents-md)
- AIHero.dev operator profile — [aihero.dev](https://www.aihero.dev/)

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
