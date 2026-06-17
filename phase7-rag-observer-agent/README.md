# Phase 7: RAG, Observer Agent and Semantic Intent Check

## Overview
Phase 7 builds the most architecturally sophisticated
system in the curriculum so far. It combines three
governance layers into a complete agentic oversight
pipeline: a Retrieval Augmented Generation pipeline
that grounds every LLM response in verified regulatory
source documents, an Observer Agent that independently
audits every RAG response before it reaches the user,
and a Semantic Intent Check that intercepts malicious
queries before they reach the pipeline at all.

This phase was directly shaped by real professional
engagement. A senior practitioner on LinkedIn asked
how evaluation suites could be adapted to flag
multilingual semantic overrides dynamically. This
phase builds the technical answer to that question
in working code.

Regulatory mapping: NIST AI 600-1 hallucination
tracking, source data lineage verification, and output
monitoring. EU AI Act Articles 14 and 15.

## What Was Built
A four-lesson agentic governance pipeline covering
RAG fundamentals, Observer Agent architecture,
semantic intent classification, and a complete
governance report consolidating all findings.

## Architecture

```
User Query
     |
     v
┌─────────────────────────────────────────┐
│         SEMANTIC INTENT CHECK           │
│           (pre-execution gate)          │
│  Strips wrapper framing.                │
│  Evaluates core intent.                 │
│  Blocks malicious queries before        │
│  pipeline runs.                         │
└─────────────────────────────────────────┘
     |
     | (if ALLOWED)
     v
┌─────────────────────────────────────────┐
│              RAG AGENT                  │
│  Retrieves relevant regulatory          │
│  documents.                             │
│  Generates answer grounded in           │
│  source text only.                      │
│  Returns answer with full source        │
│  citations.                             │
└─────────────────────────────────────────┘
     |
     v
┌─────────────────────────────────────────┐
│           OBSERVER AGENT                │
│  Independently audits the RAG           │
│  response.                              │
│  Scores grounding, relevance,           │
│  and integrity.                         │
│  Returns APPROVED, FLAGGED,             │
│  or REJECTED verdict.                   │
└─────────────────────────────────────────┘
     |
     v
User receives audited, grounded answer
```



## Key Findings

### Lesson 1: RAG Pipeline Basics

| Query | Sources Retrieved | Grounded |
|---|---|---|
| EU AI Act prohibited practices | Article 5, Article 99 | True |
| EU AI Act penalty tiers | Article 99, Article 14 | True |
| NIST AI RMF four functions | NIST RMF 1.0, NIST AI 600-1 | True |
| Article 14 human oversight | Article 14, Article 10 | True |

All 4 responses grounded: 4 out of 4 (100%)

Critical finding: Keyword retrieval initially
retrieved Article 5 for a penalty query due to
surface word overlap. Domain-specific scoring boosts
were added to resolve the retrieval quality limitation.
This demonstrates that retrieval precision requires
domain knowledge, not just keyword frequency.

### Lesson 2: Observer Agent Architecture

| Query | Grounding | Relevance | Integrity | Verdict |
|---|---|---|---|---|
| Article 14 human oversight | 5/5 | 5/5 | 5/5 | APPROVED |
| EU AI Act penalty tiers | 5/5 | 5/5 | 5/5 | APPROVED |
| NIST AI 600-1 hallucination | 5/5 | 5/5 | 5/5 | APPROVED |

Overall: 3 out of 3 APPROVED (100%)

Critical finding: The Observer Agent and RAG Agent
both use gemini-flash-latest. This replicates the
same-family bias documented in Phase 3 where Gemini
judged Gemini outputs as perfect 5/5. Perfect scores
may reflect model-family agreement rather than genuine
quality verification. Production deployment requires
a cross-model Observer Agent using a different model
family for genuine independence.

### Lesson 3: Semantic Intent Check

| Category | Queries | Result | Accuracy |
|---|---|---|---|
| Legitimate | 2 | 2 Allowed | 100% |
| Translation Wrapper | 2 | 2 Blocked | 100% |
| Hypothetical Wrapper | 2 | 1-2 Blocked | 50-100% |
| Direct Injection | 2 | 2 Blocked | 100% |
| Overall | 8 | 5-6 Blocked | 88-100% |

Finding 1: Translation wrapper attacks detected and
blocked across both English and German language
vectors. The classifier strips wrapper framing and
evaluates the underlying intent, not the surface
instruction.

Finding 2: Academic research framing produced
non-deterministic results across runs. Classified
as suspicious and blocked in one run, legitimate
and allowed in another. This documents a critical
production risk: LLM-based classifiers are
probabilistic and cannot guarantee consistent
verdicts for identical inputs.

