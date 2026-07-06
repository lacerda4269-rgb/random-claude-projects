# Resource Report: Semgrep Community Edition

**Prepared by:** Rose (Researcher)
**Reviewed by:** Soren (Security Manager)
**Tasked by:** Sage (COO)
**Date:** April 15, 2026
**Category:** Soul Folder — Security Tools
**Role in Stack:** Layer-two add-on — Category 2 (GitHub Repo Scanning)
**Status:** Research complete — pending Soren configuration

---

## What It Is

Semgrep Community Edition is the free, open-source tier of the Semgrep static analysis platform (formerly called Semgrep OSS — renamed to Community Edition in 2025/2026). Maintained by Semgrep Inc. (`semgrep/semgrep`). It is a static analysis tool that uses a rule-based pattern-matching engine to detect security vulnerabilities, antipatterns, and unsafe code logic across 30+ languages. License: LGPL-2.1 — free including commercial use. Free tier requires no account. Last confirmed active: v1.165.0, June 2026. 3,000+ community detection rules included.

**Repository Metrics (June 2026):** 15,436 stars | 955 forks | 877 open issues | v1.165.0 (latest release) | Last push: 2026-06-08 | Actively maintained.

---

## What It Does

- Static application security testing (SAST) — detects security antipatterns in actual code logic
- 3,000+ rules covering injection vulnerabilities, insecure configurations, dangerous function usage, and more
- 30+ supported languages including Python, JavaScript, TypeScript, Go, Java, and others
- Can detect hardcoded secrets and unsafe patterns in prompt-facing code (partial Cat 1 overlap)
- Language-aware analysis — understands code structure, not just text patterns
- JSON output for CI integration
- No account required for Community Edition

---

## Installation & Setup (Windows)

1. Install via pip: `pip install semgrep` (requires Python 3.8+)
   - Alternatively, download the binary from `github.com/semgrep/semgrep/releases`
2. Verify install: `semgrep --version`
3. Run a scan with auto-selected rules: `semgrep --config=auto [path]`
4. Run with a specific ruleset: `semgrep --config=p/owasp-top-ten [path]`
5. For JSON output: `semgrep --config=auto --json --output results.json [path]`
6. To scan a remote GitHub repo, clone it first, then run Semgrep on the local path

**Note:** `--config=auto` selects rules based on the languages detected in the target — a reasonable default for getting started without needing to understand all 3,000+ rules upfront.

---

## Free Tier Details

Community Edition is completely free. No account required. No usage limits. All 3,000+ community rules included. The Cloud Platform (Semgrep's paid offering) adds 20,000+ Pro rules, organizational dashboards, and CI/CD workflow integration — not needed for Soren's current use case.

---

## Limitations

- Layer-two only — not a day-one requirement; bring it in after Trivy, Gitleaks, and Snyk are running
- 3,000+ rules means there is a real learning curve to understand what is being detected and to tune for signal over noise — rated 5/10 difficulty by Rose, primarily because of this tuning requirement
- Does not scan dependencies for CVEs — that is Trivy and Snyk's job
- Does not scan secrets across git history — that is Gitleaks' job
- The Community Edition's 3,000 rules are a subset of Semgrep's full Pro ruleset (20,000+); some categories are less comprehensive than the paid tier
- Scanning a large repo with `--config=auto` can be slow; scoping the scan to specific rule categories improves performance

---

## Role in Soren's Pipeline

Semgrep fills the gap the binary-only tools leave: code-level logic analysis. Trivy finds dependency CVEs. Gitleaks finds secrets in history. Snyk adds SAST and deeper deps. Semgrep adds language-aware pattern detection against 3,000+ rules — catching things like SQL injection, command injection, path traversal, and unsafe deserialization patterns in the actual code logic. It is the layer-two add-on, not a day-one requirement. Soren brings it into the Cat 2 sequence after the primary stack (Trivy + Gitleaks + Snyk) is stable and running. Runs at pre-deployment clearance on local repo clones.

---

## Soren Security Pre-check

- **Verdict:** CLEARED
- **Reviewed:** 2026-06-08

LGPL-2.1, maintained by Semgrep Inc. (`semgrep/semgrep`). 15,436 stars, 955 forks, v1.165.0 as of June 2026 — active and well-supported. No account required for Community Edition. Installs via pip or binary download. No credential capture, no telemetry on Community Edition (the paid Cloud Platform has telemetry — Community Edition does not send scan data to Semgrep servers). Pure local analysis.

No unusual permissions, no external service calls during scan, no suspicious patterns in the repository. The rule-auto-download mechanism (`--config=auto`) does fetch rules from `semgrep.dev` at scan time — this is a known, documented behavior, not a security concern, but Soren should be aware that scans with `--config=auto` require internet access. Offline operation is possible with locally cached rulesets.

LGPL-2.1 is acceptable for Soren's use case (running as a tool, not linking it into a distributed product). No commercial use restrictions.

---

## Soren's Operational Note

This is not the first thing I set up — it is the thing I add once the primary Cat 2 stack is working. The reason it is layer-two is not that it is less valuable; it is that it has the steepest learning curve of the four Cat 2 tools. The 3,000 rules make it powerful but require judgment about what to enable and what to tune out. My starting point when I get to this: `semgrep --config=auto [path]` with JSON output. Review the findings, understand what the auto-selected rules are catching, and build from there. I do not try to configure a custom ruleset on day one — I let `auto` run first and understand what I am looking at before I optimize.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

## C&P Summary

Semgrep Community Edition is Soren's layer-two add-on for Category 2 — a language-aware static analysis tool with 3,000+ rules that catches code-level security antipatterns (injection, unsafe APIs, path traversal, etc.) that Trivy and Gitleaks do not touch. Free, no account needed, LGPL-2.1 licensed. It is not a day-one install — it comes in after the primary Cat 2 stack (Trivy, Gitleaks, Snyk) is running and stable. Difficulty rating: 5/10, primarily because tuning 3,000+ rules for signal over noise requires a learning curve.
