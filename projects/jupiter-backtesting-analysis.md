# Quantitative Research & Backtesting Suite: Jupiter Tennis

**Role:** Quantitative Systems Architect & Research Engineer  
**Focus:** Discrete-Event Simulation, Markovian Transition Modelling, Interactive Analytics  
**Stack:** Python 3.10+, Pandas, NumPy, Streamlit, Plotly, SciPy  
**Status:** Proprietary Research Ecosystem (Codebase private; UI walkthrough, video demonstration, and architectural breakdown below)

---

## 📌 Research Objective

While the Jupiter execution engine manages live exchange order books, quantitative models demand empirical validation against historical tick datasets before deploying risk capital.

The Jupiter Backtesting Suite provides a dedicated simulation and research platform engineered to:
* Reconstruct discrete-time point and game transitions across multi-season ATP and WTA datasets.
* Stress-test order fill matching modes (`REALISTIC` vs `PERFECT`), queue execution styles (`SWEEP`, `IOC`, `FOK`), slippage thresholds, and order timeout expirations.
* Audit real-time mathematical pricing divergence against historical central limit order book (CLOB) odds.
* Model capital compounding curves, trailing trade reinvestment, and multi-factor portfolio health scores.

<p align="center">
  <img src="../assets/jupiter-tennis-backtest-demo.gif" alt="Jupiter Tennis Backtest Execution Demo" width="850"/>
  <br>
  <em>Figure 1: Real-time simulation showing parameter configuration, live match ingestion iterations, running equity ticks, and synchronised diagnostic charts.</em>
</p>

---

## 🎬 Full System Demonstration

For an end-to-end recorded walkthrough of the backtest execution loop, performance scorecard computation, and deep match drill-downs, view the full high-definition video:

> 🎥 **Walkthrough Video:** [Watch the Jupiter Backtesting & Analytics Engine Demo](../assets/jupiter-tennis-backtest-demo.mov)  
> *(Note: You can also drag and drop `jupiter-tennis-backtest-demo.mov` directly into the GitHub browser editor to generate an embedded HTML5 video player).*

---

## 🔬 Modeling Pipeline & Simulation Engine

```text
┌─────────────────────────────────────────────────────────────┐
│                Historical Exchange Raw Data                 │
│     • MongoDB Documents: Scorelines, Volumes, Price Feeds   │
└──────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────┐
│                 Simulated Execution Engine                  │
│  ├── Dynamic Match Processing Iteration                     │
│  ├── CLOB Queue Position & Matching (SWEEP / IOC / FOK)     │
│  ├── Execution Delays & Tick Slippage Enforcement           │
│  └── Trailing Trade-Level Compounding Engine                │
└──────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────┐
│                Analytics & Evaluation Suite                 │
│  ├── Multi-Factor Weighted Scoring Algorithm (0–100)        │
│  ├── Account Equity Trajectory (HV Stepped Line)            │
│  └── Synchronised 4-Pane Match Viewer (Markov, MCI, Volume) │
└─────────────────────────────────────────────────────────────┘

```

### 1. Ingestion & Discrete Fill Emulation
The backtest engine iterates over historical fixtures while enforcing execution constraints via `st.session_state.order_management`:
* **Matching Modes:** Evaluates both `REALISTIC` fill emulation (enforcing book depth liquidity requirements and max matched volume ratios) and zero-friction `PERFECT` baseline modes.
* **Execution Styles:** Tests multi-level `SWEEP` orders, Immediate-Or-Cancel (`IOC`), and Fill-Or-Kill (`FOK`) routines against volatile market books.
* **Friction & Latency:** Simulates network transmission lag via configurable entry and exit delay seconds alongside strict slippage tick bands.

### 2. Capital Management & Trailing Compounding
* **Dynamic Sizing:** Supports fixed stakes, auto-staking percentage allocations, and recovery staking models.
* **Reinvestment Compounding:** Features periodic interval compounding alongside continuous **Trailing Compounding**, dynamically reinvesting configurable percentages of realised net profit on a trade-by-trade basis with absolute upper exposure caps.

