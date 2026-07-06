# Resource Report: Ruflo (formerly Claude Flow)

**URL:** https://github.com/ruvnet/ruflo
**Date Researched:** 2026-06-01 | **Updated:** 2026-06-08
**Researched by:** Rose | Security pre-check: Soren | Report by: Rose
**Clearance Status:** ⛔ REJECTED — confirmed malware (Issue #1461, open and unresolved). Prompt injection (Issue #1375) was remediated in v3.5.40 and is now closed. Malware finding alone is disqualifying. Do not catalog as active resource. Research record preserved per SOP.
**Soren Update 2026-06-08:** Issue #1375 (prompt injection) confirmed CLOSED — remediated in v3.5.40. Issue #1461 (Trojan:JS/CryoStealz.AE!MTB) remains OPEN and unresolved. Rejection stands on the basis of #1461. Reconsideration gate is unchanged: confirmed malware remediation with independent verification required.

---

## C&P Summary

Ruflo is a multi-agent orchestration platform for Claude Code that promises to deploy coordinated swarms of specialized AI agents. It has 58,471 GitHub stars (updated 2026-06-08) and a polished pitch. It also has confirmed malware (a credential-stealing trojan found in its skill files by Microsoft Defender), confirmed prompt injection via its MCP tool descriptions (hidden instructions that add the repo owner as a contributor to users' repos without consent), a history of shipping obfuscated code that silently deleted files on user machines, and multiple unresolved high-severity vulnerabilities including unauthenticated MCP endpoints and SQL injection. The security remediation the maintainer published in 2026 was partial — the malware report remains open and unresolved. Rejected. The multi-agent swarm concept is genuinely useful; this implementation of it is not safe for the team's library.

---

## What It Is

Ruflo (formerly Claude Flow, rebranded at v3.5.0 in February 2026) is a TypeScript multi-agent orchestration platform for Claude Code. Claims: 100+ specialized agents in coordinated swarms, adaptive memory with HNSW-indexed vector database integration, self-learning swarm intelligence using "neural patterns," RAG integration. 58,471 stars (updated 2026-06-08), MIT license, TypeScript (86.2%), maintained by RuvNet (Reuven Cohen). Last pushed: 2026-06-08 — still actively maintained. Open issues: 636. Latest known: v3.10.31 (May 31, 2026).

---

## Security Findings — Basis for Rejection

| # | Severity | Flag | Status |
|---|----------|------|--------|
| 1 | CRITICAL | Confirmed malware — `Trojan:JS/CryoStealz.AE!MTB` detected by Microsoft Defender in `.agents/skills/` (Issue #1461, March 27, 2026) | Open — unresolved |
| 2 | CRITICAL | Prompt injection via MCP tool descriptions — hidden instructions that add repo owner as contributor to users' repos without consent (Issue #1375) | Unresolved |
| 3 | CRITICAL | Obfuscated destructive preinstall script — versions 3.1.0-alpha.55 through 3.5.2 shipped with obfuscated code that silently deleted npm cache files outside package scope with all errors suppressed | Removed without explanation after external disclosure |
| 4 | HIGH | Persistent artifacts after uninstallation — .swarm files reappear after deletion, background processes persist post-uninstall | Unresolved |
| 5 | HIGH | Unauthenticated MCP endpoints — `/mcp/*` accepts arbitrary POST requests with zero authentication | Unresolved |
| 6 | HIGH | SSRF vulnerabilities — user-configurable URLs have no allowlist or private IP blocking | Unresolved |
| 7 | HIGH | Unresolved SQL injection in memory-initializer.ts | Open since January 2026 |
| 8 | HIGH | Path traversal — sanitizePath bypass; community PR (#1292) rejected without merger | Unresolved |
| 9 | HIGH | Command injection — execSync usage; partially patched only | Partial |
| 10 | MEDIUM | Stub/fake features — multiple advertised features are hardcoded stubs; core capability claims partially unverified | Confirmed by code audit |
| 11 | MEDIUM | Unpinned dependencies — supply chain exposure unaddressed | Unresolved |
| 12 | INFO | No security infrastructure — no SECURITY.md, no vulnerability disclosure policy, no Dependabot | — |

The v3.5.40 "Security Remediation" (Issue #1384) addressed the SQL injection and removed the obfuscated preinstall script. **Soren update 2026-06-08:** Issue #1375 (prompt injection) has been confirmed CLOSED — remediated in v3.5.40. Issue #1461 (Trojan:JS/CryoStealz.AE!MTB, March 27, 2026) remains OPEN and unresolved as of this review date.

---

## Soren Security Pre-check

- **Verdict:** REJECTED
- **Checked (2026-06-08):** Issue #1461 (Trojan:JS/CryoStealz.AE!MTB) status — OPEN, unresolved; Issue #1375 (prompt injection) status — CLOSED, remediated in v3.5.40; full security findings table above; maintainer remediation history (v3.5.40 partial); repo activity (58,471 stars, pushed 2026-06-08 — still active); open issues (636)
- **Notes:**

| # | Severity | Flag | Current Status |
|---|----------|------|----------------|
| 1 | CRITICAL | Trojan:JS/CryoStealz.AE!MTB — Issue #1461 | **OPEN — UNRESOLVED.** Malware detected by Microsoft Defender in `.agents/skills/` directory. No maintainer confirmation of full remediation. This finding alone is disqualifying. |
| 2 | CRITICAL | Prompt injection via MCP tool descriptions — Issue #1375 | **CLOSED — REMEDIATED** in v3.5.40. Hidden instructions that added repo owner as contributor to users' repos — removed. Positive change; does not offset #1461. |
| 3 | CRITICAL | Obfuscated destructive preinstall script | **REMOVED** in v3.5.40. Prior versions silently deleted files outside package scope. Removal confirmed. |
| 4 | HIGH | Multiple remaining HIGH findings (items 4–9 above) | Persistent artifacts, unauthenticated MCP endpoints, SSRF, path traversal — unresolved as of last available review. |

**Rejection basis:** Issue #1461 (confirmed malware, open and unresolved) is the primary disqualifier. Even with #1375 remediated, a credential-stealing trojan in the skill files with no confirmed cleanup by the maintainer is an unacceptable risk. The partial remediation record (v3.5.40 addressed some items, not others) does not provide sufficient confidence.

**Reconsideration gate (updated):** Confirmed closure of Issue #1461 with maintainer acknowledgment of full malware removal, plus independent third-party security audit confirming all remaining HIGH items resolved. Both conditions must be met before reconsideration. Note that #1375 closure is a positive signal — the maintainer is responsive to pressure. That responsiveness does not change the gate.

---

## Master Library Assessment

- **Verdict:** REJECT — do not catalog as active resource
- **Research record:** Preserved per SOP (rejected items retain their research record)
- **Future reconsideration gate:** See Soren Security Pre-check section above — both conditions (Issue #1461 confirmed resolved + independent audit of remaining HIGH findings) must be met

---

## Note to Jay

The multi-agent swarm coordination concept this tool represents is architecturally sound and relevant to future team builds. Ruflo's specific implementation is not. When a clean alternative in this space exists or when Ruflo demonstrates sustained security remediation with third-party verification, it is worth revisiting. As of June 2026, the malware finding alone is disqualifying.

---

---

## Report Version Log

| Version | Date | What Changed |
|---------|------|--------------|


*Report by Rose — Research Specialist | Session 201 | 2026-06-01*
*Updated by Rose | Session 230 | 2026-06-08*
*Prompt Injection Check: REMEDIATED — Issue #1375 (prompt injection via MCP tool descriptions) confirmed CLOSED; addressed in v3.5.40. Malware Issue #1461 (Trojan:JS/CryoStealz.AE!MTB) remains OPEN. Rejection stands.*
*Clearance: REJECTED. Do not deploy. Do not catalog as active ML resource.*
*Soren review: 2026-06-08*

Sources:
- https://github.com/ruvnet/ruflo
- https://github.com/ruvnet/ruflo/issues/1375 (Security Audit — Multiple Critical Concerns)
- https://github.com/ruvnet/ruflo/issues/1461 (Trojan:JS/CryoStealz.AE!MTB confirmation)
- https://github.com/ruvnet/ruflo/issues/1384 (v3.5.40 Security Remediation Overview)