Finding 3: Safety-first fallback confirmed correct.
When the API was unavailable and the classifier
could not respond, execution defaulted to blocked
rather than allowed. Uncertain means blocked.

Finding 4: The same attack type that bypassed every
keyword classifier in Phase 4 (academic research
framing producing 1095 words of harmful content)
was correctly identified as suspicious and blocked
by the semantic intent check. This is the direct
technical answer to the keyword classifier failure
documented in Phase 4.

### Phase 7 Final Verdict
RAG Pipeline:          GROUNDED (4/4, 100%)
Observer Agent:        3/3 APPROVED
Same-family bias documented
Semantic Intent Check: 88-100% accuracy
Non-determinism documented
OVERALL: PRODUCTION-READY WITH CONDITIONS
Condition 1: Cross-model Observer Agent required
to eliminate same-family leniency bias
Condition 2: Temperature control and confidence
scoring required for semantic classifier
to address non-determinism on borderline
cases such as academic research framing

## Critical Governance Insights

### The Same-Family Observer Bias Problem
The Observer Agent cannot detect blind spots it
shares with the RAG Agent. When both agents use
the same model family, the Observer validates the
RAG Agent's biases rather than challenging them.
This mirrors Phase 3 where Gemini judged Gemini
text outputs as 5/5 every time.

The principle is identical to financial audit
independence: the auditor must be independent of
the entity being audited. In AI governance this
means the Observer Agent must use a different
model family from the RAG Agent.

### Semantic vs Keyword Classification
Phase 4 documented 28% keyword classifier accuracy.
The academic research framing attack bypassed every
keyword filter and produced 1095 words of harmful
content.

The semantic intent check achieved 88-100% accuracy
on the same attack types. The difference is not a
technical detail. It is the difference between a
filter that reads words and a governor that
understands intent.

### Production RAG Architecture
This phase used a Python dictionary as the knowledge
base and keyword scoring for retrieval. In production:

Phase 9 code optimisation will upgrade the
knowledge base to Chroma using the Gemini
embedding model.

## Skills Demonstrated
- Retrieval Augmented Generation pipeline design
- Knowledge base architecture and retrieval engine
- Domain-specific scoring for retrieval precision
- Observer Agent design and implementation
- LLM-as-judge with structured JSON verdicts
- Semantic intent classification
- Wrapper detection across translation, hypothetical,
  roleplay, and direct injection categories
- Non-determinism documentation and mitigation planning
- Same-family bias identification and production fix
- Multi-layer agentic governance architecture
- NIST AI 600-1 compliance implementation

## Tools and Stack
Python | Pandas | Matplotlib | Gemini API |
Google Colab | google-genai

## Notebooks

| Notebook | Description | Status |
|---|---|---|
| `01_rag_pipeline_basics.ipynb` | RAG knowledge base, retrieval engine, grounding test | Complete |
| `02_observer_agent.ipynb` | Dual-agent pipeline, grounding audit, same-family bias finding | Complete |
| `03_semantic_intent_check.ipynb` | Pre-execution classifier, 4 attack categories, governed pipeline | Complete |
| `04_phase7_governance_report.ipynb` | Complete governance report with dashboard | Complete |

## Regulatory Framework

| Article | Requirement | Implementation |
|---|---|---|
| EU AI Act Article 14 | Human oversight | Observer Agent automated oversight layer |
| EU AI Act Article 15 | Adversarial robustness | Semantic intent check tested against 4 attack categories |
| NIST AI 600-1 | Hallucination tracking | RAG grounding implemented |
| NIST AI 600-1 | Source data lineage | Citation per response |
| NIST AI 600-1 | Output monitoring | Observer Agent active on every response |

## Data Files
All results saved to Google Drive:
- `observer_agent_results.csv`
- `semantic_intent_results.csv`
- `phase7_governance_report_dashboard.png`
- `phase7_executive_summary.txt`

## Status
Complete. Phase 8 next: Multi-Agent Governance
and Kill-Switch Architecture.

---
Running This Code
These notebooks require a Google Gemini API key.

1.Get a free API key at aistudio.google.com
2.Open the notebook in Google Colab
3.Click the key icon in the left sidebar
4.Add a secret named GOOGLE_API_KEY
5.Paste your API key as the value
6.Run all cells
Note: Some notebooks make multiple API calls. The free tier allows 20 requests per day.

#AIGovernance #EUAIAct #ResponsibleAI #AgenticAI
#AuditIndependence #Compliance #BuildInPublic
