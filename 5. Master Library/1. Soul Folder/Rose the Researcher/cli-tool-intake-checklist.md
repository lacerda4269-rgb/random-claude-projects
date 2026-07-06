# CLI Tool Intake Checklist

**Owner:** Rose — Research Specialist
**Version:** 0
**Created:** 2026-06-02
**Status:** Active

---

## Purpose

This checklist fires whenever Rose evaluates a CLI tool as a candidate for the Master Library. It documents the standard intake sequence Rose follows for every candidate CLI tool before the research report is finalized. Applies to all CLI candidates regardless of how the research task originated.

This is not a deep security audit — that is Soren's role. This checklist ensures the research report contains the minimum required information for Soren to run a full clearance evaluation.

---

## Checklist

### 1. Current Version

- Identify the version being evaluated (the one assessed in this report)
- Check the repository or official release page for a more recent release
- If a newer version exists: note it explicitly and flag whether the report covers the latest or a prior version
- Record: `Version evaluated: X.X.X | Latest available: X.X.X | Delta: [none / minor / major]`

---

### 2. License

- Identify the license type (MIT, Apache 2.0, GPL v2/v3, AGPL, proprietary, unlicensed, etc.)
- Flag any of the following:
  - **Copyleft** (GPL, AGPL, LGPL) — note the implication: derivative works or projects linking this tool may inherit the license requirement
  - **Commercial use restrictions** — flag explicitly; some licenses prohibit commercial use without a paid tier
  - **Unlicensed** — treat as restricted; unlicensed code has no grant of rights
- Record: `License: [type] | Flag: [none / copyleft / commercial restriction / unlicensed]`

---

### 3. CVE Sweep

- Check for known vulnerabilities against the specific version being evaluated
- Sources: NVD (nvd.nist.gov), Snyk (snyk.io/vuln), OSV (osv.dev), GitHub Security Advisories
- Check both the tool itself and any notable dependencies if documented
- Record: `CVE check: [clean / N CVEs found — detail in report] | Sources checked: [list]`
- If CVEs are found: include version number, severity, and whether a patched version exists

---

### 4. Alternatives Comparison

- Note at least 1–2 alternatives evaluated and why this tool is preferred — or note if none were found
- Alternatives check serves two purposes: (1) ensures the team is not adopting an inferior tool when a better-fit option exists; (2) gives Soren and future teams context on the decision
- If no meaningful alternatives exist: state that explicitly (not a red flag — just document the finding)
- Record: `Alternatives evaluated: [tool A, tool B] | Preferred because: [reason] | OR: No meaningful alternatives found`

---

### 5. Summary Rating

After completing all four checks above, assign a summary rating:

| Rating | Meaning |
|--------|---------|
| **Clean** | All four checks pass — no flags, current version, permissive license, no CVEs, alternatives noted |
| **Flagged** | One or more items need Soren's attention — document the flag clearly in the report |
| **Hold** | A serious concern exists (major CVE, restrictive license, no licensing) — do not advance to clearance pipeline without Sage's review first |

Record: `Summary rating: [Clean / Flagged / Hold] | Flags: [none / list flags]`

---

## Output

These five checklist findings feed directly into the **Soren Pre-check** section of the research report. Each finding is stated explicitly — Soren uses this section to determine whether a full clearance review is warranted and where to focus.

A research report for a CLI candidate that does not include these five fields is incomplete.

---

## Notes

- This checklist does not replace Soren's security review — it prepares the report for it
- Rose classifies the output type (Resource report vs. Fact-finding) per SOP §3 — CLI tools are always Resource reports
- If a Hold rating is reached, flag to Sage before delivering the report; do not route to Soren without Sage's awareness

---

*Created by Cosmo — Session 203 (Item 106 — CLI tool intake checklist build)*
*Applies to: Rose (Research Specialist)*
