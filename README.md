# RAG-Based Intelligent Academic Assistant Using Large Language Models

> **Master Thesis --- Integrated M.Tech. in Artificial Intelligence**\
> **Student:** Divyansh Rathore\
> **Supervisor:** Dr. Garima Jain\
> **Academic Year:** 2026--27

## Overview

This project develops and experimentally evaluates a
**Retrieval-Augmented Generation (RAG)** pipeline for academic question
answering.

The central goal is to make answers **grounded in academic documents**
rather than relying only on an LLM's learned knowledge. Relevant
evidence is retrieved from an academic document collection and provided
to an LLM for answer generation.

This is designed as an **experimental study, not simply a chatbot**.

## Research Problem

The project investigates how major RAG design choices affect:

-   retrieval quality
-   answer correctness and relevance
-   answer faithfulness
-   citation correctness
-   latency and computational cost

Core research problem:

> How can the major design choices of an academic RAG pipeline be
> systematically evaluated to determine their impact on retrieval
> quality, answer faithfulness, citation correctness, and computational
> cost?

## Research Gap

Existing research has studied individual components such as chunking,
embeddings, sparse/dense retrieval, reranking, faithfulness, and
citation evaluation.

This project focuses on the **joint effect of selected RAG design
choices in a controlled academic question-answering setting**.

## Research Questions

### RQ1 --- Chunking

How does chunking strategy affect retrieval effectiveness?

Metrics: Precision@k, Recall@k, MRR@k.

### RQ2 --- Embeddings and Retrieval

How do embedding models and retrieval methods affect retrieved-passage
relevance?

Methods: Sparse, Dense, Hybrid.\
Additional metric: retrieval latency.

### RQ3 --- Reranking

Does reranking improve quality enough to justify its added latency?

Metrics: MRR@k, Precision@k, Faithfulness, Latency.

### RQ4 --- Grounded Generation

Does retrieval-grounded generation improve faithfulness and citation
correctness?

Configurations: Non-RAG, Basic RAG, Selected RAG, Reranked RAG.

Question types: Single-hop, Multi-hop, Cross-document.

### RQ5 --- Evaluation Reliability

Do automated evaluation scores agree with human judgement?

Comparison: Automated evaluation vs Human judgement.

## System Architecture

### Offline --- Knowledge Base

``` text
Academic Documents
        ↓
PDF Extraction
        ↓
Cleaning
        ↓
Structure Detection
        ↓
Chunking
        ↓
Embeddings
        ↓
Index
```

### Online --- Question Answering

``` text
User Question
      ↓
Query Processing
      ↓
Candidate Retrieval
      ↓
Optional Reranking
      ↓
Context Construction
      ↓
LLM Generation
      ↓
Answer + Evidence
```

### Evaluation

``` text
Question Set
     ↓
Run Configurations
     ↓
Retrieval
     ↓
Answer Quality
     ↓
Faithfulness
     ↓
Citation Correctness
     ↓
Latency / Computational Cost
```

## Current Implementation

The initial knowledge-base and retrieval prototype has been implemented.

``` text
Academic PDF
    ↓
Text Extraction — 471 pages
    ↓
Chunking — 764 chunks
    ↓
all-MiniLM-L6-v2
    ↓
Embeddings
    ↓
ChromaDB
    ↓
Semantic Retrieval
    ↓
Top-5 Relevant Chunks
    ↓
Retrieved Context
```

### Completed

-   PDF text extraction using Python/PyPDF
-   471-page academic PDF processing
-   overlapping text chunking
-   764 chunks
-   `all-MiniLM-L6-v2` embeddings
-   persistent ChromaDB indexing
-   text and metadata storage
-   semantic top-5 retrieval
-   retrieval-to-context pipeline

### Next

-   LLM-based answer generation
-   evidence-grounded answers
-   citation generation/correctness checking
-   baseline RAG
-   reranking
-   controlled experiments
-   multi-hop/cross-document evaluation
-   failure analysis
-   human validation
-   final evaluation

