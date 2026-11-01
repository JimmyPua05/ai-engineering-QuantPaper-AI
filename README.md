# QuantPaper AI — A Research-Grounded Quantitative Finance Code Assistant

> An AI-powered assistant that helps students and beginner quantitative finance researchers understand research papers and translate selected quantitative finance methods into Python code.

## Problem Statement

Quantitative finance research papers often contain mathematical formulas and technical methodologies that can be difficult for students and beginners to understand and implement correctly. Although Large Language Models (LLMs) can generate Python code, their outputs may contain implementation errors or fail to follow the methods described in the original research. An AI engineering solution combining Retrieval-Augmented Generation (RAG), LLM-based code generation, and automated testing could help users retrieve relevant research evidence, generate implementations, and evaluate their correctness.

## Evidence of the Problem

- **ResearchCodeBench (2025):** Research on evaluating code generation from research papers provides a relevant benchmark for investigating how well AI systems translate research into code.  
  Source: https://proceedings.neurips.cc/paper_files/paper/2025/hash/cd0d0a873cc3e601c76f46dccc3d4c5f-Abstract-Datasets_and_Benchmarks_Track.html

- **QuantCode-Eval (2026):** A related evaluation resource for quantitative research code generation that may help inform the project's evaluation methodology. Its findings and scope should be verified against the full paper before making specific claims.  
  Source: https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6801618

## Initial Related Work / Existing Approaches

- **Paper2Code (ICLR 2026):** Investigates generating code from research papers. It provides a relevant reference for designing a research-to-code workflow. The specific limitations and differences from QuantPaper AI need to be confirmed by reviewing the paper.  
  Source: https://proceedings.iclr.cc/paper_files/paper/2026/hash/41b6674c28a9b93ec8d22a53ca25bc3b-Abstract-Conference.html

- **ResearchCodeBench (2025):** Provides a benchmark related to code generation from research papers. It can inform the evaluation of generated implementations, although a benchmark alone does not provide the complete application proposed in this project.  
  Source: https://proceedings.neurips.cc/paper_files/paper/2025/hash/cd0d0a873cc3e601c76f46dccc3d4c5f-Abstract-Datasets_and_Benchmarks_Track.html

- **QuantCode-Eval (2026):** Relevant to evaluating code generation for quantitative research. Its evaluation methods and limitations should be examined to identify a specific engineering gap that QuantPaper AI can address.  
  Source: https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6801618

## Project Objectives

- **O1:** To develop a RAG system that retrieves relevant information from selected quantitative finance research papers and provides source references.
- **O2:** To generate Python implementations of selected quantitative finance methods based on retrieved research evidence.
- **O3:** To evaluate generated implementations using predefined test cases and verified reference implementations.

## Target Users

- Undergraduate students learning quantitative finance.
- Beginners who want to understand and implement quantitative finance research methods.
- Students and researchers who want to translate mathematical methods from research papers into Python code.

## Data Sources

- **Volatility Managed Portfolios** — Moreira and Muir, NBER Working Paper 22208. A candidate research paper for the initial corpus.  
  URL: https://www.nber.org/papers/w22208

- **Time Series Momentum** — Moskowitz, Ooi, and Pedersen. A candidate paper for exploring and implementing a quantitative finance method.  
  URL: https://doi.org/10.1016/j.jfineco.2011.11.003

- **ResearchCodeBench** — A related research benchmark that may inform evaluation design.  
  URL: https://proceedings.neurips.cc/paper_files/paper/2025/hash/cd0d0a873cc3e601c76f46dccc3d4c5f-Abstract-Datasets_and_Benchmarks_Track.html



## Weekly Progress

| Week | Focus | Deliverable | Status |
|------|-------|-------------|--------|
| W1 | System map + project scope | README + project scope document | ✅ Completed |
| W2 | Related work review + data source selection | Literature review + confirmed data sources | ⬜ Not started |
| W3 | Data processing + retrieval design | Document-processing and retrieval prototype | ⬜ Not started |
| W4 | RAG implementation | Working research retrieval and question-answering prototype | ⬜ Not started |
| W5 | Python code generation | Initial code-generation prototype | ⬜ Not started |
| W6 | Automated validation | Test cases and reference implementations | ⬜ Not started |
| W7 | Evaluation | Experimental results and comparison | ⬜ Not started |
| W8 | Documentation and refinement | Updated README + final project documentation | ⬜ Not started |