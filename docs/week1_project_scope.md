# QuantPaper AI — Week 1 Project Scope

## Project Name
QuantPaper AI — A Research-Grounded Quantitative Finance Code Assistant

## Domain
AI Engineering / Quantitative Finance / Research Code Generation

## Problem Statement
Quantitative finance students and beginner researchers may find it difficult to translate mathematical formulas and methodological descriptions in research papers into correct, executable Python implementations. An LLM can generate code from natural-language instructions, but the generated implementation may misinterpret formulas, omit assumptions, or fail to reproduce the method described in the source.

QuantPaper AI will be a document-grounded assistant that retrieves relevant passages from selected, publicly accessible quantitative finance research papers, explains the methodology, generates Python implementations for a small number of selected methods, and checks the generated code using predefined tests. The initial scope is educational research and code reproduction, not investment advice or live trading.

## Evidence of the Problem

**Evidence 1 — Research-to-code implementation is challenging.** ResearchCodeBench evaluates how well language models implement methods described in recent machine-learning research papers. Its findings provide evidence that generating a correct implementation from a paper remains a challenging task.

Source: ResearchCodeBench, NeurIPS 2025.  
URL: https://proceedings.neurips.cc/paper_files/paper/2025/hash/cd0d0a873cc3e601c76f46dccc3d4c5f-Abstract-Datasets_and_Benchmarks_Track.html

**Evidence 2 — Quantitative strategy reproduction is challenging.** QuantCode-Eval studies whether generated code can reproduce quantitative trading strategies described in finance papers. It is directly relevant to the proposed problem of translating financial research into code.

Source: QuantCode-Eval, SSRN (2026).  
URL: https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6801618



## Initial Related Work / Existing Approaches

### 1. Paper2Code
**Source:** Paper2Code, ICLR 2026.  
URL: https://proceedings.iclr.cc/paper_files/paper/2026/hash/41b6674c28a9b93ec8d22a53ca25bc3b-Abstract-Conference.html

**Approach:** A framework for transforming machine-learning research papers into code repositories.

**Key limitation / gap to investigate:** Its primary focus is machine-learning research. This project will investigate a narrower workflow for selected quantitative-finance methods, with source-grounded explanations and explicit executable tests. This is a proposed distinction, not a claim that Paper2Code lacks all validation features.

### 2. ResearchCodeBench
**Source:** ResearchCodeBench, NeurIPS 2025.  
URL: https://proceedings.neurips.cc/paper_files/paper/2025/hash/cd0d0a873cc3e601c76f46dccc3d4c5f-Abstract-Datasets_and_Benchmarks_Track.html

**Approach:** A benchmark for evaluating LLMs' ability to implement methods from recent machine-learning research.

**Key limitation / gap to investigate:** It is an evaluation benchmark rather than the proposed interactive assistant for explaining selected quantitative-finance papers and generating tested implementations. The project will use a small, controlled evaluation set suited to its educational use case.

### 3. QuantCode-Eval
**Source:** QuantCode-Eval, SSRN (2026).  
URL: https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6801618

**Approach:** Evaluates reproduction of quantitative trading strategies described in finance papers.

**Key limitation / gap to investigate:** The proposed project focuses on an accessible student workflow that combines retrieval of source passages, explanation of methodology, code generation, and deterministic tests for selected methods. This scope difference should be confirmed by reviewing the full paper and its accompanying materials.

## Engineering Gap / Limitation
A generated program can run without errors yet still implement a research method incorrectly—for example, by using the wrong lookback window, omitting a condition, or misinterpreting a formula. The project will investigate whether combining retrieval from the source paper, source-linked explanations, and deterministic tests can improve the correctness and traceability of Python implementations for a small set of selected quantitative-finance methods.

The project will not attempt to reproduce arbitrary papers, prove that a strategy is profitable, or provide personalised investment recommendations.

## Initial Project Objectives

**O1:** To design and develop a retrieval-augmented assistant that finds relevant passages in selected quantitative-finance research papers and answers questions with source references.

**O2:** To generate Python implementations for one or two selected methods using the retrieved paper content and clearly stated assumptions.

**O3:** To evaluate the system using manually verified reference implementations and predefined test cases, measuring functional correctness, methodological fidelity, citation support, and execution reliability.

## Target Users
Undergraduate students, quantitative-finance learners, and beginner researchers who want to understand and implement methods described in quantitative-finance research papers.

## Data Sources (at least 2)

**Source 1:** ResearchCodeBench paper and benchmark description — useful as evidence and related work, rather than necessarily as the assistant's main knowledge corpus.  
URL: https://proceedings.neurips.cc/paper_files/paper/2025/hash/cd0d0a873cc3e601c76f46dccc3d4c5f-Abstract-Datasets_and_Benchmarks_Track.html

**Source 2:** QuantCode-Eval paper and benchmark description — useful as evidence and related work; verify access to any full text or associated data.  
URL: https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6801618

**Source 3:** Moreira and Muir, “Volatility Managed Portfolios,” NBER Working Paper 22208 — a candidate research paper for the assistant's document corpus.  
URL: https://www.nber.org/papers/w22208

**Source 4:** Moskowitz, Ooi, and Pedersen, “Time Series Momentum” — a candidate research paper for the assistant's document corpus.  
URL: https://doi.org/10.1016/j.jfineco.2011.11.003



## Similar to EduAdvisor
Both systems use document retrieval to answer user questions with evidence from source documents. Both require document processing, retrieval, grounded response generation, and evaluation of answer quality.

## Different from EduAdvisor
EduAdvisor answers questions about university courses and academic policies. QuantPaper AI focuses on interpreting selected quantitative-finance research papers, generating Python implementations of described methods, and checking the implementations against predefined tests. Evaluation therefore includes executable tests and methodological fidelity, not only answer quality.

## Responsible AI Risks

**Risk 1 — Incorrect or incomplete code:** The generated implementation may misinterpret a formula, use incorrect parameters, or omit a paper's assumptions.  
**Mitigation:** Link generated explanations to source passages, state uncertain assumptions, and run predefined tests against manually verified reference implementations.

**Risk 2 — Unsupported explanations or citations:** The assistant may provide an explanation or citation that does not support the generated code.  
**Mitigation:** Display the relevant passages, check that citations refer to retrieved source text, and allow the system to abstain when evidence is insufficient.

**Risk 3 — Financial misuse or overclaiming:** Users may mistake working code or a successful test result for proof that a strategy is profitable or suitable for real trading.  
**Mitigation:** Keep the system educational, use synthetic or clearly documented example data where practical, avoid personalised investment recommendations, and state that software tests do not establish profitability.
