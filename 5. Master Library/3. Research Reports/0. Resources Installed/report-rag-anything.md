# Resource Report: RAG-Anything

**URL:** https://github.com/HKUDS/RAG-Anything
**Date Researched:** 2026-03-29
**Researched by:** Rose | Security pre-check: Soren | Trivy install scan: Soren (2026-06-12) | Report by: Sophia
**Already in Master Library?** No — gap item from old source list. Note: LightRAG (same org, different tool) is already in Section 8.

---

## What It Is
An all-in-one multimodal RAG (Retrieval-Augmented Generation) framework that processes mixed documents — PDFs, Office files, images, tables, equations, charts — in one unified pipeline. Built on LightRAG with MinerU for extraction.

## What It Does
- Processes: text, images, tables, equations, charts in one pipeline
- Built on LightRAG (already in index) — extends it to multimodal
- MinerU-powered extraction for complex document formats
- 21k stars, v1.3.1 (May 21, 2026), 19 releases, MIT-compatible license, HKUDS organization (updated 2026-06-08)

## How It Differs from LightRAG (already in index)
LightRAG = text-focused RAG with knowledge graph retrieval. RAG-Anything = multimodal extension — adds image, table, equation, and chart processing. If you ever build a knowledge base from mixed documents (PDFs with charts, technical manuals), RAG-Anything handles what LightRAG cannot.

## Relevance to This Project
Phase 3 knowledge base potential. If a searchable knowledge base is ever built from mixed documents (strategy docs, technical manuals, research PDFs), RAG-Anything is the more capable tool over LightRAG for multimodal content.

## Master Library Assessment
- **Proposed Section:** 8 — Alternative Tools & Notable Ecosystem
- **Proposed Tier:** 3
- **Rationale:** Low current priority. Only relevant if building a multimodal knowledge base — not in current scope. High awareness value given the HKUDS org already in the index (LightRAG).

## Soren Security Review

### Pre-check (Research Phase)
- **Verdict:** CLEARED
- **Checked:** 21k stars, v1.3.1 (May 21, 2026), 19 releases, HKUDS organization (same org as already-cleared LightRAG and Nanobot), MIT-compatible license (updated 2026-06-08). No malicious patterns detected.
- **Notes:** Same trusted org as LightRAG. Consistent security posture.

### Trivy Install Scan (2026-06-12 — Session 245)
- **Verdict:** CLEARED
- **Scanned:** raganything==1.3.1, lightrag-hku==1.5.2, mineru==3.3.1, mineru_vl_utils==1.0.5 via `trivy fs requirements.txt` (Trivy v0.71.0, DB updated 2026-06-12)
- **CVEs found:** 0
- **Install notes:**
  - Heavy dependency chain: torch 2.12.0, transformers 4.57.6, gradio 6.8.0, MinerU 3.3.1 installed as part of the package. Gradio (web UI framework) is a transitive dependency — not exposed in normal programmatic use.
  - Three dependency downgrades occurred at install: pandas 3.0.3→2.3.3, huggingface_hub 1.17.0→0.36.2, tokenizers 0.23.1→0.22.2. No CVEs introduced by downgrade; these reflect raganything's pinned dependency requirements. Monitor if other tools relying on huggingface_hub 1.x exhibit unexpected behavior.
  - Import verification passed: `import raganything`, `import lightrag`, `import mineru` all clean.
- **Final verdict: CLEARED — no conditions.**

## Recommendation
Add to Section 8, Tier 3. Phase 3 awareness item. Preferred over LightRAG if multimodal document processing is needed.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---
*Report by Sophia | Session 31 | 2026-03-29*
*Updated by Rose | Session 230 | 2026-06-08*

---

## C&P Summary

RAG-Anything is a multimodal RAG framework from HKUDS (same organization as LightRAG) that processes mixed documents — PDFs, Office files, images, tables, equations, and charts — in a single unified pipeline built on LightRAG with MinerU-powered extraction. 21k stars, v1.3.1 (May 21, 2026), MIT-compatible license (updated 2026-06-08). The key distinction from LightRAG: where LightRAG handles text-focused retrieval, RAG-Anything extends it to handle visual and structured content that LightRAG cannot. Relevant to this team in a future phase if a knowledge base needs to be built from mixed-format documents (strategy docs, technical manuals, research PDFs with charts). Phase 3 awareness item at Tier 3.

---

## Soren Security Pre-check
- **Verdict:** CLEARED
- **Checked:** 21k stars, v1.3.1 (May 21, 2026), 19 releases, HKUDS organization (same org as already-cleared LightRAG and Nanobot), MIT-compatible license (updated 2026-06-08). No malicious patterns detected.
- **Notes:** Same trusted org as LightRAG. Consistent security posture.

---
*Consolidated S264 (dual-Soren merge): this canonical retains BOTH the research-phase **Soren Security Review** + Trivy install scan (2026-06-12, from the category copy, above) AND the install-phase **Soren Security Pre-check** (reattached from the install-folder copy). Category copy superseded; no Soren provenance lost. ML Stage 1.*
