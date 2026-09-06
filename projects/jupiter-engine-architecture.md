# Systems Architecture: Jupiter Event-Driven Trading Engine

**Role:** Quantitative Systems Architect & Systems Engineer  
**Focus:** Dual Ingestion (WebSockets & REST), Finite State Machines, Mobile Remote C2  
**Stack:** Python 3.10+, Asynchronous WebSockets, REST APIs, Telegram Bot API, Linux (Vultr VPS)  
**Status:** Proprietary Commercial Infrastructure (Codebase private; architectural breakdown and metrics below)

---

## 📌 Architectural Overview

Jupiter is an automated, event-driven algorithmic trading engine engineered for high-frequency prediction markets and central limit order book (CLOB) sports exchanges. 

Operating in fast-paced live sports markets introduces severe operational risks: REST polling rate limits, API timeouts, slippage during critical game points, and state ambiguity. Jupiter neutralises these bottlenecks by combining a dual-mode ingestion layer (hybrid WebSocket push streaming with fallback REST polling), a deterministic Finite State Machine (FSM), and a plug-and-play strategy interface.

<p align="center">
  <img src="../assets/jupiter-tennis-ssh-terminal.png" alt="Jupiter Production Daemon on Linux VPS" width="850"/>
  <br>
  <em>Figure 1: Production daemon initialising on Linux VPS, compiling scenario matrix into RAM and spinning up session threads.</em>
</p>

---

## 🏗️ Ingestion & Execution Pipeline

The architecture strictly decouples market ingestion, execution logic, and remote operator controls.

<!-- Replace the path below once you export your diagram from Lucidchart -->
<p align="center">
  <img src="../assets/jupiter-system-pipeline.png" alt="Jupiter System Pipeline Diagram" width="850"/>
  <br>
  <em>Figure 2: End-to-end execution pipeline from exchange push feeds to local state cache and remote controls.</em>
</p>

### 1. Dual Ingestion Layer: Streaming & Polling
* **Low-Latency Push Streaming:** Leverages direct TLS WebSockets with packet conflation (configurable, down to 500ms intervals) to capture market depth updates and order fill confirmations without polling overhead.
* **Automated REST Fallback:** Maintains a thread-safe REST polling engine (configurable interval, default 2s) to dynamically audit exchange state, verify token authorisations, and provide resilience against WebSocket disconnections.
* **Local In-Memory Cache:** Subscribes to private execution streams to locally track gross profit, exposure limits, and pending order expirations, avoiding external network hops during critical risk calculations.

---

## 🔄 Deterministic Finite State Machine (FSM)

To prevent race conditions, duplicate execution, or over-exposure during high-volatility events, every active market operates within a rigid state machine:

| State | Operational Behaviour | Concurrency Lock |
| :--- | :--- | :--- |
| **`OBSERVATION`** | Flat position (£0 liability). Stream listeners parse price delta matrices and order books against strategy parameters. | Unlocked |
| **`TRANSACTION`** | **Critical Mutex Lock.** Mid-API call dispatch (entry or hedge). Engine is locked to eliminate duplicate orders or race conditions. | **LOCKED** |
| **`PENDING_ENTRY`** | Order dispatched. Engine awaits the private Order Stream to confirm matched or partially matched volume. | Partially Locked |
| **`MANAGEMENT`** | Active exposure. Continuously calculates stop-loss, profit-take targets, and trailing hedging triggers. | Unlocked |
| **`PENDING_EXIT`** | Neutralisation order submitted. Synchronising with execution streams to confirm exposure return to zero. | **LOCKED** |

<!-- VIDEO OR GIF OF THE MATCH POSITION AUTO-CLOSING -->
<p align="center">
  <img src="../assets/jupiter-auto-close-trade.gif" alt="Automated Trade Cashout and Telegram Alert" width="350"/>
  <br>
  <em>Figure 3: Live match execution showing algorithmic position exit, automated profit neutralisation, and sub-second alert dispatch.</em>
</p>

---

## 📱 Mobile Command & Control (C2) and Operations

Rather than relying on local GUI dependencies, Jupiter features a fully headless, mobile-first operations interface built on the Telegram Bot API.

<table>
  <tr>
    <td width="33%" align="center">
      <img src="../assets/telegram-controller.png" alt="Main Dashboard C2" />
      <br><strong>System Control Hub</strong>
    </td>
    <td width="33%" align="center">
      <img src="../assets/telegram-controller-live-matches.png" alt="Active Session Routing" />
      <br><strong>Session Discovery</strong>
    </td>
    <td width="33%" align="center">
      <img src="../assets/telegram-controller-live-match.png" alt="Runtime Parameter Adjustment" />
      <br><strong>Per-Market Overrides</strong>
    </td>
  </tr>
</table>

* **Dynamic In-Flight Parameter Tuning:** Operators can toggle auto-staking, modify maximum stake liability, alter sweep levels, and adjust order expiry timeouts directly from mobile devices without restarting background daemons.
* **Isolated Asynchronous Communications:** Notifications, P&L reporting, and alerts operate inside an independent `asyncio` event loop to guarantee messaging delays never block exchange execution threads.

<p align="center">
  <img src="../assets/telegram-alerts.png" alt="Automated Trade Logs and Realised PnL" width="450"/>
  <br>
  <em>Figure 4: Asynchronous order dispatch logs, automated cashouts, and final P&L reconciliation alerts.</em>
</p>

---

## 🧠 Pluggable Strategy Architecture

The engine decouples core execution mechanics from mathematical and quantitative strategies using a modular registry pattern:

* **Modular Strategy Interface:** Isolated execution pipelines that inherit standard trade parameters, market state subscriptions, and order dispatch abstractions without exposing underlying alpha logic.
* **Pre-Loaded Scenario Matrices:** Pre-computes thousands of scenario transition matrices directly into RAM (e.g. 6,000+ ATP scenarios) upon system initialisation, ensuring sub-millisecond evaluation against live ticks without runtime database lookups.
* **Dynamic Registration:** New quantitative models, volatility triggers, and machine learning scoring mechanisms can be registered into the system registry seamlessly without modifying the core state engine or network adapters.
