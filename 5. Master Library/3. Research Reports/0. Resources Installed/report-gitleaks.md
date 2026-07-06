# Resource Report: Gitleaks

**Prepared by:** Rose (Researcher)
**Reviewed by:** Soren (Security Manager)
**Tasked by:** Sage (COO)
**Date:** April 15, 2026
**Category:** Soul Folder — Security Tools
**Role in Stack:** Primary (secrets layer) — Category 2 (GitHub Repo Scanning)
**Status:** Research complete — pending Soren configuration

---

## What It Is

Gitleaks is an open-source secrets scanner from the `gitleaks/gitleaks` GitHub project. It is purpose-built for detecting hardcoded secrets in git repositories — API keys, tokens, passwords, and similar sensitive material anywhere in the git history. GitHub: 27,593 stars (as of 2026-06-08). Current version: v8.30.1, released March 21, 2026. License: MIT — fully free including commercial use. Ships as a single binary with no runtime dependencies. The creator has shifted primary focus to TruffleHog, but Gitleaks continues to receive regular releases and remains actively maintained.

---

## What It Does

- Scans git repositories for hardcoded secrets across the full commit history
- Detects API keys, tokens, passwords, and other sensitive credential types
- Supports pre-commit hooks for real-time secret detection before commits land
- Outputs findings in SARIF format for CI integration
- Fast, pattern-based detection — single binary, no external service calls
- Windows binary available, no additional dependencies

---

## Installation & Setup (Windows)

1. Go to the Gitleaks GitHub releases page: `github.com/gitleaks/gitleaks/releases`
2. Download the Windows binary for the current release (v8.30.1 as of this report)
3. Move `gitleaks.exe` to a folder on your system PATH
4. Verify install: `gitleaks version`
5. Scan a local repo: `gitleaks detect --source [path-to-repo]`
6. Scan with verbose output: `gitleaks detect --source [path] --verbose`
7. For JSON/SARIF report output: `gitleaks detect --source [path] --report-format sarif --report-path gitleaks-report.sarif`
8. Pre-commit hook setup: run `gitleaks protect --staged` before commits to catch secrets before they land in history

---

## Free Tier Details

Completely free. No usage limits. No account required. No API key required. Runs entirely locally. There is no paid tier.

---

## Limitations

- Pattern-based detection — will not catch secrets that do not match its known patterns; novel or obfuscated secrets may be missed
- Does not verify whether detected secrets are still live or valid; TruffleHog does that (but TruffleHog is optional in this stack for that specific reason — it adds complexity and AGPL license concerns)
- Secrets scanning only — no dependency CVE scanning, no IaC misconfig detection, no SAST; Trivy covers those layers
- Full history scans on large repositories with long commit histories can be slow

---

## Builder Footprint

- **Integration type:** CLI (Go static binary) — single binary download; `gitleaks.exe` on PATH; no account, no API key; SARIF/JSON/table output modes; pre-commit hook mode available
- **Extension points:** Custom rule files (`.gitleaks.toml`) allow adding or overriding detection patterns beyond the built-in set; `--output` and `--report-format` flags support pipeline integration; `gitleaks protect --staged` enables pre-commit integration for team repos
- **Build complexity signal:** Lowest — download binary, add to PATH, run; same effort level as Trivy per Soren's operational note; one-time pre-commit hook setup is optional but recommended for team repos
- **Known conflicts:** None. Works alongside Trivy (Cat 2 complement — different coverage layers: Trivy = current repo state; Gitleaks = full git history). No Python environment or version conflicts. Creator has shifted primary focus to TruffleHog — monitor for extended dormancy, though active releases continue.

## Role in Soren's Pipeline

Gitleaks is the dedicated secrets layer in Category 2. Trivy catches secrets as a secondary capability, but Gitleaks is the purpose-built tool for full git history secret scanning — it goes deeper and is more thorough specifically on that signal. The standard Cat 2 scan sequence is Trivy first (broad CVE/secret/IaC sweep), then Gitleaks (dedicated secrets deep-scan across full history). Any secret finding from either tool warrants investigation before the resource is cleared. Runs at pre-deployment clearance only.

---

## Soren's Operational Note

**Re-reviewed 2026-06-08 — verdict confirmed. CLEARED (core infrastructure).** Rose's freshness sweep: still at v8.30.1 (March 21, 2026 — no new release in ~2.5 months), stars 27,593, last push 2026-06-04. Actively maintained. No new CVEs or security disclosures. No changes to operational standing. Core Cat 2 secrets scanner; no action required.

Gitleaks is the second binary I install after Trivy — same process, same effort level. The thing that makes Gitleaks valuable on top of Trivy is the full history scan. Trivy scans what is currently in the repo. Gitleaks scans every commit ever made — so if someone committed a key three months ago, deleted it, and pushed a clean version, Trivy misses it and Gitleaks catches it. That is the specific gap it fills. My standard run: `gitleaks detect --source [repo-path] --verbose` on any local clone before I clear it. The pre-commit hook is worth setting up on the team's own repos once we are past this initial stack setup phase — it prevents the problem rather than just catching it after the fact.

---

## C&P Summary

Gitleaks is Soren's dedicated secrets scanner for Category 2 — a single binary that scans the full git commit history of a repository for hardcoded API keys, tokens, and passwords. It fills the gap Trivy leaves: Trivy scans the current repo state, Gitleaks scans every commit ever made. MIT licensed, no account needed, Windows binary available. It runs immediately after Trivy in the Cat 2 pre-deployment scan sequence. TruffleHog (which verifies whether found secrets are still live) is intentionally excluded from the primary stack due to added complexity and AGPL license concerns — Gitleaks handles the detection layer.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

---
*Consolidated to single canonical, Session 264 — the fresher category copy was promoted to `0. Resources Installed`; the stale install-folder copy (older stats, missing the freshness sweep / version log) was superseded. No unique content lost. ML Stage 1.*
