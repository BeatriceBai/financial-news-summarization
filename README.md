# Evaluating LLM Summaries of Financial News for Investment Research

**Research question.** How can we summarize financial news articles for investment research, and how do we measure summary quality?

## Overview

This project builds and evaluates an LLM-based pipeline that summarizes financial news for equity research analysts. It compares two prompting approaches on 49 articles across 5 tickers (AAPL, AMZN, GOOGL, MSFT, NVDA):

- **Approach A (baseline):** Ticker-aware prose summary (<=100 words).
- **Approach B (structured):** Relevance-triaged, grounded JSON output with relevance label, event type, <=50-word summary, key facts, sentiment, and information quality.

A five-level evaluation framework (deterministic checks, human-labelled relevance, LLM rubric scoring, pairwise preference, and evaluator validation) measures each approach on faithfulness, ticker focus, coverage, and conciseness.

## Repository Contents

```
financial_news_summarization.ipynb   # Main notebook (EDA, methodology, evaluation, analysis)
Financial_News_Summarization_Writeup.pdf  # Written report
requirements.txt                     # Python dependencies
.env.example                        # Template for API key
data/
  input/
    news_articles.json               # 49 financial news articles
    reviewer_ratings.csv             # Independent human spot-check ratings
  output/
    llm_cache/                       # Cached LLM responses (enables re-runs without API key)
    figures/                         # Generated plots
    summaries.csv                    # Generated summaries
    pointwise_judgments.csv          # Judge rubric scores
    pairwise_judgments.csv           # Judge pairwise preferences
    ...                              # Other intermediate outputs
```

## Getting Started

### Prerequisites

- Python 3.10+
- An Anthropic API key (optional if running from cache)

### Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/BeatriceBai/financial-news-summarization.git
   cd financial-news-summarization
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. (Optional) Set up your API key:
   ```bash
   cp .env.example .env
   # Edit .env and add your ANTHROPIC_API_KEY
   ```

### Running the Notebook

```bash
jupyter notebook financial_news_summarization.ipynb
```

All LLM responses are cached in `data/output/llm_cache/`, so the notebook re-runs fully from cache without an API key. Without a key or cache, Part 1 (EDA) still runs; Parts 4-5 (experimentation and analysis) are skipped.

## Models Used

| Role | Model |
|------|-------|
| Summarizer (generator) | `claude-sonnet-5` |
| Evaluator (judge) | `claude-opus-5-5` |

## Notebook Structure

1. **Exploratory Data Analysis** - Article coverage, length, numeric density, relevance, event types, data quality
2. **Methodology Design** - Two summarization approaches and their design rationale
3. **Evaluation Framework** - Five-level evaluation: deterministic checks, relevance triage, LLM rubric, pairwise preference, evaluator validation
4. **Experimentation** - Summary generation, judge scoring, evaluator trust checks, slice analysis, error taxonomy
5. **Analysis & Recommendations** - Results, what worked, recommendations, limitations, next steps
