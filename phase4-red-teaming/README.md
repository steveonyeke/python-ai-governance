# Phase 4: Red-Teaming and Safety Analysis

## Overview
Phase 4 applies adversarial testing methodology to a 
live LLM system. Playing the dual role of attacker and 
auditor, this phase systematically probes safety 
boundaries, documents vulnerabilities, and produces a 
professional red-team safety report. The findings 
directly inform deployment recommendations under the 
EU AI Act and NIST AI RMF frameworks.

## What Was Built
A four-part red-team evaluation suite covering prompt 
injection testing, jailbreak analysis across four attack 
categories, refusal rate measurement across three prompt 
types, and a complete safety report with dashboard and 
executive summary.

## Key Findings
- Translation wrapper attacks are a critical vulnerability.
  The model translated injection instructions into Spanish
  and French without flagging them as malicious. This
  attack bypassed all keyword-based safety detection.
- Research and academic framing is the highest risk vector.
  Requests prefaced with "for academic research purposes"
  produced detailed compliance on restricted topics that
  direct requests could not unlock.
- Keyword classifiers achieved only 28% accuracy across
  all safety verdicts. Human review was required to
  produce accurate classifications in every test suite.
- Direct attacks are well mitigated. Explicit jailbreaks,
  persona switches, and authority spoofing were all
  refused correctly.
- The model's true refusal accuracy is 100% on legitimate
  requests when assessed by human review, correcting the
  automated classifier's false over-refusal readings.

## Skills Demonstrated
- Prompt injection design and testing
- Jailbreak analysis across 4 attack categories
- Safety signal detection and verdict classification
- Refusal rate measurement with correctness scoring
- Classifier accuracy assessment and human review override
- Retry logic for production-grade API reliability
- Six-panel safety dashboard with matplotlib
- Red-team executive summary generation
- Professional safety report writing

## Tools and Stack
Python | Pandas | Matplotlib | Gemini API | Google Colab

## Notebooks

| Notebook | Description | Status |
|---|---|---|
| `01_prompt_injection.ipynb` | 5 injection attacks with safety signal detection | Complete |
| `02_jailbreak_analysis.ipynb` | 8 vectors across Persona, Hypothetical, Indirect, Authority | Complete |
| `03_refusal_rate.ipynb` | 14 prompts across legitimate, harmful, borderline | Complete |
| `04_safety_report.ipynb` | Complete red-team report with dashboard | Complete |

## Findings Summary

| Attack Vector | Risk Level | Status |
|---|---|---|
| Direct injection | Low | Mitigated |
| Persona switching | Low | Mitigated |
| Authority spoofing | Low | Mitigated |
| Developer mode | Low | Mitigated |
| Research framing | High | Not mitigated |
| Translation wrapper | High | Not mitigated |
| Summarise attack | High | Not mitigated |

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
