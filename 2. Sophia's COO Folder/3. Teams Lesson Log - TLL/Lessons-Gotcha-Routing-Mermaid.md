=======================================================================
  MERMAID CODE
  Workflow: Lessons and Gotcha Routing
  Version: v1.0 — 2026-05-31
  How to use: Copy everything inside the code block below.
               Paste into mermaid.live. Export as PNG.
=======================================================================

```mermaid
%%{init: {'theme': 'dark', 'themeVariables': {'primaryColor': '#1E3A5F', 'primaryTextColor': '#ffffff', 'primaryBorderColor': '#4A9EFF', 'lineColor': '#7EB8D4', 'secondaryColor': '#1A2744', 'tertiaryColor': '#1A2744'}}}%%
flowchart TD
    classDef startEnd fill:#00695C,stroke:#004D40,color:#ffffff
    classDef process fill:#1565C0,stroke:#0D47A1,color:#ffffff
    classDef decision fill:#E65100,stroke:#BF360C,color:#ffffff

    START([Something happened this session]):::startEnd
    Q{What happened?}:::decision
    START --> Q

    Q -->|Sage mistake or correction| SA_Q
    Q -->|Agent lesson| SB_REPORT
    Q -->|Operational trap or recurring gap| SC_Q

    subgraph SA["  SECTION A — SAGE CORRECTIONS  "]
        SA_Q{Specific to THIS project only?}:::decision
        SA_YES["Write to: lessons.md\nproject memory folder"]:::process
        SA_NO["Write to: lessons_global.md\nglobal folder"]:::process
        SA_HOT["HOT PATH: Also clearly universal mid-project?\nPromote to lessons_global.md immediately\nDo not wait for AAR"]:::process
        SA_Q -->|YES — project specific| SA_YES
        SA_Q -->|NO — clearly universal| SA_NO
        SA_YES --> SA_HOT
    end

    subgraph SB["  SECTION B — AGENT LESSONS  "]
        SB_REPORT[Agent reports lesson to Sage]:::process
        SB_SOPHIA["Sage routes to Sophia:\nwhat happened, why, rule going forward"]:::process
        SB_LOG["Sophia logs in Team-Lessons-Log.md\nSame session — no queuing"]:::process
        SB_Q{Clearly universal AND agent-specific?}:::decision
        SB_HOT["HOT PATH: Promote immediately\nSage updates agent soul same session\nSophia marks as promoted"]:::process
        SB_AAR["Mark: AAR — pending review\nReviewed at project close"]:::process
        SB_REPORT --> SB_SOPHIA --> SB_LOG --> SB_Q
        SB_Q -->|YES| SB_HOT
        SB_Q -->|NO or BORDERLINE| SB_AAR
    end

    subgraph SC["  SECTION C — GOTCHA.MD  "]
        SC_Q{First or second+ occurrence\nof this same gap?}:::decision
        SC_FIRST[First occurrence:\nCorrect and move on]:::process
        SC_SECOND["Second+ or immediate trap:\nSophia logs in Gotcha.md — same session"]:::process
        SC_FORMAT["Entry: Type, Counter, Status\nWhat Happened, Root Cause\nFix Applied, Watch-Out Rule"]:::process
        SC_Q -->|First| SC_FIRST
        SC_Q -->|Second or immediate| SC_SECOND
        SC_SECOND --> SC_FORMAT
    end

    SA_YES --> DONE([Entry written. Done.]):::startEnd
    SA_NO --> DONE
    SA_HOT --> DONE
    SB_HOT --> DONE
    SB_AAR --> DONE
    SC_FIRST --> DONE
    SC_FORMAT --> DONE
```
