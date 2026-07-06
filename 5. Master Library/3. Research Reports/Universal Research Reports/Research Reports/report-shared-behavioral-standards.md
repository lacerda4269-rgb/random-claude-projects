# Feynman Research Report — Topic 3: Shared Behavioral Standards Architecture in Multi-Agent AI

**Researched by:** Feynman (Academic Research Specialist)
**Directed by:** Sage (CEO) — Dr. Frankenstein Phase 2, Session 168
**Date:** 2026-05-21
**Output type:** Fact-finding — Design Input (not a deployable resource; Soren review not required)
**Prompt Injection Check:** None detected

---

## Task Summary

This report answers one central architectural question: in a multi-agent AI system where every agent has a "soul document," is it better to copy team-wide behavioral rules into each agent's document individually — or to centralize those rules in a shared governance layer that all agents inherit from?

The question was triggered by Cosmo's Phase 2 audit, which flagged the current "copy into every soul" pattern as the largest unresolved architectural issue on the team. This report draws on academic papers, practitioner production reports, and the documented behavior of leading multi-agent frameworks (LangGraph, CrewAI, AutoGen, OpenAI Swarm, Anthropic's own systems) to give Project 5 a research-grounded answer.

Plain language throughout. Technical terms are explained when introduced.

---

## Findings

### 1. The "Copy vs. Inherit" Problem in Multi-Agent Systems

**What the literature says:**

The copy-into-every-agent approach has a formal name in software design: it violates the DRY principle — "Don't Repeat Yourself." DRY is one of the oldest and best-tested rules in software engineering. Its core idea: every piece of knowledge in your system should have exactly one authoritative source of truth. When you copy the same information into ten places, you now have ten places that can drift apart. The literature on multi-agent AI systems confirms this problem applies directly to behavioral rules.

A 2025 empirical study across 1,642 execution traces in production multi-agent systems found that token duplication rates reach **86% in flat agent topologies** — meaning the vast majority of what agents pass around is redundant content, not unique work. The study linked this duplication directly to higher failure rates and increased coordination overhead. (Source: Token Coherence paper, arXiv 2603.15183)

The same body of research found that **inter-agent misalignment accounts for 32.3% of observed production failures** — and that "loss of conversation history where agents revert to stale artifact states" is a primary driver. In plain English: when agents each hold their own copy of shared rules, those copies go stale and diverge, and the divergence causes real failures.

**The software design parallel:**

In traditional software, there are two main patterns for sharing behavior across components: inheritance and composition.

- *Inheritance* means a child "is a" version of a parent. It gets the parent's rules automatically and can add its own on top.
- *Composition* means a component "has a" behavior module plugged into it. It doesn't copy the behavior — it references a shared module.

Modern software design strongly favors composition over inheritance because inheritance creates tight coupling (change the parent, every child breaks) while composition allows shared behavior to be updated in one place. The research literature on multi-agent AI systems is beginning to arrive at the same conclusion: copying rules into every agent document is analogous to copy-pasting code across dozens of files instead of writing a shared function. It works until something changes.

**The core finding:** The copy model is not wrong in principle, but it has a known and predictable failure mode — update lag and rule drift. As the team grows and rules evolve, keeping copies synchronized becomes an operational burden that compounds with scale.

---

### 2. Architectural Patterns for Shared Governance in Multi-Agent Systems

Several distinct architectural patterns have emerged in the literature and practitioner community for applying consistent behavioral standards across a team of agents. Here are the most relevant:

**Pattern A — Shared Constitutional Layer (Centralized Constitution)**

This is the closest direct equivalent to what Cosmo flagged. Rather than duplicating rules into each agent, a single "constitution" document defines team-wide behavioral standards. All agents are initialized with or pointed to this shared document before receiving their individual role instructions.

The academic work on this is now substantial. The paper "Evolving Interpretable Constitutions for Multi-Agent Coordination" (arXiv 2602.00755, February 2026) demonstrated that a single shared constitution applied across all agents in a team **outperformed per-agent rule sets by 123%** on a Societal Stability Score that combines productivity, survival, and conflict metrics. Critically, the evolved shared constitution also **reduced inter-agent communication by 98.6%** — because agents with consistent internalized standards spend less time negotiating, clarifying, and correcting each other.

