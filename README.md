# Quant Projects

A collection of quantitative finance projects built to develop practical skills in systematic trading, risk modelling, and portfolio construction. Worked through independently, using AI assistance to help debug code, learn new libraries, and refine implementations — the ideas, structure, and research behind each project are my own.

Built in Python. Each project has a Streamlit dashboard, CLI, and test suite.

---

## Projects

| # | Project | What it does | Key concepts |
|---|---------|--------------|--------------|
| 1 | [Equity Factor Model](./Equity-Factor/) | Cross-sectional momentum, value, quality factors with long-short backtesting | Factor construction, decile portfolios, Sharpe/Sortino/Calmar |
| 2 | [Options Pricer](./Options-Pricer/) | Black-Scholes pricing engine with all Greeks and IV solver | BS-Merton, Delta/Gamma/Vega/Theta, Newton-Raphson IV |
| 3 | [Monte Carlo Portfolio Simulator](./Monte-Carlo-Portfolio-Simulator/) | 10,000 portfolio paths via GBM, VaR, CVaR, probability of ruin | Geometric Brownian Motion, Itô correction, Cholesky correlation |
| 4 | [Efficient Frontier](./Efficient-Frontier-Mean-Variance-Optimiser/) | Markowitz mean-variance optimisation, Max Sharpe, Min Vol portfolios | SLSQP optimisation, Capital Market Line, random feasible set |
| 5 | [CAPM / Factor Regression](./CAPM-Factor-Regression/) | CAPM and Fama-French 3-factor regressions with rolling estimates | OLS, matrix algebra, alpha/beta, return decomposition |
| 6 | [Python Portfolio Tracker](./Python-Portfolio-Tracker/) | Live P&L, sector exposure, and performance metrics from a holdings CSV | yfinance, Sharpe, drawdown, benchmark comparison |
| 7 | [Correlation and Heatmap Dashboard](./Correlation-and-Heatmap-Dashboard/) | Rolling correlation matrix with regime shift detection | Rolling correlation, crisis detection, animated heatmap |
| 8 | [TSMOM](./Time-Series-Momentum-Model-(TSMOM)/) | Time-series momentum with GARCH volatility scaling | Moskowitz-Ooi-Pedersen (2012), GARCH, volatility targeting |
| 9 | [Volatility Targeting](./Time-Series-Momentum-Model-(TSMOM)/) | Scales position size so portfolio vol hits a target | Realised vol, vol scaling, trend following |
| 10 | [Relative Value Pairs Trading](./Relative-Value-Pairs-Trading-Model/) | Statistical arbitrage via cointegration and z-score spreads | Engle-Granger, Johansen, mean reversion, spread z-score |
| 11 | [Macro Regime Allocation Model](./Macro-Regime-Allocation-Model/) | Classifies economy into growth/inflation quadrants and allocates assets | Bridgewater All Weather, FRED API, PMI/CPI regime detection |
| 12 | [PCA / Risk Factor Model](./Risk-Factor-and-Correlation-Model/) | Extracts latent risk factors from a stock universe via PCA | Principal Component Analysis, factor loadings, rolling PCA |
| 13 | [Full Backtest with Vectorbt](./Full-Backtest-with-Vectorbt/) | Professional momentum backtest with transaction costs and slippage | vectorbt, position sizing, underwater curve |
| 14 | [Alphalens Factor Analysis](./Alphalens-Factor-Analysis/) | Industry-standard factor evaluation: IC, turnover, quantile returns | Information Coefficient, factor decay, Quantopian methodology |
| 15 | [NLP News Sentiment](./NLP-News-Sentiment/) | Scrapes financial headlines, classifies sentiment with FinBERT, maps scores to forward returns | FinBERT, HuggingFace Transformers, NewsAPI, sentiment → alpha pipeline |
| 16 | [Financial Statement Analyser](./Financial-Statement-Analyser/) | Pulls 10-K/10-Q data via SEC EDGAR, computes Piotroski F-Score, Altman Z-Score, margin trends, LLM MD&A summary | SEC EDGAR API, Piotroski, Altman, LLM integration |
| 17 | [Active Trading Dashboard](./Active-Trading/) | TradingView-style live chart with toggleable indicators and FX pair handling | Technical analysis, real-time data, multi-asset scanning |
| 18 | [Macro Intelligence Dashboard](./Macro-Dashboard/) | FRED macro data visualisation with VIX term structure and regime overlay | FRED API, VIX term structure, macro indicators |
| 19 | [Signal Rule Engine](./Signal-Bot/) | Multi-asset scanner with CCI + Ichimoku signals, audio alerts, batch backtest ranking | Rule-based signals, session state, auto-refresh |
| 20 | [Encyclopedia](./Encylopedia/) | Greek alphabet, university-level quant finance formulas, and strategy reference | Educational reference, formula library |
| 21 | [Unified Trading Signal Bot](./Signal-Bot/) | Ensemble of all strategy signals → vol-targeted sizing → paper trade execution via Alpaca API | Signal aggregation, risk overlay, live paper trading |
| 22 | [Earnings Call NLP Analyser](./Earnings-Call-NLP-Analyser/) | Ingests earnings call transcripts, runs FinBERT + Ollama sentiment per management topic, forecasts short-term price direction | FinBERT, Ollama, transcript parsing, topic segmentation, call sentiment → alpha |
| 23 | [Balance Sheet Driver Decomposition](./Balance-Sheet-Driver-Decomposition/) | Extended DuPont decomposition — traces ROE through every income statement and balance sheet driver to identify the primary value levers for any stock | DuPont, ROE/ROA decomposition, IS→BS driver mapping, SEC EDGAR |
| 24 | [Universal Strategy Backtester](./Universal-Strategy-Backtester/) | Define any strategy — long/short equity, momentum, mean reversion, VIX-regime, RSI/MACD algo — via YAML template or plain English via Ollama; parsed and backtested on any ticker with full tearsheet | Ollama NLP → strategy DSL, vectorbt, long/short, regime filters, VIX/RSI/MACD |
| 25 | [Advanced Stock Screener](./Advanced-Stock-Screener/) | Screens any universe (S&P 500, Russell 1000, NASDAQ, custom) against fundamental filters, technical filters, and custom ratio formulas; outputs ranked candidates with full IS/BS/CF data | Multi-index universe, SEC EDGAR + yfinance, custom ratio engine, dynamic screener |