> **Note:** The current implementation is an initial prototype. Final
> controlled experimental results have not yet been reported.

## Controlled Experiments

  -----------------------------------------------------------------------------
  Experiment              Comparison                    Main Measurements
  ----------------------- ----------------------------- -----------------------
  **E0**                  Non-RAG vs Basic RAG          Correctness,
                                                        faithfulness, latency

  **E1**                  Fixed-size vs                 Precision@k, Recall@k,
                          alternative/structure-aware   MRR@k, index size
                          chunking                      

  **E2**                  Sparse vs Dense vs Hybrid     Retrieval quality,
                          retrieval                     retrieval latency

  **E3**                  Reranking OFF vs ON           MRR@k, Precision@k,
                                                        faithfulness, latency

  **E4**                  Non-RAG → Basic RAG →         Correctness,
                          Selected RAG → Reranked RAG   faithfulness, citation
                                                        correctness, latency

  **E5**                  Automated vs Human evaluation Agreement
  -----------------------------------------------------------------------------

## Evaluation Metrics

### Retrieval

-   **Precision@k**
-   **Recall@k**
-   **MRR@k**

### Answer

-   Answer correctness
-   Answer relevance

### Trust

-   Faithfulness
-   Citation correctness

### Efficiency

-   Retrieval/reranking latency
-   End-to-end latency
-   Computational/resource cost

## Failure Analysis

The project investigates where a failure occurs:

1.  **Retrieval failure** --- relevant evidence is not retrieved.
2.  **Ranking failure** --- relevant evidence is retrieved but ranked
    too low.
3.  **Generation failure** --- the answer is incorrect or contains
    unsupported claims.
4.  **Citation failure** --- cited evidence does not support the
    associated claim.

## Single-Hop vs Multi-Hop

**Single-hop:** one relevant passage can generally answer the question.

``` text
Question → Relevant Passage → Answer
```

**Multi-hop:** evidence from multiple passages must be combined.

``` text
Question → Passage A + Passage B → Combined Evidence → Answer
```

**Cross-document:** evidence may come from multiple academic documents.

## Technology Stack

-   Python 3.11
-   pypdf / PyPDF
-   Sentence Transformers
-   `all-MiniLM-L6-v2`
-   ChromaDB
-   PyTorch
-   Transformers
-   Streamlit
-   Git / GitHub

## Research Workflow

``` text
Literature Review
       ↓
Research Gap
       ↓
Research Questions
       ↓
System Architecture
       ↓
Initial Implementation
       ↓
Baseline RAG
       ↓
Controlled Experiments
       ↓
Failure Analysis
       ↓
Human Validation
       ↓
Evidence-Based Conclusions
```

## Expected Contribution

The project does **not** claim RAG, embeddings, chunking, or reranking
as new technologies.

The intended contribution is an empirical study of how selected RAG
design choices behave in an **academic question-answering setting**,
evaluated across:

> **Retrieval quality + Answer quality + Faithfulness + Citation
> correctness + Computational cost**

## Status

  Area                      Status
  ------------------------- -------------------------------
  Literature review         Completed for Review 1
  Research gap              Established
  Research questions        5 defined
  Experimental framework    Designed
  PDF processing            Implemented
  Chunking                  Implemented
  Embeddings                Implemented
  ChromaDB indexing         Implemented
  Semantic retrieval        Initial prototype implemented
  Baseline RAG generation   Next stage
  Reranking                 Planned
  Controlled experiments    Planned
  Multi-hop evaluation      Planned
  Failure analysis          Planned
  Human validation          Planned
  Final evaluation          Planned

------------------------------------------------------------------------

**Project:** RAG-Based Intelligent Academic Assistant Using Large
Language Models\
**Status:** Initial prototype and research design completed; controlled
implementation and evaluation in progress.
