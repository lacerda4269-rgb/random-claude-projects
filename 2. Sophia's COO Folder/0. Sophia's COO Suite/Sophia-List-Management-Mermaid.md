=======================================================================
  MERMAID CODE
  Workflow: Sophia's Pending and Completed Lists
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

    START([Something needs to be captured]):::startEnd
    Q{What kind of thing?}:::decision
    START --> Q

    Q -->|Source material change\nsoul, SOP, MG, template, CLAUDE.md| TRIAGE
    Q -->|Operational trap or recurring gap| GOTCHA_Q
    Q -->|Agent lesson| TLL_START
    Q -->|Sage lesson| SAGE_L["Route to lessons.md or lessons_global.md\nSee Lessons and Gotcha Routing workflow"]:::process

    subgraph PC["  PENDING CHANGES — TRIAGE  "]
        TRIAGE{Rate 0 to 10}:::decision
        T_NOW["0 to 2: Handle NOW\nDo immediately\nGoes straight to Completed Changes"]:::process
        T_DISCUSS["3 to 4: C&P Discussion\nSophia surfaces for quick call\nDecide: do now or queue"]:::process
        T_QUEUE["5+: Standard Queue\nAdd to correct section in Pending Changes"]:::process
        TRIAGE -->|0-2| T_NOW
        TRIAGE -->|3-4| T_DISCUSS
        TRIAGE -->|5+| T_QUEUE
    end

    T_QUEUE --> SEC_Q{Section assignment}:::decision
    SEC_Q -->|Working on it this session| SEC1[Section 1: ACTIVE]:::process
    SEC_Q -->|Named activation point before close| SEC2[Section 2: DEFERRED NAMED]:::process
    SEC_Q -->|AAR only — true post-project| SEC5[Section 5: PENDING AAR]:::process
    SEC_Q -->|No named home yet| SEC3[Section 3: DEFERRED NO HOME]:::process
    SEC_Q -->|Behavioral standard not yet formalized| SEC6[Section 6: BEHAVIORAL STANDARDS ACTIVE]:::process
    SEC_Q -->|Project notes, goals, or operator observations| SEC4[Section 4: NOTES & OBJECTIVES]:::process

    subgraph XFER["  TRANSFER — Pending to Completed  "]
        TR_TRIG["Trigger: Session Close — primary\nAlso: Jay request, COHK, AAR\nNEVER mid-session or compact"]:::process
        TR_Q{Item at terminal status?\nComplete or Closed?}:::decision
        TR_NO[Not eligible — stays on Pending Changes]:::process
        TR_BATCH["Sophia presents batch to Sage — Sage confirms\nSophia moves items to Completed Changes\nUpdates Quick Stats on both files"]:::process
        TR_TRIG --> TR_Q
        TR_Q -->|NO| TR_NO
        TR_Q -->|YES| TR_BATCH
    end

    subgraph GOTCHA["  GOTCHA.MD  "]
        GOTCHA_Q{First or second+ occurrence?}:::decision
        GOTCHA_1[First: correct and move on]:::process
        GOTCHA_2["Second+ or immediate trap:\nSophia logs same session"]:::process
        GOTCHA_FMT["Format: Type, Counter, Status\nWhat Happened, Root Cause\nFix Applied, Watch-Out Rule"]:::process
        GOTCHA_Q -->|First| GOTCHA_1
        GOTCHA_Q -->|Second or immediate| GOTCHA_2 --> GOTCHA_FMT
    end

    subgraph TLL["  TEAM LESSONS LOG  "]
        TLL_START[Agent reports lesson to Sage]:::process
        TLL_LOG[Sophia logs same session]:::process
        TLL_Q{Clearly universal AND agent-specific?}:::decision
        TLL_HOT["HOT PATH: Sage updates agent soul\nSophia marks as promoted"]:::process
        TLL_AAR["Mark: AAR — pending review"]:::process
        TLL_START --> TLL_LOG --> TLL_Q
        TLL_Q -->|YES| TLL_HOT
        TLL_Q -->|NO| TLL_AAR
    end
```
