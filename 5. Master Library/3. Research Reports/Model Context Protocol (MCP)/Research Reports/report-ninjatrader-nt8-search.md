# NinjaTrader 8 — AI Integration Search Report

**Search conducted:** 2026-04-18
**Researched by:** Rose | Session 60
**Objective:** Find existing tools (MCPs, CLIs, GitHub repos, plugins) that give Claude or an AI agent access to NinjaTrader 8 data or trade execution in near real-time or live data mode — analogous to the TradingView MCP already in the library.

## Top-Level C&P — Ranked Comparison

Two purpose-built NinjaTrader MCP servers exist as of this search date. Both are brand new (April 2026), have minimal community traction, and are independent projects — not affiliated with each other or with NinjaTrader. Neither has gone through any community vetting. That said, they both exist, both claim to do exactly what we need, and one of them (felipekuhn87) has a notably cleaner and more complete architecture.

The felipekuhn87 repo takes the top spot because its design is purpose-built for live execution: it splits the NinjaTrader side into two separate NinjaScript components — one for reading market data (streaming via WebSocket), one for order execution — and bridges both through a Node.js MCP server. That is a well-structured, separation-of-concerns approach. The ozmnf4 repo is also a legitimate MCP server but offers two modes (local desktop and cloud Ecosystem API), which adds flexibility but also complexity. The remaining three candidates are pre-AI tools (Python/JS wrappers for NT8 file or socket APIs) that are useful ecosystem context but are not MCP-native and would require meaningful work to become agent-compatible.

Bottom line: the ecosystem for Claude + NinjaTrader 8 is embryonic. What exists is very new, low-traction, and unvetted. That is not a reason to ignore it — it is a reason to evaluate carefully before committing.

**Ranking: felipekuhn87 > ozmnf4 > TheSnowGuru/CSharpNinja > miasmos/ninjatrader > benlaube/trading-bot-ninjatrader**

---

## Candidate 1 — ninjatrader-claude-mcp-byFelipeKuhn — Top Pick