The Multi-Agent Constitutional Learning paper (MAC, arXiv 2603.15968, March 2026) extended this by showing that shared constitutional rule sets — where rules can be proposed, critiqued, and refined — achieved **50% improvement over prior prompt optimization methods** while producing "human-readable and auditable rule sets." This is directly relevant to the team's soul document architecture.

**Pattern B — Operator-Level System Prompt Injection**

This is the approach used in production by Anthropic's own multi-agent systems. Rather than embedding governance rules in each agent's individual specification, governance rules are injected at the operator level — before each agent ever receives its role-specific instructions. Think of it as: operator rules → agent identity → agent task. The governance layer wraps every agent automatically.

Anthropic's production architecture documents confirm that "each agent uses its own configuration (model, system prompt, tools, MCP servers, and skills)" — but the operator-level layer sits above all of this and applies universally. This is the platform-enforced equivalent of a shared constitution.

**Pattern C — Orchestrator-Enforced Governance (Hub and Spoke)**

The practitioner production report "Multi-Agent in Production in 2026: What Actually Survived" found that governance in production systems that held up is **predominantly orchestrator-centric, not distributed across agents**. The pattern: a lead agent or orchestrator enforces behavioral standards through artifact validation, phase gates, and output checks — rather than relying on every individual agent to correctly self-apply rules from its own copy. The article reports that adding a centralized governance layer "pushed defense success from 0.32 to above 0.89" in systems that had previously relied on per-agent rule enforcement.

**Pattern D — Template + Override (Shared Foundation, Agent-Specific Extensions)**

This is a middle path, and the one most directly relevant to the soul document architecture. The SOUL.md pattern practitioner guide (agentconn.com) describes it as: "one shared SOUL.md template with agent-specific overrides." Every agent starts from the same shared behavioral foundation. Agent-specific identity, role, and values are then layered on top. The cascade works: "the most specific definition wins."

This pattern maps cleanly to how the team's agents are actually structured — each agent has both team-wide rules and role-specific rules. The architectural change would be separating these instead of mixing them. Team-wide rules live in one place. Agent-specific rules live in the individual soul. Agents compose the two at initialization.

**Pattern E — Skills and Hooks as Behavioral Overlays**

This is the pattern Cosmo pointed at when he flagged the behavioral rules as "the largest skill candidate he has seen." In Claude Code's own architecture, skills and hooks are external files that can be injected into any agent's context — they are not copied into the agent's core document. A hook fires automatically before or after defined actions. A skill is loaded on assignment, not pre-loaded everywhere. This is a composition pattern: the behavioral rule lives in one place, gets referenced by many agents, and updating it updates it everywhere simultaneously.

The LLM Constitutional Multi-Agent Governance (CMAG) paper (arXiv 2603.13189) formalized this as a "two-stage framework that interposes between the LLM policy compiler and the agent population" — a governance layer that sits between the underlying model and the individual agents, rather than being embedded inside each agent. CMAG achieved an Ethical Cooperation Score of 0.741, a 14.9% improvement over unconstrained optimization, while preserving agent autonomy and integrity at 0.985 and 0.995 respectively.

---

### 3. Failure Modes of Each Approach

**Failure modes of copying rules into every agent document:**

1. **Rule drift.** When the same rule lives in ten places, keeping all ten in sync requires deliberate effort every time the rule changes. In practice, some copies get updated and some don't. Agents then operate under subtly different behavioral standards, producing inconsistent team behavior that is hard to diagnose.

2. **Update lag.** There is always a gap between when a rule is updated in one agent and when it propagates to all others. During that gap, the team is operating with mismatched standards.

3. **Specification bloat.** Each agent's soul grows with every new team-wide rule. The more rules accumulate, the larger each document becomes, the more context window space is consumed loading behavioral standards that are identical across every agent, and the harder it becomes to identify what is actually unique to each agent.

