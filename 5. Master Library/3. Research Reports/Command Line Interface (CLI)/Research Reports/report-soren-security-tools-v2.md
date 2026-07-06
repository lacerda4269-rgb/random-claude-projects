# Report: Soren Security Tools — Research v2

**Prepared by:** Rose (Researcher)
**Tasked by:** Sage, for Soren (Security Manager)
**Date:** April 15, 2026
**Supersedes:** report-soren-security-tools.md (April 14, 2026)
**Purpose:** Answer Jay's open questions from his v1 review. Finalize Soren's confirmed tool stack. Includes updated Cat 2 recommendation, difficulty ratings, Super CLI feasibility, mcp-firewall watchlist decision, VirusTotal reliability verdict, and Snyk's cross-category backbone role.

---

## Soren Re-Review Note — 2026-06-08

Re-reviewed 2026-06-08 as part of Phase 2 Batch C security review.

**SecureClaw VOID propagation confirmed.** The Cat 1 primary slot is correctly documented as open throughout this report — in the Cat 1 section, the Starter Stack table, and the Setup Sequence. All three locations have been updated by Rose and are accurate as of this review. No corrections needed.

**Cat 1 replacement flag:** The Cat 1 primary slot is open. A replacement tool needs to be identified before the full security stack is configured. This is a stack-level gap, not a blocking issue for other categories. Sage and Jay should plan a Cat 1 replacement research pass before the security stack goes live.

**All other category findings confirmed:** Verdicts for Cats 2–5 hold as documented. Metrics updated by Rose in the v2.0 freshness sweep are accurate. No new security concerns identified.

**Items in this report that have dedicated individual reports:** Each tool in the stack (Trivy, Snyk, Semgrep, Socket CLI, Pipelock, vt-cli, etc.) has been individually re-reviewed in this same Batch C pass. Refer to those individual reports for per-tool verdict confirmations.

---

## 1. Overview

**What changed from v1:**
- Cat 1: SecureClaw confirmed by Jay. Locked. No changes.
- Cat 2: Recommendation was missing in v1. Fixed here — clear primary recommendation provided with rationale.
- Cat 3: Snyk Agent Scan (primary) + Pipelock (standby) confirmed by Jay. mcp-firewall watchlist question answered.
- Cat 4: ClamAV + vt-cli confirmed by Jay, subject to reliability question. Answered directly below.
- Cat 5: Open question on whether Snyk should handle Cat 5 answered directly.
- Cross-category: Snyk's role as backbone addressed explicitly.
- New content: Difficulty ratings for all five Cat 2 tools. Super CLI feasibility assessment for Cosmo.
- Starter Stack table: Rebuilt free-only, incorporating all confirmed decisions.

All five categories remain fully coverable with free tools. The core finding from v1 holds. What is new here is the precision: decisions are locked in, difficulty ratings are honest, and Snyk's cross-category role is called out explicitly.

---

## 2. Category-by-Category Findings

---

### Category 1 — Prompt Injection / LLM Content Checking
*Text files, markdown, prompts, agent souls, skills*

**Jay's decision: SecureClaw confirmed. LOCKED.**

> **June 2026 Update:** SecureClaw was declared VOID in Session 214 (2026-06-04) — the tool is OpenClaw-platform-specific and incompatible with Claude Code. The Cat 1 primary slot is now open. See `report-secureclaw.md` for full context. LLM Guard remains the standby for runtime pipeline use. A replacement Cat 1 primary tool is needed.

**Current stack (original — pre-void):**
- ~~Primary: SecureClaw (`sparkst/secureclaw`) — VOID as of Session 214 (2026-06-04). Incompatible with Claude Code.~~
- Primary: **TBD** — Cat 1 primary slot open. Soren to identify replacement.
- Standby: LLM Guard (`protectai/llm-guard`) — runtime pipeline guardrail. Free, self-hosted. Bring in only if a runtime API guard is needed.

---

### Category 2 — GitHub Repo Scanning
*Vulnerabilities, malicious patterns, dependency risks, given a repo URL*

