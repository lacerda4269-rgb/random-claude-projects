# Feynman Research Report — Topic 2: SOP-to-Automation Conversion Methodologies

**Researched by:** Feynman (Academic Research Specialist)
**Directed by:** Sage (CEO) — Dr. Frankenstein Phase 2, Session 168
**Date:** 2026-05-21
**Output type:** Fact-finding — Design Input (not a deployable resource; Soren review not required)
**Prompt Injection Check:** None detected

---

## Task Summary

This report answers the question: what does the field — academic, practitioner, and AI-specific — know about converting documented step-by-step procedures (SOPs) into automated, event-driven workflows? And specifically: how do you decide which steps become auto-triggering hooks, which become on-demand skills, which become scheduled cron jobs, and which stay as manual documented steps?

The research covered five sub-questions: (1) SOP-to-automation conversion methodology, (2) event-driven architecture fundamentals applied to AI agent systems, (3) visual workflow design tools and frameworks, (4) decision frameworks for hook vs. skill vs. cron classification, and (5) what practitioners building multi-agent AI systems are actually doing.

---

## Findings

### 1. SOP-to-Automation Conversion — What the Field Says

**The core problem the field has been working on:** A standard operating procedure is a document someone reads and follows. An automated workflow is a system that reads the situation and follows itself. Converting between these two forms is not trivial — it requires deciding which steps can be expressed as unambiguous rules, which steps require judgment, and which steps depend on conditions that the system can detect automatically.

**Business Process Automation (BPA) and Robotic Process Automation (RPA)** are the two main practitioner fields that have been solving this problem for decades, well before AI agents entered the picture.

- **BPA** is the broad category: any use of software to execute repeating tasks or processes in a business where manual effort can be replaced. BPA includes workflow management systems, integration platforms, and decision automation.
- **RPA** is more specific: software "bots" that mimic exactly what a human does on a computer interface — clicking, typing, reading screens, filling forms. RPA is popular because it doesn't require changing the underlying systems; it just automates the human's mouse and keyboard actions.

**The key insight from the RPA field on what makes a process step automatable:**

The literature converges on the same criteria across multiple sources. A step is a good automation candidate when it has:

1. **High repetition and volume** — The step happens often enough that automation pays for itself. A step done once a year is not worth automating. A step done dozens of times a day is.
2. **Rule-based logic** — The step follows clear "if X, then Y" logic. It does not require subjective judgment or creativity.
3. **Structured inputs and outputs** — The data flowing in and out is predictable in format. Unstructured text, images requiring interpretation, or highly variable inputs are poor automation candidates.
4. **Stability** — The underlying process does not change frequently. If the step changes every month, any automation built around it will break constantly.
5. **Low exception rate** — The step has few edge cases that require human intervention. High-exception processes cost more to automate than they save.

**Emerging AI-specific work:** A 2025 academic paper (arXiv 2504.00029, authored by Leo Ardon and colleagues) specifically addressed converting documented procedures into structured executable plans using large language models. The approach — referred to as SOPSA (SOP Structured Analysis) — proposes decomposing SOPs into modular sub-plans that can be reasoned about and executed separately. The paper found that sub-SOP decomposition and data-driven refinement of execution semantics are the critical challenges in achieving robust, explainable end-to-end automation. In plain English: breaking a big SOP into smaller, cleaner chunks is the foundation — and the hard part is getting those chunks to have clear enough edges that a system can decide which chunk applies in a given situation.

**Practitioner tools in 2025:** Platforms like Tallyfy and Process Street have taken a middle path — they don't fully automate SOPs, but they turn them into trackable, conditional digital workflows where the software enforces structure even while humans execute the steps. This "structured execution" model is a useful bridge concept: it makes SOPs enforceable before they are automatable.

---

### 2. Event-Driven Architecture (EDA) — Fundamentals and Application to AI Agent Systems

**What event-driven architecture is, in plain English:**

In a traditional system, components talk to each other directly: Component A calls Component B, waits for a response, then continues. This is called request/response (or synchronous communication). It works, but it creates tight coupling — if B is slow, A is stuck; if B changes, A breaks.

Event-driven architecture flips this. Instead of A calling B directly, A publishes an *event* — a notification that something happened ("session started," "file written," "task completed"). Any component that cares about that event picks it up and reacts. A does not wait. A does not need to know who is listening. This is called asynchronous, loosely coupled communication.

