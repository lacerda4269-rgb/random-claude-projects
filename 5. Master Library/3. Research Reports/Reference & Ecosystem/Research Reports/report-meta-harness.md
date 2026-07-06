# Resource Report: Meta-Harness

**URL:** https://github.com/stanford-iris-lab/meta-harness
**Date Researched:** 2026-04-21
**Researched by:** Rose | Security pre-check: Soren (pending) | Report by: Rose
**Already in Master Library?** No

---

## What It Is

Meta-Harness is an open-source research framework from Stanford's IRIS Lab for automated, end-to-end optimization of model harnesses — the code that wraps around a fixed LLM and controls what information the model stores, retrieves, and sees while doing a task. It is the reference implementation for the paper "Meta-Harness: End-to-End Optimization of Model Harnesses" (arXiv 2603.28052, March 2026), authored by Yoonho Lee, Roshen Nair, Qizheng Zhang, Kangwook Lee, Omar Khattab, and Chelsea Finn, representing Stanford, MIT, and KRAFTON.

## What It Does

Meta-Harness runs an outer optimization loop: a proposer agent (defaulting to Claude Code) reads a filesystem containing the source code, execution traces, and scores of every prior harness candidate, then proposes an improved harness. The new harness is evaluated against benchmark tasks, logs are written back to the filesystem, and the loop repeats. Each step can access up to 10M tokens of diagnostic context from prior runs — compared to at most 26K tokens for previous methods.

The repo ships two reference experiments:
1. **Online text classification memory-system search** — discovered the Label-Primed Query harness, achieving 48.6% vs. the previous state-of-the-art ACE at 40.9% (7.7-point gain, using 4x fewer context tokens)
2. **Terminal-Bench 2.0 scaffold evolution** — the discovered harness achieved 76.4% on Terminal-Bench 2.0 using Claude Opus 4.6, ranking #2 on the leaderboard and surpassing the hand-engineered Terminus-KIRA agent (74.7%)

A companion repo (`meta-harness-tbench2-artifact`) contains the Terminal-Bench 2.0 artifact in detail.

## Who Built It

Stanford IRIS Lab (Intelligent Robotic Systems), led by Chelsea Finn (Professor) and Yoonho Lee (PhD researcher). Collaboration with MIT and KRAFTON. Academic research lab releasing a cleaned paper implementation, not a commercial product.

## Activity Level

- **Stars:** 1,000+
- **Forks:** 43 (approx.)
- **License:** MIT
- **Primary Language:** Python (98.9%), Shell (1.1%)
- **Paper published:** March 30, 2026 (arXiv 2603.28052)
- **Activity:** Growing since paper publication — stars nearly doubled since initial report. No versioned releases; paper-coupled publication model.
- **Updated:** 2026-06-08

## Dependencies

Uses `uv` as the package manager with `pyproject.toml`. Core dependencies include `anthropic`, `litellm`, `tenacity`, and `harbor>=0.1.44`. Requires Python >=3.12. Assumes Claude Code as the proposer agent by default; other agents supported through adapter scripts.

## How It Works

1. An initial harness candidate is placed in the search filesystem
2. The proposer agent (Claude Code) reads the filesystem — source code, execution traces, scores of all prior candidates — via standard CLI tools (grep, cat, etc.)
3. The proposer writes a new candidate harness
4. The harness is evaluated on benchmark tasks; scores and traces are logged back to the filesystem
5. The loop repeats, with each iteration able to perform counterfactual diagnosis across all prior runs to identify specific failure modes and propose targeted fixes

The framework is domain-agnostic. An `ONBOARDING.md` guide walks users through applying it to new task types.

## Relevance to This Project

Notable for two reasons: (1) It uses Claude Code as a first-class agent in an automated optimization loop — the same environment this project runs in. (2) The harness concept — the code wrapped around a model that manages context, memory, retrieval, and prompting — is exactly what this project is designing across its agent system. Meta-Harness represents academic-grade thinking on how to improve that wrapper layer automatically. Worth studying as a design reference, not for direct installation.

## Master Library Assessment

- **Proposed Section:** 7 — Reference & Ecosystem
- **Proposed Tier:** 2
- **Rationale:** This is an academic research framework, not a deployable tool for direct use. Its value is as a design reference and evidence of where the field is heading on automated harness engineering. The direct Claude Code dependency makes it particularly relevant context for this project. Section 7 is the right home — ecosystem knowledge, not infrastructure.

## Soren Security Pre-check

- **Verdict:** PENDING — not yet reviewed
- **Notes for Soren:** Low concern profile. MIT license, Python-only, runs locally. Key items: (1) Star count has grown to ~1k — now past fresh-paper-drop territory, consistent with genuine adoption. (2) Dependencies are well-known Python packages (anthropic, litellm, tenacity). (3) No telemetry indicated. (4) Claude Code is the default proposer — no unfamiliar execution environment.

## Recommendation

Enter the library in Section 7 at Tier 2. No install needed or recommended — this is a study reference. Relevant to any future work on improving agent harness design, context management, and automated system optimization. The paper (arXiv 2603.28052) is worth reading alongside the repo.

---

## C&P Summary

Meta-Harness is a research tool from Stanford that automatically improves the "wrapper" code around an AI model — the instructions, memory settings, and context rules that tell the model what to pay attention to and how to organize information while it works. Instead of humans manually tuning that wrapper, Meta-Harness runs a loop where an AI agent (by default, Claude Code) reads the results of previous attempts, figures out what went wrong, and proposes a better version. It ships with two real examples showing measurable performance gains on standard AI benchmarks. For this project, it is most useful as a design reference — it describes, at a technical research level, how to think about and improve the scaffolding built around AI models, which is exactly what this project's agent system is.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---

## Sources

- [GitHub — stanford-iris-lab/meta-harness](https://github.com/stanford-iris-lab/meta-harness)
- [arXiv 2603.28052 — Meta-Harness: End-to-End Optimization of Model Harnesses](https://arxiv.org/abs/2603.28052)
- [arXiv HTML full paper](https://arxiv.org/html/2603.28052v1)
- [Project page — yoonholee.com/meta-harness](https://yoonholee.com/meta-harness/)
- [GitHub — meta-harness-tbench2-artifact](https://github.com/stanford-iris-lab/meta-harness-tbench2-artifact)
- [HuggingFace paper page](https://huggingface.co/papers/2603.28052)