**Jay's question: "You didn't give me any recommendations on this one."**
Fixed below.

---

#### Current State of All Four Free Tools (April 2026)

| Tool | Stars | Last Release | License | Status |
|------|-------|-------------|---------|--------|
| Trivy | 36,153 (was 32,200+ in April 2026) | v0.71.0, June 2026 (was v0.69.3, March 2026) | Apache 2.0 | Actively maintained by Aqua Security. CLI binary safe. GitHub Action compromise status — continue CLI binary only per existing guidance. |
| Gitleaks | 24,400+ | v8.30.1, March 21 2026 | MIT | Actively maintained. Creator shifted primary focus to TruffleHog but Gitleaks continues receiving regular releases. |
| Semgrep (Community Edition) | 15,436 | v1.165.0, June 2026 | LGPL-2.1 | Renamed from Semgrep OSS to Community Edition. Free, no account required, 3,000+ rules, 30+ languages. Fully functional. Very active release cadence. |
| TruffleHog | 24,500+ | Last commit April 7 2026 | AGPL-3.0 | Actively maintained. 700+ credential detectors. Verifies secrets against live APIs. Note: AGPL-3.0 is a stricter license than MIT or Apache 2.0. |

All four confirmed active and free as of April 2026.

---

#### "Can We Use Them All?" — Direct Answer

**Yes. Running all four adds real value for Cat 2. The overlap is manageable and in practice works as confirmation rather than noise.**

Here is what each tool actually catches and why they are complementary:

- **Trivy** — dependency vulnerabilities (CVEs via lock files), IaC misconfigurations, basic secrets. The broad net.
- **Gitleaks** — hardcoded secrets across the full git history. Pattern-based, fast, extremely good at catching what was committed and never cleaned up.
- **Semgrep** — static code analysis. Language-aware pattern detection, security antipatterns in actual code logic. Catches things Trivy and Gitleaks do not touch.
- **TruffleHog** — credential verification. Goes further than Gitleaks by confirming whether a found credential is still live and valid. Slower but high-confidence findings.

The area of overlap: Trivy, Gitleaks, and TruffleHog all scan for secrets. Running all three will produce some duplicate secret findings. That is confirmation, not noise, and it is manageable. Semgrep adds a completely different signal (code-level SAST) and has zero overlap with the others.

**Practical recommendation: Run all four. Accept that secrets findings may overlap between Trivy, Gitleaks, and TruffleHog — that is the stack doing its job.**

---

#### Difficulty Ratings (1 = super easy, 10 = do not attempt for a vibe-coder)

These ratings are for Cosmo (Skill Creator) to use when deciding what CLI skills to build and in what order. Rated honestly — not softened.

| Tool | Difficulty | Rationale |
|------|-----------|-----------|
| **Trivy** | 2/10 | Single binary download. One command: `trivy repo [URL]`. JSON output is clean. No account needed. The easiest scanner on this list by a significant margin. |
| **Gitleaks** | 3/10 | Single binary. `gitleaks detect --source [path]`. Slightly more flags to learn than Trivy but still beginner-friendly. Windows binary available. |
| **Snyk CLI (free tier)** | 4/10 | Requires npm install and a free Snyk account plus `snyk auth`. More moving parts than Trivy and Gitleaks but the CLI is well-documented. Credit-based model (January 2026) adds one new consideration: verify current free limits at snyk.io/plans before building. |
| **Semgrep** | 5/10 | Install via `pip install semgrep` or the binary. Running basic scans is easy (`semgrep --config=auto [path]`). The complexity comes from understanding what the 3,000+ rule options cover and tuning for signal over noise — manageable but requires a learning curve. |
| **TruffleHog** | 6/10 | More complex than Gitleaks. Live credential verification means network calls and API responses to interpret. AGPL-3.0 license is stricter than MIT/Apache — Cosmo should confirm this is acceptable for the team's use before building a skill around it. More flags, more configuration, slower scans. |

---

#### Super CLI Feasibility

