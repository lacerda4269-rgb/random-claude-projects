# Resource Report: SecureClaw

---

> ## OpenClaw Use Only — Not for This Computer
>
> **OpenClaw Use Only — Not for This Computer.** SecureClaw was researched exclusively for use with OpenClaw. OpenClaw will not be installed on this machine. This report is retained as reference only. Do not attempt to install or deploy SecureClaw in this environment.

---

> ## ⚠ VOID — DO NOT USE
>
> **Status:** VOID
>
> **Reason:** SecureClaw (adversa-ai/secureclaw) is an OpenClaw-platform-specific tool — incompatible with Claude Code. This report was researched under incorrect assumptions about the tool's compatibility. The tool does not function as described in this report for a Claude Code environment.
>
> **Session:** 214 (2026-06-04)
>
> **Action:** This entry is not eligible for Master Library cataloging. Removed from Soren's tool stack.
>
> **Re-reviewed 2026-06-08 — VOID confirmed.** Source repository `sparkst/secureclaw` returns 404 (Rose freshness sweep, June 8). Repo is gone. VOID status is correct and final. No further action required. Report retained as historical record only.

---

**Prepared by:** Rose (Researcher)
**Reviewed by:** Soren (Security Manager)
**Tasked by:** Sage (COO)
**Date:** April 15, 2026
**Category:** Soul Folder — Security Tools
**Role in Stack:** Primary — Category 1 (Prompt Injection / LLM Content)
**Status:** VOID — incompatible with Claude Code; not eligible for Master Library cataloging (Session 214, 2026-06-04)

---

## What It Is

SecureClaw is an open-source CLI scanner from the `sparkst/secureclaw` GitHub project, purpose-built to detect prompt injection risks, exposed API keys, and insecure AI tool configurations in files and directories. It is a newer project with a smaller community than more established security tools, but it is actively maintained, fully free, and carries no telemetry. License is open source with no usage restrictions. Installed via pipx from the GitHub repository directly.

---

## What It Does

- Scans files and directories for prompt injection patterns
- Detects exposed API keys and hardcoded secrets in text files
- Flags insecure AI tool configurations
- Applies 28 detection patterns aligned to the OWASP LLM Top 10
- Outputs results as JSON for CI pipeline integration
- Pure pattern-matching — no model calls, no external API calls, no phone-home behavior

---

## Installation & Setup (Windows)

1. Ensure Python 3.9 or higher is installed
2. Install pipx if not already present: `pip install pipx`
3. Install SecureClaw: `pipx install git+https://github.com/sparkst/secureclaw.git`
4. Verify install: `secureclaw --version`
5. Run a scan: `secureclaw scan [path]`
6. For JSON output (CI integration): `secureclaw scan [path] --output json`

---

## Free Tier Details

Completely free. No usage limits. No account required. No API key required. Self-contained — runs entirely local with no external calls. There is no paid tier.

---

## Limitations

- Smaller community and less battle-tested than established tools like Semgrep or Trivy
- Pattern-based only — will not catch novel injection techniques that fall outside its 28 detection patterns
- Not designed for runtime pipeline use — this is a file-based scanner, not a live guardrail
- Does not scan binary files, compiled code, or containers
- Not a replacement for LLM Guard if a runtime API-level guardrail is ever needed

---

## Builder Footprint

- **Integration type:** CLI (Python/pipx) — installed via `pipx install git+https://github.com/sparkst/secureclaw.git`; invoked as `secureclaw scan [path]`; JSON output for pipeline integration
- **Extension points:** 28 detection patterns are viewable and reviewable; Soren can submit new patterns upstream; JSON output can be piped into a logging or alerting workflow; `--output json` flag enables CI integration (Inferred from documentation — not explicitly documented; "submit new patterns upstream" is inferred capability, not a documented contribution path)
- **Build complexity signal:** Low — pipx install; Python 3.9+ required; no account, no API key, no configuration file; single command to scan a directory
- **Known conflicts:** Python environment: confirm pipx-managed environment does not conflict with Snyk Agent Scan (Python 3.13+) or LLM Guard (Python 3.12) — pipx isolates by default, so this is low risk but worth verifying at install time. Do not confuse with runtime guardrail use case — SecureClaw is a pre-deployment file scanner only; LLM Guard is the runtime standby.

## Role in Soren's Pipeline

SecureClaw is Soren's primary tool for Category 1 — prompt injection and LLM content checking. It runs before any file enters the Master Library: soul files, skills, prompts, markdown, and agent configuration files all pass through SecureClaw at the pre-deployment clearance stage. It does not run at runtime — for that, LLM Guard is the standby. This is a pre-deployment, file-based scan only.

---

## Soren's Operational Note

> **OpenClaw Use Only — Not for This Computer.** SecureClaw was researched exclusively for use with OpenClaw. OpenClaw will not be installed on this machine. This report is retained as reference only. Do not attempt to install or deploy SecureClaw in this environment.

This is my first line of defense for everything in the Soul Folder — anything that touches prompt text, agent identity, or LLM configuration gets scanned before it goes into the library. The command is simple: `secureclaw scan [path]`. I run it on the whole folder, not individual files, so nothing slips through. JSON output is what I want for any logged scan run — it gives me a clean record of what was checked and what was found. The two things I need to confirm before I go live with this: (1) verify the GitHub repo is still active and the install via pipx works cleanly on Windows 11, and (2) review the 28 detection patterns once so I understand exactly what it is and is not catching. This is not an AI-based scanner — it is pattern matching. That is fine for what I need. I need it to catch obvious injection strings, exposed keys, and OWASP LLM antipatterns before they reach the library. Nothing more.

---

## C&P Summary

SecureClaw is an open-source CLI tool that scans files and directories for prompt injection patterns, exposed API keys, and OWASP LLM Top 10 violations using 28 detection rules. It is Soren's primary Category 1 tool — every soul file, skill, prompt, and markdown document runs through it before entering the Master Library. Completely free, no account needed, pure local pattern-matching with no telemetry. It covers the pre-deployment file-scan layer only; LLM Guard is the standby if a runtime API guardrail is ever needed.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
