# QuantPaper AI — Architecture Decisions and Traceability

**Version:** 1.0

## Section 1 — Architecture Decision Records

### ADR-01: Include Research Paper Knowledge Access

| Item | Description |
|---|---|
| Decision | Include a research-paper retrieval component. |
| Requirement / Constraint | FR2, FR3, RAI1 — responses must be grounded in selected research papers and provide source references. |
| Alternatives Considered | Base language model only; static document lookup; retrieval-based knowledge access. |
| Selected Option | Retrieval-based access to the selected research-paper collection. |
| Trade-off Accepted | Adds document processing and retrieval complexity, but improves access to relevant evidence and source traceability. |

### ADR-02: Include Code Validation

| Item | Description |
|---|---|
| Decision | Include a separate code validation and test-running component. |
| Requirement / Constraint | FR5, NFR2, RAI2 — generated implementations must be tested and validation results must be reported accurately. |
| Alternatives Considered | Generate code only; generate code and check syntax; generate code and compare results against predefined tests and verified references. |
| Selected Option | Generate code and validate it using predefined tests and manually verified reference implementations. |
| Trade-off Accepted | Requires additional test-case development and reference implementations, but provides stronger evidence than code generation or syntax checking alone. |

### ADR-03: Include Explicit Scope Control

| Item | Description |
|---|---|
| Decision | Include an explicit scope and request-control capability. |
| Requirement / Constraint | RAI3 — the application must not provide personalized investment advice or support live trading. |
| Alternatives Considered | Rely only on the language model's instructions; include an explicit scope-control step. |
| Selected Option | Include an explicit scope-control step in the request flow. |
| Trade-off Accepted | Adds processing complexity and may occasionally reject a borderline valid request, but makes the intended application boundary clearer. |

## Section 2 — Initial Requirements Traceability Matrix

| Objective | Requirement | Evaluation Criterion | Architecture Element | Later Evidence |
|---|---|---|---|---|
| O1 | FR2 / NFR1 | Research Passage Retrieval | Research Paper Retrieval | Recall@5 results on manually labelled questions. |
| O1 | FR3 / RAI1 | Citation Support | Retrieved Passages and References | Citation-source verification results. |
| O2 | FR4 / NFR2 | Methodological Correctness | Language Model + Code Validation | Comparison against verified reference implementations. |
| O3 | FR5 / RAI2 | Validation Reporting | Code Validation and Test Runner | Validation-report test results. |
| O3 | RAI3 / RAI4 | Responsible Use and Execution Safety | Scope Control + Controlled Code Execution | Safety and scope test results. |

## Section 3 — Architecture Review

The V1 architecture is designed around the main requirements of QuantPaper AI.

The research-paper retrieval component supports evidence-grounded explanations. The language model supports explanation and Python code generation. The validation component provides a way to compare generated implementations against predefined tests and verified references.

The architecture also includes scope control and controlled code execution to address responsible AI risks.

The design intentionally avoids committing to specific models, vector databases, frameworks, or deployment platforms at this stage. These choices can be refined during implementation.

### Final Review

- Each major component is linked to at least one requirement.
- Research evidence and references are represented in the information flow.
- Code validation is separated from code generation.
- Scope and safety controls are included.
- The architecture remains conceptual and can be simplified or refined as implementation progresses.