=======================================================================
  MERMAID CODE
  Workflow: Research Report Request Pipeline
  Version: v1.1 — 2026-05-31 (CQC-A: fact-finding report storage routing added at point of delivery)
  How to use: Copy everything inside the code block below.
               Paste into mermaid.live. Export as PNG.
=======================================================================

```mermaid
%%{init: {'theme': 'dark', 'themeVariables': {'primaryColor': '#1E3A5F', 'primaryTextColor': '#ffffff', 'primaryBorderColor': '#4A9EFF', 'lineColor': '#7EB8D4', 'secondaryColor': '#1A2744', 'tertiaryColor': '#1A2744'}}}%%
flowchart TD
    classDef startEnd fill:#00695C,stroke:#004D40,color:#ffffff
    classDef process fill:#1565C0,stroke:#0D47A1,color:#ffffff
    classDef decision fill:#E65100,stroke:#BF360C,color:#ffffff

    START([Agent identifies research need]):::startEnd
    RULE["Cardinal Rule: Agents NEVER contact Rose directly\nAll requests route through Sage first"]:::process
    START --> RULE

    subgraph P1["  PART 1 — REQUEST SUBMISSION  "]
        SUBMIT["Agent submits to Sage:\nWhat, why, format needed"]:::process
        CEQ{CEO Relevance Check:\nAligned with agent domain and current task?}:::decision
        REJECT([Request rejected\nSage returns with explanation]):::startEnd
        SUBMIT --> CEQ
        CEQ -->|NO| REJECT
    end

    CEQ -->|YES| R1

    subgraph P2["  PART 2 — ROSE EXECUTES  "]
        R1["Step 1: Receive and Clarify\nScope, format, depth, constraints"]:::process
        R1Q{Anything unclear?}:::decision
        R1ASK[Stop — ask Sage before searching]:::process
        R2["Step 2: Research\nPrioritize authoritative and recent sources\nDate all information"]:::process
        R3{Step 3: Classify Output\nAnything downloadable or deployable?}:::decision
        RESOURCE["Resource Report\ntool, CLI, MCP, script, file"]:::process
        FACTFIND["Fact-Finding Report\ninformation only"]:::process
        R4["Step 4: Compile Report\nTask Summary — Output Type — Findings\nC&P Summary — Sources — Additional Findings"]:::process
        R1 --> R1Q
        R1Q -->|YES| R1ASK
        R1Q -->|NO| R2
        R2 --> R3
        R3 -->|YES or UNCLEAR| RESOURCE
        R3 -->|Clearly NO| FACTFIND
        RESOURCE --> R4
        FACTFIND --> R4
    end

    R4 --> DELIVER["Rose delivers to Sage\nStates output type in delivery"]:::process
    DELIVER --> ROUTE{Sage routes by output type}:::decision

    ROUTE -->|Fact-Finding Report| SAGE_DIRECT["Sage reviews directly\nNo Soren involved"]:::process
    ROUTE -->|Resource Report| SOREN_R["Soren — Security Review"]:::process
    SOREN_R --> SOREN_Q{Cleared?}:::decision
    SOREN_Q -->|NOT CLEARED| REJECT2([Resource rejected\nDoes not enter library\nSage handles]):::startEnd
    SOREN_Q -->|CLEARED| LEXI["Lexi catalogs in Master Library\nFull Database + Quick Reference + C&P Summary"]:::process

    LEXI --> SOPHIA_LOG["Sophia logs resource to:\nProject Resources Log"]:::process
    SOPHIA_LOG --> ACQ_DONE["Sage reviews — acquisition complete"]:::process
    ACQ_DONE -.->|If Cosmo build triggered| DIAG12(["→ See the Cosmo Build Pipeline\ndiagram (Cosmo-Skill-Creator-Mermaid.md)"]):::startEnd

    SAGE_DIRECT --> RPT_ROUTE{Report storage routing}:::decision
    RPT_ROUTE -->|Project-specific| WORKTREE_STORE["File to WorkTree\nProject-scoped research"]:::process
    RPT_ROUTE -->|Universal value| ML12_STORE["File to ML Folder 12\nUniversal Research Reports"]:::process
    WORKTREE_STORE --> DONE([Findings delivered. Project continues.]):::startEnd
    ML12_STORE --> DONE
    ACQ_DONE --> DONE
```