**Why this matters for AI agent systems:**

One key source (Confluent, 2025) made the argument explicitly: "Agents are similar to microservices: They're autonomous, decoupled, and capable of handling tasks independently. But agents go further." The claim is that AI agents are *especially* well-suited to event-driven design because they need to react to changing conditions in real time, not just at scheduled intervals.

A second major practitioner source (Atlan, 2025) quantified the performance benefit: event-driven systems can reduce AI agent latency by 70–90% compared to polling approaches (where an agent checks repeatedly "has anything changed?"). That is because polling wastes compute cycles checking when nothing has changed, whereas events only trigger processing when state actually changes.

**The four design patterns for event-driven multi-agent systems** (sourced from Confluent's engineering blog, 2025):

**Pattern 1: Orchestrator-Worker**
A central agent distributes tasks to worker agents through a shared event stream. Workers pull tasks and emit results downstream. This is the pattern this team already uses — Sage as orchestrator, specialized agents as workers. The event-driven version makes it asynchronous: the orchestrator does not wait for each worker to finish before moving on.

**Pattern 2: Hierarchical Agent**
Agents are organized in layers. A top-level agent delegates to mid-level agents, which delegate further. Each level uses the same event-driven techniques. This handles complex problems that need to be decomposed into subproblems. The key benefit over request/response: topology changes (adding or removing agents) do not require rewiring the whole system.

**Pattern 3: Blackboard**
A shared knowledge base (implemented as a shared data stream or topic) where agents post findings and pick up each other's work without talking directly. Multiple agents contribute to the same problem asynchronously. An aggregator synthesizes the results. This pattern is useful when no single agent owns the full answer.

**Pattern 4: Market-Based**
Agents bid or negotiate through a shared channel. A market-maker selects the best response. This handles decentralized resource allocation — useful when multiple agents could handle a task and you want the best one selected dynamically.

**Event-driven vs. scheduled vs. on-demand — the core tradeoff table:**

| Dimension | Event-Driven | Scheduled (Cron) | On-Demand (Invoked) |
|---|---|---|---|
| Trigger | A condition becomes true | A time interval passes | A human or agent decides to start it |
| Latency | Near-zero (fires immediately) | Fixed delay (wait for next window) | Variable (depends on when invoked) |
| Compute waste | Low (fires only when needed) | High (fires even if nothing to do) | None (fires only when called) |
| Predictability | Lower (fires at unpredictable times) | High (fires at known times) | Depends on caller |
| Best for | Time-sensitive state changes | Regular maintenance, batch work | Complex judgment tasks, human-in-the-loop |
| Worst for | Stable batch jobs | Unpredictable data arrival | High-frequency automated steps |

A data pipeline practitioner source (Prefect, 2024) added a practical insight: scheduled pipelines are better when protecting system resources matters — you can schedule heavy jobs at off-peak times. Event-driven pipelines are better when data freshness is the priority. Another source (CloverDX, 2024) identified a specific failure mode of scheduled systems: if data arrives slightly late, the next scheduled window has to process both batches, creating cascading load spikes. Event-driven avoids this by processing as things arrive.

---

### 3. Visual Workflow Design

**Why visual representation matters:**

The research consistently found that visual and textual workflow documentation serve different purposes and audiences. Text SOPs are good for human reading, edge case documentation, and reasoning about intent. Visual representations are better for understanding flow, identifying bottlenecks, communicating across teams, and — critically — serving as executable specifications that automation engines can read directly.

**BPMN — Business Process Model and Notation:**

BPMN is the international standard for visually representing business processes. It was developed by the Object Management Group (OMG) and is now at version 2.0. It matters for this team because it is the academic and enterprise framework that formalized the visual-to-executable bridge.

BPMN has three core element types:
- **Events** — things that happen (start events, end events, intermediate events that fire mid-process). This is the EDA concept in visual form.
- **Activities** — things that are done (tasks, sub-processes). These map directly to SOP steps.
- **Gateways** — decision points (AND, OR, XOR logic). These are the branching conditions in a workflow.

The key BPMN insight for this team: a BPMN diagram is not just a picture — it can be *executed* by a BPMN engine (like Camunda). The model *is* the workflow. When you draw a BPMN diagram, you are simultaneously creating documentation and a runnable process definition. This is exactly the "SOPs becoming executable" vision Jay described.

**Visual workflow platform tiers (2025–2026 landscape):**

The market has separated into three clear tiers:

*Tier 1 — No-code visual automation (Zapier, Make, n8n):*
These are designed for connecting existing services (SaaS apps, APIs) through visual drag-and-drop interfaces. Zapier is the most accessible and has 8,000+ integrations. Make (formerly Integromat) adds branching and parallel processing that Zapier's linear model cannot. n8n is open-source, self-hostable, and has deep AI integration (LangChain nodes). None of these are BPMN-standard — they use their own visual models.

*Tier 2 — Developer-oriented durable execution (Temporal, Inngest, Trigger.dev):*
These are for engineers building workflows that must survive crashes, retries, and long-running processes. Temporal is the most powerful — it treats code as workflows, providing full auditability and replay. Not visual in the traditional sense, but highly reliable.

*Tier 3 — Enterprise BPMN process modeling (Camunda, Signavio, Trisotech):*
Full BPMN 2.0 support, formal process modeling, and direct execution via workflow engines. Used when the process model itself needs to be auditable, shareable, and executable.

**Visual vs. textual: when each helps:**

The research finding is consistent: visual representations excel when you need to understand *flow and dependencies* — which step follows which, what the branches are, where things can fail. Text excels when you need to understand *intent, nuance, and edge cases* — why a step is done a certain way, what to do when the unusual happens. The ideal system has both: a visual representation for structure and flow, a textual SOP for context and rationale.

---

### 4. Hook vs. Skill vs. Cron — Decision Framework

This is the most directly relevant section for Cosmo's work. The field does not have a single published framework specifically for the hook/skill/cron classification problem in the context of AI agent systems — this is a genuinely new design problem that has not been formally codified. However, the research provides enough raw material to construct one.

**What Claude Code's own documentation says (sourced from ofox.ai's complete guide, 2026):**