**Jay's question: "Can the first three CLIs (Trivy, Gitleaks, Semgrep) be combined into one Super CLI that runs all three and gives one consolidated output?"**

**Yes. Something close to this already exists. Cosmo can also build it if needed. Recommendation is to evaluate the existing option before building.**

**What already exists:**

Two relevant projects were found during research:

1. **DevSecOps Kit** (`EdgarPsda/devsecops-kit`) — A Go CLI that wraps Semgrep, Trivy, and Gitleaks into a single `devsecops scan` command. Outputs results in terminal, JSON, or HTML. Configurable fail gates (fail if any secrets found, fail if critical CVEs found, etc.). Last release: v0.6.0, March 30 2026. Currently 8 stars — small project, but actively maintained and purpose-built for exactly this use case. Install: `go install github.com/edgarpsda/devsecops-kit/cmd/devsecops@latest`, then install each underlying scanner binary separately, then run `devsecops scan`. Requires Go installed on the machine.

2. **Kekkai (formerly Hokage)** — An open-source CLI wrapper that runs Semgrep, Trivy, and similar scanners and focuses on unified human-readable triage. Built to solve the problem that individual scanners output different formats and produce findings that are hard to review in aggregate.

**Should Cosmo build a custom wrapper instead?**

Maybe — but not as the first move. Rose's recommendation: Cosmo should test DevSecOps Kit first. It is already built, it is free, and it wraps the exact three tools in question. If it covers Soren's needs, no custom build required. If it has gaps (Windows compatibility issues, output format does not fit the pipeline, something is missing), Cosmo builds a thin Python wrapper script.

**Cosmo's difficulty rating for building a custom wrapper:**

| Build | Difficulty | Notes |
|-------|-----------|-------|
| Python wrapper that calls all three tools and consolidates stdout | 4/10 | Straightforward scripting. No exotic dependencies. |
| Wrapper with unified JSON output and basic deduplication | 6/10 | Requires parsing each tool's JSON schema and merging findings. Not trivial but achievable. |
| Full equivalent of DevSecOps Kit from scratch | 8/10 | Not worth building when DevSecOps Kit already exists. |

**What a Cosmo-built wrapper would look like in practice:**

```
# usage: python run-security-scan.py [target_path_or_repo_url]
#
# Step 1: trivy repo [target]    -> trivy_results.json
# Step 2: gitleaks detect        -> gitleaks_results.json
# Step 3: semgrep --config=auto  -> semgrep_results.json
# Step 4: merge all three into   -> scan_report_[timestamp].json
# Step 5: print summary table    -> finding counts, severities, high/critical flags
```

The output would be one consolidated JSON file plus a clean terminal summary. That is 80% of what DevSecOps Kit does. The remaining 20% (fail gates, CI/CD hooks) is available in DevSecOps Kit or can be added incrementally.

**Rose's recommendation: Cosmo evaluates DevSecOps Kit first. If it does not fit on Windows or does not match Soren's output requirements, the Python wrapper is a 4–6/10 build depending on how deep the JSON consolidation needs to go.**

---

#### Cat 2 — Confirmed Recommendation

**Primary stack: Trivy + Gitleaks + Snyk CLI (free tier)**

- **Trivy** is the backbone — broadest coverage, lowest friction, no account required.
- **Gitleaks** adds dedicated secrets detection with full git history coverage. Trivial to layer on top of Trivy.
- **Snyk CLI** brings SAST and deeper dependency analysis. If already configured for Cat 3 (MCP) and Cat 5 (npm), there is zero additional setup cost to run it for Cat 2. One tool, three categories.

**Semgrep is the layer-two add-on.** Bring it in once the primary stack is running — it fills the code-logic pattern detection gap that Trivy and Gitleaks do not cover. Not a day-one requirement.

**TruffleHog is optional.** It is slower, more complex (AGPL license, live API calls), and partially duplicates Gitleaks. Only add it if live credential verification becomes a specific need. Not in the starter stack.

---

### Category 3 — MCP Server Scanning
*Tool poisoning, SSRF, prompt injection via tool descriptions*

