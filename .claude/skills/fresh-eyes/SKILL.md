---
name: fresh-eyes
description: "Zero-prior-context review. Use when you need a truly unanchored second opinion on a target (a file, a folder, or a whole folder tree) — a review by freshly spawned agents who have never seen any prior analysis, to-do list, team notes, or conversation about it. Spawns fresh sub-agents, one per independent scope, each rating its scope 0-10 against a supplied rubric, then consolidates into one owned report. Use it to pressure-test a structure, audit a template for completeness, or get an honest \"how bad is it\" read free of anchoring. Distinct from a role-diverse review — this is pure freshness, no expertise lens."
---

# fresh-eyes — Zero-Prior-Context Review

Get an unanchored read on a target. The invoking orchestrator spawns fresh sub-agents that
have seen nothing — no prior findings, no to-do lists, no team notes, no conversation — and
each one rates its scope 0-10 against a rubric you supply. The orchestrator then consolidates
their independent reads into one rated report and owns the result.

The value of this skill is the *absence* of context. A reviewer who has already seen the
analysis, the plan, or the discussion is anchored to it and will tend to confirm it. A fresh
reviewer cannot. Every safeguard below exists to protect that freshness. If the anti-anchoring
rule is broken, the skill produces nothing of value — it just echoes what was already thought.

## When to use

- Pressure-testing a structure, template, or design for completeness or gaps.
- Auditing a folder tree for a specific quality (e.g. "is this a truly universal, blank,
  reusable template?").
- Getting an honest severity read ("how much needs to change?") without anchoring it to the
  existing plan.
- Any time a second opinion is only useful if it is genuinely independent of the first.

## When NOT to use

- When you want a role-specific or expertise-driven review (use the role-diverse reviewer
  instead — that is a different, complementary tool).
- When the reviewer *should* build on prior analysis. This skill deliberately throws prior
  analysis away; if continuity is the goal, this is the wrong tool.

## Inputs

The invocation supplies three things. If any is missing, ask for it before spawning anything.

1. **Target** — the path(s) and scope to review. A single file, a folder, or a folder tree.
2. **Review question / lens** — the exact question each fresh agent answers (e.g. "What is
   needed to make this a truly universal, blank, reusable template?"). One clear question.
3. **Severity rubric (0-10)** — the scale each agent rates against. Default rubric, used unless
   the invocation overrides it:
   - **0** — nothing needs changing; the target fully meets the question's standard.
   - **1-3** — minor changes; small gaps or polish only.
   - **4-6** — moderate changes; real gaps that need work but the foundation holds.
   - **7-9** — major changes; significant rework required.
   - **10** — massive changes; the target does not meet the standard and needs a near-rebuild.

## Procedure (the orchestrator executes this)

### Step 1 — Confirm the three inputs

Confirm target, question, and rubric are all present and unambiguous. Missing or vague input
gets one targeted clarifying question — never a guess. Do not proceed on a shaky brief.

### Step 2 — Break the target into independent scopes

- **Single file or single folder:** one scope, one fresh agent.
- **Folder tree:** split into independent scopes — by default, one scope per top-level
  folder/level. Each scope is reviewed by its own fresh agent. Pick a split where the scopes
  are genuinely independent so the agents do not need to coordinate.
- For tree reviews, each agent is instructed to **read EVERY README (and equivalent index/
  overview file) at its level** so its read is complete for that scope.
- Keep the number of scopes sensible. If a tree is large, scope by top level and let each agent
  recurse within its own branch. Do not spawn one agent per file.

### Step 3 — Spawn fresh agents IN PARALLEL (anti-anchoring is enforced here)

Spawn one `Agent` (subagent_type `general-purpose`) per scope. **Make all the Agent calls in a
single message** so they run concurrently.

**CRITICAL ANTI-ANCHORING RULE — this is the whole point of the skill:**

Each fresh agent receives ONLY:
- the raw target path(s) for its scope,
- the review question / lens,
- the 0-10 rubric.

Each fresh agent must NEVER receive, and you must NEVER include in its prompt:
- prior findings, conclusions, or any earlier review of this target,
- to-do lists, pending-item lists, or backlogs,
- team notes, session notes, conversation history, or what anyone else thinks,
- your own opinion, hint, or expected answer,
- the ratings or findings of any other fresh agent.

If you are tempted to "give the agent context so it does a better job" — stop. That context is
exactly what this skill exists to exclude. The agent reads the raw target cold. That is the
feature, not a limitation.

Pass each fresh agent this prompt template, substituting `{SCOPE_PATHS}`, `{REVIEW_QUESTION}`,
and `{RUBRIC}` only:

> You are a fresh reviewer with zero prior context. You have not seen any prior analysis,
> to-do list, notes, or conversation about this target, and you must not ask for any. Review
> based ONLY on what you read at the path(s) below.
>
> **Target to review:** `{SCOPE_PATHS}`
> **Review question:** {REVIEW_QUESTION}
> **Severity rubric (0-10):** {RUBRIC}
>
> Instructions:
> 1. Read everything in scope. If the target is a folder or tree, read EVERY README and every
>    index/overview file at every level within your scope, then read enough of the actual
>    contents to answer the question — do not rate from README claims alone.
> 2. Answer the review question for this scope.
> 3. Give ONE severity rating, 0-10, using the rubric above.
> 4. Support every finding with file-cited evidence — name the file (absolute path) and what in
>    it drove the finding. No unsupported assertions.
>
> Return your findings as raw structured data in exactly this shape. Your final message IS the
> returned data — it is read by an orchestrator, not by a person. Do not write a human-facing
> note, a greeting, or a sign-off. Do not write any files.
>
> ```
> SCOPE: {SCOPE_PATHS}
> RATING: <0-10>
> HEADLINE: <one line — the single most important takeaway for this scope>
> FINDINGS:
>   - <finding> | evidence: <absolute/path/to/file> — <what in it>
>   - <finding> | evidence: <absolute/path/to/file> — <what in it>
> WHAT-WOULD-LOWER-THE-RATING: <the concrete changes that would move this scope toward 0>
> ```

### Step 4 — Collect the returns

Wait for all fresh agents. Each returns its structured block. If an agent returns something
malformed or empty, note it — do not invent a rating to fill the gap.

### Step 5 — Synthesize ONE owned report

The orchestrator consolidates. Do not pass the fresh agents' raw returns up as the deliverable —
own the synthesis. Produce:

1. **Per-scope rating table:**

   | Scope | Rating (0-10) | Headline |
   |-------|---------------|----------|
   | ...   | ...           | ...      |

2. **Overall rating** — your judgment across scopes (state how you derived it: highest-severity,
   average, or weighted — say which and why; do not just average blindly if one scope is a 10).

3. **Consolidated findings** — grouped, deduplicated, each with its file-cited evidence carried
   through from the fresh agents.

4. **What would lower the rating** — the concrete change list, ordered by severity.

The orchestrator owns this report. The fresh agents produced inputs; the synthesis and the call
are the orchestrator's.

## Notes

- This skill applies to NO standing or named agent. It always spawns freshly created, context-
  free agents. There is no "assign this to <agent>" — freshness is the requirement.
- Parallel dispatch matters: independent scopes reviewed at the same time are both faster and
  more independent (no agent sees another's output).
- If the invocation overrides the default rubric, use the supplied one verbatim and pass that to
  the agents — the rubric is an input, not a fixed scale.