4. **Maintenance burden that scales poorly.** With 5 agents, updating a rule requires 5 edits. With 15 agents, 15 edits. The burden is linear with team size. The research confirms this: token duplication rates of 86% in flat topologies are the documented cost of this approach at scale.

5. **Inconsistency detection lag.** Because each agent holds its own copy, behavioral inconsistencies between agents are not visible until agents interact. By then, compounding errors may have already propagated. The research on agent drift (arXiv 2601.04170) confirms that "a single atomic falsehood can spread into system-level false consensus" once one agent's rules diverge from the team's standard.

**Failure modes of centralizing rules in a shared governance layer:**

1. **Context loading risk.** If the shared behavioral rules are not reliably injected into each agent's context at initialization, agents may operate without them. In session-based LLM systems, there is no guaranteed persistence — if the shared rules don't load, agents have no behavioral standard at all. This is the single biggest operational risk of centralization.

2. **Specificity loss.** A single shared document cannot capture everything. If behavioral rules are too generic at the shared level, agents may apply them inconsistently depending on their specific role context. The fix is the template+override pattern — shared foundation plus role-specific extensions.

3. **Single point of failure for rule errors.** A mistake in the shared constitution propagates to every agent simultaneously, whereas a mistake in one agent's copy only affects that agent. Centralization amplifies both correct rules and incorrect ones equally.

4. **Auditability tradeoff.** When rules are in every soul document, it is easy to inspect any agent and see exactly what behavioral standards it is operating under. With a shared layer, you need to look at two documents — the shared constitution and the agent-specific soul — to get the full picture. This is a minor friction, but it is real.

**LLM-specific failure patterns that differ from traditional software:**

Traditional software agents follow rules deterministically — they either have the rule or they don't. LLM-based agents are probabilistic. This means:

- Even when a rule is present in the context, it may not be applied consistently. The agent drifts stochastically, not just from missing information.
- "Role drift" — where agents gradually deviate from their designated responsibilities — happens even when role definitions are explicit (RoleFix paper, Preprints.org 2603.0348). Copying a rule into a soul document does not guarantee it is followed. Neither does centralizing it. What matters is how reliably it loads, how prominently it appears in context, and how regularly compliance is checked.
- Context window pollution is a real and specific risk. As interaction histories grow, behavioral rules that appeared early in a long context get progressively deprioritized. The agent starts to weight recent conversational content over foundational behavioral standards. This is a structural property of transformer-based LLMs, not a bug in any specific architecture.

---

### 4. Constitutional AI and Related Approaches

**What Constitutional AI is:**

Constitutional AI (CAI) is a method developed by Anthropic starting around 2022. Instead of trying to hand-code every rule for how an AI should behave, CAI gives the model a "constitution" — a set of principles and values — and trains the model to use that constitution to evaluate and correct its own behavior. The model is taught to ask: "Does this response violate the constitution?" If yes, revise it.

The key insight of CAI is that you can get more consistent, principled behavior by training on a small, well-designed set of values than by trying to enumerate every specific prohibited behavior. It is a governance architecture based on principles rather than rules.

**How CAI applies to multi-agent teams:**

CAI was originally designed for single agents. Applying it to multi-agent teams is an active research area. The key challenge: in a single-agent system, the constitution is applied once, to one model. In a multi-agent team, you need the constitutional principles to be consistently applied across every agent, every session, every interaction — and you need the agents' constitutions to be compatible with each other, not just internally consistent.

Three recent papers address this directly:

The "Evolving Interpretable Constitutions for Multi-Agent Coordination" paper (arXiv 2602.00755) found that a single shared constitution — discovered through an evolutionary algorithm rather than hand-crafted by humans — outperforms both human-designed constitutions and generic prosocial principles ("be helpful, harmless, honest"). The evolved constitution achieved 123% higher stability than human-designed baselines. This is significant: it suggests that team-wide behavioral standards should be designed for the team as a whole, not assembled from what sounds reasonable for individual agents.

The MAC (Multi-Agent Constitution Learning) paper (arXiv 2603.15968) demonstrated that treating the constitution as a shared modular structure — where rules can be independently added, edited, or removed — produces better outcomes than either fixed per-agent rules or generic prompts. The "modular" framing maps directly to the skill architecture Cosmo identified.

