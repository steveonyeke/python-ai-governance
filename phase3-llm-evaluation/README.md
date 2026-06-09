# Phase 3: LLM Evaluation

## Overview
Phase 3 applies professional evaluation methodology to 
a live LLM system. Moving beyond basic data collection, 
this phase tests model behaviour systematically across 
three dimensions: consistency, prompt sensitivity, and 
automated quality scoring. The phase culminates in a 
complete evaluation report combining data, visualizations, 
and an AI-generated executive summary.

## What Was Built
A four-part evaluation suite covering consistency testing, 
prompt sensitivity analysis, LLM-as-judge scoring, and a 
final evaluation report with a six-panel dashboard and 
professional executive summary.

## Key Findings
- The model is highly consistent. Repeated prompts showed
  variance of only 3 words on short prompts and 25 words
  on open-ended prompts, both rated as consistent.
- Prompt framing significantly affects tone. Provocative
  framing triggered 4x more alarmist language than formal
  framing on identical topics. This is a real vulnerability
  in deployed AI systems.
- LLM-as-judge produces leniency bias. Using Gemini to
  judge Gemini outputs resulted in perfect 5/5 scores
  across all dimensions. Same-family evaluation is not
  objective evaluation.
- Keyword classifiers are fundamentally limited. They
  cannot distinguish between a word used in a refusal
  context and the same word used in a compliance context.
  Human review is always required.

## Skills Demonstrated
- Consistency measurement with standard deviation analysis
- Prompt sensitivity testing across 4 framing styles
- Tone scoring using alarmist and measured language signals
- LLM-as-judge pipeline with JSON response parsing
- Judge bias identification and documentation
- Six-panel evaluation dashboard with matplotlib
- AI-generated executive summary using structured prompts
- Professional eval report writing

## Tools and Stack
Python | Pandas | Matplotlib | Gemini API | Google Colab

## Notebooks

| Notebook | Description | Status |
|---|---|---|
| `01_consistency_testing.ipynb` | Same prompt repeated 3 times across 2 styles | Complete |
| `02_prompt_sensitivity.ipynb` | Same topic across 4 framing styles | Complete |
| `03_llm_as_judge.ipynb` | Automated quality scoring with bias detection | Complete |
| `04_first_eval_report.ipynb` | Complete evaluation report with dashboard | Complete |

## Status
Complete

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
