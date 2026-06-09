# Phase 5: Bias Auditing and EU AI Act Compliance

## Overview
Phase 5 applies statistical fairness methodology to a live 
LLM system and maps findings directly to EU AI Act Article 10 
compliance requirements. This phase bridges technical bias 
detection and regulatory documentation, producing the kind 
of evidence-based compliance assessment that organisations 
deploying high-risk AI systems are legally required to conduct.

This is not theoretical governance. Every finding is measured, 
every metric is calculated, and every conclusion is mapped to 
a specific legal article with a formal compliance verdict.

## What Was Built
A four-part bias auditing suite covering demographic bias 
detection, statistical fairness metrics, EU AI Act compliance 
mapping, and a complete bias audit report with dashboard and 
regulatory documentation.

## Key Findings

### Demographic Bias Detection
The same leadership scenario was presented with identical 
credentials across three demographic dimensions. Only names 
and demographic markers changed.

Gender variance: 4 sentiment points. HIGH signal.
Age variance: 4 sentiment points. HIGH signal.
Ethnicity variance: 1 sentiment point. LOW signal.

The most significant qualitative finding: the model used 
the word "claimed" when describing a young candidate's 
credentials, language never applied to any other demographic 
with identical qualifications. This is algorithmic ageism 
expressed in a single word.

### Statistical Fairness Metrics

| Dimension | Disparate Impact Ratio | Legal Threshold | Status |
|---|---|---|---|
| Gender | 0.43 | 0.80 | FAILS |
| Ethnicity | 0.80 | 0.80 | PASSES |
| Age | 0.20 | 0.80 | CRITICALLY FAILS |

### EU AI Act Article 10 Compliance Assessment

| Article | Requirement | Status |
|---|---|---|
| Article 10(2)(f) | Bias examination in outputs | NON-COMPLIANT |
| Article 10(5) Gender/Age | Discrimination risk examination | NON-COMPLIANT |
| Article 10(5) Ethnicity | Discrimination risk examination | COMPLIANT |
| Article 14 | Human oversight measures | REQUIRES ACTION |
| NIST Mitigate | Risk prioritisation | REQUIRES ACTION |

Deployment verdict: NOT APPROVED for hiring or leadership 
assessment contexts without bias mitigation and human 
oversight implementation.

Organisations deploying this system in its current state 
face potential fines of up to 15 million euros or 3% of 
global annual turnover under EU AI Act Article 99(3) for 
high-risk AI data governance violations.

## Skills Demonstrated
- Controlled bias testing with demographic variants
- Sentiment scoring and qualitative language analysis
- Demographic parity calculation
- Disparate impact ratio using the 80% rule
- Normalised sentiment gap measurement
- EU AI Act Article 10 compliance mapping
- Formal compliance log production
- Regulatory summary generation
- NIST AI RMF Mitigate function documentation

## Tools and Stack
Python | Pandas | NumPy | Matplotlib | Gemini API | Google Colab

## Notebooks

| Notebook | Description | Status |
|---|---|---|
| `01_demographic_bias_detection.ipynb` | Bias testing across gender, ethnicity, age | Complete |
| `02_fairness_metrics.ipynb` | Disparate impact, parity, sentiment gap | Complete |
| `03_eu_ai_act_compliance_mapping.ipynb` | Article 10 compliance mapping and formal log | Complete |
| `04_bias_audit_report.ipynb` | Complete audit report with dashboard | Pending |

## Regulatory Framework
- EU AI Act Article 10: Data and Data Governance
- EU AI Act Article 14: Human Oversight
- EU AI Act Article 99(3): Penalties for high-risk violations
- NIST AI RMF: Mitigate function

## Status
Phase 5 in progress. Lesson 4 (Bias Audit Report) pending.

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
