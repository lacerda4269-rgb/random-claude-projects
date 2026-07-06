# Resource Report: ClamAV

**Prepared by:** Rose (Researcher)
**Reviewed by:** Soren (Security Manager)
**Tasked by:** Sage (COO)
**Date:** April 15, 2026
**Category:** Soul Folder — Security Tools
**Role in Stack:** Primary — Category 4 (File / Malware Scanning)
**Status:** Research complete — pending Soren configuration

---

## What It Is

ClamAV is an open-source antivirus engine maintained by Cisco Talos (`Cisco-Talos/clamav`). It is the standard open-source antivirus solution — widely deployed, thoroughly documented, and actively maintained by Cisco. Designed as a CLI-accessible scanner for automated pipelines. License: GPL — fully free. Cross-platform including Windows. Signature database auto-updates via `freshclam`. Not a real-time background scanner by default — it is a command-line scan tool that Soren runs on demand.

---

## What It Does

- Detects viruses, trojans, worms, and general malware
- Detects Microsoft Office macro viruses
- Mobile malware detection
- Recursive directory scanning (`clamscan -r [directory]`)
- Single file scanning (`clamscan [file]`)
- Signature database updated via `freshclam` — pulls from Cisco Talos threat intelligence
- CLI output can be piped or logged for pipeline integration

---

## Installation & Setup (Windows)

1. Download the ClamAV Windows MSI installer from the official site: `clamav.net`
2. Run the MSI installer — installs `clamscan.exe` and `freshclam.exe` to the install directory
3. Add the ClamAV install directory to your system PATH
4. Navigate to the ClamAV install folder and configure:
   - Rename `clamd.conf.sample` → `clamd.conf`
   - Rename `freshclam.conf.sample` → `freshclam.conf`
5. Edit `freshclam.conf`: remove or comment out the `Example` line at the top of the file
6. Run `freshclam` to download and initialize the virus signature database (this downloads ~250MB of signatures on first run — takes a few minutes)
7. Verify: `clamscan --version`
8. Run a file scan: `clamscan [filepath]`
9. Run a recursive directory scan: `clamscan -r [directory]`

**Note:** ClamAV has the most involved setup of any tool in Soren's stack, but it is well-documented. The conf file renaming and `freshclam` initialization are the only non-obvious steps. Once configured, it runs cleanly.

---

## Free Tier Details

Completely free. No usage limits. No account required. No API key required. GPL license — free including commercial use with standard GPL obligations. Signature updates via `freshclam` are also free. There is no paid tier for ClamAV itself.

---

## Limitations

- Signature-based detection only — catches known, catalogued threats well (~60% detection rate against known malware), but performs weakly against zero-days and novel behavioral threats (15–35% on fresh malware)
- Not a behavioral scanner — it does not detect malware based on what a file tries to do; it matches against a database of known signatures
- Detection rate is significantly lower than VirusTotal's multi-engine consortium (35–60% vs. 95–98%) — this is why vt-cli runs as the second-opinion complement
- More setup steps than the binary-drop tools in the rest of the stack (Trivy, Gitleaks)
- Signature database must be kept current via `freshclam` — if the database goes stale, detection rate drops

---

## Builder Footprint

- **Integration type:** Desktop application + CLI — installed via Windows MSI installer; `clamscan.exe` and `freshclam.exe` on PATH; no account, no API key; recursive directory or single-file scan modes
- **Extension points:** `clamscan -r [directory]` for recursive scans; JSON/CSV output for pipeline integration; `freshclam` signature update schedule configurable as a Windows Task Scheduler job; clamd (daemon mode) available for high-volume scan pipelines if needed (Task Scheduler integration and clamd daemon-mode pipeline use are inferred from documentation — not explicitly documented as extension points) (Inferred from documentation — not explicitly documented)
- **Build complexity signal:** Medium — MSI install + conf file renaming (`clamd.conf.sample` → `clamd.conf`, `freshclam.conf.sample` → `freshclam.conf`) + removing `Example` line + `freshclam` first-run (~250MB download); one-time effort per Soren's note; subsequent use is single-command
- **Known conflicts:** Signature database must be kept current via `freshclam` — stale database degrades detection rate significantly; consider scheduling `freshclam` as a recurring task. Does not conflict with Bitdefender (different operational layers — ClamAV is deliberate on-demand scan; Bitdefender is always-on background).

## Role in Soren's Pipeline

ClamAV is the first-pass local scanner for Category 4. When any file is downloaded and queued for library entry, ClamAV runs first: fast, local, zero telemetry, no rate limit, fully offline. It catches known malware immediately without touching an external service. Anything ClamAV flags gets escalated — checked with vt-cli for a 70+ engine second opinion. Anything ClamAV clears that warrants closer inspection (suspicious origin, unusual file type) also gets a vt-cli follow-up. The combination of local-first (ClamAV) plus multi-engine confirmation (vt-cli) is what makes Cat 4 reliable.

---

## Soren's Operational Note

**Re-reviewed 2026-06-08 — verdict confirmed. CLEARED (core infrastructure).** Rose's freshness sweep confirms ClamAV v1.5.2 (March 4, 2026) remains current — no new release, no CVEs, no security disclosures. Stars: 6,720; last push 2026-06-05 — Cisco Talos actively maintaining. No changes to operational standing. This is core infrastructure in Soren's Cat 4 stack; no action required.

ClamAV is the most setup-involved tool in my stack, but the setup is a one-time event and the documentation is solid. The conf file renaming is the step that trips people up — it is not obvious that both `.sample` files need to be renamed and the `Example` line needs to be removed from `freshclam.conf`. Do that step carefully and the rest is straightforward. Once running, my standard workflow: `clamscan [file]` or `clamscan -r [directory]` before anything enters the library. I keep `freshclam` on a regular schedule so the signature database does not go stale — a stale database significantly reduces detection coverage. The detection rate limitation is real: ClamAV will not catch everything. That is exactly why vt-cli runs as the second layer. ClamAV is the fast, compliant, offline first pass. vt-cli is the thorough multi-engine second opinion.

---

## C&P Summary

ClamAV is Soren's primary local scanner for Category 4 — an open-source antivirus engine maintained by Cisco Talos that scans files and directories for known viruses, trojans, worms, and macro malware. Free, no account, fully offline, GPL licensed. Detection rate is ~35–60% against known threats — solid for a first-pass local scan, but signature-based only with no behavioral analysis. That is why vt-cli runs as the second layer for multi-engine confirmation. ClamAV has the most setup steps of any tool in the stack (conf file configuration and `freshclam` initialization), but it is well-documented and a one-time effort.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
