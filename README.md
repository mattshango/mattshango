# Matthew Enubuje
### Technical Writer & Quantitative Data Analyst

Hi, I'm Matthew 👋

I operate at the intersection of **quantitative systems engineering**, **machine learning research**, and **developer documentation**. 

My core domain expertise spans **prediction markets and sports exchange infrastructure**, **Real-World Asset (RWA) tokenisation protocols**, and **applied artificial intelligence**. Whether engineering event-driven execution daemons running on headless Linux VPS environments, training deep sequence models across 40M+ exchange ticks, or authoring institutional GitBook architecture for decentralised finance, I focus on turning complex technical mechanics into clear, structured, and production-ready systems.

---

### ⚡ Domain Expertise & What I Do

* **Sports Prediction Markets & Exchange Infrastructure:** Architecting event-driven WebSocket engines, deterministic finite state machines (FSM), order book liquidity models, and custom backtesting pipelines in Python.
* **Real-World Asset (RWA) Protocols & Web3:** Translating complex smart contract interactions, overcollateralisation logic, algorithmic stabilisation, and liquidation mechanisms into structured developer-first documentation.
* **Applied AI & Deep Sequence Modelling:** Researching market microstructure inefficiencies using PyTorch (Context-Aware GRUs), temporal heartbeat alignment, NLP sentiment scoring, and LLM evaluation.

---

### 📬 Connect With Me

<a href="https://www.linkedin.com/in/matthew-e-7b161410b/" target="_blank" rel="noopener noreferrer"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"/></a>
<a href="mailto:matthew_enubuje@outlook.com"><img src="https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"/></a>

📍 **Location:** London, UK (Open to remote and hybrid technical writing / quantitative data roles)

---

## 🎓 Education & Academic Research

### Master of Science (MSc) in Computer Science with Artificial Intelligence
**University of Wolverhampton** | *Specialisation: Deep Sequence Modelling & Applied NLP*

#### 📄 Academic Research & Pre-prints

* **Discovering Short-Term Inefficiencies in High-Frequency Sports Markets via Deep Sequence Modelling** *Author:* Matthew Enubuje  
  *Focus:* Context-Aware Recurrent Architectures, Multivariate Time-Series, Limit Order Book Microstructure  
  * **Abstract:** Architected a PyTorch Context-Aware Gated Recurrent Unit (GRU) to forecast $\ge 0.20$ implied probability drops within 300-second windows across 40M+ ATP tick records. Achieved an average Out-of-Sample Walk-Forward Optimisation ROI of **+257.10%** across 16,500+ blind evaluation trades under a 1:2 risk/reward framework.  
  📁 <a href="https://docsend.com/view/b8naukekju6wbpre" target="_blank" rel="noopener noreferrer">**Read Full Paper (Instant Access via DocSend)**</a>

* **Sentiment Analysis in Tennis: Correlating Sentiment Scores with Match Outcomes and Odds Movements** *Author:* Matthew Enubuje  
  *Focus:* Natural Language Processing, VADER Lexicon Modelling, K-Means Volatility Clustering  
  * **Abstract:** Analysed live fan sentiment during professional tournaments by pairing streamed social text data with set-by-set exchange odds across 180 matches. Applied VADER polarity scoring and K-Means clustering ($k=3$) to identify behavioural lag and pricing inefficiencies during match momentum shifts.  
  📁 <a href="https://docsend.com/view/m4mrv375b7kfkahu" target="_blank" rel="noopener noreferrer">**Read Full Paper (Instant Access via DocSend)**</a>

---

## 🛠️ Core Technical Stack

### Languages & Data Modeling
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=postgresql&logoColor=white)

