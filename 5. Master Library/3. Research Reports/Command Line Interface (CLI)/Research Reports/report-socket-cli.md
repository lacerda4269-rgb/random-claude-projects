# Resource Report: Socket CLI

**Prepared by:** Rose (Researcher)
**Reviewed by:** Soren (Security Manager)
**Tasked by:** Sage (COO)
**Date:** April 15, 2026
**Category:** Soul Folder — Security Tools
**Role in Stack:** Complement (behavioral) — Category 5 (npm / Package Scanning)
**Status:** Research complete — pending Soren configuration

---

## What It Is

Socket CLI is the command-line interface for Socket Security's supply chain analysis platform. **Repo note (June 2026):** The GitHub repository has moved from `socketdev/socket-cli-js` to `SocketDev/socket-cli` — update bookmarks and any automated checks. Latest version: v0.14.67. It analyzes package behavior (network calls, filesystem access, shell execution, obfuscated code) rather than just checking a CVE database. Installed via npm. License: open source. Free tier covers open-source projects; private repos require a paid plan.

---

## What It Does

- Behavioral analysis of npm packages — detects packages that make unexpected network calls, spawn shells, access the filesystem, or contain obfuscated code
- Supply chain attack detection — catches compromised maintainer accounts, typosquatting, and malicious packages that have no CVE record
- Scans `package.json` and installed packages for behavioral risk signals
- Flags packages that have had recent suspicious changes (even if no CVE has been published yet)
- JSON and table output
- Works on Windows via npm install

---

## Installation & Setup (Windows)

1. Ensure npm is installed (comes with Node.js)
2. Install Socket CLI: `npm install -g @socketsecurity/cli`
3. Verify: `socket --version`
4. Create a scan: `socket scan create` (in a project directory with a `package.json`)
5. Review findings in the CLI output or follow the link to the Socket dashboard for the full report

**Note:** A free Socket account may be required for the full scan results — verify against current Socket documentation at `socket.dev` before setting up.

---

## Free Tier Details

- Free tier covers open-source projects
- **Private repositories require a paid plan** — paid plans start at approximately $25/month
- At current team scale (one operator, small private library, non-commercial use), Snyk handles the primary Cat 5 scanning for private repos; Socket is the behavioral complement layer
- The free tier is sufficient if Socket is used primarily for evaluating open-source npm packages before they are brought into the project

**Private repo limitation:** Socket's free tier is designed for open-source projects. If Soren needs to scan private npm packages regularly, either a paid Socket plan or Snyk (which handles private repos within its own free tier limits) is the path forward.

---

## Limitations

- Free tier does not cover private repositories — relevant for the team's own packages
- Does not replace CVE-based scanning — Socket's behavioral analysis is additive, not a substitute for npm audit or Snyk
- Paid plan (~$25/month) is required for full private repo support
- Newer platform than npm audit and Snyk — smaller community; verify active maintenance before treating as a core dependency

---

## Role in Soren's Pipeline

Socket CLI is the behavioral layer of Category 5. npm audit catches known CVEs in the dependency database. Snyk adds deeper CVE analysis and SAST on the same basis. Neither of those tools catches a package that is behaviorally malicious but has no CVE record — a compromised npm package that exfiltrates data, spawns a shell, or makes unexpected network calls. Socket catches that. It is the add-on for supply chain attack detection, not the foundation. The Cat 5 sequence: npm audit first (zero-effort CVE floor), Snyk second (deeper CVE and SAST via the already-configured account), Socket third (behavioral analysis for anything that warrants it).

---

## Soren Security Pre-check

- **Verdict:** CLEARED — conditions apply
- **Reviewed:** 2026-06-08

**Repo URL change assessment (priority flag):**

Rose flagged that the repository moved from `socketdev/socket-cli-js` to `SocketDev/socket-cli`. I assessed this as follows:

- **Same organization, different repo name:** The GitHub org `SocketDev` (capitalization change only — GitHub org names are case-insensitive) is the official Socket Security organization. This is a rebrand/rename, not a transfer to a different owner.
- **Redirect confirmed:** Rose confirmed a permanent redirect from the old URL. GitHub redirects on repo renames within the same org are automatic and persistent — this is the standard GitHub mechanism for a legitimate org rename.
- **No namespace hijack indicators:** A repo hijack would involve a different org, a different maintainer account, or a fork appearing to replace the original. None of those conditions apply here. The move is from `socketdev` → `SocketDev` (same entity, capitalization only) and the repo name changed from `socket-cli-js` → `socket-cli` (reflecting the tool's expansion beyond JS-only).
- **Publisher continuity:** Socket Security is an established, funded security company. The rebrand is consistent with the company's documented expansion of the CLI beyond the original Node.js-only scope.
- **Install command unchanged:** `npm install -g @socketsecurity/cli` — npm package name unchanged. No supply chain risk from the repo move.

**Assessment:** Legitimate organization rename. Not a hijack. The existing clearance conditions hold.

**Conditions on clearance:**
1. Install via the npm package name (`@socketsecurity/cli`) — do not clone and build from source unless specifically needed.
2. Free tier is open-source projects only. Do not use against private repositories without a paid plan.
3. Verify current free tier account requirements at socket.dev before integrating into a recurring workflow (terms may evolve).
4. Socket is the behavioral add-on for Cat 5 — not a day-one install. Bring in only when supply chain behavioral detection is a specific priority.

---

## Soren's Operational Note

I do not need this running on day one — Snyk and npm audit together cover the CVE layer well. Socket becomes relevant when I am specifically reviewing npm packages from less-vetted sources, or when supply chain attack detection is a priority for a specific resource. The limitation I keep in mind: Socket's free tier is open-source projects only. For private repos, Snyk handles it. Socket is my behavioral add-on for open-source npm packages specifically, not my primary scanner. When I do install it: `npm install -g @socketsecurity/cli` and verify the current account requirements at socket.dev — the free tier terms are worth a quick confirm before I integrate it into a recurring workflow.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|

## C&P Summary

Socket CLI is Soren's behavioral add-on for Category 5 — it detects supply chain attacks by analyzing npm package behavior (network calls, shell spawning, filesystem access, obfuscation) rather than checking a CVE database. This fills the gap that npm audit and Snyk leave: a malicious package with no CVE record. Free tier covers open-source projects; private repos require a paid plan (~$25/month). At current scale, Snyk handles private repo scanning for Cat 5, and Socket is brought in specifically for behavioral analysis of open-source npm packages. It is the third layer in the Cat 5 sequence — not a day-one install.
