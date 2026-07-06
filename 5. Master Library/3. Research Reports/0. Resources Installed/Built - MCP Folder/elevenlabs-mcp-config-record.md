# ElevenLabs MCP — Config Record

**Tool:** elevenlabs-mcp (ElevenLabs)
**Version:** 0
**Wired:** 2026-06-04 — Session 218 CP1 (activated Session 219)
**Wired by:** Sage (CEO) — P7 Sandbox install queue
**Security status:** ACTIVE — **ACCEPT** (Soren COHK review, Session 256, Item 159)
**Research report:** Section 6 → 1. Research Reports → report-elevenlabs-mcp.md

---

## .mcp.json config (project-level)

Wired to `.mcp.json` in project root. Transport is **stdio** via `uvx elevenlabs-mcp`. The live API key is in `.mcp.json`; that file is git-ignored and must never be committed (added to `.gitignore` Session 219).

## Transport

**stdio** — `uvx elevenlabs-mcp`. Confirmed against `.mcp.json` Session 256: no HTTP / SSE transport configured.

---

## Security Disposition — ACCEPT (Item 159, Session 256)

**Verdict:** ACCEPT — status ACTIVE.

**CVE-2025-66416 (HIGH — DNS rebinding) in bundled mcp 1.12.4:** out of scope **as configured**. The vulnerability affects HTTP-transport MCP servers (DNS rebinding against an HTTP listener). This server runs over **stdio** (`uvx elevenlabs-mcp`), verified in `.mcp.json` — there is no HTTP listener to rebind against. The CVE therefore does not apply to this deployment.

**Why the earlier mitigation was dropped:** A `--with mcp>=1.23.0` workaround was attempted Session 219 to pull a patched mcp; it caused an MCP connection error (-32000) because elevenlabs-mcp 0.9.1 pins `uvicorn==0.27.1` while `mcp>=1.23.0` requires `uvicorn>=0.31.1` — an irreconcilable dependency conflict. The workaround was removed Session 221. With the stdio-transport reasoning above, no mitigation is needed for the current configuration.

### Conditions

1. **Stay on stdio.** This acceptance is valid only while the server runs over stdio (`uvx elevenlabs-mcp`). If transport ever changes to HTTP/SSE, CVE-2025-66416 comes back into scope — re-review before any such change.
2. **Sandbox / local single-user use only.**
3. **Upgrade trigger:** any `elevenlabs-mcp >0.9.1` that relaxes the `uvicorn==0.27.1` pin or bundles `mcp>=1.23.0` → upgrade then, and drop this exception (the patched mcp removes the underlying CVE regardless of transport).

---

*Config record by Sophia (COO) — Session 256, 2026-06-16 (Item 159 close; ACCEPT disposition per Soren COHK review). Created this session — the record was referenced in P7-AAR-Record Entry 5 as existing but had never actually been written; this is the first physical copy.*