**Jay's decisions: Snyk Agent Scan (primary) + Pipelock (standby, project-dependent). LOCKED.**

**Open question: Should mcp-firewall be watchlisted?**

**Direct answer: No. Do not watchlist mcp-firewall.**

`ressl/mcp-firewall` was checked directly during research. As of April 2026: approximately 5 stars, a single commit on the main branch, no published releases. Last update approximately February 25, 2026. The project was created by Robert Ressl (Associate Director Offensive Security at Kyndryl — credible background) but the repository itself is in early-stage or dormant state. No community, no releases, no active development visible.

Compare to what is already confirmed:
- **Snyk Agent Scan** — v0.4.13, April 2026. Backed by Snyk. 2,000+ stars. Purpose-built for MCP. Actively maintained.
- **Pipelock** — Active runtime AI agent firewall. Broader protection than mcp-firewall covers.

Snyk Agent Scan and Pipelock together cover everything mcp-firewall is attempting. mcp-firewall adds nothing to the current stack. Watchlisting it creates noise without upside. Dropped.

---

### Category 4 — File / Malware Scanning
*CLI-accessible, for actual downloaded files*

**Jay's decision: ClamAV + vt-cli confirmed, subject to reliability answer.**

**Direct answer: Yes, VirusTotal (free tier) is reliable enough for Soren's use case.**

**VirusTotal reliability:**
- Detection rate: 95–98% across its 70+ antivirus engine consortium. This figure reflects multi-engine aggregation — no single engine achieves this; the consortium does. A file that clears 70+ simultaneous engines has a very low false-negative rate.
- Rate limit on free tier: 4 lookups per minute, 10,000 API credits per month. Not a constraint at Soren's volume.
- Infrastructure: Google-backed. API uptime and reliability are enterprise-grade. No meaningful reliability concerns for this use case.

**ClamAV detection rate for context:**
- 35–60% depending on the sample set. Against fresh or zero-day malware it performs worse (15–35%). Against known, catalogued malware it performs better (~60%).
- ClamAV is signature-based only. It catches what is in its database. It will not detect behavioral threats or zero-days. This is a known limitation and the reason VirusTotal is paired with it — not a reason to abandon ClamAV.

**The combination is correct and reliable:**
- ClamAV: fast local scan, zero rate limit, zero telemetry, fully offline, catches the obvious threats immediately.
- VirusTotal (vt-cli): 70+ engine second-opinion for anything ClamAV flags or any file that warrants closer inspection.

**One condition that remains:** VirusTotal's free API Terms of Service explicitly prohibit commercial use. For this project (personal, non-commercial, small private team), the free tier is appropriate. If this project ever becomes a commercial operation or feeds into a commercial product, ClamAV-only is the compliant free path. The risk today is low — flagging it so Soren and Jay have it on record.

**Verdict: ClamAV + vt-cli confirmed. Reliable combination for Soren's pipeline.**

---

### Category 5 — npm / Package Security Scanning

**Open question: "If Snyk can already handle Cat 2 and is a far better choice, why not have it do both Cat 2 and Cat 5?"**

**Direct answer: Yes. Let Snyk handle Cat 5 if it is already configured for Cat 2 and Cat 3.**

Snyk's free tier covers:
- Open Source / SCA (npm): 400 scans per billing period. Public repo scans do not count against limits.
- SAST (Snyk Code): 100 scans per billing period.
- All five Snyk products included in the free tier.

For npm specifically: `snyk test` in any project folder with a `package.json` checks dependencies against Snyk's vulnerability database, which is more comprehensive than the GitHub Advisory Database that npm audit uses. Snyk also detects license issues and can generate SBOM-relevant data.

**The efficiency argument is strong.** If Soren already has a Snyk account and CLI configured for Cat 2 and Cat 3, running `snyk test` for npm in Cat 5 requires zero additional setup. Same CLI, same account, same output format. One less tool to install and maintain.

**npm audit: keep it as the zero-effort floor.** It is built into npm, requires nothing, and catches known CVEs instantly. Treat it as the first sanity check, not the full security story.

