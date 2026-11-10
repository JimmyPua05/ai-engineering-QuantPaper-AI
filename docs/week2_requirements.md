# QuantPaper AI — Requirements Specification

**Version:** 1.0  
**Project:** A Research-Grounded Quantitative Finance Code Assistant

## Section 0 — Project Framing & Application Scope

### Problem Evidence

Quantitative finance research papers describe methods through mathematical formulations, assumptions, and experimental procedures. Reproducing these methods in Python requires users to interpret the methodology and translate it into executable code.

Recent work on paper-to-code generation and quantitative code evaluation provides evidence that this is an active engineering problem:

1. **Paper2Code (ICLR 2026):** Investigates transforming machine-learning research papers into code repositories. It provides a relevant reference for research-to-code workflows.
2. **ResearchCodeBench (2025):** Provides a benchmark related to generating code from research papers and can inform evaluation design.
3. **QuantCode-Eval (2026):** Studies quantitative strategy reproduction and provides a domain-relevant reference for evaluating generated quantitative finance code.



### Existing Approaches

| Approach | What it addresses |
|---|---|
| Paper2Code | Research-paper-to-code generation workflow |
| ResearchCodeBench | Benchmarking research-related code generation |
| QuantCode-Eval | Evaluation of quantitative finance code or strategy reproduction |

### Project / Engineering Gap

A generated implementation may execute without errors but still differ from the methodology described in the original research paper. For example, it may use an incorrect lookback window, omit a methodological condition, or misinterpret a mathematical formula.

This project investigates whether combining paper-based retrieval, source-grounded code generation, and automated testing can improve the traceability and methodological correctness of generated quantitative finance implementations.

This is a practical engineering gap, not a claim of scientific novelty.

### Project Objectives

- **O1 — Design:** Design a retrieval-augmented system that retrieves relevant information from selected quantitative finance research papers and provides source references.
- **O2 — Develop:** Develop a code-generation capability that produces Python implementations of selected quantitative finance methods based on retrieved research evidence.
- **O3 — Evaluate:** Evaluate generated implementations using predefined test cases and manually verified reference implementations.

### Intended Users

- Undergraduate students studying quantitative finance.
- Beginners learning to translate quantitative finance research into Python.
- Students and researchers exploring quantitative methods from academic papers.

### Supported Tasks

1. Ask questions about selected quantitative finance research papers.
2. Retrieve relevant passages from the selected papers.
3. Explain the methodology and important assumptions.
4. Generate Python implementations of selected methods.
5. Provide references to the research passages used.
6. Run predefined tests against generated implementations and report the results.

### Information / Knowledge Domain

Selected publicly accessible quantitative finance research papers and their described mathematical methods, assumptions, and implementation procedures.

Initial candidate papers:

- Moreira and Muir — *Volatility Managed Portfolios*.
- Moskowitz, Ooi and Pedersen — *Time Series Momentum*.

### Operating Context

An educational research assistant used by students through an AI application interface. The initial prototype will focus on a small, controlled collection of research papers and a limited number of quantitative finance methods.

### Important Constraints

- Limited project development time and computing resources.
- Availability and accessibility of research papers.
- Difficulty translating mathematical descriptions into unambiguous implementation rules.
- Need for manually verified reference implementations.
- Generated code must be tested in a controlled execution environment.
- Copyrighted research papers must not be redistributed through the public repository without permission.

### Explicit Out-of-Scope Tasks

- Personalized investment or financial advice.
- Live trading or automated trade execution.
- Claims that a tested implementation is profitable.
- Generating and validating arbitrary quantitative strategies outside the selected research corpus.
- Reproducing an entire research paper without a defined implementation scope.

### Evaluation Focus

Does combining research-paper retrieval, source-grounded code generation, and automated testing produce Python implementations that are more traceable and methodologically consistent with selected quantitative finance papers?

---

## Section 1 — Functional Requirements

| ID | Requirement — The system SHALL | Scope Boundary — SHALL NOT |
|---|---|---|
| FR1 | Accept user questions about the selected quantitative finance research papers. | Answer as though unsupported papers are part of its knowledge corpus. |
| FR2 | Retrieve relevant passages from the selected research papers to support its responses. | Present unrelated passages as supporting evidence. |
| FR3 | Provide source references for explanations based on retrieved research content. | Present unsupported claims as if they were stated in the paper. |
| FR4 | Generate Python implementations of selected quantitative finance methods using the retrieved research evidence and explicitly stated assumptions. | Claim that generated code is an exact reproduction when important methodological details remain unresolved. |
| FR5 | Validate generated implementations using predefined test cases and report the test results. | Treat successful execution alone as proof of methodological correctness. |
| FR6 | Indicate when the available research evidence is insufficient to answer a question or implement a method reliably. | Invent missing formulas, parameters, or methodological assumptions. |

## Section 2 — Non-Functional Requirements

| ID | Quality Attribute | Requirement | Measurement Method | Metric | Initial Threshold |
|---|---|---|---|---|---|
| NFR1 | Retrieval Quality | The system shall retrieve relevant research passages for supported questions. | Evaluate a manually labelled set of questions and relevant passages. | Recall@5 | ≥ 80% |
| NFR2 | Correctness | Generated implementations shall produce outputs consistent with manually verified reference implementations on predefined test cases. | Run generated and reference implementations on identical test inputs. | Test-case pass rate | ≥ 80% |
| NFR3 | Reliability | The system shall successfully process supported research-paper queries without unexpected application failures. | Run a predefined workload of supported queries. | Successful query rate | ≥ 90% |
| NFR4 | Performance | The system shall return responses within an acceptable interactive time. | Measure end-to-end response time across the evaluation workload. | p90 response latency | ≤ 15 seconds |
| NFR5 | Code Execution Reliability | The system shall generate implementations that execute successfully in the controlled environment for supported code-generation tasks. | Execute generated implementations using a predefined set of tasks. | Successful execution rate | ≥ 90% |

*Thresholds are proposed targets for the initial prototype. They should be reviewed after the evaluation dataset and implementation scope are finalised.*

## Section 3 — Responsible AI Requirements

| ID | Responsible AI Risk | Requirement | Measurement Method | Metric | Initial Threshold |
|---|---|---|---|---|---|
| RAI1 | Unsupported explanations | The system shall provide source references for research-grounded explanations and indicate when sufficient evidence cannot be retrieved. | Inspect a curated set of responses and verify citations against the original passages. | Citation-source match rate | ≥ 95% |
| RAI2 | Incorrect generated code | The system shall report validation results and distinguish successful test execution from proven methodological correctness. | Test generated-code reports against predefined expected reporting behaviours. | Correct validation-report rate | ≥ 95% |
| RAI3 | Unsafe or misleading financial use | The system shall identify out-of-scope requests for personalized financial advice or live trading and provide an appropriate refusal or redirect. | Test a curated set of out-of-scope financial queries. | Appropriate refusal-and-redirect rate | ≥ 95% |
| RAI4 | Unsafe code execution | The system shall execute generated code in a controlled environment that prevents unauthorized access to sensitive files, credentials, and external network resources. | Run code-execution safety test cases and inspect environment restrictions. | Unauthorized access incidents | 0 |

## Initial Evaluation Notes

The proposed targets are intended for a small educational prototype. Passing tests does not establish that a strategy is profitable or that it will perform well in live markets.

The project should use selected research methods, documented assumptions, controlled test inputs, and manually verified reference implementations.
