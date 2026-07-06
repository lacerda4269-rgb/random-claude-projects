# Agent Soul Proper Format — Informational Report

**Report Type:** Fact-finding — informational only; routes directly to Sage, no Soren pipeline
**Researcher:** Rose
**Date:** 2026-05-03
**Requested by:** Jay (Item 15, Session 106 batch — companion to Item 5)
**Context:** Jay's concern: "I don't want our agents to start getting bloated." This report informs Project 7 (Final MG/SOP + Soul Review) and the ML Index soul upgrade concept.

---

**C&P Summary:** Soul files (sometimes called SOUL.md or persona files) are the documents that define who an AI agent is — their name, role, personality, values, working style, and behavioral rules. The practitioner community has reached strong consensus on what works: soul files should be short (200-400 words, ideally under 50 lines), focused exclusively on identity and principles (not operational procedures), and written in concrete language rather than vague abstractions. The main failure mode is bloat — rules accumulate reactively, operational details creep in, and what should be a lean identity document becomes a dense manual that the model either ignores or gets confused by. There is an emerging open standard (SoulSpec) and enough practitioner writing to triangulate solid best practices. Jay's concern about agent bloat is well-founded, and this research provides the framework for addressing it.

---

## Research Findings

### PART 1 — THE EMERGING STANDARD: WHAT PRACTITIONERS AGREE ON

The SOUL.md pattern has reached critical mass in 2025-2026. Multiple independent sources have converged on a similar set of principles.

**The five-section consensus structure (Verified — cross-sourced):**

1. **Core Identity** — Name, role, primary orientation. One clear expertise statement. Specific, not generic.
2. **Values & Operating Principles** — The beliefs that guide judgment calls. Concrete behaviors, not abstract virtues. "Correctness over cleverness" not "I value quality."
3. **Communication Style** — Tone, format preferences, response texture. Voice consistency — written in the agent's own voice.
4. **Hard Limits / Boundaries** — Never-do behaviors, regardless of instructions. Lead with limits before personality.
5. **Continuity Instructions** — How the agent maintains consistency across sessions.

**Optional but documented in multiple sources:**
- Domain expertise listing (specific tools, technologies, experience)
- Sample interaction (one example of ideal behavior)
- Anti-patterns (what NOT to do — often more useful than what to do)

---

### PART 2 — LENGTH AND SCOPE

This is the clearest and most consistent finding across all sources.

**The consensus:**
- 200-400 words total (AgentConn, multiple sources) — **Verified cross-sourced**
- Under 50 lines (Jagodana) — **Verified**
- "Longer files don't produce better agents; they produce slower, more confused ones" (AgentConn) — **Verified**
- Prompts over 2,000 words → agents follow early instructions well and ignore later ones (Runyard) — **Verified cross-sourced**
- Instruction budget: ~150-200 instructions with reasonable consistency for frontier LLMs (aihero.dev) — **Verified**

The implication is direct: a soul file that exceeds 400 words is not carrying more useful identity — it is competing against itself. Instructions in the second half of a long soul file are systematically less likely to be followed than instructions in the first half.

---

### PART 3 — WHAT BELONGS IN A SOUL FILE

Soul files are philosophical, not operational.

**What belongs:**
- Who the agent is (identity, role, name)
- What the agent values (principles, judgment anchors)
- How the agent communicates (voice, tone, style)
- What the agent will not do (hard limits)
- How the agent maintains consistency (continuity signals)

**What explicitly does NOT belong:**
- Tool configurations and capability definitions (separate systems)
- Factual knowledge and domain knowledge bases (use a knowledge base or skill)
- SOPs and runbooks (operational documents — separate files)
- Project-specific details (project memory or config files)
- Frequently-changing details (anything that will need updating)
- Large manuals or reference material embedded directly
- Anything that could be stored in a skill and retrieved on-demand

The clearest articulation from SoulSpec: "AGENTS.md defines how agents work on your code. SoulSpec defines who your agent is." The soul is identity. Everything else is operational.

---

### PART 4 — FAILURE MODES AND ANTI-PATTERNS

**Bloat (Primary failure mode):**
- Reactive accumulation: adding rules every time something goes wrong without removing obsolete ones
- No audit cadence: files grow but are never trimmed
- Comprehensiveness bias: trying to cover every scenario instead of establishing identity
- Treating the soul file as a knowledge base, manual, or SOP document
- Result: "balls of mud" — dense, unmaintainable, self-contradicting

