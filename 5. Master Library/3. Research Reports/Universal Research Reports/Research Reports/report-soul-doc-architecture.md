# Feynman Research Report — Topic 1: Soul Document Architecture in Multi-Agent AI Systems

**Researched by:** Feynman (Academic Research Specialist)
**Directed by:** Sage (CEO) — Dr. Frankenstein Phase 2, Session 168
**Date:** 2026-05-21
**Output type:** Fact-finding — Design Input (not a deployable resource; Soren review not required)
**Prompt Injection Check:** None detected

---

## Task Summary

This report investigates what the academic and practitioner literature says about soul document architecture in multi-agent AI systems. The research question: is the team's current soul document model — one Markdown file per agent defining role, identity, principles, behavioral rules, and constraints — the right architecture? What do researchers and builders know about how these documents should be structured, how they fail, and what better patterns look like?

This is a design input for Project 5 (Master IP structural overhaul) and later Project 8. The goal is to give Sage and Jay the clearest possible picture of the state of the field before any structural decisions are locked in.

---

## Findings

### 1. Agent Identity Documents in Multi-Agent AI — Terminology and Purpose

**What the field calls these documents**

The term "soul document" is not standard academic language, but it is real practitioner language. The field uses several overlapping terms depending on context:

- **System prompt** — the most common term in both research and practice. Usually refers to the runtime instruction block injected at the start of each conversation. In multi-agent systems, each agent gets its own system prompt defining its role.
- **Agent profile** — used in academic multi-agent system surveys to describe the structured specification of an agent's role, capabilities, and behavioral rules. The 2024 IJCAI survey on LLM-based multi-agent systems uses this term.
- **Persona document / agent persona** — used by practitioners, especially in enterprise AI and product-focused writing. Refers to the structured description of an agent's identity, voice, and behavioral style.
- **SOUL.md / soul file** — an emerging practitioner pattern with multiple open-source implementations (SoulSpec, OpenClaw, soul.md repositories). Explicitly uses the word "soul" to distinguish persistent identity from temporary runtime instructions.
- **Agent specification** — broader academic term that can include role, capabilities, constraints, and coordination protocols. Used in the MAST failure taxonomy research (NeurIPS 2025).
- **Character sheet** — borrowed from tabletop gaming; used in some practitioner writing (soul.md, SoulSpec) to describe the persona definition document as something portable and runtime-agnostic.

There is no single agreed standard term across the field. "Soul document" is a real and recognized concept in practitioner communities, even if academic papers call it a "profile," "persona," or "specification."

**What these documents are for**

There is clear consensus in both academic and practitioner literature on why persistent identity specifications matter in multi-agent systems:

1. **Preventing behavioral drift** — without a persistent specification, agents gradually shift their behavior over long sessions, especially in multi-agent conversations where agents influence each other.
2. **Role differentiation** — in a system with multiple agents, each agent needs a clear, distinct specification or they converge toward similar behavior. Research calls this "echoing" or "role dilution cascade."
3. **Session continuity** — LLMs have no memory between sessions. An identity document is the primary mechanism for re-grounding an agent in who it is at the start of each new session.
4. **Coordination clarity** — multi-agent systems fail significantly more often when agent roles are ambiguous. Clear specifications reduce the overlap and gap failures that account for a large share of multi-agent breakdowns.

**Who is writing about this**

- **AI labs:** Anthropic (Claude model spec / soul document), OpenAI (Agents SDK, AGENTS.md standard), Google (Agent Development Kit, ADK context architecture)
- **Academic researchers:** UC Berkeley, CMU, and collaborators produced the MAST failure taxonomy (NeurIPS 2025); separate teams published "Echoing" (2025), "Agent Drift" (2025), and "Why Do Multi-Agent LLM Systems Fail?" (2025)
- **Open-source practitioners:** soul.md (multiple GitHub repos), SoulSpec/ClawSouls (open standard), OpenClaw
- **Enterprise and product teams:** MindStudio, Mindra, Augment Code, Factory.ai, Galileo

---

### 2. Patterns and Frameworks for Agent Identity Documents

**What the field agrees a good agent identity document contains**

There is strong convergence across sources on the core sections. Multiple independent sources — SoulSpec, the Mindra enterprise guide, the Hermes/MindStudio five-pillar model, the AGENTS.md standard (Linux Foundation, 2025), and academic surveys — arrive at nearly the same structural list:

