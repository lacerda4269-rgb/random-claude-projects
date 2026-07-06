# MoneyPrinterTurbo — Install Record

**Tool:** MoneyPrinterTurbo (harry0703)
**Version:** 0
**Installed:** 2026-06-04 — Session 218 CP1
**Installed by:** Sage (CEO) — P7 Sandbox install queue
**Security status:** CLEARED WITH CONDITIONS (Soren, Session 214; re-confirmed 2026-06-08). Sandbox use only until pillow CVEs cleared.
**Research report:** Section 5 → 1. Research Reports → report-moneyprinterturbo.md
**URL:** https://github.com/harry0703/MoneyPrinterTurbo
**License:** MIT

---

## Install

```bash
git clone https://github.com/harry0703/MoneyPrinterTurbo
cd MoneyPrinterTurbo
pip install -r requirements.txt
```

Cloned to `C:\ClaudeTools\MoneyPrinterTurbo\`. `pip install -r requirements.txt` completed.

## Dependency conflict — pillow (structural, unresolved)

Soren's clearance condition was **pillow ≥ 12.2.0**. This could NOT be met: `moviepy 2.2.1` pins `pillow < 12.0`, creating a direct and unresolvable conflict. Installed at **pillow 11.3.0**. Not resolvable without a moviepy upgrade.

## What it does

End-to-end short-form video generation pipeline (the most complete in the Movie Studio batch). No native MCP — custom integration via HTTP API required for agent-native use. First tool to reach for when short-form video production is in scope.

## CVE scan

Trivy v0.71.0 + Gitleaks v8.30.1. Trivy: 0 CRITICAL, **3 HIGH + 3 MEDIUM** — all in `pillow` 11.3.0 (image-processing attack vectors; low exploitability in sandbox use). Flagged for Soren at next COHK.

## Conditions (from Soren review)

1. Pin pillow ≥ 12.2.0 before deployment — **currently unmet** (structural moviepy conflict).
2. Sandbox use only until the pillow 11.3.0 CVEs are cleared.

---

*Install record by Sophia (COO) — Session 259, 2026-06-17. Authored on Jay's direct approval to reconcile a false "created" claim in P7-AAR-Record Entry 3: the record was cited as existing but had never been written; this is the first physical copy. Install facts pulled from the existing research report + MU-IP Installed copy on disk — not invented.*