The CMAG paper (arXiv 2603.13189) proposed applying constitutional constraints at a layer between the LLM and the agents — a centralized filter rather than a per-agent embedded rule set. Their system preserved agent autonomy at 0.985 while enforcing ethical constraints, which is the right balance for a team like this one where agents need both consistent standards and the freedom to operate within their specific lanes.

**What CAI looks like for a specialized team:**

Rather than embedding "no-blame culture, loop prevention protocol, three-altitude framework" into every agent's soul document, a CAI-inspired approach would define these as a shared team constitution: a small, clear set of principles that every agent is initialized with before receiving its role-specific identity. The soul document then focuses on what is genuinely unique to the agent — its role, its values, its escalation chain, its domain expertise. The team-wide standards live in one document, loaded once, referenced everywhere.

Anthropic's own published constitution (January 2026) demonstrates this at the model level: rather than listing every prohibited behavior, it establishes a priority hierarchy and explains the reasoning behind each principle. The goal is not compliance with a checklist — it is internalization of a value system. That framing is exactly what the soul documents are trying to achieve at the team level.

---

### 5. Practical Recommendations from the Field

**What the literature recommends for small specialized agent teams:**

The convergent recommendation across the academic papers, practitioner production reports, and framework documentation is a layered architecture with clear separation between shared and agent-specific standards. For a team of 5-8 specialized agents, the pattern that holds up in production is:

**Layer 1 — Shared Team Constitution (one document, loaded first for every agent):**
Team-wide behavioral standards. No-blame culture. Loop prevention. Three-altitude framework. Dialog standards. Escalation chain. These rules are identical across all agents. They live in exactly one place. Every agent loads this document before loading its own soul.

**Layer 2 — Agent-Specific Soul (one document per agent, loaded second):**
Role definition. Domain expertise. Agent-specific values and priorities. Lane discipline. Escalation specifics. Anything that is genuinely unique to this agent. The soul document is shorter because it does not repeat what Layer 1 already covers.

**Layer 3 — Skills and Hooks (external files, assigned per agent per project):**
Executable behavioral overlays for specific tasks. These are not identity — they are capability. They live outside both the constitution and the soul and are loaded only when assigned.

**What actually holds up at runtime vs. what looks good on paper:**

The production evidence is clear on several points:

