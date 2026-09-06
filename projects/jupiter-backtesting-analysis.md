# Quantitative Research & Backtesting Suite: Jupiter Tennis

**Role:** Quantitative Systems Architect & Research Engineer  
**Focus:** Historical Market Simulation, Discrete Markovian Modeling, Interactive Analytics  
**Stack:** Python 3.10+, Pandas, NumPy, Streamlit, Plotly  
**Status:** Proprietary Research Ecosystem (Codebase private; UI walkthrough and methodology below)

---

## 📌 Research Objective

While the Jupiter execution engine manages live exchange order flow, quantitative strategies require rigorous empirical validation against historical market dynamics before capital deployment. 

The Jupiter Backtesting Suite is a dedicated research environment engineered to:
* Replay historical exchange tick data through a simulated execution harness.
* Audit Markovian hold and break transition probabilities against live market odds divergence.
* Model capital compounding curves, execution friction, liquidity constraints, and downside drawdowns across multi-tournament datasets.

<!-- STREAMLIT DASHBOARD OVERVIEW -->
<p align="center">
  <img src="../assets/jupiter-backtest-demo.gif" alt="Jupiter Streamlit Backtest Interface" width="850"/>
  <br>
  <em>Figure 1: Streamlit-based interactive backtesting workbench featuring dynamic parameter configuration, capital allocation models, and live simulation streaming.</em>
</p>

---

## 🖥️ Interactive Research Workbench (Streamlit)

The research pipeline provides a dynamic parameter tuning interface built with Streamlit, decoupling model logic from presentation.

### 1. Granular Execution & Risk Controls
The configuration engine exposes four discrete operational parameter layers:
* **Market & Tour Filters:** Dynamic segmentation across ATP and WTA tours, market liquidity minimums (`Min Liquidity Required`), and trade matching ratios (`Max Matched Ratio`).
* **Execution & Matching Settings:** Models exchange queue latency, order timeouts, and maximum allowable slippage ticks during volatile score transitions.
* **Staking & Compounding Engines:** Toggles between fixed liability, periodic compound schedules (e.g. 30-day horizons), and continuous trailing compounding per trade with absolute capital caps.
* **Global Risk Limits:** Configurable circuit-breakers including daily maximum loss thresholds, win streak multipliers, and drawdown tripwires.

---

## 📊 Quantitative Metrics & Performance Diagnostics

The evaluation suite calculates an automated **System Health Score (e.g. 78/100 · Robust Rating)** weighted across capital expansion, consistency, and downside preservation:

| Metric Category | Indicators Captured | Purpose & Interpretation |
| :--- | :--- | :--- |
| **Portfolio Growth** | Total P&L, ROI (%), Compounded Growth | Measures net alpha generation over fixed historical baselines. |
| **Risk-Adjusted Return** | **Sharpe Ratio (1.49)**, **Sortino Ratio (0.22)** | Benchmarks excess return relative to total and downside-only volatility. |
| **Trade Dynamics** | Win Rate (44.2%), Profit Factor (1.38) | Audits statistical expectancy; confirms strategy resilience with asymmetric payouts. |
| **Execution Quality** | Average Trade (£0.66), Avg Win (£8.67) vs Avg Loss (£-4.97) | Validates that payout skew comfortably covers exchange spread friction. |
| **Capital Preservation** | Maximum Drawdown (£-54.46 / -4.48%) | Audits peak-to-trough drawdowns against systemic risk boundaries. |

---

## 📈 Multi-Pane Synchronised Match Viewer

To inspect individual strategy decisions, the platform includes a synchronised, multi-pane diagnostic viewer built in Plotly:

* **Odds & Breakpoint Trajectory:** Plots historical decimal odds tick-by-tick across Set 1 and Set 2, identifying exact moments where market pricing diverges from statistical models.
* **MCI Momentum (%):** Visualises intra-match momentum shifts between competing players, benchmarking pressure curves against serve dynamics.
* **Markov Hold Probability:** Displays dynamic real-time probability curves projected by internal transition models, auditing deviations against theoretical reference thresholds (e.g. *Expected Hold 50.0%*, *-40% Jeopardy Trigger*).
* **Matched Volume Profile:** Displays bar charts of matched liquidity (£) over time to ensure executed signals align with real-world exchange volume rather than thin books.

---

## 🛠️ Stack & Research Tooling

* **Data Engineering & Vectorisation:** Python 3.10+, Pandas, NumPy
* **Visualisation & Analytics UI:** Streamlit, Plotly Graph Objects
* **Statistical Modeling:** Discrete Markov Chain transitions, Custom Weighted Score Algorithms
* **Serialisation:** Structured JSON/CSV backtest run exporters