### Data Infrastructure & Webhooks
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)
![Telegram](https://img.shields.io/badge/Telegram_Bot-26A5E4?style=for-the-badge&logo=telegram&logoColor=white)
![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)

### Documentation & Version Control
![GitBook](https://img.shields.io/badge/GitBook-3884FF?style=for-the-badge&logo=gitbook&logoColor=white)
![Markdown](https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)

---

## 📂 Featured Technical Projects

### 1. Protocol Architecture & Developer Documentation: Quintes
**Focus:** Technical Writing • System Specifications • Tokenomic Mechanics  
🔗 <a href="https://quintes.gitbook.io/quintes" target="_blank" rel="noopener noreferrer">**Live Documentation**</a>

Architected the complete public-facing documentation suite and developer knowledge base for an institutional Real-World Asset (RWA) protocol:

* **System Primitives & Tokenomics:** Structured comprehensive reference documentation defining dual-token models, overcollateralisation debt mechanisms, and algorithmic yield dynamics.
* **Liquidation & Risk Workflows:** Formulated clear technical specifications explaining liquidation triggers, PegKeepers, and stability pool operations for developers and institutional partners.
* **Information Architecture:** Built a standardised taxonomy separating high-level conceptual overviews from low-level smart contract integration parameters, accelerating partner onboarding.

📁 *Architecture Overview & Case Study: [`/docs/quintes-case-study.md`](./docs/quintes-case-study.md)*

---

### 2. Jupiter Tennis: Event-Driven Algorithmic Trading Engine
**Focus:** Systems Architecture • WebSocket Streaming • Finite State Machine (FSM)  
🔒 **Proprietary Commercial Pipeline** *(Codebase private; architectural breakdown and UI demo below)*

An automated, high-frequency, event-driven trading execution engine designed for live prediction markets and exchange order books. The system bypasses REST polling limitations via direct WebSocket stream ingestion, local state synchronisation, and strict concurrency controls:

* **Low-Latency Streaming Architecture:** Built a zero-latency WebSocket stream listener with packet conflation to process market books and order fills in milliseconds while remaining within rate constraints.
* **Deterministic Finite State Machine (FSM):** Implemented a thread-safe `TradingSession` lifecycle engine across discrete operational states (`OBSERVATION`, `TRANSACTION`, `PENDING_ENTRY`, `MANAGEMENT`, `PENDING_EXIT`) to prevent execution race conditions and double-order submission.
* **Local Order & Risk Cache:** Subscribed directly to private order streams, maintaining an in-memory cache to compute real-time gross profit, liability, and timeout logic locally without external round-trips.
* **Asynchronous Telemetry & Telemetry Persistence:** Deployed an `asyncio` background loop for real-time Telegram trade updates and built automated batch exporters persisting point-by-point match statistics, serve metrics, and execution logs to MongoDB.

<p align="center">
  <img src="./assets/jupiter-engine-cli.gif" alt="Jupiter Engine CLI Demo" width="700"/>
</p>

📁 *System Design & FSM Lifecycle Spec: [`/projects/jupiter-engine-architecture.md`](./projects/jupiter-engine-architecture.md)*

---

### 3. Jupiter Backtesting & Quantitative Analytics Suite
**Focus:** Quantitative Analysis • Historical Simulation • Interactive Visualisation  
🔒 **Proprietary Research Ecosystem** *(Internal analytics hub; visual walkthrough below)*

A dedicated backtesting and quantitative simulation suite built in Python to evaluate algorithmic trading strategies, historical parameter sensitivity, and risk drawdowns across multi-season datasets:

* **Discrete-Time Transition Modelling:** Built predictive models in Python (pandas, NumPy) designed specifically to forecast point-to-game and game-to-set transition states and match outcomes.
* **Historical Market Simulation:** Backtested execution logic against historical market data feeds, verifying fill assumptions, slippage constraints, and odds volatility.
* **Interactive Streamlit Analytics Dashboard:** Engineered a multi-parameter web interface allowing quantitative exploration of entry thresholds, surface splits (Clay, Hard, Grass), break-point conversions, and maximum drawdowns.
* **Telemetry Data Reconstruction:** Parsed chronological arrays of match dictionaries stored in MongoDB to reconstruct point-by-point match momentum curves and strategy equity paths.

<p align="center">
  <img src="./assets/jupiter-tennis-backtest-demo.gif" alt="Jupiter Streamlit Backtest UI" width="700"/>
</p>

📁 *Quantitative Pipeline & Backtesting Breakdown: [`/projects/jupiter-backtesting-analysis.md`](./projects/jupiter-backtesting-analysis.md)*

---

## 💼 Core Experience & Background

* **Technical Writer** | *Quintes* (Jul 2024 – Present · Contract)  
  * Designed and authored the complete technical documentation suite on GitBook, translating complex smart contract interactions, overcollateralisation parameters, and liquidation logic into structured developer references.
* **AI Evaluation & Alignment Specialist** | *Independent Technical Consultant* (Nov 2025 – Present · Contract)  
  * Evaluated and optimised frontier Large Language Model (LLM) responses across reinforcement learning from human feedback (RLHF) and fine-tuning pipelines, designing adversarial test cases and benchmarking multi-modal reasoning.
* **Senior Marketing Manager** | *TradrLab* (Feb 2022 – Jul 2024)  
  * Spearheaded product marketing and technical communications for a natural-language AI algorithmic trading platform, scaling early user adoption across quantitative finance and trading communities.
* **Business Developer & Sales** | *Facesoft* (Mar 2019 – Aug 2019)  
  * Executed hybrid technical writing, developer relations, and business development initiatives for an Imperial College London-incubated computer vision and AI facial recognition startup.

---

## 📄 Contact & Direct Inquiries
* Direct Email: `matthew_enubuje@outlook.com`
* Based in London, UK (Open to remote and hybrid technical writing / data roles)
