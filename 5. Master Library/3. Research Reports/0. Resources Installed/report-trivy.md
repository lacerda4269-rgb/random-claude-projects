# Resource Report: Trivy

**Prepared by:** Rose (Researcher)
**Reviewed by:** Soren (Security Manager)
**Tasked by:** Sage (COO)
**Date:** April 15, 2026
**Category:** Soul Folder — Security Tools
**Role in Stack:** Primary — Category 2 (GitHub Repo Scanning)
**Status:** ✅ INSTALLED (CLI binary, `C:\ClaudeTools\Soren-security\`) — Soren CLEARED with one dormant condition (GitHub Action; CLI binary unaffected)

---

## What It Is

Trivy is an open-source security scanner from Aqua Security (`aquasecurity/trivy`). It is the most-starred open-source security scanner on GitHub: 36,153 stars (was 32,200+ in April 2026), 513+ contributors. Current version: v0.71.0 (was v0.70.0 in May 2026; was v0.69.3 in March 2026). License: Apache 2.0 — fully free including commercial use. Actively maintained by a large community with Aqua Security as the corporate backer. Ships as a single static binary — no runtime dependencies.

---

## What It Does

- Scans remote GitHub repos by URL for dependency vulnerabilities (CVEs via lock files)
- Detects hardcoded secrets within repos
- Identifies IaC (Infrastructure as Code) misconfigurations
- Scans containers, filesystems, and Kubernetes clusters (beyond repo scanning)
- Reads package lock files to identify npm and other dependency CVEs
- Outputs results in multiple formats including JSON, SARIF, and table
- No account required, no internet-connected service dependency

---

## Installation & Setup (Windows)

1. Go to the Trivy GitHub releases page: `github.com/aquasecurity/trivy/releases`
2. Download `trivy_x.x.x_windows-64bit.zip` (replace x.x.x with current version)
3. Unzip the archive
4. Move `trivy.exe` to `C:\ClaudeTools\Soren-security\` (established tool home for this project)
5. Verify install: `trivy --version`
6. Run a repo scan: `trivy repo https://github.com/org/repo`
7. For JSON output: `trivy repo --format json --output results.json https://github.com/org/repo`

**Critical flag — do NOT use the GitHub Action:** Trivy's official GitHub Action was compromised twice in March 2026. The CLI binary is fully safe. If the GitHub Action is ever used (not currently planned), pin it to a specific commit SHA.

---

## Free Tier Details

Completely free. No usage limits. No account required. No API key required. The CLI binary runs entirely locally — it pulls vulnerability data from Trivy's own database, not a commercial API. There is no paid tier for the CLI.

---

## Limitations

- Secrets detection is a secondary feature — Trivy catches obvious hardcoded secrets but is not as thorough as Gitleaks for full git history secret scanning; run Gitleaks alongside Trivy for comprehensive secrets coverage
- Does not perform SAST (static application security testing) — it finds dependency CVEs and misconfigs, not code logic vulnerabilities; Snyk CLI or Semgrep covers that layer
- Behavioral analysis of packages is not in scope — Socket CLI handles that
- GitHub Action is compromised as of March 2026 — CLI binary only

---

## Builder Footprint

- **Integration type:** CLI (Go static binary) — single binary download; `trivy.exe` on PATH; no install script, no account, no API key; JSON/SARIF/table output modes available
- **Extension points:** Output format (`--format json`, `--format sarif`) configurable per scan; scanners can be selectively enabled/disabled (`--scanners vuln,secret,misconfig`); Soren can add Trivy to CI/CD pipelines via CLI command (not GitHub Action — see Known Conflicts); custom policy files configurable for IaC scanning (CLI flags are documented; CI/CD pipeline integration via CLI command and custom policy file support are inferred from documentation — not explicitly documented as extension points) (Inferred from documentation — not explicitly documented)
- **Build complexity signal:** Lowest possible for a security tool — unzip binary, add to PATH, run; no dependencies, no runtime requirements, no configuration file needed for standard use
- **Known conflicts:** GitHub Action compromise status (March 2026) — as of 2026-05-14 the trivy-action repo shows v0.36.0 released April 22, 2026, suggesting post-compromise maintenance activity, but comprehensive resolution cannot be confirmed from available sources. Continue using CLI binary only until Soren explicitly verifies post-compromise action status. CLI binary is safe and unaffected. Does not conflict with Gitleaks, Snyk, or any other Cat 2 tool — they run in sequence, not in parallel.

## Role in Soren's Pipeline

Trivy is the backbone of Category 2 repo scanning. When Soren receives a GitHub repo URL to clear before any code or tool enters the library, Trivy is the first and broadest scan — it checks dependencies for known CVEs, scans for secrets, and flags IaC misconfigurations in a single command. It runs at pre-deployment clearance, not runtime. Gitleaks runs after Trivy to add dedicated full-history secrets scanning. Snyk CLI adds SAST and deeper dependency analysis on top of that. Trivy sets the floor; the other Cat 2 tools add layers.

---

## Soren Security Pre-check

- **Verdict:** CLEARED — one ongoing condition
- **Re-reviewed:** 2026-06-08 — verdict confirmed.

Apache 2.0, maintained by Aqua Security. 36,153 stars, v0.71.0, last push 2026-06-08. Most-starred open-source security scanner on GitHub. Single static binary — no external service calls, no account, no telemetry. CLI binary is clean and unaffected by the GitHub Action compromise (March 2026).

**Ongoing condition:** The Trivy GitHub Action was compromised in March 2026. As of the May 2026 review, the action repo showed v0.36.0 (April 2026) suggesting post-compromise maintenance, but comprehensive resolution could not be fully confirmed. **This condition carries forward unchanged.** Use CLI binary only until Soren explicitly verifies that the GitHub Action compromise has been fully resolved and the action is safe to use. For this project (no CI/CD integration currently), this condition is dormant — it activates if GitHub Actions integration is ever proposed.

**Re-reviewed 2026-06-08 — verdict confirmed.** Stars updated 35k → 36,153; version updated v0.70.0 → v0.71.0; forks confirmed (459); last push 2026-06-08. No new CVEs against CLI binary. GitHub Action status not re-verified this sweep — ongoing condition carries forward.

---

## Soren's Operational Note

Trivy is my simplest setup of the entire stack — download a binary, add it to PATH, run one command. No account, no API key, no install process beyond unzipping. I should get this configured first in the Cat 2 sequence because it is the fastest win and the broadest coverage in one shot. The output I want for any formal clearance scan is JSON — `trivy repo --format json --output results.json [URL]` — so I have a file-based record of what was scanned and what was found. The one thing I keep in mind every time: Trivy's GitHub Action is off-limits unless I pin it to a specific commit SHA. I am using the CLI binary, not the Action, so this is not an active concern — just something to remember if CI/CD integration ever comes up.

---

## C&P Summary

Trivy is Soren's primary Category 2 tool — a single static binary that scans remote GitHub repo URLs for dependency CVEs, hardcoded secrets, and IaC misconfigurations. It is the most-starred open-source security scanner on GitHub (36,153 stars as of June 2026), maintained by Aqua Security, and requires no account or API key. It runs at pre-deployment clearance and forms the base layer of the Cat 2 stack; Gitleaks adds dedicated secrets scanning on top, and Snyk CLI adds SAST. Current version v0.71.0. The CLI binary is fully safe — the GitHub Action was compromised in March 2026; as of 2026-05-14 the action repo shows continued maintenance (v0.36.0, April 2026) but resolution of the compromise cannot be fully confirmed from available sources. Use CLI binary only until Soren explicitly verifies.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