- Centralized governance layers outperform distributed per-agent enforcement **when they reliably load**. The failure mode of centralization is not the architecture — it is the implementation. If the shared document does not consistently appear in every agent's context, agents operate without it.
- The orchestrator-centric governance pattern (where the lead agent or a supervisor validates outputs) performs better than peer-to-peer rule enforcement. A 2026 production analysis found that adding a centralized governance layer improved defense success from 0.32 to 0.89.
- Role drift happens regardless of architecture, but it is significantly worse when agents hold inconsistent copies of behavioral standards. The RoleFix protocol (structured role declarations at each turn, hybrid drift detection, self-repair mechanisms) is a lightweight mitigation that works independently of whether rules are centralized or distributed.
- Shared constitutions reduce inter-agent communication overhead. The research finding that optimized constitutions reduce communication by 98.6% is counterintuitive but documented: agents with consistent internalized values spend less time negotiating and correcting each other.
- **The template+override pattern is the practical middle path.** A shared foundation that every agent loads, plus agent-specific extensions in the individual soul. This is used by multiple production-grade soul document systems (SOUL.md pattern, OpenClaw's cascade loading). It solves the update problem without losing agent specificity.

**What IBM's AI governance research adds:**

IBM's enterprise governance framework explicitly states that "controls must be architectural, not procedural, to scale effectively." Telling agents to follow rules (procedural) does not scale. Building the rules into the layer of the system that every agent loads at initialization (architectural) does. This is the core argument for a shared team constitution layer.

---

## Key Takeaways for the Team

- **The copy-into-every-soul model is the industry's known anti-pattern for exactly the failure modes Cosmo identified.** Token duplication at 86%, update lag, rule drift, and specification bloat are all documented in the literature as the predictable costs of this approach. The team is not doing something unusual — this is how many systems start. It just does not scale well.

- **The recommended architecture for a 5-8 agent specialized team is a two-layer system:** a shared team constitution (one document, loaded first, team-wide standards only) plus agent-specific souls (individual documents, role-specific content only). This is the template+override pattern, and it is the convergent recommendation across both academic research and practitioner production reports.

- **Centralizing rules solves the update problem but creates a context-loading dependency.** If the shared constitution does not reliably load for every agent in every session, agents operate without it. Project 5 needs to solve this with a reliable injection mechanism — a skill, a hook, a session-start load sequence, or an operator-level system prompt — before centralizing rules is safe.

- **Skills and hooks are the right mechanism for executable behavioral standards** (loop prevention protocol, three-altitude framework, escalation chain). These are not identity claims — they are operational rules. They belong in external files that can be updated in one place and applied everywhere simultaneously. Cosmo's instinct to flag these as skill candidates is supported by the literature.

- **Constitutional AI research confirms that team-wide principles should be designed for the team as a whole, not assembled by extrapolating from individual agent rules.** The evolved constitutions in the academic research outperformed both hand-crafted and per-agent rules. This suggests Project 5 should consider designing the shared team constitution from the team's operational reality up, rather than by extracting the common sections from existing soul documents.

---

## C&P Summary

Right now, every agent on the team has a copy of the same behavioral rules — no-blame culture, loop prevention, three-altitude thinking, and so on — pasted into their individual soul document. That approach works, but the research is clear that it has a predictable failure mode: the copies drift apart over time, updates have to happen in multiple places, and as the team grows, the maintenance burden multiplies. The academic literature calls this an anti-pattern (it violates the "Don't Repeat Yourself" principle from software design), and production data from real multi-agent systems confirms that token duplication rates hit 86% and that rule divergence accounts for roughly a third of observed failures.

The recommended fix, both from the research papers and from what actually holds up in production, is a two-layer architecture: a single shared "team constitution" document that contains all the rules that apply to every agent equally, plus a shorter individual soul document for each agent that covers only what is genuinely unique to that agent's role. Every agent loads the shared constitution first, then their own soul on top. When a team-wide rule changes, you update one file and it applies everywhere immediately. This is the same pattern that Anthropic uses at the model level with Constitutional AI — define the principles once, apply them universally, and let each agent add its specific role-based identity on top.

The one risk of centralizing rules is that if the shared document fails to load for some reason, agents have no behavioral standards at all. So Project 5's design work needs to include a reliable mechanism for ensuring the shared constitution actually reaches every agent at the start of every session — whether that is a skill, a hook, or a session-start protocol. That implementation detail is what separates an architecture that looks good on paper from one that holds up in production.

---

## Sources

- [Evolving Interpretable Constitutions for Multi-Agent Coordination — arXiv 2602.00755](https://arxiv.org/abs/2602.00755)
- [MAC: Multi-Agent Constitution Learning — arXiv 2603.15968](https://arxiv.org/abs/2603.15968)
- [LLM Constitutional Multi-Agent Governance (CMAG) — arXiv 2603.13189](https://arxiv.org/abs/2603.13189)
- [Agent Drift: Quantifying Behavioral Degradation in Multi-Agent LLM Systems — arXiv 2601.04170](https://arxiv.org/abs/2601.04170)
- [Token Coherence: Adapting MESI Cache Protocols for Multi-Agent LLM Systems — arXiv 2603.15183](https://arxiv.org/abs/2603.15183)
- [Multi-Agent in Production in 2026: What Actually Survived — Medium / Micheal Lanham](https://medium.com/@Micheal-Lanham/multi-agent-in-production-in-2026-what-actually-survived-f86de8bb1cd1)
- [SOUL.md: The Persistent Agent Identity Pattern — AgentConn Blog](https://agentconn.com/blog/soul-md-persistent-agent-identity-pattern-guide/)
- [Why Multi-Agent LLM Systems Fail and How to Fix Them — Augment Code](https://www.augmentcode.com/guides/why-multi-agent-llm-systems-fail-and-how-to-fix-them)
- [Anthropic's Multi-Agent Blueprint: What Production Adds — Fountain City](https://fountaincity.tech/resources/blog/anthropic-multi-agent-blueprint-production/)
- [How We Built Our Multi-Agent Research System — Anthropic Engineering](https://www.anthropic.com/engineering/multi-agent-research-system)
- [Multiagent Sessions — Claude API Docs / Anthropic](https://platform.claude.com/docs/en/managed-agents/multi-agent)
- [Claude's New Constitution — BISI Report](https://bisi.org.uk/reports/claudes-new-constitution-ai-alignment-ethics-and-the-future-of-model-governance)
- [Multi-Agent System Architecture Guide for 2026 — ClickIT Tech](https://www.clickittech.com/ai/multi-agent-system-architecture/)
- [Detecting and Repairing Role Drift in Multi-Agent Collaboration — Preprints.org 202603.0348](https://www.preprints.org/manuscript/202603.0348)
- [The Orchestration of Multi-Agent Systems: Architectures, Protocols, Enterprise Adoption — arXiv 2601.13671](https://arxiv.org/html/2601.04170v1)
- [CrewAI vs LangGraph vs AutoGen — DataCamp Tutorial](https://www.datacamp.com/tutorial/crewai-vs-langgraph-vs-autogen)
- [Agent System Design Patterns — Databricks](https://docs.databricks.com/gcp/en/generative-ai/guide/agent-system-design-patterns)
- [OpenAI Swarm: Lightweight Multi-Agent Orchestration Guide — Morph](https://www.morphllm.com/openai-swarm)
- [AI Agent Frameworks Compared: LangGraph vs CrewAI vs AutoGen — PEC Collective](https://pecollective.com/blog/ai-agent-frameworks-compared/)
- [Don't Repeat Yourself — DevIQ](https://deviq.com/principles/dont-repeat-yourself/)
- [Composition Over Inheritance in System Design — Medium / Debby Lee](https://medium.com/@debby1ee/composition-over-inheritance-in-system-design-f9f714626931)

---

## Additional Findings

**The communication reduction effect is significant and underappreciated.** The finding that a shared optimized constitution reduces inter-agent communication by 98.6% is not just an academic curiosity. In practical terms, it means agents with genuinely internalized shared standards spend far less time renegotiating, clarifying, and correcting each other mid-task. For this team, that would translate to shorter context windows, faster sessions, and fewer escalations triggered by agents operating on different assumptions.

**The "living specification" pattern is worth attention for Project 5.** The Augment Code guide describes keeping behavioral standards in a "living document that updates to reflect reality" — meaning the shared constitution is not static. It evolves as the team learns. This maps directly to the team's current practice of updating soul documents through the AAR process. The architectural change is consolidating where that update happens, not changing the cadence.

**OpenAI Swarm's approach illustrates the minimal viable governance model.** Swarm defines an agent as a system prompt plus a list of functions. Only the active agent's instructions appear in context at any given time. There is no per-agent duplication of team-wide rules because Swarm's architecture does not support persistent per-agent documents at all. This is a more radical simplification than what this team needs, but it illustrates that the "copy rules into every agent" pattern is not a universal requirement — it is an architectural choice, and other valid choices exist.

**The context window pollution risk deserves explicit attention in Project 5.** Multiple research papers (Agent Drift, MAST taxonomy, Token Coherence) identify context window pollution as a primary mechanism of behavioral degradation in LLM-based agents. Behavioral rules that appear early in a long context are progressively deprioritized as the context fills with recent conversation. This affects both centralized and distributed approaches — but centralized approaches are better positioned to address it because a shared constitution can be structured for prominence and re-loaded at defined checkpoints more easily than rules distributed across many individual soul documents.

**Prompt injection risk is higher with centralized governance layers.** The research confirms that hub injection (attacking the orchestrator or shared policy layer) produces system-wide failures in multi-agent systems — 100% failure rates in LangGraph in the documented tests. If the team moves to a centralized team constitution, that document becomes a high-value target for prompt injection. Project 5 should include Soren's input on the security implications of centralizing behavioral standards before finalizing the architecture.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
