# AI Governance & Agentic Audit Suite

### A Working Regulatory Evidence Engine for EU AI Act, NIST AI RMF, and Cross-Border Deployer Compliance

This repository is the technical foundation of Afrispan Data Labs, an AI deployment assurance practice for SMEs, built first for Ghana and West Africa. It is not a teaching log. It is a working evidence suite: nine phases of governance code, each one tested against its own failure modes, synthesized into a documentation layer that turns regulatory text into something a deployer can actually produce on demand.

Every claim in this README is backed by code in this repository, real measured output, or both. Nothing here is aspirational.

---

## What This Repository Actually Proves

Four governance principles recur across the codebase, found by direct testing, not assumed in advance:

**An AI system cannot audit itself.** Phase 3 found that Gemini scoring Gemini's own text output produced near-perfect, structurally lenient scores. Phase 7 found the identical pattern in a different system, an Observer Agent auditing a RAG pipeline built on the same model family. The fix is structural, not a better prompt: a different model family must do the auditing.

**Surface pattern-matching fails at the edges, in every form it takes.** Phase 4's keyword classifier hit 28% accuracy and missed a research-framing attack that produced 1,095 words of harmful content. Phase 6's tool-calling system silently remapped an unrecognized input to the nearest known category instead of flagging it. Phase 7's semantic classifier, built specifically to fix Phase 4's failure, succeeded at 88-100% accuracy but introduced a new failure: non-deterministic verdicts on borderline cases. Each fix bought real accuracy and introduced a new, more subtle failure mode in its place.

**Monitoring is not governing.** A system that detects a critical breach and keeps running is a monitor. Phase 8's kill-switch halts execution completely the instant a breach is detected, and nothing resumes until a named human resolves it.

**Authority is not judgment.** Before Phase 8's kill-switch accepts a human override, it surfaces the specific breach, the article of law violated, and the quantified legal exposure, then requires a substantive documented position before execution can resume. In the live demonstration, 4 minutes and 33 seconds elapsed between breach detection and the abort decision, the measurable evidence that a human actually engaged with the finding rather than reflexively clicking through it.

These four findings, and the full evidence behind them, are synthesized in **`AI_Governance_in_Practice.docx`**, the capstone document tying all nine phases together.

---

## The Regulatory Documentation Suite

Phase 9 converts the working code above into deployer-facing documentation, built as general-purpose generators, not one-off scripts:

| Deliverable | What It Does |
|---|---|
| **FRIA Template** | Generates a Fundamental Rights Impact Assessment per critical breach, not per audit. Accepts automated evidence from a real audit log or manual client intake, and tags every field AUTOMATED, ATTESTED, or MISSING so a reader can see exactly how strong the evidence behind it is. |
| **Conformity Report** | Scores a system against 22 obligations across EU AI Act, NIST AI RMF, NIST AI 600-1, and ISO/IEC 42001 in one report. Untested obligations are marked NOT ASSESSED, never silently omitted. One piece of evidence can satisfy several frameworks at once, and the report shows that mapping explicitly. |
| **Cross-Border Framework** | Tests whether EU AI Act and NIST evidence actually transfers to Nigeria (NDPA 2023) and Canada. The honest finding: most of it does not. As of June 2026, Canada has no binding federal AI law, AIDA died with Bill C-27 in January 2025, making it the only G7 nation without one at the time of writing. Nigeria's NDPA Section 37 transfers cleanly for human oversight; most other obligations only partially transfer or have no local equivalent at all. |
| **AI Governance in Practice** | The capstone synthesis. Walks all nine phases in order, then names the four cross-phase findings above as recurring governance principles, not isolated bugs. |

Every generator in this suite was verified against real data from this repository's own audit logs before being treated as finished, including catching and fixing real bugs along the way: missing NIST AI 600-1 coverage, two EU AI Act articles with unmapped existing evidence, and a data-integrity defect that would have let manual intake silently overwrite automated evidence.

---

## The Nine Phases

| Phase | Focus | What Was Built |
|---|---|---|
| 01 | Python Foundations | Core language skills for AI evaluation work |
| 02 | Data Handling & Visualization | Pandas, Matplotlib, structured evaluation output |
| 03 | LLM Evaluation | Consistency testing, prompt sensitivity, LLM-as-judge, first appearance of same-family evaluator bias |
| 04 | Red-Teaming & Safety Analysis | Adversarial testing across 8 attack vectors, 28% keyword classifier accuracy exposed |
| 05 | Bias Auditing & EU AI Act Compliance | Disparate impact ratios (age 0.20, gender 0.43, ethnicity 0.80), qualitative linguistic bias found in generated text |
| 06 | Function Calling & Tool-Use Auditing | Agentic tool-use safety testing, silent input-remapping risk discovered |
| 07 | RAG, Observer Agent & Semantic Intent Check | Three-layer agentic pipeline, same-family Observer bias confirmed, classifier non-determinism documented |
| 08 | Multi-Agent Governance & Kill-Switch | Real human-in-the-loop kill-switch, immutable SHA-256 hash-chained audit log, authority-vs-judgment enforcement |
| 09 | Portfolio Synthesis & Regulatory Suite | Code optimization, FRIA template, Conformity Report, Cross-Border Framework, capstone synthesis |

All nine phases are complete. Phase 9's portfolio launch (this README, LinkedIn posts, capstone article) happens once, after every deliverable above is finished, which it now is.

---

## Tech Stack

- **Language:** Python
- **Data & Visualization:** Pandas, Matplotlib, NumPy
- **Evaluation:** Gemini API (`gemini-flash-latest`), Google Colab
- **Vector Search:** Chroma (current), with a deferred persistent-storage and incremental-ingestion pipeline ready for when client work needs it
- **Agent Orchestration:** Pure Python for the production governance pipeline (Phase 8); a minimal, explicitly non-production LangGraph demonstration exists in Phase 9 as a scoped technical exploration, not an adopted upgrade
- **Documentation Generation:** `docx` (Node.js) for the brand-styled capstone document

---

## Running the Code

Notebooks require a Google Gemini API key. Get a free key at [aistudio.google.com](https://aistudio.google.com) and add it to Colab secrets as `GOOGLE_API_KEY` before running.

All notebooks include saved outputs, so results can be reviewed without re-running the code.

---

## Connect

**Steve Onyeke** | Founder, Afrispan Data Labs
*AI Quality Analyst, Turing*

[LinkedIn](https://linkedin.com/in/steveonyeke) | [GitHub](https://github.com/steveonyeke/python-ai-governance)