**Ambiguity and contradiction:**
- Conflicting directives ("always ask before acting" + "work autonomously") cannot both be followed. The model must choose one — usually the earlier instruction.
- Vague values ("be helpful," "be thorough") provide no behavioral anchor. The model defaults to its base behavior.
- Generic personas: research shows adding a generic persona in system prompts "did not improve model performance and sometimes had negative effects." The persona must be specific and coherent to matter.

**Over-specification:**
- Trying to specify behavior for every scenario produces an agent that follows rules mechanically rather than exercising judgment in the spirit of those rules.
- The goal is a clear enough identity that the agent can extrapolate correct behavior to novel situations — not a rulebook that covers every case.

**Persona hijacking:**
- "The model is designed to treat the persona it is assigned seriously and will sometimes ignore instructions in order to maintain adherence to the described persona." (Runyard) — a persona that is too rigid or internally inconsistent can cause the model to prioritize persona consistency over task instructions.

**Missing hard limits:**
- Multiple sources identify the absence of explicit "never do" behaviors as a critical gap. Agents without clear limits make their own interpretation in ambiguous situations.

---

### PART 5 — THE SOUL vs. OPERATIONS DISTINCTION

| Belongs in Soul | Belongs Elsewhere |
|---|---|
| Identity (name, role, what I am) | SOPs and runbooks |
| Principles (what I value) | Skill assignments |
| Voice and communication style | Project context |
| Hard limits | Tool configurations |
| Team relationship dynamics | Workflow procedures |
| Continuity signals | Domain knowledge bases |

The failure mode most relevant to Jay's concern is when operational content migrates into soul files. This happens gradually — a lesson gets added here, a procedure gets noted there — and over time the soul becomes an operational manual with some identity content buried inside it.

**The audit question:** For each line in a soul file, ask: "Does this tell me who this agent is, or does it tell me what this agent should do?" If the answer is "what to do," it belongs in an SOP, a skill, or a project config — not a soul file.

---

### PART 6 — THE SOULSPEC OPEN STANDARD

SoulSpec ([soulspec.org](https://soulspec.org/)) is the most structured framework found. Its file architecture:

- `soul.json` — required manifest (metadata, versioning, compatibility, discovery)
- `SOUL.md` — required core personality (values, communication style, opinions, behavioral guidelines)
- `IDENTITY.md` — optional (name, role, backstory)
- `AGENTS.md` — optional operational layer (workflows, task handling, tool usage, memory patterns — NOT soul content)
- `STYLE.md` — optional communication preferences
- `HEARTBEAT.md` — optional autonomous check-in patterns
- `examples/` — optional good/bad output samples

**Key architectural insight from SoulSpec:** What we call a "soul file" they break into two: identity/personality (SOUL.md) and operational behavior (AGENTS.md). These are deliberately separate. Our system currently merges them. That is a design choice, not a mistake — but it is worth evaluating whether the merged approach is serving us or generating the bloat Jay is concerned about.

---

### PART 7 — WHAT "DONE" LOOKS LIKE FOR A WELL-DESIGNED SOUL

From practitioners surveyed:
- Clear role definition that tells the agent not just what to do but how to think
- Concrete language throughout — specific, not generic
- Anti-patterns included — what NOT to do, often more useful than what to do
- Hard limits defined explicitly before personality content
- Written in the agent's own voice (if the agent is casual, write the soul casually)
- Version controlled and treated as a code artifact
- Reviewed on a regular cadence — quarterly minimum
- Tested for consistency: identical prompts across sessions should produce similar outputs

---

## Sources

- SoulSpec.org — [soulspec.org](https://soulspec.org/)
- AgentConn.com — SOUL.md pattern guide — [agentconn.com](https://agentconn.com/blog/soul-md-persistent-agent-identity-pattern-guide/)
- Jagodana.com — Agent soul files — [jagodana.com](https://www.jagodana.com/blogs/agent-soul-files-defining-ai-agent-personality)
- Runyard.io — System prompts best practices 2026 — [runyard.io](https://runyard.io/blog/ai-agent-system-prompts-guide)
- GitHub Blog — Lessons from 2,500+ repositories — [github.blog](https://github.blog/ai-and-ml/github-copilot/how-to-write-a-great-agents-md-lessons-from-over-2500-repositories/)
- Microsoft Security Blog — Failure modes in agentic AI — [microsoft.com](https://www.microsoft.com/en-us/security/blog/2025/04/24/new-whitepaper-outlines-the-taxonomy-of-failure-modes-in-agentic-ai-systems/)
- MindStudio — AI agent failure pattern recognition — [mindstudio.ai](https://www.mindstudio.ai/blog/ai-agent-failure-pattern-recognition)
- AIHero.dev — Complete guide to AGENTS.md — [aihero.dev](https://www.aihero.dev/a-complete-guide-to-agents-md)

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
