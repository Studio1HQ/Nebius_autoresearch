<div align="center">

<img src="https://raw.githubusercontent.com/Studio1HQ/Studio1HQ/main/assets/banners/Nebius_autoresearch.webp" alt="Prompt AutoResearch with Nebius: An agent that iteratively improves a system prompt on Nebius Token Factory" width="100%" />

<br />
<br />

# Prompt AutoResearch with Nebius

### An agent that iteratively improves a system prompt on Nebius Token Factory

A small autoresearch demo where an LLM agent on Nebius Token Factory proposes system prompts, runs them, scores them with an LLM judge and learns from the history. It also vendors Karpathy's original autoresearch code.

<br />

[![Built by Studio1](https://img.shields.io/badge/Built_by_Studio1-f97316?style=for-the-badge&logo=data%3Aimage%2Fsvg%2Bxml%3Bbase64%2CPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAxNjAgMTYwIiBmaWxsPSJub25lIj48cGF0aCBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTAgMzVDMCAxNi42ODA3IDE0LjA3NDQgMS42NDg0NCAzMiAwLjEyNjk1M1YxNDFINTEuMDUyM0M1Mi40MzA4IDEzNy4zNDQgNTQuNzQ0NiAxMzMuNjg5IDU3Ljk5MzggMTMwLjAzM0M2MS4xNDQ2IDEyNi41MDggNjQuNjg5MiAxMjMuNDQgNjguNjI3NyAxMjAuODI5QzcyLjU2NjIgMTE4LjM0OSA3Ni4zNTY5IDExNi43ODIgODAgMTE2LjEyOVY4Ni43NTQ0Qzc1LjQ3MDggODcuOTI5MiA3MS4zODQ2IDg5LjY5MTkgNjcuNzQxNSA5Mi4wNDE1QzY0IDk0LjUyMjUgNjAuNzUwOCA5Ny40NiA1Ny45OTM4IDEwMC44NTRDNTYuNTM0NSAxMDIuNzIgNTUuMjU0NSAxMDQuNjU5IDU0LjE1MzkgMTA2LjY3MVYwSDEyNUMxNDQuMzMgMCAxNjAgMTUuNjY5OSAxNjAgMzVWMTI1QzE2MCAxNDQuMzMgMTQ0LjMzIDE2MCAxMjUgMTYwSDEyNFYxOEgxMDQuOTQ4QzEwMy41NjkgMjEuNjgxNiAxMDEuMjU1IDI1LjM2MjggOTguMDA2MiAyOS4wNDQ0Qzk0Ljg1NTQgMzIuNTk0MiA5MS4zMTA4IDM1LjY4NDEgODcuMzcyMyAzOC4zMTRDODMuNDMzOCA0MC44MTIgNzkuNjQzMSA0Mi4zODk2IDc2IDQzLjA0NzRWNzIuNjMwNEM4MC41MjkyIDcxLjQ0NzMgODQuNjE1NCA2OS42NzI0IDg4LjI1ODUgNjcuMzA1N0M5MiA2NC44MDc2IDk1LjI0OTIgNjEuODQ5MSA5OC4wMDYyIDU4LjQzMDdDOTkuNDY1NSA1Ni41NTEzIDEwMC43NDUgNTQuNTk4NiAxMDEuODQ2IDUyLjU3MjNWMTYwSDM1QzE1LjY3IDE2MCAwIDE0NC4zMyAwIDEyNVYzNVoiIGZpbGw9IiNmZmZmZmYiLz48L3N2Zz4K)](https://studio1hq.com)
[![Built with Nebius](https://img.shields.io/badge/Built_with_Nebius-141414?style=for-the-badge)](https://nebius.com)

[Nebius docs](https://docs.tokenfactory.nebius.com) &nbsp;·&nbsp; [Nebius](https://nebius.com) &nbsp;·&nbsp; [More examples](https://github.com/Studio1HQ) &nbsp;·&nbsp; [studio1hq.com](https://studio1hq.com)

</div>

<br />

## Overview

This repo holds two versions of AutoResearch side by side. `original_autoresearch/` is Andrej Karpathy's original code, which optimises neural network training. `nebius_autoresearch/` is a modified demo that uses [Nebius Token Factory](https://docs.tokenfactory.nebius.com) to optimise a system prompt instead.

In the Nebius version an agent proposes a system prompt, an experiment runs it, a judge scores the output, and the result is saved so the agent can learn from it on the next round. The sample task is to explain Vector Databases to a 5-year-old.

## Features

- **Idea, experiment, evaluation loop**: the agent reasons over recent history, proposes a new prompt, and the result is logged.
- **LLM-driven agent**: `agent.py` asks the model for a `THOUGHT` and a `PROMPT`, using the last three experiments as context.
- **LLM judge**: `scorer.py` asks the model for a score from 0.0 to 1.0 on simplicity, analogy, accuracy and engagement.
- **Resumable log**: every experiment is stored in `results.json`, and the loop continues from where it stopped.
- **Progress reports**: a summary of the best prompt so far prints every 25 experiments.
- **Original code included**: Karpathy's `train.py`, `prepare.py` and `analysis.ipynb` are kept for comparison.

## Tech stack

| Layer | Tool |
| --- | --- |
| LLM | [Nebius Token Factory](https://docs.tokenfactory.nebius.com), `meta-llama/Llama-3.3-70B-Instruct` |
| HTTP client | [requests](https://requests.readthedocs.io) against the OpenAI-compatible endpoint |
| Language | Python 3.10 or later |
| Original code | [Karpathy's autoresearch](https://github.com/karpathy/autoresearch) with PyTorch |

## Getting started

### Prerequisites

- Python 3.10 or later
- `requests` (`pip install requests`)
- A Nebius API key

### Installation

```bash
git clone https://github.com/Studio1HQ/Nebius_autoresearch.git
cd Nebius_autoresearch/nebius_autoresearch
pip install requests
```

### Environment variables

| Variable | Description |
| --- | --- |
| `NEBIUS_API_KEY` | Nebius API key. The code reads it from the environment, so export it in your shell: `export NEBIUS_API_KEY="your_api_key_here"`. |

### Run

```bash
python main.py
```

The loop reads the goal from `program.md`, prints the agent's thought process and the score for each experiment, and saves everything to `results.json`. To run the original version instead, open `original_autoresearch/` and inspect `train.py`; it has its own `pyproject.toml` and `uv.lock`.

## How it works

```text
nebius_autoresearch/
  main.py         orchestrator: loads goal and history, runs the loop
  program.md      research goal
  agent.py        proposes the next system prompt
  experiment.py   runs the prompt to produce an explanation
  scorer.py       LLM judge, returns a score from 0.0 to 1.0
  client.py       Nebius Token Factory API client
  results.json    experiment log
original_autoresearch/
  train.py, prepare.py, analysis.ipynb, progress.png
```

`main.py` sets `ITERATIONS = 250` and resumes from the number of entries already in `results.json`. `client.py` posts to `https://api.tokenfactory.nebius.com/v1/chat/completions` with temperature 0.7 and `max_tokens` 4096. Example output from the sub-README:

```text
--- Iteration 1/5 ---
Agent is thinking...
[Agent Thought]: The previous attempt was too technical. I will try a LEGO analogy.
Proposed Prompt: You are a helpful teacher who explains things using LEGO blocks...
Response Length: 115 chars
Score: 1.0/1.0
```

The sub-README describes five iterations, while `main.py` is set to 250. Change `ITERATIONS` in `main.py` to match the run you want.

## Resources

- [Karpathy's autoresearch](https://github.com/karpathy/autoresearch): the original project.
- [nebius-autoresearch](https://github.com/Studio1HQ/nebius-autoresearch): a related Studio1 repo that applies the same idea to a real data pipeline.
- [Nebius Token Factory docs](https://docs.tokenfactory.nebius.com): API and models.
- [Nebius](https://nebius.com): the platform site.

<br />

---

<div align="center">

<a href="https://studio1hq.com">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/Studio1HQ/website/main/brand/studio1-logo-on-dark.svg" />
    <img src="https://raw.githubusercontent.com/Studio1HQ/website/main/brand/studio1-logo-on-light.svg" alt="Studio1" width="160" />
  </picture>
</a>

Built by **[Studio1](https://studio1hq.com)**, the technical content and DevRel partner for devtool teams. Made with [Nebius](https://nebius.com).<br />
Browse more open-source examples at [github.com/Studio1HQ](https://github.com/Studio1HQ).

[![Website](https://img.shields.io/badge/studio1hq.com-0b0807?style=for-the-badge&logo=googlechrome&logoColor=white)](https://studio1hq.com)
[![Book a call](https://img.shields.io/badge/Book_a_strategy_call-f97316?style=for-the-badge&logo=googlecalendar&logoColor=white)](https://cal.com/studio1/collab)
[![X](https://img.shields.io/badge/%40Studio1HQ-141414?style=for-the-badge&logo=x&logoColor=white)](https://x.com/Studio1HQ)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0a66c2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/company/studio1hq/)

<sub><a href="https://studio1hq.com">studio1hq.com</a> · Technical content, docs, video and DevRel for devtools</sub>

</div>
