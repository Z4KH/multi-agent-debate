# Hierarchical Multi-Agent Debate for Financial Trading

**From financial news to explainable trading decisions through a diverse team of LLM agents.**

Can LLMs interpret news sentiment well enough to make accurate short-term trades? Can a simulated fundamental trading firm, built from agents with different evidence and investment perspectives, turn that reasoning into portfolio returns?

This project explores those questions with a modular Python framework that organizes financial analysis into a hierarchy of specialists, debates, and decision makers. It connects real news and market data to structured trading signals, with saved debate transcripts that make each decision inspectable.

## How it works

1. **Organize the evidence.** Categorize news into topics such as earnings, product launches, and regulation, then assign data shards to specialist leaf agents.
2. **Challenge the interpretation.** Specialists debate within topic clusters alongside investor persona agents that contribute distinct investment philosophies and broader context.
3. **Bring different views together.** Head agents synthesize each cluster's arguments. A greedy reclustering algorithm groups them to maximize disagreement, using a weighted combination of justification embedding similarity and confidence in buy/sell positions.
4. **Make a portfolio-aware decision.** A final agent produces a buy, sell, or wait signal, share quantity, confidence, next-day return forecast, and justification. The simulation tracks trades and portfolio value over time.

The design addresses a central challenge: how to reason over large news streams without placing all evidence into every agent's context. A rolling news window, configurable data-shard budgets, and hierarchical synthesis distribute the analysis across specialists. Different evidence gives agents distinct starting points; diversity-aware reclustering keeps competing interpretations in the discussion.

The debate engine accepts separate prompt, utility, and LLM components, allowing the reasoning structure to be reused beyond the trading experiment.

## Repository structure

| Path | Purpose |
| --- | --- |
| [`debate/`](debate/) | Agent roles, topic categorization, data sharding, cluster debates, and hierarchical orchestration. |
| [`reasoning/`](reasoning/) | LLM integration and response generation. |
| [`data/`](data/) | News datasets and collection scripts for Finnhub, Alpha Vantage, and Yahoo Finance. |
| [`webscraper/`](webscraper/) | Asynchronous news scraping pipeline. |
| [`experiments/`](experiments/) | Simulation runner, configuration, trading prompts, similarity scoring, and portfolio tracking. |
| [`experiments/results/`](experiments/results/) | Debate transcripts, trade histories, portfolio records, and analysis notebook. |
| [`debate/examples/NVIDIA_debate/`](debate/examples/NVIDIA_debate/) | A self-contained example of the debate framework. |

Start with [`experiments/main.py`](experiments/main.py) for the simulation and [`debate/debate.py`](debate/debate.py) for the core orchestration.

## Results

The [research report](report.pdf) evaluates separate NVDA, AAPL, and TSLA trading simulations over **May 2025**, using Finnhub news and Yahoo Finance prices. Each began with **$1 million**, with Gemini 1.5 Flash powering three debate rounds per cluster and one hidden layer.

| Stock | Final portfolio value | Total return |
| --- | ---: | ---: |
| TSLA | $1,023,415.01 | **+2.34%** |
| NVDA | $1,013,839.26 | **+1.38%** |
| AAPL | $994,123.95 | **-0.59%** |

The reported simulations produced positive returns on two of three stocks, pairing decisive trades with conservative positioning. The repository captures the reasoning behind those outcomes, connecting each news-driven debate to a trading decision and its portfolio impact.

Compared with the single-agent baseline, the debate framework took a markedly more conservative approach, opting to wait or hold existing positions far more often. Competing perspectives pulled the aggregate decision toward a neutral position, making restraint a natural outcome of synthesizing diverse views.
