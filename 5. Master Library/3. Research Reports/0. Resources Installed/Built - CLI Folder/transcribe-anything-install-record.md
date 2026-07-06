# transcribe-anything — Install Record

**Tool:** transcribe-anything (zackees)
**Version:** 0
**Installed:** 2026-06-04 — Session 218 CP1
**Installed by:** Sage (CEO) — P7 Sandbox install queue
**Security status:** CLEARED WITH CONDITIONS (Soren) — license discrepancy condition carries forward; v4.0.0 major-version bump assessed, no security regression
**Research report:** Section 5 → 1. Research Reports → report-transcribe-anything.md
**URL:** https://github.com/zackees/transcribe-anything

---

## Install

```bash
pip install transcribe-anything
```

Single command; CLI immediately available. Install method unchanged across the v3.2.10 → v4.0.0 jump — no new attack surface at install time.

## Version confirmed

Install pulled **v4.0.0** (PyPI). Note: at the time the research report was first filed it cited v3.2.10 as latest; the actual install pulled v4.0.0 — a major-version bump. New `--device sensevoice` backend present in v4.0.0 is not covered in the current research report (noted for next freshness sweep).

## What it does

CLI transcription utility — converts audio/video (meetings, interviews, recordings) into searchable text; Whisper transcription, speaker diarization, multiple output formats. Ingests YouTube URLs directly (plus TikTok, local files, videos without captions). Sole audio/video transcription tool in the stack as of Session 222, when mcp-youtube was removed (failed in testing) and transcribe-anything confirmed as its replacement — full transcript of an ~8 min video in under 5 minutes, CPU backend.

## CVE scan

Trivy: 0 CVEs (Session 218).

## Conditions (from Soren review)

1. Use for personal, non-commercial workflows (MIT license assumed authoritative).
2. Resolve the MIT (GitHub) vs. BSD-3-Clause (PyPI metadata) license discrepancy with the maintainer before any production use. GitHub is treated as source of truth.

---

*Install record by Sophia (COO) — Session 259, 2026-06-17. Authored on Jay's direct approval to reconcile a false "created" claim in P7-AAR-Record Entry 2: the record was cited as existing but had never been written; this is the first physical copy. Install facts pulled from the existing research report + MU-IP Installed copy on disk — not invented.*