Claude Code makes a clear distinction between hooks and skills based on two dimensions: *trigger type* and *determinism*.

- **Hooks** fire automatically at system lifecycle events (25 distinct points including SessionStart, SessionEnd, PreToolUse, PostToolUse, UserPromptSubmit, PermissionRequest). They execute deterministic code — they cannot hallucinate, they cannot be misunderstood. They are enforcement mechanisms.
- **Skills** are invoked — either by Claude's reasoning or by a human command. They are reusable prompt templates or procedure documents. They are for knowledge transfer and repeatable workflows, not enforcement.

The guide's own decision rule: "Create a hook when you need deterministic enforcement. Create a skill when you keep pasting the same playbook into chat."

**Cron jobs** (time-based triggers) are separate from both — they fire on a schedule, regardless of system state. Claude Code supports cron-based automation through its scheduling capability, separate from the hook lifecycle.

**Synthesized decision framework** (assembled from RPA literature + EDA literature + Claude Code documentation):

Ask these questions about each SOP step:

**Question 1: Does this step need to fire automatically, or is it fine to invoke manually?**
- Must fire automatically (no human decides to start it) → candidate for hook or cron
- Fine to invoke manually → candidate for skill or documented step

**Question 2: If automatic — what triggers it?**
- A system event (session starts, file is written, tool is used, task completes) → **Hook**
- A point in time (every day at midnight, every week on Monday, every hour) → **Cron job**
- A real-world condition becoming true (new data arrives, an error is detected, a threshold is crossed) → **Event-driven trigger** (advanced EDA)

**Question 3: Does this step require judgment or can it be expressed as deterministic logic?**
- Deterministic (clear rules, no exceptions, same output for same input) → automatable (hook or cron)
- Requires reasoning, context, or judgment → skill or documented step (let Claude reason through it)

**Question 4: How often does this step run, and does frequency matter?**
- Runs every session/every tool use/every commit — high frequency, must be fast → hook (lowest overhead)
- Runs daily/weekly — predictable schedule → cron
- Runs when conditions are right — irregular, time-sensitive → event trigger

**Question 5: What happens if this step is skipped?**
- System breaks, security is compromised, data is lost → enforce it as a hook (deterministic, cannot be forgotten)
- Work is duplicated or quality suffers → skill (make it easy to invoke, but allow judgment about when)
- Nice to have, not critical → documented step (keep it as text, do not automate yet)

**The field's core insight applied to this team:** The RPA literature's criteria map cleanly onto the hook/skill/cron decision. Steps that are high-frequency, rule-based, stable, and have zero tolerance for being skipped → hooks. Steps that are repeatable and benefit from standardization but require invocation → skills. Steps that are batch-oriented, periodic, and resource-intensive → cron. Steps that are complex, judgment-heavy, or low-frequency → documented steps.