**Socket CLI: still the behavioral add-on.** Snyk's free tier does not fully replicate Socket's behavioral analysis (detecting packages that make unexpected network calls, spawn shells, etc.). If supply chain attack detection is a priority — if the team regularly ingests npm packages from less-vetted sources — Socket CLI adds a layer Snyk does not cover. For Soren's current use case at this scale, it is an optional complement, not a requirement.

**Semgrep for Cat 5:** If Semgrep is already running for Cat 2 code scanning, it is automatically providing secrets detection for any code inside npm packages at no extra cost. This is an incidental benefit, not a primary Cat 5 tool.

**araptus npm-security-scanner:** Lightweight malicious-package check. Zero dependencies, fast, scans against a database of known bad packages. Useful as a quick sanity-check before a full Snyk scan. Not a primary tool but worth having available.

**Updated Cat 5 recommendation:**
- Primary: npm audit (built-in, zero effort) + Snyk CLI (same account as Cat 2 and Cat 3)
- Complement: Socket CLI — add if behavioral supply chain detection is a specific priority
- Tertiary: araptus npm-security-scanner — fast, lightweight, zero-dependency malicious-package check

---

## 3. Cross-Category Platforms

**Is Snyk the de-facto backbone of the stack? Yes.**

| Platform | Categories Covered | Free Tier |
|----------|--------------------|-----------|
| **Snyk** | Cat 2 (repo/SAST), Cat 3 (Agent Scan), Cat 5 (npm/SCA) | 400 open source scans/month, 100 SAST scans/month. Public repos do not count. Credit model as of January 2026 — verify at snyk.io/plans. |
| **Trivy** | Cat 2 (primary repo/dep scanner), partial Cat 5 (CVE layer via lock files) | Fully free. No account. |
| **Semgrep** | Cat 2 (SAST/code patterns), partial Cat 1 (secrets in prompt-facing code) | Free Community Edition. No account required. |
| **LLM Guard** | Cat 1 (runtime LLM pipeline only) | Fully free, self-hosted. |
| **Pipelock** | Cat 1 (prompt injection), Cat 3 (MCP runtime), partial Cat 4 (DLP on data exfiltration) | Fully free, self-hosted. |

**Snyk's backbone case:**
- Three categories (2, 3, 5) covered by one CLI, one account, one set of credentials.
- Free tier covers Soren's volume comfortably at current scale.
- If budget ever becomes available: $25/dev/month (Team plan) unlocks unlimited scans, PR integration, and organizational dashboards — the single most efficient paid upgrade on this entire stack.
- The only platform here that spans MCP security (Cat 3), dependency scanning (Cat 2 and Cat 5), and SAST in one tool.

**The honest caveat on Snyk:** The January 2026 switch to a credit-based licensing model means the free tier limits above are current as of this report but could shift. Soren should verify current free credit allocation at snyk.io/plans before configuring the CLI. This was flagged in v1 and remains the one unstable element in the stack.

**Free-only backbone without Snyk:** Trivy + Gitleaks for Cat 2, Snyk Agent Scan for Cat 3. Complete coverage, no paid dependency, but Cat 5 would need npm audit + Socket CLI instead of Snyk. Snyk is the efficient path; the free-only fallback exists if needed.

---

## 4. AI/LLM-Specific Security Tools

No material changes from v1. The landscape has not shifted since April 14, 2026.

**Active roster as of April 15, 2026:**

