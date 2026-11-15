# QuantPaper AI — Week 3 Pipeline Decisions

**Version:** 1.0  
**Project:** QuantPaper AI — A Research-Grounded Quantitative Finance Code Assistant  
**Date:** 16 November 2026

## 1. Purpose

This document records the data engineering decisions made when designing the Week 3 data-processing pipeline for QuantPaper AI.

QuantPaper AI aims to help undergraduate students and beginner quantitative finance researchers understand research papers and translate selected quantitative finance methods into Python. The system requires reliable access to research-paper content so that it can retrieve relevant passages, provide source references, and support research-grounded code generation.

The Week 3 pipeline focuses on preparing PDF research papers into structured text chunks while maintaining source traceability and repeatable processing.

## 2. Requirements Traceability

The pipeline decisions are based on the following requirements from the Week 2 requirements specification.

| Requirement ID | Requirement | Data Engineering Implication |
|---|---|---|
| FR2 | Retrieve relevant passages from selected research papers. | Research-paper text must be extracted, cleaned, and divided into manageable chunks. |
| FR3 | Provide source references for research-grounded explanations. | Source filenames and processing metadata must be retained. |
| FR4 | Generate Python implementations using retrieved research evidence and explicitly stated assumptions. | The prepared content must preserve important methodological descriptions, formulas, assumptions, and implementation details as far as possible. |
| RAI1 | Provide source references and indicate insufficient evidence. | The pipeline must maintain source provenance and avoid presenting extracted content as complete when extraction has limitations. |

These requirements justify selecting research-paper PDFs as the primary data source and implementing a document-processing pipeline.

## 3. Selected Data Sources

Two quantitative finance research papers were selected for the initial document collection.

| Source ID | Research Paper | Purpose |
|---|---|---|
| S01 | *Volatility Managed Portfolios* — Moreira and Muir (2017) | Provides research content about volatility-managed portfolio strategies. |
| S02 | *Time Series Momentum* — Moskowitz, Ooi, and Pedersen (2012) | Provides research content about time-series momentum strategies. |

Both papers are relevant to the project's initial quantitative finance scope and can support future retrieval and code-generation experiments.

The source metadata, file details, access information, and inspection evidence are recorded in `docs/week3_data_inventory.md`.



## 4. Data Preparation Decision

### 4.1 Selected processing pathway

**Decision:** Use Pathway A — PDF/TXT document processing.

The selected papers are PDF documents containing research descriptions, mathematical explanations, and quantitative finance methodologies.

The pipeline uses PDF text extraction to obtain textual content before cleaning and chunking it for downstream retrieval.

Other pathways, such as image, audio, and time-series processing, are not included in this initial pipeline because they are not required for the current document-based prototype.

### 4.2 Chunking approach comparison

Two chunking approaches were considered:

- **Fixed-size chunking:** Splits extracted text into chunks using a fixed character limit.
- **Paragraph-aware chunking:** Attempts to split text around paragraph boundaries while respecting the configured chunk size.

The comparison uses the same research-paper input where documented.

| Comparison Item | Fixed-size Chunking | Paragraph-aware Chunking |
|---|---|---|
| Splitting method | Uses a fixed character boundary. | Uses paragraph boundaries where possible. |
| Chunk size configuration | 500 characters. | 500 characters. |
| Output for Time Series Momentum | 206 chunks. | 206 chunks. |
| Observed limitation | May split words or sentences at chunk boundaries. | Did not demonstrate a clear improvement in the recorded comparison; similar mid-word splitting artifacts were observed. |

For *Time Series Momentum*, both approaches produced 206 chunks. The inspected output also showed similar mid-word splitting artifacts.

The comparison therefore did not demonstrate a meaningful improvement from paragraph-aware chunking for this particular input.

For *Volatility Managed Portfolios*, the recorded fixed-size export produced 220 non-empty chunks. The current inventory records the fixed-size export and its boundary-splitting limitation; it does not record a separate numerical paragraph-aware comparison for this paper.

### 4.3 Final preparation decision

**Selected method: Fixed-size character chunking with a 500-character chunk size (`fixed-char-500`).**

Reasons for the decision:

1. It provides a simple and consistent chunking configuration.
2. The recorded Time Series Momentum comparison did not show a reduction in the number of chunks or a clear improvement from paragraph-aware chunking.
3. The method is straightforward to reproduce and inspect.
4. It is sufficient for the initial document-processing prototype, subject to later retrieval-quality evaluation.

**Accepted trade-off:** Fixed-size chunking can split words, sentences, mathematical expressions, or other meaningful content across chunk boundaries. This may affect the quality of later retrieval and should be considered during evaluation.

## 5. ETL Pipeline Decision

The project uses an **ETL (Extract, Transform, Load)** approach.

| Stage | Processing Activity | Expected Output |
|---|---|---|
| Extract | Read PDF files and extract their textual content using `pypdf`. | Extracted document text. |
| Transform | Clean unnecessary whitespace and split the extracted text into 500-character chunks. | Structured text chunks. |
| Load | Export the prepared chunks into JSONL files for later retrieval development. | Prepared JSONL documents. |

The JSONL format is selected because it stores each chunk as an individual structured record and can retain associated metadata.

This pipeline prepares document content for future retrieval. It does not yet create embeddings, a vector database, or a complete RAG system.

## 6. Batch or Streaming Decision

**Decision: Use batch processing.**

The initial data sources are static PDF research papers rather than continuously updated data streams.

Batch processing is suitable because:

