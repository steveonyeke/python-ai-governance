# Phase 2: Data Handling and Visualization

## Overview
Phase 2 transforms raw LLM outputs into structured, analysable datasets. A professional evaluator does not just run tests, they capture results, measure them with metrics, and communicate findings visually. This phase builds the data pipeline that every subsequent evaluation phase depends on.

## What Was Built
A complete data collection and visualization pipeline that automatically captures LLM responses, measures them across multiple metrics, saves results permanently to Google Drive, and produces professional evaluation dashboards with matplotlib.

## Key Findings
- Response length is a real signal. Models that are consistently verbose on open-ended prompts may be padding responses, a concern in high-stakes deployments.
- Response time varies significantly by topic complexity.Broader governance questions took up to 20 seconds,suggesting deeper reasoning on abstract topics.
- Keyword scoring reveals vocabulary gaps. The model consistently avoided the word "governance" when discussing the EU AI Act, using "regulation" instead. This is a finding about model vocabulary, not just topic coverage.
- Saving data to Google Drive is essential. Colab resets wipe local files. Permanent storage is a professional requirement, not an optional extra.

## Skills Demonstrated
- Pandas DataFrames for structured eval data
- CSV saving and reloading for persistent results
- Google Drive integration for permanent storage
- Word count and response time metrics
- Keyword coverage scoring
- Matplotlib bar charts and multi-panel dashboards
- Professional eval report formatting

## Tools and Stack
Python | Pandas | Matplotlib | Google Colab | Google Drive

## Notebooks

| Notebook | Description | Status |
|---|---|---|
| `01_pandas_basics.ipynb` | First eval dataset with pandas | Complete |
| `02_full_eval_pipeline.ipynb` | Complete pipeline with timing metrics | Complete |
| `03_visualizing_eval_results.ipynb` | Eval dashboard with matplotlib | Complete |

## Status
Complete

---
## Running This Code

These notebooks require a Google Gemini API key.

1. Get a free API key at aistudio.google.com
2. Open the notebook in Google Colab
3. Click the key icon in the left sidebar
4. Add a secret named GOOGLE_API_KEY
5. Paste your API key as the value
6. Run all cells

Note: Some notebooks make multiple API calls.
The free tier allows 20 requests per day.
