

# TRIPPULSE: Multi-Agent Travel Planning with Review-Grounded Reasoning

> Anonymous EMNLP Submission

## Overview

TRIPPULSE is a multi-agent framework for review-grounded travel itinerary generation. It decomposes planning into specialized domain agents (accommodations, transportation, meals, attractions, and events) coordinated by a Global Orchestrator, with a scheduling backend that enforces spatio-temporal and budget feasibility.

## Repository Structure
```
TRIPPULSE/
├── agentic_trip_with_pro_cons/   # Domain-specific agents and orchestrator
├── core/                         # LLM wrapper
├── tools/                        # Utility tools
├── data_manager/                 # Database interface and calls
├── evaluation/                   # RGPA and TripCraft evaluation metrics
├── run.py                        # Entry point
└── agentic.yaml                  # Environment configuration
```
## Environment Setup

### Prerequisites
- Python 3.10+
- [Anaconda](https://www.anaconda.com/download) or [Miniconda](https://docs.conda.io/en/latest/miniconda.html)

### Installation

**Step 1: Clone the repository**
```bash
git clone <repo_url>
cd trippulse
```

**Step 2: Create and activate the conda environment**
```bash
conda env create -f agentic.yml
conda activate agentic
```

**Step 3: Verify installation**
```bash
conda list
python --version
```

**Step 4: Set up API keys**

Create a `.env` file in the root directory:
```bash
cp .env.example .env
```
Then fill in your API keys:

OPENAI_API_KEY=your_key_here
TOGETHER_API_KEY=your_key_here   # for open-source models


## Running TRIPPULSE

```bash
# LLM-based scheduler
python run.py --scheduler llm --model gpt-5 --duration 3

# Deterministic algorithmic scheduler
python run.py --scheduler deterministic --model gpt-5 --duration 3
```

| Argument | Options |
|---|---|
| `--scheduler` | `llm`, `deterministic` |
| `--duration` | `3`, `5`, `7` |
| `--model` | `gpt-5`, `llama-3.1-70b`, `phi-4`, `mistral-nemo`, `qwen-2.5-7b`, `deepseek-r1` |

## Evaluation

```bash
# Constraint satisfaction + temporal metrics (TripCraft)
python evaluation/evaluation_metrics.py --results_dir outputs/

# Review-Grounded Persona Alignment (RGPA)
python evaluation/rgpa.py --results_dir outputs/
```

## Dataset

The augmented TripCraft benchmark includes **111,628 reviews** across **10,746 entities** (accommodations from Airbnb, restaurants and attractions from TripAdvisor), distilled into structured Pros/Cons using Qwen3-4B-Instruct.

| Domain | Source | Entities | Reviews |
|---|---|---|---|
| Accommodations | Airbnb | 2,395 | 18,094 |
| Restaurants | TripAdvisor | 3,765 | 42,541 |
| Attractions | TripAdvisor | 4,586 | 50,993 |
| **Total** | | **10,746** | **111,628** |

*Note: We will release the comprehensive codebase and publish the dataset upon acceptance.
```
