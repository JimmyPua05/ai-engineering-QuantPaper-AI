# QuantPaper AI — Evaluation Criteria

**Version:** 1.0

| Objective / Requirement ID | Evaluation Criterion | Capability Bucket | Measurement Method | Metric | Initial Threshold | User Outcome |
|---|---|---|---|---|---|---|
| O1 / FR2 / NFR1 | Research Passage Retrieval | Domain-specific capability | Use manually labelled questions and check whether relevant passages appear in the top five retrieved results. | Recall@5 | ≥ 80% | Users can locate relevant evidence from research papers. |
| O1 / FR3 / RAI1 | Citation Support | Instruction-following capability | Inspect generated explanations and verify whether cited passages actually support the claims. | Citation-source match rate | ≥ 95% | Users can trace explanations back to the original research. |
| O2 / FR4 / NFR2 | Methodological Correctness | Domain-specific capability | Compare generated implementation outputs with manually verified reference implementations using identical test inputs. | Test-case pass rate | ≥ 80% | Users receive implementations that reproduce the selected method on predefined tests. |
| O2 / FR4 | Code Generation Reliability | Generation capability | Generate implementations for a predefined set of supported methods and check whether the code can execute in the controlled environment. | Successful execution rate | ≥ 90% | Users receive usable Python implementations rather than code that fails immediately. |
| O3 / FR5 / RAI2 | Validation Reporting | Instruction-following capability | Check whether the assistant reports passed and failed tests accurately and avoids claiming that execution success proves methodological correctness. | Correct validation-report rate | ≥ 95% | Users can understand what the tests establish and what remains uncertain. |
| O3 / RAI3 / RAI4 | Responsible Use and Execution Safety | Instruction-following capability | Test out-of-scope financial requests and code-execution safety scenarios. | Appropriate refusal rate; unauthorized access incidents | ≥ 95%; 0 incidents | Reduces misleading financial use and unsafe code execution. |
| O1–O3 / NFR4 | Response Latency | Cost and latency | Measure end-to-end response time across a predefined workload. | p90 response latency | ≤ 15 seconds | Users receive sufficiently responsive interactions. |

## Evaluation Dataset

The initial evaluation set should contain:

1. Supported research questions with manually identified relevant passages.
2. Questions requiring explanation of a formula or methodology.
3. Code-generation tasks for selected quantitative finance methods.
4. Test inputs with expected outputs from manually verified reference implementations.
5. Out-of-scope questions involving personalized investment advice or live trading.
6. Code-execution safety test cases.

## Important Evaluation Limitations

- Retrieval quality does not prove that the generated explanation is correct.
- Successful code execution does not prove methodological correctness.
- Passing predefined test cases does not prove that every possible input is handled correctly.
- Passing tests does not establish profitability or future investment performance.

The most important criterion is **Methodological Correctness**, because the project's central purpose is to help users translate research methods into Python faithfully. A program that executes successfully but implements the wrong formula or assumptions does not solve the main problem.