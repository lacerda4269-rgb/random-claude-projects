# Cross Talk / Fire Drill Workflow

**Paired SOP:** CrossTalk-FireDrill-SOP.md (SOPs folder)
**Jay's version — visual workflow replaces a written Jay SOP for this process**
**Version:** 0

---

**Version log:**

| Version | Date | Notes |
|---|---|---|
| v1.0 | (session unknown) | Initial build |
| v1.1 | 2026-05-24 | Version tracking added (no prior version recorded). HR13 sync — CrossTalk-FireDrill-SOP.md updated to v1.2 (administrative note removal only; no diagram changes required). Project 5 Phase 2 Final Alignment Sweep, Session 176. |

---

```mermaid
flowchart TD

    START([TRIGGER\nJay or Sage calls it\nNo fixed cadence — runs on judgment]):::startEnd

    START --> READY

    READY["Readiness Check\n• Documents accessible and current enough to audit?\n• Agents have worked with the material they are reviewing?\n• Jay available for the decision gate?"]:::step

    READY --> BRIEF

    BRIEF["Scope Brief — Sage to All Agents\n• Each agent reviews their own domain only\n• Lens: What is broken, missing, incomplete,\n  or unconnected to a real trigger in YOUR area?\n• Independence rule: no cross-sharing until all reports are in"]:::step

    BRIEF --> REVIEW

    REVIEW["Bottom-Up Review — All Agents Independent\nEach agent reports:\nItem label · What was found · Why it matters\n\nSage and Sophia run their own pass after all reports are in"]:::step

    REVIEW --> FILTER

    FILTER["Sophia Filters — WHY Lens\nAccept · Accept with context · Flag to Jay · Confirm deferral\n\nCOO pass: file consistency · Gotcha entries · list health"]:::step

    FILTER --> ROUTE

    ROUTE["Sage Routes by Rating\n0–2: Sage handles — no Jay input\n3–5: Sage handles — FYI to Jay\n6–10: Jay decision required"]:::step

    ROUTE --> CONTENT
    ROUTE --> TRIGGER_P
    ROUTE --> TIMING
    ROUTE --> BLANK_SYNC

    subgraph THREE_PASS [Three-Pass Audit — All Accepted Findings Sorted Here]
        CONTENT["Content Pass\nIs every step present,\nin the right order, and complete?\n\nExample: step missing from SOP;\ndocument referenced but does not exist"]:::pass

        TRIGGER_P["Trigger Pass\nIs there a mechanism that actually fires each step?\nBeing in an SOP is NOT a trigger.\n\nExample: Hard Rule 5 exists but did not fire at project open;\nclearance deferred to first live use with no mechanism to ensure it runs"]:::pass

        TIMING["Timing Pass\nAre steps firing at the correct point\nin the sequence?\n\nExample: step fires too late — gap was live for multiple sessions;\nstep fires too early — state changes outpace the documentation"]:::pass
    end

    CONTENT --> JAY_GATE
    TRIGGER_P --> JAY_GATE
    TIMING --> JAY_GATE

    JAY_GATE["Jay Decision Gate\nAll 6–10 rated items presented with Sage recommendation\nJay approves · redirects · or defers each item\n0–5 items reported as FYI — no decision required"]:::gate

    JAY_GATE --> RESOLVE

    RESOLVE["Resolution and Tracking\n• Gotcha.md entries — operational watch items logged\n• Sophia pending list — items queued to named projects\n• Soul and SOP corrections actioned or queued\n• LHF and Suggested Project Order status updated\n• Permanent review report filed — never deleted"]:::step

    RESOLVE --> PARKED{All items resolved\nor formally parked\nwith a named home?}:::check

    PARKED -- Not yet --> JAY_GATE

    PARKED -- Yes --> CLOSE

    CLOSE([PROJECT CLOSE GATE\nJay full review and explicit approval required\nNo agent or Sage can close this independently\nStatus Complete — Dependency gate lifts]):::startEnd


    classDef startEnd fill:#1b4332,color:#ffffff,stroke:#081c15,stroke-width:3px
    classDef step fill:#264653,color:#ffffff,stroke:#1a3040,stroke-width:1px
    classDef pass fill:#5c3317,color:#ffffff,stroke:#3d2210,stroke-width:1px
    classDef gate fill:#7b1d1d,color:#ffffff,stroke:#560d0d,stroke-width:2px
    classDef check fill:#343a40,color:#ffffff,stroke:#212529,stroke-width:1px
```