**URL:** https://github.com/felipekuhn87/ninjatrader-claude-mcp-byFelipeKuhn
**Type:** MCP Server (Node.js bridge + NinjaScript C# components)

### C&P Summary
This is a purpose-built MCP server that connects Claude Code directly to NinjaTrader 8 for both live market data reading and trade execution. It works by installing two NinjaScript files into NinjaTrader — one that streams market data via WebSocket (port 8000) and one that handles order execution (port 8002) — and then running a Node.js bridge that translates between those WebSockets and Claude via MCP protocol. Claude gets 17 tools: market data reading, position status, order entry and management, and indicators. The three-component architecture (NinjaScript data streamer + NinjaScript executor + Node.js bridge) is clean and well-separated. The repo was created April 9, 2026 and has had no further commits since creation. 4 stars as of June 2026 — minimal community traction. For Nick and the NinjaTrader workflow, this is the most directly relevant thing currently available.

### What It Is
A three-component MCP server — two NinjaScript files installed into NT8 plus a Node.js bridge — that gives Claude live market data and trade execution capabilities inside NinjaTrader 8.

### What It Does
- Streams real-time market data via WebSocket from NT8 (port 8000): OHLCV bars, current bar data, bid/ask/last, volume, indicator values, time and sales tape
- Handles order execution via a separate WebSocket (port 8002): enter long/short with risk parameters, adjust stops and targets, set breakeven, cancel orders, flatten positions
- 17 total MCP tools across market reading, order execution, and position management
- Node.js bridge connects Claude to both NT8 WebSocket streams via stdio (MCP protocol)
- Manual installation of two NinjaScript files required into NT8
- **Stars:** 4 | **Forks:** 0 | **Language:** C# (NinjaScript) + JavaScript (bridge) | **License:** None
- **Created:** 2026-04-09 | **Last pushed:** 2026-04-09 | *(Stars as of June 2026 — slow growth, no further commits since creation)*

### MCP Tool Manifest — Candidate 1 (felipekuhn87)

- **Tool count:** 17 tools
- **Tools:**
  - `get_market_data` — Read current OHLCV bar, bid/ask/last, and volume from NT8 data stream (port 8000)
  - `get_current_bar` — Get current bar data for a configured instrument
  - `get_indicator_value` — Retrieve a configured indicator's current value
  - `get_time_sales` — Read time and sales tape data
  - `get_position_status` — Check current open position size and direction
  - `get_account_info` — Get account balance, buying power, and P&L
  - `enter_long` — Enter a long position with configured risk parameters
  - `enter_short` — Enter a short position with configured risk parameters
  - `adjust_stop` — Adjust the stop loss on the current position
  - `adjust_target` — Adjust the profit target on the current position
  - `set_breakeven` — Move stop loss to breakeven on the current position
  - `cancel_order` — Cancel a specific pending order by ID
  - `cancel_all_orders` — Cancel all pending orders
  - `flatten_position` — Close the current position immediately at market
  - `get_orders` — List all current open and pending orders
  - `get_fills` — Retrieve filled order history for the session
  - `get_connection_status` — Check NT8 WebSocket connection health on both ports
- **Transport type:** stdio (Node.js bridge connecting to NT8 WebSocket streams on ports 8000 and 8002)
- **settings.json registration:**
```json
{
  "mcpServers": {
    "ninjatrader-mcp": {
      "command": "node",
      "args": ["/path/to/ninjatrader-claude-mcp-byFelipeKuhn/index.js"]
    }
  }
}
```
Note: Requires manual installation of two NinjaScript .cs files into NT8. Soren C# file review is a hard gate before any NT8 installation — demo, paper, or live.

### Relevance to This Project
Directly relevant. Nick (NinjaTrader specialist) needs exactly this kind of interface: live data in, execution out, Claude as the brain. The WebSocket-based data streaming is the right architecture for near-real-time use. File-polling approaches (NT8 old AT Interface) add latency and complexity. This is the closest thing to a TradingView MCP equivalent for NT8 that currently exists.

### Security Preliminary
- **No license.** All-rights-reserved by default.
- **Brand new, single developer, zero community history.** Provenance essentially unknown.
- **NinjaScript files install directly into NT8 with full platform access** — highest-risk surface in the stack. Soren must review both .cs files carefully before these go anywhere near a live NT8 instance. This is non-negotiable.
- **WebSocket ports 8000 and 8002 opened on the local machine** — standard for this type of integration but worth noting as a local network exposure surface.
- No tests, no CI, no audit trail.

### Recommendation
High-priority Soren review candidate. File in Section 4 (MCP Servers) as a Tier 2 item — valuable when the NinjaTrader workflow phase begins, but security clearance required before any deployment. Do not install NinjaScript files into NT8 without Soren sign-off.

---

## Candidate 2 — ninjatrader-mcp (ozmnf4)

**URL:** https://github.com/ozmnf4/ninjatrader-mcp
**Type:** MCP Server (Node.js, dual-mode: local desktop + cloud Ecosystem API)

### C&P Summary
This is a Node.js MCP server that gives Claude access to NinjaTrader in two modes: local desktop mode (connects to a NinjaScript HTTP server running in NT8 on port 7890) and cloud mode (uses NinjaTrader official Ecosystem API). In local mode it exposes 20+ tools including account info, positions, orders, real-time quotes, historical OHLCV bars, and NinjaScript indicator values. In cloud mode it uses NT official API credentials. The dual-mode design is flexible but means local mode still requires a NinjaScript add-on installed separately. Created April 5, 2026, 17 stars and 5 forks as of June 2026 — more community traction than Candidate 1 but no new commits since creation. No license. Less architecturally clean than felipekuhn87 but potentially more flexible due to the cloud API option.

### What It Is
A dual-mode Node.js MCP server that connects Claude to NinjaTrader 8 through either a local HTTP bridge inside NT8 or NinjaTrader cloud Ecosystem API.

### What It Does
- Local mode: connects to a NinjaScript add-on running an HTTP server inside NT8 on port 7890
- Cloud mode: connects via NinjaTrader official Ecosystem API with credentials
- 20+ MCP tools: account management, position monitoring, order placement/modification/cancellation, real-time quotes, historical OHLCV bars, market depth/order book, NinjaScript indicator values, health check
- Environment variable configuration for mode switching
- **Stars:** 17 | **Forks:** 5 | **Language:** JavaScript | **License:** None
- **Created:** 2026-04-05 | **Last pushed:** 2026-04-05 | *(Stars/forks as of June 2026 — more traction than Candidate 1, still no new commits since creation)*

### MCP Tool Manifest — Candidate 2 (ozmnf4)

- **Tool count:** 20+ tools (local mode and cloud mode expose similar tool sets)
- **Tools (representative):**
  - `get_account_info` — Account balance, buying power, P&L, and account status
  - `get_positions` — List all open positions and their details
  - `get_orders` — List all pending and filled orders
  - `place_order` — Place a new order (market, limit, stop) on a configured instrument
  - `modify_order` — Modify price or quantity of an existing order
  - `cancel_order` — Cancel a specific order by ID
  - `cancel_all_orders` — Cancel all open orders
  - `get_real_time_quote` — Get live bid/ask/last for an instrument (local mode)
  - `get_historical_bars` — Retrieve historical OHLCV bar data for a given timeframe
  - `get_market_depth` — Retrieve DOM (Depth of Market / order book) data
  - `get_indicator_values` — Get NinjaScript indicator current values
  - `get_instrument_info` — Retrieve instrument metadata (tick size, point value, etc.)
  - `health_check` — Check NT8 bridge connection status (port 7890 for local mode)
  - `switch_mode` — Switch between local desktop mode and cloud Ecosystem API mode
  - *(additional tools vary by mode; cloud mode exposes NT Ecosystem API endpoints)*
- **Transport type:** stdio (Node.js; local mode connects to NT8 HTTP bridge on port 7890; cloud mode connects to NinjaTrader Ecosystem API)
- **settings.json registration:**
```json
{
  "mcpServers": {
    "ninjatrader-mcp": {
      "command": "node",
      "args": ["/path/to/ninjatrader-mcp/index.js"],
      "env": {
        "MODE": "local",
        "NT8_PORT": "7890"
      }
    }
  }
}
```
Note: Local mode requires NinjaScript add-on installed in NT8 (Soren C# review = hard gate). Cloud mode requires NinjaTrader Ecosystem API credentials — separate credential management design required before any live API deployment.

### Relevance to This Project
Similar relevance to Candidate 1. The cloud mode option is notable: if NT8 is running on a remote machine, cloud mode via the Ecosystem API avoids local port exposure. That could matter for Nick workflow depending on how the trading setup is structured.

### Security Preliminary
- **No license.** Same default all-rights-reserved concern.
- **Very new, zero community history.** Same provenance concerns as Candidate 1.
- **Local mode opens port 7890 inside NT8** — same local network exposure pattern.
- **Cloud mode uses NinjaTrader Ecosystem API credentials** — live API keys for a trading account. Key management and storage must be reviewed carefully.
- **NinjaScript add-on required for local mode.** Soren must review before any NT8 installation.

### Recommendation
File in Section 4 (MCP Servers) as a Tier 2 item alongside Candidate 1. The dual-mode design gives it a different risk/flexibility profile. Soren review required before deployment. Nick should evaluate both candidates together when the NinjaTrader workflow phase begins.

---

## Candidate 3 — CSharpNinja-Python-NinjaTrader8-trading-api-connector (TheSnowGuru)

**URL:** https://github.com/TheSnowGuru/CSharpNinja-Python-NinjaTrader8-trading-api-connector-drag-n-drop
**Type:** Python/C# Bridge (pre-AI, not MCP-native)

### C&P Summary
A drag-and-drop connector that links NinjaTrader 8 to Python via a C# DLL and socket-based communication. Not an MCP server and not built for AI agents — it predates that ecosystem. Gives Python scripts bidirectional access to NT8: account data, tick and candle data, orders, and positions. Stars: 18. Last updated July 2024. Could serve as a data access layer that a Pete-written Python script talks to — but would require a custom MCP or CLI wrapper to become Claude-native. Worth knowing about as ecosystem context; not a direct install candidate.

### What It Is
A C# DLL plus socket-based connector that exposes NinjaTrader 8 data and execution to external Python applications.

### What It Does
- Bidirectional socket communication between NT8 (C# strategy) and external code
- Exposes: account info, tick/candle data, instrument metadata, positions, orders
- Order operations: open, close, modify, stop-loss/take-profit adjustment
- Demo version supports 5 currency pairs + DAX; paid version presumably broader
- Discord community and documentation provided
- **Stars:** 18 | **Last updated:** Jul 2024 | **Language:** C#/Python

### Relevance to This Project
Indirect. Pete (Python/quant) could use this as the NT8 data access layer for a Python-based agent workflow, but it would need a MCP or CLI wrapper to be Claude-native. The most established Python-NT8 connector in the search results.

### Security Preliminary
- More established than the April 2026 MCPs (18 stars, Discord community).
- Socket-based communication from NT8. Standard pattern.
- Demo/paid split suggests a commercial product — license terms should be reviewed before any use.

### Recommendation
Section 8 (Alternative Tools) — awareness item for Pete and Nick. Not an active build candidate but useful reference for how Python-NT8 connectivity was solved before MCP existed.

---

## Candidate 4 — ninjatrader JS wrapper (miasmos)

**URL:** https://github.com/miasmos/ninjatrader
**Type:** JavaScript npm package (file API wrapper, pre-AI)

### C&P Summary
A lightweight TypeScript npm package wrapping NinjaTrader 8 file-based AT Interface (Automated Trading Interface). Handles orders, positions, and connection status through file polling — not WebSockets. Last commit 2021, 23 stars. Could be used as a data layer for a Node.js MCP server but file-polling is slow and unreliable for near-real-time data. The ozmnf4 and felipekuhn87 MCPs are both better architectures.

### What It Is
A TypeScript npm package wrapping NT8 file-based AT Interface for order placement and position tracking from Node.js.

### What It Does
- Place and cancel market/limit orders with stop-loss
- Track order status (filled, rejected) and position changes via file polling
- Connection status monitoring for NT8 data feeds
- npm installable; class-based API
- **Stars:** 23 | **Last updated:** Jun 2021 | **Language:** TypeScript

### Relevance to This Project
Low. File-based polling is not suitable for near-real-time data. Useful as historical reference for how the NT8 file API works but outclassed by WebSocket-based approaches.

### Security Preliminary
- Older repo with more community history.
- File API access requires NT8 AT Interface to be enabled — local only, no external network exposure.
- No obvious red flags.

### Recommendation
Not worth filing. Awareness only — documents a valid but outdated NT8 integration pattern.

---

## Candidate 5 — trading-bot-ninjatrader (benlaube)

**URL:** https://github.com/benlaube/trading-bot-ninjatrader
**Type:** Rules-based trading bot (Tradovate/NinjaTrader Cloud API, not MCP)

### C&P Summary
A rules-based automated trading bot for MNQ and MES futures using Tradovate and NinjaTrader Cloud APIs. Not an MCP server. Not built for Claude or AI agents. A standalone bot with its own logic that uses NT cloud API as its execution backend. Low stars (3), last updated November 2025. Included here because it confirms that NinjaTrader cloud API is being used by the broader community for bot execution — relevant context for the ozmnf4 MCP cloud mode.

### What It Is
A standalone rules-based futures trading bot using Tradovate/NinjaTrader Cloud API for MNQ and MES execution.

### What It Does
- Automated futures trading for MNQ/MES
- Uses Tradovate and NinjaTrader Cloud API for execution
- Rules-based, not AI-driven
- **Stars:** 3 | **Last updated:** Nov 2025

### Relevance to This Project
Minimal. Confirms cloud API usage patterns. Not a Claude integration target.

### Security Preliminary
Low stars, limited community review. Standard caution applies.

### Recommendation
Not worth filing. Ecosystem context only.

---
*Report by Rose | Session 60 | 2026-04-18*

---

## Soren Formal Security Review — NinjaTrader NT8 Search

**Date:** 2026-04-18
**Reviewer:** Soren

### Overall Assessment

The NT8 MCP candidate pool presents the highest-risk security profile in this research batch — by a significant margin. The core issue is architectural: both viable candidates require NinjaScript C# files to be installed directly inside NinjaTrader 8, which runs them with full platform access. Unlike an MCP server that reads local files or queries an API, code deployed inside NT8 operates within a live trading platform connected to real brokerage accounts and real money. A malicious or buggy NinjaScript file has access to the order execution layer. There is no sandbox. Additionally, both candidates were created by single developers within the last two weeks, carry no licenses, have zero community vetting history, and have never been reviewed by anyone outside the original author. The broader NT8 MCP ecosystem is embryonic — that is not disqualifying, but it means none of the normal trust signals (sustained community use, external audits, forks showing adoption) are present. Both candidates require Soren's full deployment-time scan of the NinjaScript C# files before any installation into NT8 proceeds. That scan is non-negotiable regardless of what this pre-deployment review finds.

---

### Candidate 1 — felipekuhn87/ninjatrader-claude-mcp-byFelipeKuhn
**Verdict:** FLAG

- No license declared. All-rights-reserved by default. Legal exposure if the C# files contain code lifted from third-party sources.
- Created 2026-04-09. Single developer. 4 stars, 0 forks as of June 2026. No new commits since creation. No community review. Provenance is essentially unknown — there is no established track record for this author.
- The three-component architecture (NinjaScript data streamer + NinjaScript executor + Node.js bridge) is well-separated by design, which is a point in its favor. Clean architecture reduces the likelihood of unintentional execution surface, but does not eliminate the risk from intentional malicious code.
- Two NinjaScript (.cs) files install directly into NT8 with full platform access. These files must be read line-by-line by Soren at deployment time. This is the primary risk surface — a C# file inside NT8 can place orders, cancel orders, and access all account data. No installation proceeds without that scan.
- WebSocket ports 8000 (data) and 8002 (execution) opened on the local machine. Standard pattern for this integration type. Acceptable if the machine is not externally accessible; confirm firewall scope before deployment.
- Node.js bridge exposes 17 MCP tools to Claude — market data, order entry, position management. The breadth of the execution surface is appropriate for the use case but should be scoped carefully: Claude should only be able to call tools the workflow actually requires.
- No tests, no CI, no audit trail. Means errors — whether bugs or something worse — are harder to detect post-deployment.
- FLAG condition: NinjaScript files must be reviewed in full at deployment. No installation into NT8 — demo, paper, or live — before that review is complete. License status should be resolved before any code from this repo is adapted or redistributed.
- **DORMANCY NOTE (2026-06-08):** Zero commits since repo creation on 2026-04-09 — dormant from day one. This is now confirmed across two review cycles. Dormancy does not change the security flags; the NinjaScript scan requirement is unchanged. However, if the repo remains inactive at the time of deployment evaluation, the team should factor in the absence of any bug fixes, dependency updates, or author responsiveness before committing to this candidate. Re-evaluate activity status at the start of the NinjaTrader workflow phase.
- *Re-reviewed 2026-06-08 — FLAG verdict confirmed. Dormancy reinforced with extended inactivity data. All original flag conditions unchanged and still in force.*

---

### Candidate 2 — ozmnf4/ninjatrader-mcp
**Verdict:** FLAG

- No license declared. Same all-rights-reserved exposure as Candidate 1.
- Created 2026-04-05. Single developer. 17 stars, 5 forks as of June 2026 — more traction than Candidate 1 but no new commits since creation. No community review. Slightly older than Candidate 1 but the provenance concern is identical.
- Dual-mode design (local desktop via NinjaScript HTTP server on port 7890, plus cloud mode via NinjaTrader Ecosystem API) adds deployment flexibility but also adds credential management risk that Candidate 1 does not have.
- Local mode: NinjaScript add-on installs inside NT8 on port 7890. Same rule applies — Soren must review the NinjaScript files in full at deployment time before any NT8 installation.
- Cloud mode: uses NinjaTrader Ecosystem API credentials (live API keys for a brokerage account). This is a meaningful escalation in risk. API key storage, rotation policy, and access scope must all be defined before cloud mode deployment. Keys must never be hardcoded; environment variable handling should be reviewed for correct scoping.
- 20+ MCP tools exposed to Claude. Broader tool surface than Candidate 1. Review which tools cloud mode exposes specifically — live brokerage API keys paired with broad tool access is the highest-risk configuration in this entire batch.
- FLAG conditions: (1) NinjaScript files for local mode require full Soren review before any NT8 installation. (2) Cloud mode requires a separate credential management review — key storage, rotation, and access scoping — before any live-API deployment. Nick should evaluate both candidates together; the cloud mode option may suit specific workflow needs but carries its own distinct risk layer.
- **DORMANCY NOTE (2026-06-08):** Zero commits since repo creation on 2026-04-05 — dormant from day one. Confirmed across two review cycles. Same dormancy evaluation guidance as Candidate 1 applies here. Cloud mode credential risk flag is unchanged and remains the highest-risk configuration in this batch regardless of repo activity.
- *Re-reviewed 2026-06-08 — FLAG verdict confirmed. Dormancy reinforced with extended inactivity data. All original flag conditions unchanged and still in force.*

---

### Candidate 3 — TheSnowGuru (awareness only, not filing)
**Verdict:** AWARENESS — not filing

- More established than the April 2026 MCPs (18 stars, Discord community, last updated July 2024). The longer history provides slightly more confidence, but community size is still small.
- Demo/paid licensing split needs review before any use — commercial terms may restrict adoption.
- C# DLL and socket-based communication from NT8. Same general architectural concern as the MCP candidates: code inside NT8 with platform access. Any future evaluation should include a DLL source review.
- Not an MCP-native tool. If Pete ever evaluates this as a Python-NT8 data layer, Soren review of the DLL and C# components applies before deployment.
- No current action required. Awareness item only.

---

### Candidates 4 & 5 — miasmos, benlaube (not filing)
**Verdict:** AWARENESS — not filing

- miasmos/ninjatrader: File-polling approach via NT8 AT Interface. No external network exposure beyond the local machine. Older repo (2021), more community history than the April 2026 candidates, but outclassed by WebSocket-based architectures. No current deployment path; no security action required.
- benlaube/trading-bot-ninjatrader: Rules-based trading bot using NinjaTrader Cloud API. Not Claude-native, not an MCP candidate. Low stars (3), limited review. If this code is ever referenced as a cloud API pattern, the credential handling should be reviewed. No current action required.

---

### Soren's Recommendation to Sage

Two items need to reach Jay before any NinjaTrader MCP work begins.

First: the pre-deployment scan requirement is a hard gate. Neither felipekuhn87 nor ozmnf4 installs into NT8 — demo, paper, or live — without Soren reviewing the NinjaScript C# files line by line. This is not a standard caution note. NinjaScript runs inside the trading platform with full order execution access. That scan happens at deployment time, per project policy, and it is non-negotiable regardless of what the workflow timeline looks like.

Second: the ozmnf4 cloud mode specifically needs a credential management design before it is deployed in any form using live NinjaTrader Ecosystem API keys. Jay should know this mode exists and carries a distinct risk profile from local mode. If the NinjaTrader workflow phase plans to use cloud mode, that design work happens before keys are generated or stored anywhere.

Both candidates are cleared to file in Section 4 as Tier 2 items with FLAG status noted. Filing is not deployment. They are available for Nick and the team to evaluate when the NinjaTrader workflow phase begins. Deployment requires the scans described above. Note: as of June 2026, neither repo has received any new commits since creation (April 2026) — both remain dormant. The security posture flags are unchanged; the inactivity adds a maintenance risk note.

---

## Report Version Log
| Version | Date | What Changed |
|---------|------|--------------|
