# /validate-pending-list — Quick Stats Validation Skill

**Owner:** Cosmo (Skill Creator)
**Companion to:** Hook 7 (`quick-stats-validation-hook.json`)
**Trigger:** `/validate-pending-list`
**Scope:** Read-only validation — does NOT modify any file

---

## What This Does

Validates that the Quick Stats numbers at the top of `sophia-pending-changes.md` match the actual row counts in each section. Reports all mismatches. Never modifies the file.

Runs on demand across ALL pending-changes files it can find — not just staged ones (unlike Hook 7, which only fires when the file is staged for a commit).

---

## When to Use

- Before a session close, to catch Quick Stats drift before it reaches Hook 7
- After manually editing the pending list, to verify counts before committing
- Anytime the Quick Stats feel out of sync

---

## Instructions

When this skill is invoked, perform the following steps:

1. **Find all `sophia-pending-changes.md` files** recursively under the project root. The COO's lives at `Sophia's COO Folder → Operational Files → sophia-pending-changes.md`; any active P/M Lead may also keep one in their personal folder. Search recursively so every pending list is found regardless of the project's structure.

2. **For each file found**, run the validation logic below.

3. **Report findings** — one block per file checked.

---

## Validation Logic

For each file:

**Step 1 — Parse Quick Stats line**
Find the line: `**Quick Stats:** \`Active: N | Deferred Named: N | ...\``
Extract all 7 key:value pairs.

**Step 2 — Count actual rows per section**

Identify the 6 section boundaries using `## Section N —` headers:
- Section 1 → Active
- Section 2 → Deferred Named (all subsections combined)
- Section 3 → Deferred No Home
- Section 4 → Notes & Objectives
- Section 5 → Pending AAR
- Section 6 → Behavioral Standards Active

**Data row definition:** A line that:
- Starts with `|`
- Is NOT a header row (contains `| # |`, `| Status |`, `| Triage |`, `| Meaning |`, etc.)
- Is NOT a divider row (matches `|---|...`)

Count all data rows in each section's range.

**Step 3 — Count Complete ✓ (pending transfer)**
Across ALL sections: count data rows where the line contains both `Complete` and `✓` (the checkmark character U+2713).

**Step 4 — Compare and report**

| Section | Quick Stats Says | Actual | Match? |
|---------|-----------------|--------|--------|

If all match: report `All Quick Stats counts verified ✓` for that file.
If any mismatch: list the mismatches clearly with `← MISMATCH` markers.

**This skill never modifies the file.** It reports findings only. The operator updates the Quick Stats line manually.

---

## Output Format

```
Validating: [file path]

  SECTION                              STATS SAYS   ACTUAL
  ────────────────────────────────────────────────────────
  Active                               0            0       ✓
  Deferred Named                       13           13      ✓
  Deferred No Home                     2            2       ✓
  Notes & Objectives                   0            0       ✓
  Pending AAR                          1            1       ✓
  Behavioral Standards Active          0            0       ✓
  Complete ✓ (pending transfer)        0            0       ✓

  Result: All Quick Stats counts verified ✓
```

If mismatches found:

```
  Result: MISMATCHES FOUND — update Quick Stats line before committing.
  FIX: Change Quick Stats to: Active: 0 | Deferred Named: 14 | ...
```

Provide the corrected full Quick Stats line as part of the fix output so the operator can paste it directly.
