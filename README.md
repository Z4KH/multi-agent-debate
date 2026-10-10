# Multi-Agent LLM System for Financial Decision Making

**Explainable, real-time stock trading powered by structured multi-agent debate.**

![GitHub Repo Stars](https://img.shields.io/github/stars/Z4KH/brainrot?style=social)
![License](https://img.shields.io/github/license/Z4KH/brainrot)

---

## Overview

This project is a multi-agent financial reasoning framework that uses **Large Language Models (LLMs)** to make **short-term stock trading decisions** based on **real financial news**. Agents dynamically ingest, debate, and reason over real-world data to produce explainable buy/sell/wait decisions.

Inspired by systems like **ai-hedge-fund** and **TradingAgents**, this framework introduces:
- **Dynamic agents** allocated specific portions of the data
- Modular **hierarchical debates**
- **Static agents** (e.g., Warren Buffett-style personas)
- **Dynamic clustering** for maximizing viewpoint diversity
- **Portfolio-aware trading actions**
- **Real-world evaluation with market slippage**

---

## Key Features

- **Agent roles**: Leaf, Static, Head, and Final Decision agents
- **Diversity-maximizing clustering** and recursive debate hierarchy
- **Structured outputs**: Position, Quantity, Confidence, Projected Return
- **Fully modular API** for custom prompts, utility functions, and new asset types
- **Realistic evaluation** using delayed execution to simulate slippage/gaps

---

## Examples

Quickstart example in the [`examples/`](./examples/) directory:

- `main.py`: Full multi-agent trading simulation for NVDA/TSLA/AAPL (configurable via `config.py`)

---

## Architecture

### Layered Reasoning System

```txt
      ┌──────────────────────────────┐
      │   Real-World Financial News  │
      └────────────┬─────────────────┘
                   ▼
           [ Categorization Layer ]
                   ▼
        ┌──────────────────────────┐
        │   Leaf & Static Agents   │ ← grounded, dynamic perspectives
        └────────────┬─────────────┘
                     ▼
         [ Cluster Round-Robin Debate ]
                     ▼
            Head Agents Synthesis
                     ▼
         [ Diversity-Based Reclustering ]
                     ▼
              Final Decision Agent
                     ▼
              Trade Execution
```

---

## Roadmap

- Dynamic cluster count recalculation per iteration (rather than at initialization)
- Smarter static agent assignment to maximize diversity (replacing round-robin)
- `StaticAgentRegistry`: a configurable set of available static agent personas
- `StaticAgents` class exposing a public interface for user-defined agent creation
