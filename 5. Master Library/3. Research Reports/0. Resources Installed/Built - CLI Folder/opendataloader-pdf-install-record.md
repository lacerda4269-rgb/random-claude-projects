# opendataloader-pdf — Install Record

**Tool:** opendataloader-pdf
**Version:** 0
**Installed:** 2026-06-10 — Session 237
**Installed by:** Sage (CEO) — P7 Sandbox install queue
**Security status:** Pre-cleared — Tier 2, Apache 2.0 (Feynman tool assessment Session 234; Jay approved)
**Research report:** N/A — Feynman pre-clearance; no dedicated Rose report

---

## Install

```bash
pip install opendataloader-pdf
```

## Version confirmed

```
pip show opendataloader-pdf
Name: opendataloader-pdf
Version: 2.4.7
License-Expression: Apache-2.0
Requires: (none)
Location: C:\Users\jlacerda\AppData\Local\Programs\Python\Python313\Lib\site-packages
```

## Import test

```python
import opendataloader_pdf
# Import OK
# Exports: cli_options_generated, convert, convert_generated, run, run_jar, runner, wrapper
```

## CVE scan

Trivy filesystem scan — **0 vulnerabilities, 0 secrets detected** (2026-06-10).

## Runtime dependency

Requires Java 11+ at runtime. Confirmed: OpenJDK 25.0.3 (Temurin, 64-bit) installed at `C:\Program Files\Eclipse Adoptium\jdk-25.0.3.9-hotspot\`. Java gate check passed Session 237.

---

*Install record by Sage (CEO) — Session 237, 2026-06-10.*