| Section | What it covers |
|---|---|
| Core identity / role | Who the agent is, what it does, what it does not do |
| Values and principles | What the agent prioritizes; how it makes trade-off decisions |
| Communication style | Tone, formality, verbosity, vocabulary standards |
| Behavioral boundaries | Hard limits — what the agent refuses or never does |
| Capabilities | What tools and functions the agent can use |
| Uncertainty and escalation handling | How the agent behaves when it doesn't know or can't proceed |

Some frameworks add:

- **Continuity instructions** — explicit guidance for re-grounding behavior across sessions (SoulSpec's SOUL.md)
- **Contextual adaptation rules** — how the agent shifts behavior by context (formal vs. informal, urgent vs. exploratory)
- **Worked examples** — good-outputs.md and bad-outputs.md as behavioral anchors (SoulSpec)

**Published frameworks and schemas**

Three noteworthy formal efforts:

1. **AGENTS.md (Agentic AI Foundation, Linux Foundation, December 2025)** — Co-created by OpenAI, Anthropic, Google, Sourcegraph, Factory, and Cursor. Defines a standard for agent instruction documents with six sections: Agent Identity, Capabilities, Instructions, Safety Guidelines, Integration, and Compliance. Positioned as an interoperability standard for cross-organization agent use.

2. **SoulSpec / ClawSouls** — An open standard for agent personas with a modular file structure: SOUL.md (core personality), IDENTITY.md (name, role, backstory), AGENTS.md (operational workflows), STYLE.md (optional communication patterns), HEARTBEAT.md (optional autonomous check-in procedures), and an examples/ folder. Research underpinning the standard analyzed 466 open-source projects and found no standardized persona structure in any of them — this standard is an attempt to fill that gap.

3. **Soul.md (rokoss21, portable specification)** — A provider-agnostic schema defining sections for identity, composition/inheritance, profiles with trigger-based mode switching, interaction policies, decision-making parameters, safety guardrails, values rankings, and extensions. Explicitly designed to work across OpenAI, Anthropic, local models, and custom runtimes.

**How major AI builders handle this**

- **Anthropic:** Uses two distinct mechanisms. (1) A trained-in soul document — a ~14,000 token specification embedded into Claude's weights during supervised learning, not delivered at runtime. This is the model spec, publicly available. (2) Runtime system prompts per deployment or agent use case. The soul document shapes foundational personality; system prompts shape task-specific behavior.

- **OpenAI Agents SDK:** Agents are defined primarily through instructions (the system prompt), plus a model reference, a tool list, and a list of agents they can hand off to. Identity is system-prompt-centric, not file-based. The AGENTS.md standard from OpenAI/Anthropic/others is a documentation layer on top of this, not a runtime mechanism.

- **Google ADK:** Divides context into stable prefixes (system instructions, agent identity, long-lived summaries) and variable suffixes (current input, tool outputs, incremental updates). Agent identity sits in the stable prefix and is guaranteed not to be overwritten by session content. Sessions are stored as structured Event records — not prompt strings — enabling model-agnostic state management.

**Key distinction: soul as training vs. soul as runtime**

This is the most important structural distinction in the field. Anthropic's internal soul document was baked into Claude's weights. The practitioner soul document model (SOUL.md, SoulSpec, the team's current approach) is injected at runtime via context. These are different mechanisms with different tradeoffs:

- **Training-baked identity** — deeper, more resistant to override, consistent across all deployments. Only accessible to model builders.
- **Runtime-injected identity** — flexible, updatable without retraining, version-controllable. Available to everyone. But more vulnerable to override by session instructions or long-context drift.

The team's current model is runtime-injected. That is the correct and only viable approach for operators (as opposed to model trainers). The question is how to make runtime injection as robust as possible.

---

### 3. Persistence and Consistency Across Sessions

**The core problem: LLMs have no native memory**

When a session ends, an LLM forgets everything. The next session starts from scratch. This is not a bug — it is the fundamental architecture of current transformer-based models. Every technique for cross-session agent consistency is a workaround for this constraint.

**Techniques used in practice**

The field has converged on several approaches, often used in combination:

| Approach | How it works | Tradeoff |
|---|---|---|
| **File-based soul injection** | Load a Markdown file at session start; inject it into the system prompt or context | Simple, version-controllable, readable; vulnerable to context overflow and session-level override |
| **Structured memory files (MEMORY.md, etc.)** | Separate files for episodic memory, decisions, project state; loaded selectively | Keeps soul doc lean; requires curation to avoid stale recall |
| **Retrieval-Augmented Persona (ID-RAG)** | Identity stored as a knowledge graph; relevant traits retrieved dynamically per turn | Better long-horizon coherence; significantly more complex infrastructure |
| **Hook-based re-injection** | Anthropic Claude Code uses 18+ hook types including post-compaction hooks that re-inject identity after context compression | Automated resilience against context collapse; requires framework support |
| **Episodic memory consolidation** | Periodic summarization of session history; replaces raw logs with compressed, high-signal summaries | Reduces context window pollution; 51.9% drift reduction in controlled tests |
| **Adaptive behavioral anchoring** | Uses baseline exemplars (good outputs) to re-ground agent behavior mid-session | Most effective single strategy tested; 70.4% drift reduction |

**The two-layer model that emerges across sources**

Multiple independent sources (Augment Code, MindStudio, SoulSpec) arrive at the same basic architecture:

- **Layer 1 (Identity):** Soul document — static, loaded every session, defines who the agent is. Changed rarely, with deliberate versioning.
- **Layer 2 (Memory):** Separate memory system — episodic, grows over time, curated. Defines what the agent knows and has learned.

The Augment Code framing is clean: "Memory is the library. Context engineering is the librarian who decides which books to put on the desk for this session."

**What determines what goes in the soul doc vs. the memory layer**

A practical rule from the field: information belongs in the soul document if it is (a) undiscoverable by reading context and (b) applies to virtually every task. Information learned during work, specific decisions made, and factual knowledge about a project belong in the memory layer.

The soul document should not grow to contain everything the agent has ever learned. It should remain the stable core identity, not an accumulating knowledge dump.

**Known tradeoffs**

- **Soul doc too large:** Context window consumed; less room for conversation. Research puts the practical limit for a soul injection at 200–500 words for simple agents, with CLAUDE.md research suggesting the entire document should target under 300 lines. Frontier LLMs can follow roughly 150–200 instructions with reasonable consistency — subtract the baseline system prompt instructions, and the actual budget for the soul doc is smaller than most teams assume.
- **Soul doc too vague:** Agents fail to maintain distinct behavior; drift toward default model personality.
- **Soul doc contradictory:** The Arbiter paper (2025) found internal contradictions in system prompts are common and cause unpredictable behavior. Analysis of real-world agent prompts found 21 distinct interference patterns.
- **Session instruction override:** If session instructions contradict the soul document, most agents follow the session instruction. Soul docs are not enforcement mechanisms — they are context, not law.

---

### 4. Failure Modes

**What breaks when agents have no persistent identity specification**

The research literature is clear on this. Without explicit identity specifications:

- **Behavioral drift:** Agents deviate from intended behavior within a median of 73 interactions (Agent Drift paper, 2025). By 500 interactions, semantic drift affects roughly 50% of agents. Task success rates drop 42%.
- **Role dilution cascade:** Agents with distinct intended roles gradually converge toward similar behavior, imitating whatever strategies appear successful, destroying the specialization the system was designed around.
- **Echoing:** In agent-to-agent conversations, agents abandon assigned roles and mirror their conversational partners. Studied across 66 agent-agent configurations; echoing rates as high as 70% depending on model and domain. Completely absent in single-agent settings — this is a multi-agent-specific failure.
- **Hidden dominant agent emergence:** Without explicit identity boundaries, some agents become implicit leaders and others defer to them even when wrong, creating unintended hierarchies.
- **Behavioral copy collapse:** Agents with similar models and vague specifications become indistinguishable from each other, collapsing into a single weak strategy.

**What breaks when identity documents are poorly designed**

The MAST Failure Taxonomy (NeurIPS 2025, analysis of 150+ execution traces across five multi-agent systems) found that specification problems are the single largest failure category — 41.77% of all failures traced back to design deficiencies including unclear task specifications and inadequate role definitions. The three main failure categories:

- **FC1 — Specification and System Design Failures (41.77%):** Poor role definitions, unclear task specs, step repetition, conversation history loss, unrecognized termination conditions.
- **FC2 — Inter-Agent Misalignment (36.94%):** Communication breakdowns, task derailment, agents ignoring peer input, reasoning-action mismatches.
- **FC3 — Task Verification and Termination Failures (21.30%):** Premature termination, incomplete verification, incorrect validation.

Specific poorly-designed specification failure modes:

- **Too long / overloaded:** Context window crowded; model ignores content it deems irrelevant to the current task. Research found Claude frequently ignores CLAUDE.md content when it appears non-universal. A soul doc that tries to do everything often does nothing reliably.
- **Too vague:** Agents default to underlying model personality. No distinct behavior. No lane discipline.
- **Contradictory instructions:** When instructions conflict, agent behavior becomes unpredictable. The Arbiter paper found this is common in real deployed systems and detectable with automated tooling.
- **Role overlap between agents:** When two agents have similar or overlapping specifications in a multi-agent system, they duplicate work or leave gaps. The research found this causes both wasted effort and critical task omissions.

**The 14-percent ceiling on specification improvements alone**

Critically: the MAST research found that improved role specifications in a real system (ChatDev) produced only a +14% improvement in success rate — and still left the system "insufficiently reliable for real-world deployment." The conclusion: specification refinements alone cannot fix systemic architectural issues. Good soul docs are necessary but not sufficient. They are one layer in a system that also needs coordination protocols, verification mechanisms, and memory architecture.

---

### 5. Practitioner Perspectives

**What builders actually do**

Across blog posts, GitHub repos, and technical writeups, a consistent pattern emerges in teams that have shipped multi-agent systems:

1. **Separate identity from memory.** Soul/persona doc stays lean and stable. A separate memory layer handles what the agent has learned. This separation is nearly universal in mature implementations.

2. **Version-control soul documents.** Teams treat soul docs like code — committed to git, with change history, reviewed before updates. The Mindra enterprise guide explicitly recommends treating system prompts as product decisions involving legal, brand, and compliance review.

3. **One soul doc per agent.** No shared soul docs across agents with different roles. Each agent gets its own file. OpenClaw uses completely isolated workspace directories per agent, including separate SOUL.md files.

4. **File-based injection over hardcoded strings.** Storing identity in editable Markdown files rather than hardcoded strings in application code allows updates without redeployment. OpenClaw explicitly demonstrates this — edit the file, behavior changes on next session, no code change required.

5. **Worked examples alongside rules.** SoulSpec includes a good-outputs.md and bad-outputs.md in the spec. Anthropic's multi-agent research system embedded research heuristics directly into agent prompts as examples, not just rules. Examples anchor behavior more reliably than abstract rules alone.

6. **Adaptive behavioral anchoring for long-running systems.** For systems that run many sessions or long interactions, the Agent Drift research shows that re-grounding agents against baseline exemplars (good reference outputs) is the most effective single technique for maintaining consistency — 70.4% drift reduction vs. 51.9% for memory consolidation alone.

7. **Hook-based re-injection for context resilience.** In Claude Code, Anthropic built 18+ hook types specifically to handle context compression events. When context gets compacted, identity re-injection hooks fire automatically. Teams building on Claude Code inherit this resilience; teams building elsewhere need to engineer it explicitly.

**Real production patterns from the field**

- **Anthropic's internal multi-agent research system:** Orchestrator-worker pattern; each subagent receives its role definition, output format, tool guidance, and task boundaries explicitly in its specification. Vague instructions caused subagents to duplicate work and investigate the same topics. Explicit scaling rules embedded in prompts prevent ad-hoc agent decisions about scope. Extended thinking in the orchestrator maintains coherent identity for planning.

- **CrewAI (production framework):** Each agent defined with role, goal, and backstory. These are not cosmetic labels — they are functional constraints on how the LLM prioritizes and responds. The role/goal/backstory triad is the de facto minimum viable agent specification for this framework.

- **LangGraph:** Stateful graph execution with persistent state objects. Identity maintained through the state management system rather than pure prompt injection. More infrastructure-heavy but more robust for complex long-running agents.

- **Google ADK:** Stable prefix / variable suffix architecture. Identity guaranteed immutable across the session by architectural enforcement, not just by convention.

- **The OpenClaw architecture (open-source):** Three separated layers — SOUL.md (philosophy/behavior), IDENTITY.md (presentation/name), configuration (capabilities/permissions). Each is independently editable and independently versioned. Identity resolution follows a cascade: global config → per-agent config → workspace files → default. Most specific wins.

---

## Key Takeaways for the Team

**1. The team's current soul document architecture is not only correct — it is ahead of where most practitioners were two years ago.**
The field has converged on exactly what the team is doing: persistent, file-based, version-controlled Markdown identity documents per agent, injected at session start. The AGENTS.md standard, SoulSpec, and OpenClaw all independently arrived at this pattern. The architecture is sound.

**2. The right next question is not "should we have soul docs" but "are ours correctly scoped."**
The most documented failure mode in the field is soul documents that try to do too much. Research puts the working instruction budget for a soul doc at 150–200 instructions (roughly 200–500 words of behavioral rules). Documents that grow beyond this see diminishing returns and active reliability loss, because agents start ignoring content they deem situationally irrelevant. Project 5 should examine whether any team soul docs have grown too long, too procedural, or too vague — and refactor accordingly.

**3. Soul documents and memory are different things and need separate homes.**
The field is unambiguous: the soul doc defines identity (stable, rarely changes); the memory layer stores episodic knowledge (grows, gets curated). Blending the two into a single document creates the exact problems the literature warns against. The team's existing separation of soul files and memory files is the right call. Project 5 should confirm this separation is clean across all agents and codify it as a structural rule.

**4. Multi-agent systems have failure modes that single-agent systems don't — and soul doc quality is a primary lever.**
Echoing (agents mirroring each other), role dilution cascade, and behavioral copy collapse are multi-agent-specific failure modes that don't appear in single-agent testing. The MAST research found 41.77% of multi-agent failures trace to specification problems. Well-differentiated, specific soul documents per agent are the primary mitigation. The clearer each agent's lane, the less likely convergence. Project 5 should ensure every agent soul has genuinely distinct behavioral language — not just different roles, but different specified behaviors, decision rules, and voice.

**5. Contradictory instructions within a soul document are a documented failure mode — not a theoretical one.**
The Arbiter paper (2025) found internal contradictions in real-world agent system prompts and developed automated tooling to detect them. Every soul doc should be internally consistent. When one rule can override another, the hierarchy needs to be explicit. Project 5 review should scan for cases where behavioral rules within a single soul doc could conflict.

---

## C&P Summary

The team's soul document model — one Markdown file per agent, defining identity, role, principles, behavioral rules, and constraints, loaded at every session start — is architecturally correct. The academic and practitioner literature has independently arrived at exactly this pattern through parallel evolution. The 2025 AGENTS.md standard (created by OpenAI, Anthropic, Google, and others, donated to the Linux Foundation) formally codifies the same structure. Multiple open-source frameworks (SoulSpec, OpenClaw, soul.md) have built interoperability standards around it. The team does not need to rethink the architecture from the ground up.

What the literature does flag as high-risk: soul documents that grow too large (agents start ignoring content beyond roughly 150–200 instructions), soul documents that mix identity with episodic memory (the two need separate homes), and soul documents with contradictory internal rules (common in deployed systems, causes unpredictable behavior). The biggest specific failure risk for a multi-agent system like this team's is role dilution — when multiple agents have similar or overlapping specifications, they converge toward the same behavior over time, destroying the specialization that made the multi-agent design valuable in the first place. The research calls this "echoing" and documents rates as high as 70% in agent-to-agent conversations when identity specifications are vague. The mitigation is clear, distinct soul docs per agent with meaningfully different behavioral specifications, not just different job titles. Project 5 should treat soul doc scope, internal consistency, and differentiation across agents as the primary review criteria.

---

## Sources

1. **"Building Persona-Based Agents On Demand: Tailoring Multi-Agent Workflows to User Needs"** — arxiv.org, 2025. [https://arxiv.org/html/2604.27882](https://arxiv.org/html/2604.27882)

2. **"Hermes Agent Five Pillars: Memory, Skills, Soul, Crons, and Self-Improvement"** — MindStudio Blog. [https://www.mindstudio.ai/blog/hermes-agent-five-pillars-memory-skills-soul-crons](https://www.mindstudio.ai/blog/hermes-agent-five-pillars-memory-skills-soul-crons)

3. **"How OpenClaw Implements Agent Identity: Soul, Persona, Multi-Agent"** — MMNTM. [https://www.mmntm.net/articles/openclaw-identity-architecture](https://www.mmntm.net/articles/openclaw-identity-architecture)

4. **"Designing AI Agent Personas: How to Write System Prompts That Make Enterprise Agents Reliable, Safe, and On-Brand"** — Mindra Blog. [https://mindra.co/blog/designing-ai-agent-personas-system-prompts-enterprise](https://mindra.co/blog/designing-ai-agent-personas-system-prompts-enterprise)

5. **"How we built our multi-agent research system"** — Anthropic Engineering Blog. [https://www.anthropic.com/engineering/multi-agent-research-system](https://www.anthropic.com/engineering/multi-agent-research-system)

6. **"Echoing: Identity Failures when LLM Agents Talk to Each Other"** — arxiv.org, 2025. [https://arxiv.org/pdf/2511.09710](https://arxiv.org/pdf/2511.09710)

7. **"Agent Drift: Quantifying Behavioral Degradation in Multi-Agent LLM Systems Over Extended Interactions"** — arxiv.org, 2025. [https://arxiv.org/html/2601.04170v1](https://arxiv.org/html/2601.04170v1)

8. **"Why Do Multi-Agent LLM Systems Fail?"** — arxiv.org, 2025 (MAST taxonomy, NeurIPS). [https://arxiv.org/html/2503.13657v1](https://arxiv.org/html/2503.13657v1)

9. **"The Dark Psychology of Multi-Agent AI: 30 Failure Modes That Can Break Your Entire System"** — Medium. [https://medium.com/@rakesh.sheshadri44/the-dark-psychology-of-multi-agent-ai-30-failure-modes-that-can-break-your-entire-system-023bcdfffe46](https://medium.com/@rakesh.sheshadri44/the-dark-psychology-of-multi-agent-ai-30-failure-modes-that-can-break-your-entire-system-023bcdfffe46)

10. **"SOUL.md — The Persistent Agent Identity Pattern"** — AgentConn Blog. [https://agentconn.com/blog/soul-md-persistent-agent-identity-pattern-guide/](https://agentconn.com/blog/soul-md-persistent-agent-identity-pattern-guide/)

11. **"Agent Memory vs. Context Engineering: What Persists Between Sessions and What Doesn't"** — Augment Code. [https://www.augmentcode.com/guides/agent-memory-vs-context-engineering](https://www.augmentcode.com/guides/agent-memory-vs-context-engineering)

12. **"ID-RAG: Identity Retrieval-Augmented Generation for Long-Horizon Persona Coherence in Generative Agents"** — arxiv.org, 2025. [https://arxiv.org/pdf/2509.25299](https://arxiv.org/pdf/2509.25299)

13. **"Architecting Efficient Context-Aware Multi-Agent Framework for Production"** — Google Developers Blog. [https://developers.googleblog.com/architecting-efficient-context-aware-multi-agent-framework-for-production/](https://developers.googleblog.com/architecting-efficient-context-aware-multi-agent-framework-for-production/)

14. **soul.md (portable specification)** — GitHub, rokoss21. [https://github.com/rokoss21/soul.md](https://github.com/rokoss21/soul.md)

15. **soul.md (Claude Code / OpenClaw builder)** — GitHub, aaronjmars. [https://github.com/aaronjmars/soul.md](https://github.com/aaronjmars/soul.md)

16. **SoulSpec — The Open Standard for AI Agent Personas** — soulspec.org / ClawSouls. [https://soulspec.org/](https://soulspec.org/)

17. **"Improving Role Consistency in Multi-Agent Collaboration via Quantitative Role Clarity"** — arxiv.org, 2025. [https://arxiv.org/pdf/2604.02770](https://arxiv.org/pdf/2604.02770)

18. **"Arbiter: Detecting Interference in LLM Agent System Prompts"** — arxiv.org, 2025. [https://arxiv.org/pdf/2603.08993](https://arxiv.org/pdf/2603.08993)

19. **"Writing a Good CLAUDE.md"** — HumanLayer Blog. [https://www.humanlayer.dev/blog/writing-a-good-claude-md](https://www.humanlayer.dev/blog/writing-a-good-claude-md)

20. **"Claude 4.5 Opus' Soul Document"** — Simon Willison's Weblog, December 2025. [https://simonwillison.net/2025/Dec/2/claude-soul-document/](https://simonwillison.net/2025/Dec/2/claude-soul-document/)

21. **"Agentic Identity: The Missing Layer in Enterprise AI Architecture"** — Arion Research LLC. [https://www.arionresearch.com/blog/agentic-identity-the-missing-layer-in-enterprise-ai-architecture](https://www.arionresearch.com/blog/agentic-identity-the-missing-layer-in-enterprise-ai-architecture)

22. **AGENTS.md Standard** — Agentic AI Foundation (Linux Foundation), co-created by OpenAI, Anthropic, Google, Sourcegraph, Factory, Cursor. December 2025. [https://agentic-ai.readthedocs.io/en/latest/Standards/agents-md/](https://agentic-ai.readthedocs.io/en/latest/Standards/agents-md/)

23. **"A Practical Guide to Building Agents"** — OpenAI. [https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/)

24. **"The 2025 AI Agent Index: Documenting Technical and Safety Features of Deployed Agentic AI Systems"** — arxiv.org, 2025. [https://arxiv.org/html/2602.17753v1](https://arxiv.org/html/2602.17753v1)

25. **"AI Agent Behavioral Science"** — arxiv.org, 2025. [https://arxiv.org/pdf/2506.06366](https://arxiv.org/pdf/2506.06366)

26. **"Formalizing the Safety, Security, and Functional Properties of Agentic AI Systems"** — arxiv.org, 2025. [https://arxiv.org/pdf/2510.14133](https://arxiv.org/pdf/2510.14133)

27. **"Large Language Model based Multi-Agents: A Survey of Progress and Challenges"** — IJCAI 2024. GitHub resource: [https://github.com/taichengguo/LLM_MultiAgents_Survey_Papers](https://github.com/taichengguo/LLM_MultiAgents_Survey_Papers)

28. **Souls Directory — SOUL.md personality files for OpenClaw agents** — GitHub, thedaviddias. [https://github.com/thedaviddias/souls-directory](https://github.com/thedaviddias/souls-directory)

29. **SoulHub — 182 specialized agent soul.md files** — GitHub, yildirim9123. [https://github.com/yildirim9123/soulhub](https://github.com/yildirim9123/soulhub)

30. **"Building AI Agents with Personas, Goals, and Dynamic Memory"** — Medium, Levi Ezra. [https://medium.com/@leviexraspk/building-ai-agents-with-personas-goals-and-dynamic-memory-6253acacdc0a](https://medium.com/@leviexraspk/building-ai-agents-with-personas-goals-and-dynamic-memory-6253acacdc0a)

---

## Additional Findings

**The "soul document" term has a second, distinct meaning at Anthropic**

Anthropic uses "soul document" internally to refer to a ~14,000 token document embedded into Claude's model weights during supervised learning — not a system prompt, not a runtime file, but a training artifact that shapes the model's foundational personality. This is different from what the team calls a soul document. The team's soul documents are runtime files. Anthropic's internal soul document is a training document. Both address the same underlying problem (agent identity and values) but at completely different layers of the stack. Worth noting for conceptual clarity when discussing this architecture with anyone outside the team.

**An emerging standard specifically for enterprise accountability: agentic identity**

Separate from behavioral soul docs, there is a growing concern in enterprise AI about legal and accountability identity for agents — cryptographic provenance, audit trails, authorization chains. The OpenID Foundation acknowledged in their October 2025 whitepaper that traditional IAM (identity and access management) frameworks fail for AI agents. Emerging standards like OIDC-A and SPIFFE are attempting to solve this. This is separate from what the team's soul documents do, but is a real architectural layer that will matter as the team's agents take actions with external consequences. Not an immediate concern for Project 5, but worth flagging for Project 8 or any future project where agents interact with external systems.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

**The "specification engineering" concept**

A 2025 paper introduces "specification engineering" (SE) as a distinct discipline within enterprise multi-agent architecture — creating a machine-readable corpus of corporate policies, quality standards, organizational agreements, and instructions that enables autonomous and coherent operation of multi-agent systems at scale. This is essentially what the team's Master IP is. The paper frames SE as distinct from simple system prompting: it is an organizational layer that defines how all agents operate together, not just how each agent operates individually. This framing could be useful for structuring Project 5 — the Master IP is a specification engineering artifact, and the soul docs are one component within it.

**Context window management is the primary practical constraint on soul doc design**

Multiple sources converge on this: the soul document competes with conversation content for space in the model's context window. In practice, the soul document plus the baseline system prompt can consume a significant fraction of the available window before any conversation begins. The HumanLayer / CLAUDE.md research suggests frontier LLMs can follow 150–200 instructions reliably; Claude Code's built-in system prompt already uses about 50. That leaves a real but limited budget. Teams that are not actively managing their soul doc length tend to discover this constraint the hard way — either through truncation, instruction-ignoring, or degraded performance on long sessions.
