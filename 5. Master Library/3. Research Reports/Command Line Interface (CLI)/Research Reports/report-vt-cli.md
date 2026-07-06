# Resource Report: vt-cli (VirusTotal)

**Prepared by:** Rose (Researcher)
**Reviewed by:** Soren (Security Manager)
**Tasked by:** Sage (COO)
**Date:** April 15, 2026
**Category:** Soul Folder — Security Tools
**Role in Stack:** Complement (multi-engine) — Category 4 (File / Malware Scanning)
**Status:** Research complete — pending Soren configuration

---

## What It Is

vt-cli is the official VirusTotal command-line interface from VirusTotal (`VirusTotal/vt-cli`). VirusTotal is a Google-backed file scanning service that submits files to 70+ antivirus engines simultaneously and returns aggregated results. The free community tier provides 10,000 API credits per month. Available on Windows via binary releases or `winget`. VirusTotal infrastructure is enterprise-grade — Google-backed, high uptime, production-reliable. The CLI is open source; the VirusTotal service itself is a proprietary platform.

**Repository Metrics (June 2026):** 1,402 stars | 136 forks | 16 open issues | v1.2.0 (latest release — last push 2026-05-19) | Apache-2.0.

---

## What It Does

- Submits files to VirusTotal for simultaneous scanning across 70+ antivirus engines
- Returns a consolidated verdict: how many of 70+ engines flagged the file, and with what detection labels
- Significantly higher detection coverage than any single-engine scanner including ClamAV
- 95–98% detection rate via multi-engine aggregation
- Checks file hash against VirusTotal's database before uploading (if the file has been scanned before, results come back instantly without re-uploading)
- Windows binary available; also installable via `winget install VirusTotal.vt-cli`

---

## Installation & Setup (Windows)

1. Create a free VirusTotal community account at virustotal.com
2. Retrieve your API key from your VirusTotal profile page
3. Install vt-cli via one of two methods:
   - Option A — winget: `winget install VirusTotal.vt-cli`
   - Option B — binary: download from `github.com/VirusTotal/vt-cli/releases`, unzip, add to PATH
4. Initialize: `vt init` (prompts for API key on first run)
5. Enter your API key when prompted
6. Verify: `vt version`
7. Scan a file: `vt scan file [filepath]`
8. Check a file by hash (no upload): `vt file [sha256hash]`

---

## Free Tier Details

- Free community account provides 10,000 API credits per month
- Rate limited at 4 lookups per minute on the free tier
- **Non-commercial use only per VirusTotal Terms of Service** — see note below
- File uploads on the free tier are shared with the VirusTotal community and partner security vendors — do not upload files containing sensitive or proprietary data
- Paid/enterprise tiers: custom quote, industry pricing runs $20,000–$50,000+/year — not relevant for this team

**Non-commercial use restriction:** VirusTotal's free API Terms of Service explicitly prohibit commercial use. This team's current use (personal, private, non-commercial research) is confirmed acceptable. If this project ever becomes a commercial operation or feeds into a commercial product, vt-cli must be dropped and ClamAV becomes the sole Cat 4 scanner. This condition is on record.

---

## Limitations

- Free tier rate limit: 4 lookups per minute — not a constraint at Soren's scan volume, but would be an issue if many files needed scanning in rapid succession
- Non-commercial use restriction on the free API — see Free Tier Details
- Files uploaded to VirusTotal are shared with partner security vendors and become part of VirusTotal's database — do not scan sensitive proprietary files through the service; scan only files received from external sources
- Does not provide behavioral analysis of file execution — it aggregates signature-based results from 70+ engines; it is not a sandbox

---

## Builder Footprint

- **Integration type:** CLI (Go binary or winget install) — `winget install VirusTotal.vt-cli` or binary download; `vt init` one-time API key setup; `vt scan file [filepath]` for file submission; `vt file [sha256]` for hash lookup without re-upload
- **Extension points:** Hash-based lookup (`vt file [sha256]`) avoids re-uploading known files — faster and conserves API credits; JSON output for pipeline integration; batch file scanning via shell loops; rate limit (4/minute) manageable at current Soren scan volume
- **Build complexity signal:** Low — binary or winget install + free VirusTotal account + `vt init` API key prompt; simpler setup than ClamAV; rate limit (4 lookups/minute) is a design constraint to build around
- **Known conflicts:** Non-commercial use only per VirusTotal ToS — if this project becomes commercial, vt-cli must be replaced with ClamAV-only for Cat 4 (condition is on record in report). Do not scan proprietary or sensitive project files — VirusTotal shares uploads with partner security vendors. Only scan files received from external sources.

## Soren Security Re-Review — 2026-06-08

Re-reviewed 2026-06-08 as part of Phase 2 Batch C security review.

**Version discrepancy confirmed and resolved.** Prior entry (v1.0) listed v1.3.0, which Rose has corrected to v1.2.0 (latest release, last push 2026-05-19). The original v1.3.0 entry appears to have been a data error in the research — no v1.3.0 release exists in the GitHub releases page. The correction to v1.2.0 has no security impact. The tool is Apache-2.0, actively maintained by VirusTotal (Google), stars confirmed at 1,402.

**Existing clearance verdict confirmed.** No new CVEs, no security disclosures, no ownership changes, no license changes. Non-commercial use restriction unchanged and on record. The two standing operator conditions (no proprietary file uploads; flag commercial use to Sage immediately) are correctly documented and remain in force.

**No verdict change.**

---

## Role in Soren's Pipeline

vt-cli is the second layer of Category 4, running after ClamAV. ClamAV does the fast, local, offline first pass — catching known threats without touching an external service. vt-cli runs as the multi-engine confirmation layer: anything ClamAV flags, and any file from a suspicious or uncertain source, gets submitted for a 70+ engine second opinion. The 95–98% detection rate from multi-engine aggregation is the reason this combination is reliable — ClamAV alone at 35–60% would not be sufficient. Together they form a complete Cat 4 pipeline.

---

## Soren's Operational Note

This is the first tool I install in the full stack — it fills the most critical immediate gap and the setup is about as simple as any tool gets. The only steps that matter: create the free VirusTotal account, grab the API key, run `vt init`, paste the key in. From that point, `vt scan file [filepath]` is my second-pass command on anything that comes through Cat 4. Two things I keep front of mind: first, only scan files I received from external sources — do not run proprietary project files through VirusTotal, because they get shared with VirusTotal's partner network. Second, this stays non-commercial. If that changes for this project, I flag it to Sage immediately and we switch to ClamAV-only for Cat 4.

---

## C&P Summary

vt-cli is Soren's multi-engine second layer for Category 4 — the official VirusTotal CLI that submits files to 70+ antivirus engines simultaneously, achieving a 95–98% detection rate through aggregation. It runs after ClamAV (local first pass) to confirm or escalate findings. Free community account provides 10,000 API credits/month at 4 lookups/minute — no constraint at current volume. Key condition: VirusTotal's free API is non-commercial use only per ToS. This is acceptable for the team's current personal/private use; if the project becomes commercial, vt-cli is replaced by ClamAV-only. Do not scan proprietary or sensitive files — VirusTotal shares uploads with partner security vendors.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