---

### 5. Practitioner Perspectives — Multi-Agent AI Systems

**What AI agent framework teams are doing in 2025–2026:**

The leading multi-agent frameworks have all independently arrived at event-driven architecture as the right model for coordination. The convergence is notable:

- **CrewAI** added "Flows" in 2025 — an event-driven pipeline mode for production workloads, sitting alongside its original role-based task assignment model. Flows allow one agent's completion to automatically trigger the next stage.
- **AutoGen (AG2)** — Microsoft's rewrite of AutoGen — rearchitected around an event-driven, async-first core. The v0.4 rewrite explicitly moved away from synchronous request/response toward event streaming between agents.
- **LangGraph** models agent workflows as directed cyclic graphs — each node is an agent or step, each edge is a state transition triggered by events or conditions. The graph structure makes the workflow visualizable and executable simultaneously. This is the closest existing framework to the "SOPs as executable graphs" vision.

**What these teams are NOT doing (and why it matters):**

None of the major frameworks have a formalized SOP-to-automation conversion pipeline. The conversion from human-readable procedure to executable workflow is still done manually by engineers who understand both the procedure and the framework. This is the gap this team is trying to close with Cosmo's pipeline — and it is a genuinely novel contribution. The academic paper (arXiv 2504.00029) is one of the first formal attempts at this problem using LLMs.

**Claude Code's specific model (hooks + skills + cron)** is an implementation of a hybrid trigger architecture — deterministic hooks for enforcement, invokable skills for procedure knowledge, cron for scheduled tasks. The hook/skill distinction maps precisely onto the EDA literature's event-driven vs. on-demand trigger distinction. Claude Code has, in effect, implemented a three-tier trigger architecture that the broader EDA field describes at a conceptual level.

**One practitioner observation worth noting (MindStudio, 2025):** The concept of Claude as an "agentic operating system" — where skills chain into larger workflows — is already being described in practitioner communities. The Skills standard launched by Anthropic in late 2025 is now adopted by 30+ tools including Cursor, VS Code Copilot, and Gemini CLI. This means the skill architecture this team uses is becoming a genuine cross-platform standard, not just a Claude-specific feature.

---

## Key Takeaways for the Team

- **The hook/skill/cron decision is a trigger-type + determinism problem.** Ask two questions about every SOP step: (1) what starts this — an event, a schedule, or a human? and (2) can it be expressed as deterministic logic, or does it require reasoning? Event + deterministic → hook. Schedule + deterministic → cron. Human-invoked + reasoning → skill. Complex/judgment → documented step. This is the decision framework Cosmo needs.

- **LangGraph is the closest existing framework to Jay's "SOPs as executable graphs" vision.** It models workflows as directed graphs where nodes are agents/steps and edges are event-triggered transitions. It is both a visual and executable representation simultaneously — the thing Jay described when he said "automatable and visualizable." This is worth Cosmo studying before designing the conversion pipeline.

- **BPMN is the academic/enterprise standard for the visual side of this problem.** It has a formal standard (BPMN 2.0), proven tooling (Camunda), and the key property that the visual model *is* the executable — not a picture of a process, but the process itself. Even if the team does not use BPMN tooling directly, the conceptual model (events → activities → gateways) maps cleanly onto hooks → skills → conditional logic.

- **The SOP-to-automation conversion pipeline does not yet exist as a formal discipline.** The team is ahead of the field here. RPA has selection criteria for which steps to automate. EDA has patterns for how agents communicate. But there is no published methodology for "take an SOP document and convert it systematically into hooks, skills, and cron jobs." The arXiv 2504.00029 paper is the closest academic attempt. Cosmo's pipeline, if well-documented, would be a genuinely novel contribution.

- **Scheduled (cron) vs. event-driven is not just a performance question — it is a correctness question.** The practitioner literature (Prefect, CloverDX) shows that scheduled triggers fail in predictable ways when timing assumptions break. If a step must fire *when a condition becomes true* rather than *at a fixed time*, forcing it into a cron job creates silent failures. Design for the actual trigger type, not the convenient one.

---

## C&P Summary