---

## 🎯 Quantitative Strategy Scoring Engine

Rather than judging strategies solely by headline ROI, the suite implements a multi-factor weighting algorithm (`scoring.py`) calibrated specifically for sports exchange dynamics. The algorithm projects a composite score out of 100 with dynamic UI styling:

$$\text{Strategy Score} = 0.30(PF_{\text{norm}}) + 0.25(\text{Sharpe}_{\text{norm}}) + 0.25(DD_{\text{norm}}) + 0.10(\text{AvgTrade}_{\text{norm}}) + 0.10(\text{Ratio}_{\text{norm}})$$

```text
Composite Score Matrix
├── 90 – 100 : Gold-Standard Rating  (Gold Glow)
├── 80 – 89  : Excellent Rating      (Green)
├── 70 – 79  : Robust Rating         (Orange)
├── 60 – 69  : Average Rating        (Yellow)
└── 0  – 59  : Subpar Rating         (Red)
```

### Component Normalisation Breakdown:
1. **Profit Factor (30% Weight):** Normalised against an elite threshold of $1.50$. Break-even strategies ($PF \le 1.0$) score zero.
2. **Sharpe Ratio (25% Weight):** Annualised against an elite high-frequency target of $2.0$ ($\text{Mean} / \text{StDev} \times \sqrt{252}$).
3. **Max Drawdown (25% Weight):** Calculates true cumulative peak-to-trough percentage drops ($(\text{Balance} - \text{Peak}) / \text{Peak}$). Penalised linearly ($\max(100 - (|DD\%| \times 1.5), 0)$).
4. **Average Trade Value (10% Weight):** Normalised against an expectancy benchmark of £2.00 per trade on £1,000 base capital.
5. **Market Discovery Ratio (10% Weight):** Evaluates selective edge generation, reaching maximum score when profitable signals are captured in $\ge 50\%$ of evaluated match fixtures.

---

## 📊 Synchronised Multi-Pane Match Viewer

To diagnose individual entry and exit decisions, the workbench renders a high-resolution, 4-tier synchronised Plotly diagnostic canvas:

* **Subplot 1: Price & Odds Trajectory:** Plots historical decimal odds tick-by-tick across Set 1 and Set 2 with vertical dashed line segmentations indicating set completion transitions.
* **Subplot 2: MCI Momentum (%):** Visualises retroactively generated match context and momentum differential indices, benchmarking structural shifts around a 50% median threshold.
* **Subplot 3: Markov Hold Probability Engine:** * Renders discrete-step (`hv`) mathematical hold probabilities per player service game.
  * Dynamically projects the player's historical serve baseline (`Expected Hold %`) as a reference threshold.
  * Monitors the **-40% Jeopardy Trigger**, highlighting structural vulnerability windows and model divergence against exchange pricing.
  * Overlays subtle background vertical rectangles shading the exact start-to-finish service game intervals.
* **Subplot 4: Matched Liquidity Volume (£):** Plots market volume distribution across time, validating that algorithm execution triggers aligned with authentic market depth rather than thin, unmatchable queues.

---

## 📦 Result Export & Metadata Auditing

The system serialises complete backtesting profiles into timestamped JSON payloads (`backtest_results/`), pairing strategy metadata, user session annotations, parameter configurations, and granular trade-by-trade equity logs for version-controlled research tracking.

---

## 🛠️ Stack & Research Tooling

* **Data Engineering:** Python 3.10+, Pandas, NumPy
* **Analytics UI & Visualisation:** Streamlit, Plotly (Subplots & Custom Styling)
* **Statistical Modelling:** Markovian Transition Engines, Multi-Factor Scoring Algorithms
* **Persistence & Architecture:** MongoDB History Deserialisation, JSON Payload Archival
