# /version-check — Version Header Audit

**Skill name:** `/version-check`
**Built by:** Cosmo (Skill Creator)
**Source:** Internal — companion to Hook 6 (version-gate-hook.json)
**Soren status:** CLEARED (internal build — no external resource)
**Version:** 0
**Built:** 2026-06-12
**Item:** 152

---

## What It Does

On-demand version header audit across all `.md` files in the current working directory. Checks that every file's `**Version:**` header matches the highest version number found in its version log. Useful during the pre-close sweep to catch drift before a commit triggers Hook 6.

This skill is an audit layer only. It does NOT modify any files — it reports only.

---

## Invocation

```
/version-check
```

---

## What To Do When Invoked

Scan all `.md` files recursively in the current working directory. For each file:

1. Look for a `**Version:**` header line (pattern: `**Version:** X.Y` or `**Version:** SOP X.Y` or similar)
2. If no version header is found in the file — skip it silently (not all files have one)
3. Extract the numeric version from the header (strip prefixes like "SOP ", "v", "V" — get the X.Y or X.Y.Z number)
4. Scan the full file for all version numbers (table rows like `| X.Y |`, changelog lines like `*vX.Y`, `v X.Y`, etc.)
5. Find the highest version number present anywhere in the file
6. Compare the header version to the highest log version
7. If they do not match — record the file as a mismatch with: file path, header version, highest log version

After scanning all files, report:

```
VERSION CHECK COMPLETE
Files scanned: N
Files with version headers: M
Mismatches found: K

[If K > 0, list each:]
  FILE:    <relative path>
  HEADER:  **Version:** X.Y
  LOG MAX: X.Z
  FIX:     Update **Version:** header to match X.Z, or add a log entry for X.Y

[If K = 0:]
  All version headers match their log entries. Clean.
```

---

## Scope

- Scans ALL `.md` files recursively from the current working directory
- Does NOT modify any file
- Files without a `**Version:**` header are skipped silently
- Files with a version header but no version log entries are skipped silently (warn-only behavior — no block)
- Unreadable files are skipped silently

---

## Relationship to Hook 6

Hook 6 (`version-gate-hook.json`) runs the same check automatically on staged `.md` files at `git commit`. This skill runs on demand across all files — use it mid-session to catch drift early, before staging.

---

## Dependencies

- Current working directory must be set to the project root for full coverage
- No external tools required — pure file read + pattern match

---

*Built by Cosmo — Skill Creator | Item 152 | 2026-06-12*
*Companion to Hook 6 — version-gate-hook.json | Internal build — no external resource*
