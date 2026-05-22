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

---

## LinkedIn Post

I used an AI to evaluate an AI. Then I found the flaw.

This week I built an LLM-as-judge pipeline, a system 
where one AI model automatically scores the outputs of 
another using defined criteria: accuracy, clarity, 
and relevance.

The results came back perfect. Every response scored 
5 out of 5 across all three dimensions.

That is not a good sign. That is a red flag.

When a model judges responses from its own family, it 
scores them too generously. This is called leniency bias 
or self-serving bias, and it is a known, documented 
problem in production evaluation systems.

In AI governance terms, this matters because:

Organisations using automated LLM judges to assess their 
own models are getting inflated scores. Their evaluation 
pipeline is compromised by the same bias they are trying 
to measure.

The fix: always use a different model family as the judge.
Gemini evaluates GPT outputs. Claude evaluates Gemini.
Cross-model judging produces objective scores.

Three other findings from this phase:

→ Provocative prompt framing triggered 4x more alarmist 
  language than formal framing on identical topics
→ The model was highly consistent, variance of only 
  3 words across repeated short prompts
→ Keyword classifiers misclassify good responses that 
  use synonyms instead of exact keywords

Phase 3 complete. Six phases to go.

Full evaluation report on GitHub: [your link]

#AIGovernance #LLMEvaluation #ResponsibleAI #Python
#MachineLearning #AIPolicy #BuildInPublic