The research found that the problem this team is solving — converting documented SOPs into automatically executable workflows — is a real and recognized challenge across multiple fields, but no field has fully solved it for AI agent systems yet. Business Process Automation (BPA) and Robotic Process Automation (RPA) have been working on this for decades and have well-established criteria for what makes a process step automatable: it needs to be repetitive, rule-based, stable, and low on exceptions. The academic AI field produced a 2025 paper specifically about using LLMs to convert SOPs into structured executable plans, and found that breaking SOPs into clean sub-components is the hardest part. On the event-driven side, the research is clear: event-driven architecture (where a step fires automatically when a condition becomes true) dramatically outperforms both scheduled and on-demand approaches for time-sensitive, state-change-triggered work — and all the major AI agent frameworks (LangGraph, CrewAI Flows, AutoGen AG2) have independently arrived at event-driven design as their core model. For the hook vs. skill vs. cron decision specifically, Claude Code's own documentation provides the clearest framework: hooks are for deterministic enforcement at system lifecycle events, skills are for invokable procedures that benefit from Claude's reasoning, and cron is for time-based batch work. The visual side of the problem is well-served by BPMN (the international standard) and platforms like LangGraph (which makes workflows simultaneously visual and executable). The bottom line for Cosmo's pipeline: the conversion decision comes down to two questions per SOP step — what triggers this step (event/time/human), and can it be expressed as deterministic logic? The combination of those two answers tells you whether a step becomes a hook, a cron, a skill, or stays as a documented procedure.

---

## Sources

1. Confluent Engineering Blog — "Four Design Patterns for Event-Driven, Multi-Agent Systems" (2025): https://www.confluent.io/blog/event-driven-multi-agent-systems/
2. Confluent Engineering Blog — "The Future of AI Agents Is Event-Driven" (2025): https://www.confluent.io/blog/the-future-of-ai-agents-is-event-driven/
3. Confluent Resource — "A Guide to Event-Driven Design for Agents and Multi-Agent Systems" (ebook, 2025): https://www.confluent.io/resources/ebook/guide-to-event-driven-agents/
4. Atlan — "Event-Driven Architecture for AI Agents: Patterns and Benefits" (2025): https://atlan.com/know/event-driven-architecture-for-ai-agents/
5. arXiv 2504.00029 — "Generating Structured Plan Representation of Procedures with LLMs" (Leo Ardon et al., 2025): https://arxiv.org/pdf/2504.00029
6. arXiv 2007.10900 — "A framework to evaluate the viability of robotic process automation for business process activities" (2020): https://arxiv.org/pdf/2007.10900
7. ResearchGate — "Developing standard criteria for robotic process automation candidate process selection" (2024): https://www.researchgate.net/publication/386304744_Developing_standard_criteria_for_robotic_process_automation_candidate_process_selection
8. UiPath Blog — "5 Factors in Choosing Which Processes to Automate" (2024): https://www.uipath.com/blog/rpa/5-factors-in-choosing-which-processes-to-automate
9. SmartUI Group — "7 Key Criteria for Robotic Process Automation (RPA)": https://www.smartuigroup.com.au/7-criteria-to-identifying-processes-fit-for-rpa/
10. Blueprint Systems — "How to Select the Right Processes for RPA: Define a Criteria": https://www.blueprintsys.com/blog/rpa/select-right-processes-for-rpa
11. ofox.ai — "Claude Code: Hooks, Subagents, and Skills — Complete Guide" (2026): https://ofox.ai/blog/claude-code-hooks-subagents-skills-complete-guide-2026/
12. MindStudio — "What Is Claude's Agentic Operating System? How Skills Chain Into Business Workflows" (2025): https://www.mindstudio.ai/blog/claude-agentic-operating-system-skills-workflows
13. MindStudio — "Beyond One-Shot Prompts: 5 Claude Code Workflow Patterns Explained" (2025): https://www.mindstudio.ai/blog/claude-code-agentic-workflow-patterns
14. Prefect Blog — "Event-Driven Versus Scheduled Data Pipelines" (2024): https://www.prefect.io/blog/event-driven-versus-scheduled-data-pipelines
15. CloverDX Blog — "Event-Driven Design vs. Timetable Scheduling: What's the Difference?" (2024): https://www.cloverdx.com/blog/event-driven-design-vs-timetable-scheduling
16. KISSflow — "BPMN — An Ultimate Guide to Business Process Model and Notation" (2026): https://kissflow.com/workflow/bpm/what-is-bpmn/
17. Process Designer — "What is BPMN? Complete Guide to BPMN 2.0" (2026): https://www.processdesigner.com/resources/what-is-bpmn
18. Trisotech — "Business Process Model and Notation (BPMN) Standard": https://www.trisotech.com/bpmn/
19. Sean Falconer (Medium) — "The Future of AI Agents is Event-Driven" (2025): https://seanfalconer.medium.com/the-future-of-ai-agents-is-event-driven-9e25124060d6
20. Sean Falconer (Medium) — "AI Agents Must Act, Not Wait: A Case for Event-Driven Multi-Agent Design" (2025): https://seanfalconer.medium.com/ai-agents-must-act-not-wait-a-case-for-event-driven-multi-agent-design-d8007b50081f
21. DZone — "Designing Scalable Multi-Agent AI Systems" (2025): https://dzone.com/articles/multi-agent-ai-ddd-event-storming
22. InfoWorld — "A distributed state of mind: Event-driven multi-agent systems" (2025): https://www.infoworld.com/article/3808083/a-distributed-state-of-mind-event-driven-multi-agent-systems.html
23. OpenAgents Blog — "CrewAI vs LangGraph vs AutoGen vs OpenAgents (2026)": https://openagents.org/blog/posts/2026-02-23-open-source-ai-agent-frameworks-compared
24. gurusup — "Best Multi-Agent Frameworks in 2026: LangGraph, CrewAI...": https://gurusup.com/blog/best-multi-agent-frameworks-2026
25. Flowmondo — "n8n vs Zapier vs Make: Which Automation Tool Is Right for You?": https://www.flowmondo.com/article/n8n-vs-zapier-vs-make
26. Automation Atlas — "Temporal vs n8n (2026)": https://automationatlas.io/guides/temporal-vs-n8n-2026-comparison/
27. Zeepalm — "Event-Driven Architecture: Complete Guide [2024]": https://www.zeepalm.com/blog/event-driven-architecture-complete-guide-2024
28. Beta Systems — "Maximizing Efficiency with Event-Driven Automation": https://www.betasystems.com/resources/blog/maximizing-efficiency-with-event-driven-automation
29. Flowster — "5 Ways SOPs, Workflows, and Automation Can Supercharge Your Small Business Growth": https://flowster.app/small-business-growth-sops-workflows-and-automation/
30. Revver Docs — "The Complete Guide to SOP Management in Manufacturing: How to Digitize and Automate Your Standard Operating Procedures": https://www.revverdocs.com/the-complete-guide-to-sop-management-in-manufacturing-how-to-digitize-and-automate-your-standard-operating-procedures/