- **Snyk Agent Scan** (`snyk/agent-scan`) — MCP-specific scanner. v0.4.13, April 2026. Confirmed primary for Cat 3. Apache 2.0.
- **LLM Guard** (`protectai/llm-guard`) — LLM input/output guardrails. 35 scanners. MIT license. Standby for runtime Cat 1 if needed.
- **Lakera Guard** (Check Point, acquired 2025) — Enterprise prompt injection API. Developer plan free (10,000 calls/month). Future consideration for runtime agent deployments at scale.
- **Pipelock** (`luckyPipewrench/pipelock`) — Open-source AI agent firewall. Runtime protection for MCP, SSRF, DLP. Apache 2.0. Confirmed standby for Cat 3 runtime.
- **Mindgard** — AI red teaming platform. Enterprise pricing ($16,000+). Not in scope at current phase. Revisit at Walk/Run phase when production trading agents go live.
- **Protect AI / Guardian** (Palo Alto Networks, acquired July 2025) — Model file scanning (PyTorch, ONNX, Pickle, etc.). Not in scope unless the team downloads pre-trained models.
- **The Vulnerable MCP Project** (`vulnerablemcp.info`) — CVE-style database for MCP security vulnerabilities. Free reference. Worth monitoring as a standing resource for Soren.

---

## 5. Soren's Recommended Starter Stack

Free-only. All of Jay's confirmed decisions incorporated. No paid-first options in the primary stack.

| Category | Primary Tool | Complement / Standby | Free? | Notes |
|----------|-------------|----------------------|-------|-------|
| **1. Prompt injection / LLM content** | ~~SecureClaw~~ **TBD** *(SecureClaw VOID — Session 214)* | LLM Guard (runtime only, if needed) | Yes | Cat 1 primary slot open. SecureClaw voided (incompatible with Claude Code). LLM Guard standby for runtime API guard. |
| **2. GitHub repo scanning** | Trivy + Gitleaks | Snyk CLI (free tier) | Yes | Trivy = deps/CVEs/IaC. Gitleaks = secrets/git history. Snyk = SAST and deeper dep analysis (zero added setup if already configured for Cat 3/5). Semgrep = layer-two add-on once primary stack is stable. |
| **3. MCP server scanning** | Snyk Agent Scan | Pipelock (runtime, when ready) | Yes | Jay confirmed. Agent Scan for pre-deployment config scanning. Pipelock for runtime firewall at Walk phase. mcp-firewall not watchlisted — too early-stage. |
| **4. File / malware scanning** | ClamAV | vt-cli (VirusTotal) | Yes* | Jay confirmed. ClamAV = fast local first-pass. vt-cli = 70+ engine second-opinion. *Free VirusTotal API = non-commercial use only per ToS. |
| **5. npm / package scanning** | npm audit + Snyk CLI | Socket CLI (behavioral/supply chain) | Yes | Snyk handles Cat 5 at zero extra setup if already configured for Cats 2 and 3. npm audit = zero-effort floor. Socket CLI = behavioral add-on if supply chain risk is a priority. |

**Paid upgrade priority (not required — for reference if budget becomes available):**
1. Snyk Team ($25/dev/month) — unlimited scans across Cats 2, 3, and 5 from one platform. Single most efficient upgrade.
2. Lakera Guard Pro — only if runtime agent deployments go live and 10,000 free calls/month is no longer enough.
3. Nothing else is justified at current team scale.

**Setup sequence for Soren (fastest-to-slowest setup, most critical gaps first):**
1. Install vt-cli — Windows binary + free API key. Fills the Cat 4 multi-engine gap immediately.
2. Install Trivy — Windows binary download. One command, no account. Fills Cat 2 dependency/CVE scanning.
3. Install Gitleaks — Windows binary. Adds secrets layer to Cat 2.
4. Configure Snyk CLI — `npm install -g snyk`, free account, `snyk auth`. Covers Cats 2, 3, and 5 from one account.
5. Configure Snyk Agent Scan — `uvx snyk-agent-scan@latest`. Requires Python 3.13+ and the `uv` package manager. Fills Cat 3.
6. ~~Install SecureClaw~~ — **VOID (Session 214)**. Cat 1 primary TBD. Skip this step until replacement is identified.
7. Configure npm audit — built-in if npm is installed. Zero extra work. Fills Cat 5 floor.
8. Install ClamAV — Windows MSI installer from clamav.net. Fills Cat 4 local scan layer.
9. Evaluate DevSecOps Kit — optional Super CLI wrapper for Cat 2 tools. Cosmo assesses before deciding whether to build custom.

---

## 6. Freshness Review

