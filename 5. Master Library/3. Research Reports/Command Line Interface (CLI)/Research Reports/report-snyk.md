# Resource Report: Snyk

**Prepared by:** Rose (Researcher)
**Reviewed by:** Soren (Security Manager)
**Tasked by:** Sage (COO)
**Date:** April 15, 2026
**Category:** Soul Folder — Security Tools
**Role in Stack:** Primary (3 categories) — Backbone across Categories 2, 3, and 5
**Status:** Research complete — pending Soren configuration

---

## What It Is

Snyk is a developer security platform from Snyk Ltd. It covers dependency vulnerability scanning, SAST (static application security testing), IaC scanning, container scanning, and — through its acquisition of Invariant Labs' MCP-Scan project in June 2025 — dedicated MCP server security scanning now branded as Snyk Agent Scan. GitHub for the Agent Scan component: `snyk/agent-scan`, 2,000+ stars, v0.4.13, April 2026. The CLI and Agent Scan tool are both Apache 2.0 licensed — free including commercial use.

**Repository Metrics — Snyk CLI (June 2026):** 5,573 stars | 684 forks | v1.1305.1 (latest release) | Last push: 2026-06-08 | Actively maintained. Snyk operates a free tier with credit-based limits (changed January 2026 — verify current limits at snyk.io/plans before configuring). One account, one CLI, three categories covered.

---

## What It Does

**Category 2 — GitHub Repo Scanning:**
- Scans repositories for dependency vulnerabilities via `snyk test`
- SAST (static application security testing) — code-level pattern analysis via Snyk Code
- IaC misconfiguration detection
- Generates fix suggestions and severity ratings
- Integrates with GitHub PRs to block merges containing critical vulnerabilities

**Category 3 — MCP Server Scanning (Snyk Agent Scan):**
- Scans MCP server configurations for prompt injection embedded in tool descriptions
- Detects tool poisoning attacks
- Catches cross-origin escalation vulnerabilities
- Identifies rug pull attack patterns
- Originally built by Invariant Labs (ETH Zurich spin-off) as MCP-Scan; acquired and rebranded by Snyk in June 2025
- Compatible with Claude, Cursor, Windsurf, and other MCP clients
- CLI: `uvx snyk-agent-scan@latest` — requires Python 3.13+ and the `uv` package manager

**Category 5 — npm / Package Scanning:**
- Scans npm `package.json` and `package-lock.json` for dependency CVEs via `snyk test`
- More comprehensive vulnerability database than the GitHub Advisory Database used by npm audit
- License issue detection on npm dependencies
- SBOM-relevant data generation

---

## Installation & Setup (Windows)

**One Snyk account covers all three categories. Configure once.**

1. Create a free Snyk account at snyk.io — verify current free tier credit allocation at snyk.io/plans before proceeding (credit model changed January 2026)
2. Install Snyk CLI: `npm install -g snyk`
3. Authenticate: `snyk auth` (opens browser for OAuth login)
4. Verify: `snyk --version`
5. Run a repo dependency scan: `snyk test` (in a project directory with a lock file)
6. Run a code scan: `snyk code test`

**For Snyk Agent Scan (Category 3 — MCP scanning):**

7. Install `uv` (Python package manager): `pip install uv` or use the Windows installer from astral.sh/uv
8. Ensure Python 3.13+ is installed — this is a hard requirement for Agent Scan
9. Run: `uvx snyk-agent-scan@latest`
10. For JSON output: `uvx snyk-agent-scan@latest --json`

**Note on Python version:** Snyk Agent Scan requires Python 3.13+. LLM Guard (Cat 1 standby) requires Python 3.12 or lower. These two tools must run in separate Python environments if both are installed. Do not attempt to run both from the same environment.

---

## Free Tier Details

- Free Snyk account required (no credit card)
- Free tier includes: 400 open-source scans per billing period, 100 SAST scans per billing period
- Public repositories do not count against scan limits
- Snyk Agent Scan for MCP scanning: no meaningful scan limits at Soren's current volume
- **Credit-based model change:** Snyk moved from test-count to credit-based licensing in January 2026. The limits above reflect current published data but may shift. Verify at snyk.io/plans before configuring.
- Team plan (paid): $25/developer/month — adds unlimited scans, PR integration, organizational dashboards, AI-assisted remediation

---

## Limitations

- Requires a free account — unlike Trivy and Gitleaks, Snyk needs authentication
- Free tier credit limits may shift; the January 2026 pricing model change means these numbers are not as stable as other tools in the stack
- Snyk Agent Scan requires Python 3.13+ — conflicts with LLM Guard's Python 3.12 cap; separate environments required if both are installed
- Behavioral npm package analysis (detecting packages that spawn shells, make unexpected network calls) is not covered by Snyk — Socket CLI handles that layer
- SAST scan volume is limited on the free tier (100 scans/billing period)

---

## Builder Footprint