---

## Additional Findings

**The Agent Skills standard is going cross-platform.** Anthropic launched a formal Agent Skills open standard in late 2025, and it has been adopted by Cursor, VS Code Copilot, Gemini CLI, OpenAI Codex, and JetBrains Junie. This means skills built for Claude Code today may be usable by other AI coding environments tomorrow. Worth knowing when designing the skill architecture — interoperability is on the table.

**Domain-Driven Design (DDD) and Event Storming are emerging as the analysis methodology for EDA design in AI systems.** Event Storming is a workshop technique where you map out all the events in a system before designing the architecture. DZone (2025) explicitly named Event Storming + DDD as the right design approach for multi-agent AI systems built on event-driven architecture. For this team: when designing Cosmo's conversion pipeline, an Event Storming exercise (mapping every event that fires across a session) would be a natural precursor to classifying steps as hook, skill, or cron candidates. This is not something this team is doing yet — and it might be worth a follow-up conversation with Sage.

**The "structured execution" bridge concept.** Platforms like Tallyfy and Process Street occupy an interesting middle ground: they do not fully automate SOPs, but they make them *enforceable as digital workflows* that humans execute with system tracking. This is useful framing for any SOP steps that are not automatable (too much judgment, too many exceptions) but still need to be consistently followed. "Digitize before you automate" is a practitioner principle worth noting.

**BPMN has an execution gap that AI agents may close.** BPMN 2.0 is formally executable — you can run a BPMN model in a BPMN engine. But the gap between human-written SOPs and valid BPMN models has historically required trained process modelers to bridge. The 2025 arXiv paper suggests LLMs can close this gap — generating structured, machine-readable plan representations from natural language procedure text. If that research matures, it means an SOP written in plain English could be automatically converted into an executable BPMN or LangGraph workflow. That would be the full realization of Jay's "SOPs becoming executable" vision.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