- The selected research papers can be processed as complete documents.
- The documents do not require real-time ingestion.
- The pipeline can be rerun when a source document or processing configuration changes.
- The resulting outputs can be inspected and compared between runs.

Streaming ingestion is unnecessary for the current prototype and would introduce additional complexity without providing a meaningful benefit.

## 7. Data Storage and Output Organisation

The pipeline separates original inputs, prepared documents, and V1 pipeline outputs.

| Directory | Purpose |
|---|---|
| `data/raw/` | Stores the original PDF inputs during processing. |
| `data/processed/` | Stores prepared JSONL outputs from the Week 3 preparation experiment. |
| `data/pipeline_v1/` | Stores outputs and manifests generated by the repeatable V1 pipeline. |
| `docs/` | Stores the data inventory, pipeline diagram, and decision documentation. |
| `notebooks/` | Stores the executable Week 3 pipeline notebook. |

The two papers are processed separately to avoid overwriting each other's outputs.

Expected V1 output organisation:

```text
data/
├── raw/
│   ├── engineer Volatility Managed Portfolios.pdf
│   └── engineer Time series momentum.pdf
│
├── processed/
│   ├── engineer Volatility Managed Portfolios_prepared_text.jsonl
│   └── engineer Time series momentum_prepared_text.jsonl
│
└── pipeline_v1/
    ├── documents_volatility/
    │   ├── prepared_text.jsonl
    │   └── pipeline_manifest.json
    │
    └── documents_momentum/
        ├── prepared_text.jsonl
        └── pipeline_manifest.json
```

The original PDFs and extracted full-text outputs should remain outside the public repository unless redistribution is permitted. Documentation, pipeline code, and non-restricted metadata can be committed.

## 8. Data Lineage and Provenance Decision

**Decision:** Record source-to-output lineage for each processed PDF.

The pipeline should preserve the relationship between the original research paper and its prepared output.

The lineage record includes:

- Original source filename.
- Source file checksum (SHA-256).
- Processing method and configuration.
- Prepared output filename.
- Output checksum, where recorded.
- Processing and verification status.

The lineage manifest helps identify which source and processing configuration produced a particular prepared document.

A checksum can help detect changes to a file, but it does not prove that the source is accurate, that extraction is complete, or that redistribution is legally permitted.

The Week 3 manifest verification and V1 repeatability checks are recorded in `docs/week3_data_inventory.md`.

## 9. Validation and Failure Handling

The pipeline should validate each stage before proceeding to the next stage.

| Stage | Validation | Failure Handling |
|---|---|---|
| Source ingestion | Confirm that the PDF exists and can be opened. | Stop processing and report a missing or unreadable source. |
| Text extraction | Confirm that extracted text is non-empty. | Report extraction failure and do not export an empty document. |
| Text preparation | Confirm that chunks are generated using the selected configuration. | Report preparation failure if no valid chunks are produced. |
| Output storage | Confirm that the JSONL output exists and contains records. | Report an export failure if the file is missing or empty. |
| Lineage | Verify that source and output metadata are recorded. | Report incomplete provenance information. |
| Repeatability | Rerun the pipeline and inspect whether the expected outputs and processing records are reproduced. | Investigate differences in source files, configuration, or processing behaviour. |

Validation confirms that the pipeline produces usable outputs. It does not establish that every extracted passage accurately preserves the original paper's complete meaning.

## 10. Known Limitations

The current PDF-processing approach has several limitations:

1. **Mathematical expressions:** PDF text extraction may not preserve the original formatting of equations and mathematical symbols.
2. **Tables and figures:** Some visual information may not be represented correctly in extracted text.
3. **Page references:** Whole-document splitting may result in chunks with `page: None`, limiting precise page-level citation.
4. **Text extraction artefacts:** Extracted content may contain ligature characters, unusual spacing, or other formatting artefacts.
5. **Chunk boundaries:** Fixed-size chunking may split words, sentences, or important methodological descriptions.
6. **Copyright restrictions:** Public accessibility does not automatically permit redistribution of the original papers or extracted content.

These limitations mean that extracted chunks should be checked against the original research paper before they are used as evidence for explanations or code generation.

## 11. Final Decisions Summary

| Decision Area | Selected Decision | Reason |
|---|---|---|
| Data source | Two quantitative finance research-paper PDFs | Directly supports the project's research-grounded objectives. |
| Processing pathway | Pathway A — PDF/TXT | Matches the input format and project requirements. |
| Preparation method | Fixed-size chunking | Simple, reproducible, and no clear advantage from paragraph-aware chunking was demonstrated in the recorded comparison. |
| Chunk size | 500 characters | Consistent initial configuration for the prototype. |
| Processing architecture | ETL | Separates extraction, transformation, and output storage. |
| Processing mode | Batch | Suitable for static research documents. |
| Output format | JSONL | Stores individual chunks with structured metadata. |
| Provenance | Source and output lineage manifest | Supports traceability and repeatability. |
| Validation | Extraction, output, lineage, and repeatability checks | Helps identify processing failures. |

## 12. Conclusion

The Week 3 pipeline establishes an initial data-engineering workflow for preparing quantitative finance research papers for future retrieval.

By selecting the PDF/TXT pathway, applying fixed-size 500-character chunking, using batch ETL processing, and recording source-to-output lineage, QuantPaper AI obtains a repeatable document-preparation process aligned with FR2, FR3, FR4, and RAI1.

The prepared JSONL documents are intended to support the next development stage: research-paper retrieval and source-grounded responses.

Further improvements may include page-aware chunking, improved mathematical-content extraction, and retrieval-quality evaluation. These improvements should be considered after evaluating the current prototype.