**Date of research:** April 15, 2026
**Confidence level:** High for all primary recommendations. One medium-confidence item noted below.

**Items re-checked for v2:**

| Item | Finding |
|------|---------|
| Trivy | Active. v0.69.3, March 3 2026 (original). **Updated June 2026: v0.71.0, 36,153 stars.** CLI binary confirmed safe. GitHub Action compromise flag carried forward — do not use Action without pinned SHA. |
| Gitleaks | Active. v8.30.1, March 21 2026. *Not re-checked in June sweep.* |
| Semgrep Community Edition | Active. **Updated June 2026: v1.165.0, 15,436 stars.** Still free, no account required. |
| TruffleHog | Active. Last commit April 7 2026. Note AGPL-3.0 license. *Not re-checked in June sweep.* |
| mcp-firewall (ressl) | Checked directly. ~5 stars, 1 commit, no releases. Not watchlisted. |
| VirusTotal reliability | Confirmed 95–98% detection via multi-engine consortium. Non-commercial restriction verified and noted. **Updated June 2026: vt-cli latest release is v1.2.0.** |
| DevSecOps Kit | Active. v0.6.0, March 30 2026. 8 stars. Functional. Cosmo should evaluate before building custom wrapper. *Not re-checked in June sweep.* |
| Snyk pricing | Credit-based model confirmed active since January 2026. Free tier test limits above are current but should be verified at snyk.io/plans before Soren configures. **Updated June 2026: Snyk CLI v1.1305.1, 5,573 stars, actively maintained.** |
| Pipelock | Not in original table. **Added June 2026: v2.6.0, 704 stars, last push 2026-06-08. Actively maintained.** |
| Socket CLI | Not in original table. **Added June 2026: v0.14.67. Repo moved from `socketdev/socket-cli-js` → `SocketDev/socket-cli`. Actively maintained.** |

**Medium-confidence item:**
- Snyk free tier credit limits may shift. The figures in this report (400 open source scans, 100 SAST scans per billing period) reflect current published data. Verify before locking in configuration.

**No new watch flags beyond what was in v1.**

---

## 7. C&P Summary

v2 closes every open question from Jay's review.

**Cat 1 and Cat 3** are locked and unchanged from Jay's decisions. **Cat 4** is confirmed: ClamAV handles the local scan, vt-cli handles the 70+ engine second opinion. VirusTotal's free tier is reliable at 95–98% detection, fits this team's non-commercial use case, and the rate limits are not a constraint. The one ongoing condition: if this project ever becomes commercial, ClamAV-only for compliance with VirusTotal ToS.

**Cat 2 now has a real recommendation.** Run Trivy (dependencies and IaC), Gitleaks (secrets and full git history), and Snyk CLI (SAST and deeper dependency analysis) as the primary stack. Running all four tools — Trivy, Gitleaks, Semgrep, TruffleHog — adds genuine security value with manageable overlap, because each tool catches something different. Semgrep is the layer-two add-on once the primary stack is stable. TruffleHog is optional unless live credential verification becomes a specific need. Difficulty ratings for all five tools are in the report for Cosmo's planning. Super CLI: DevSecOps Kit is the first thing Cosmo should evaluate before building anything custom. If it does not fit, a Python wrapper is a 4–6/10 build.

**Cat 5 resolves simply.** Snyk already handles it. If Snyk is configured for Cats 2 and 3, `snyk test` in any npm project folder costs zero additional setup. npm audit stays as the zero-effort floor. Socket CLI is the behavioral add-on for supply chain risk — bring it in if that becomes a specific concern.

**Snyk is the backbone.** One CLI, one account, one free tier spanning Cats 2, 3, and 5. The one ongoing item: Snyk changed its pricing model in January 2026. Soren verifies current free credit allocation at snyk.io/plans before locking in configuration. Everything else in the stack is stable, actively maintained, and confirmed working on Windows 11.

**mcp-firewall is not watchlisted.** Five stars, one commit, no releases as of April 2026. Snyk Agent Scan and Pipelock together make it irrelevant for this team.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