- **Integration type:** CLI (npm global install) + Python runner for Agent Scan — `npm install -g snyk` for main CLI; `uvx snyk-agent-scan@latest` for MCP scanning; one Snyk account authenticates both
- **Extension points:** `snyk test` (dependency scan), `snyk code test` (SAST), `snyk iac test` (IaC) are independent commands; GitHub PR integration available on paid tier; `snyk monitor` enables continuous monitoring; JSON output for pipeline integration; Agent Scan supports `--json` flag
- **Build complexity signal:** Medium — requires a free Snyk account + CLI install + `snyk auth`; Agent Scan adds Python 3.13+ environment requirement (separate from main CLI); active monitoring of free tier credit balance required (credit model changed Jan 2026)
- **Known conflicts:** Snyk Agent Scan requires Python 3.13+; LLM Guard requires Python 3.12 — these two tools MUST run in separate Python environments if both are installed; do not attempt to share a venv. Free tier credit limits subject to change — verify at snyk.io/plans before configuring. npm install requires Node.js on PATH.

## Role in Soren's Pipeline

Snyk is the stack backbone — three categories from one account and one CLI.

- **Category 2:** `snyk test` and `snyk code test` run as part of the repo scanning sequence after Trivy and Gitleaks — adds SAST and deeper dependency analysis that neither binary-only scanner covers.
- **Category 3:** `uvx snyk-agent-scan@latest` scans MCP server configurations at pre-deployment — the primary tool for catching prompt injection in tool descriptions and tool poisoning before any MCP server enters the pipeline.
- **Category 5:** `snyk test` in any npm project folder gives CVE scanning that outperforms npm audit, at zero additional setup cost since the account is already configured for Cats 2 and 3.

The efficiency case for Snyk is clear: configuring it once covers three separate security requirements. The one ongoing maintenance item is monitoring the free tier credit balance given the January 2026 pricing model change.

---

## Soren Security Pre-check

- **Verdict:** CLEARED — conditions apply
- **Reviewed:** 2026-06-08

Apache 2.0, maintained by Snyk Ltd. — a well-established, venture-backed security company. Snyk CLI: 5,573 stars, v1.1305.1, last push 2026-06-08. Active, widely used in enterprise environments. No suspicious patterns.

**Conditions on clearance:**
1. A free Snyk account is required — creates an authentication dependency that no other tool in the stack has. If the free tier terms tighten significantly, the fallback path is Trivy + Gitleaks + npm audit (Snyk-free coverage for Cats 2 and 5) and an alternative Cat 3 MCP scanner.
2. Snyk Agent Scan requires Python 3.13+ — must run in a separate Python environment from LLM Guard (Python 3.12 cap). Do not share venvs.
3. Free tier credit limits changed January 2026 and may shift again. Verify current allocation at snyk.io/plans before configuring. Monitor credit usage after setup.
4. Snyk CLI transmits project dependency data to Snyk's servers during `snyk test` and `snyk monitor` — this is by design for their CVE database matching. Do not run against repositories or package manifests containing sensitive internal naming conventions you do not want transmitted. `snyk code test` (SAST) does involve code upload to Snyk servers — confirm this is acceptable for each codebase scanned.

**Re-reviewed 2026-06-08 — verdict confirmed.** Stars (5,573), forks (684), CLI v1.1305.1, last push 2026-06-08. No new CVEs, no ownership changes, Apache 2.0 unchanged. Guidance to verify snyk.io/plans before configuring stands.

---

## Soren's Operational Note

Snyk is the one tool in my stack that requires both an account and active monitoring of usage limits. Everything else is fire-and-forget. Snyk needs me to keep an eye on credit consumption, especially once scan volume increases. My setup sequence: configure the Snyk CLI first (before Agent Scan) — get `snyk auth` working and verify the account is active. Then layer in the Agent Scan setup separately with its own Python 3.13+ environment. The Python environment management is the one friction point in this whole stack: Agent Scan on Python 3.13+, LLM Guard (if I ever install it) on Python 3.12, everything else does not care. I need to have that environment structure set before I touch either tool. For Cat 5, once Snyk is running for Cat 2 and Cat 3, running `snyk test` in an npm project directory costs nothing extra — it is the same account, same CLI, zero new configuration.

---

## Sage's COO Note

Snyk's January 2026 credit-based pricing model change is the one moving piece in the stack. Three categories depend on it. Before Soren locks in configuration, a quick verification of current free tier limits at snyk.io/plans is worth five minutes. If the free tier has tightened significantly, the $25/month Team plan is still the single most efficient paid upgrade available — it covers Cats 2, 3, and 5 from one subscription.

---

## C&P Summary

Snyk is the backbone of Soren's security stack, covering three categories from a single account and CLI: Cat 2 (repo SAST and dependency scanning), Cat 3 (MCP server scanning via Snyk Agent Scan), and Cat 5 (npm CVE scanning). One authentication step unlocks all three. Free tier covers current scan volume — credit limits should be verified at snyk.io/plans given the January 2026 pricing model change. The one configuration constraint: Snyk Agent Scan requires Python 3.13+, which conflicts with LLM Guard's Python 3.12 cap; separate virtual environments are required if both are installed.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