---

## In Progress

| # | Project | What it does | Key concepts |
|---|---------|--------------|--------------|
| 26 | [Kalman Filter Pairs Trading](#) | Dynamic hedge ratio using Kalman filter — upgrades static OLS in pairs model | Kalman filter, state-space model, online learning |
| 27 | [Cross-Sectional Momentum — S&P 500 Universe](#) | Equity factor model re-run on full Russell 1000 with alphalens IC tearsheet | Large-cap universe, IC decay, factor stability |
| 28 | [Multi-Factor Alpha Model](#) | Combines momentum, value, quality, low-vol into composite score with IC-weighted blending | Factor combination, IC weighting, composite Z-score |
| 29 | [Order Book Microstructure Simulator](#) | Simulates a limit order book, models bid-ask spread, price impact, adverse selection | LOB dynamics, Amihud illiquidity, Kyle's lambda |
| 30 | [Execution Cost & Slippage Model](#) | Estimates real-world trading costs: market impact, spread cost, timing risk | Implementation shortfall, VWAP, slippage estimation |

---

## Project Deep Dives

### 22 · Earnings Call NLP Analyser
Earnings calls move stocks — but reading 50 pages of transcript manually is impractical at scale. This tool automates the entire process:

- **Ingestion:** pulls transcripts from uploaded PDF or web scrape; parses speaker turns (management vs analyst Q&A)
- **Topic segmentation:** splits transcript into topics — guidance, margins, competition, macro outlook, capex, buybacks
- **Dual-model sentiment:** FinBERT scores each segment (finance-domain trained); Ollama LLM generates qualitative bull/bear thesis per topic
- **Signal mapping:** aggregates topic scores into a single call sentiment score; maps historically to 1-day, 5-day, 20-day forward returns
- **Output:** Streamlit dashboard with sentiment timeline across calls, topic breakdown heatmap, historical signal accuracy, and current forward return forecast

### 23 · Balance Sheet Driver Decomposition
Most analysts look at ROE as a single number. This project decomposes it down to every underlying driver using extended DuPont:

```
ROE  =  Net Profit Margin  ×  Asset Turnover  ×  Equity Multiplier
     =  (Net Income / Sales)  ×  (Sales / Assets)  ×  (Assets / Equity)
```

Further decomposes margin into gross → operating → net, asset turnover by working capital efficiency, and leverage by debt maturity profile. For any ticker, shows which driver is responsible for ROE change year-over-year — and whether improvement is from genuine operational performance or financial engineering.

### 24 · Universal Strategy Backtester
Accepts strategies two ways:

**Template format** — precise control:
```yaml
strategy: long_short_momentum
universe: SP500
signal: 12_1_momentum
entry: signal > 0.8
exit: signal < 0.2
position_sizing: vol_target_15pct
regime_filter: VIX < 25
```

**Plain English via Ollama** — fast iteration:
> *"Go long stocks where RSI is below 30 and 3-month momentum is positive. Short stocks with RSI above 70 and negative momentum. Size by inverse volatility. Exit if VIX spikes above 30."*

Ollama parses plain English into the template format, which the backtester executes via vectorbt. Supported strategy types: long/short equity, cross-sectional momentum, time-series momentum, mean reversion, stat-arb, macro regime, technical (RSI / MACD / VIX / Bollinger). Full tearsheet output: Sharpe, drawdown, turnover, regime breakdown.

### 25 · Advanced Stock Screener
Screens across any index or custom universe with a fully dynamic filter engine:

- **Universes:** S&P 500, Russell 1000, NASDAQ 100, custom ticker list
- **Fundamental filters:** P/E, P/B, EV/EBITDA, EV/Sales, Piotroski F-Score, Altman Z-Score, revenue growth (1Y/3Y/5Y), gross/operating/net margin, ROIC, FCF yield, debt/equity, current ratio
- **Technical filters:** RSI, 1M/3M/6M/12M momentum, 52-week high/low proximity, relative volume, beta
- **Custom ratio calculator:** define any formula using available fields — e.g. `(FCF / MarketCap) / Beta` — and screen on it
- **Output:** ranked results table, sector breakdown, CSV export, individual stock deep-dive with full IS/BS/CF pulled from SEC EDGAR

---

## Stack

| Layer | Tools |
|-------|-------|
| Language | Python 3.14 |
| Data | yfinance, SEC EDGAR API, FRED API, NewsAPI |
| Quant libraries | pandas, numpy, scipy, statsmodels, arch (GARCH), pyportfolioopt, vectorbt, alphalens |
| ML / NLP | scikit-learn, HuggingFace Transformers, FinBERT, Ollama (local LLM) |
| Visualisation | Plotly, Matplotlib, Seaborn, Streamlit |
| Execution | Alpaca API (paper trading) |
| Dev | VS Code, Git, GitHub, pytest |

---

## How to Run Any Project

```bash
git clone https://github.com/pmundada769/quant-projects
cd quant-projects

# create and activate virtual environment
python3 -m venv venv
source venv/bin/activate

# navigate to any project and install its dependencies
cd "Earnings-Call-NLP-Analyser"
pip install -r requirements.txt
streamlit run app.py
```

Each project folder contains its own `requirements.txt`, `README.md`, and `instructions.txt`.

---

## Background

Started with CS50 (Harvard's intro CS course) and built these projects to bridge the gap between programming fundamentals and quantitative finance. The projects progress from pricing theory (Black-Scholes) through portfolio construction (Markowitz), risk modelling (Monte Carlo, VaR), factor research (Fama-French, PCA), systematic strategy development (TSMOM, pairs trading, macro regimes), and applied NLP for alpha generation.

Used AI assistance to help debug implementations, learn new libraries, and refine code quality — the financial logic, research direction, and project structure are my own work.

---

*Pranshu Mundada · [github.com/pmundada769](https://github.com/pmundada769)*
