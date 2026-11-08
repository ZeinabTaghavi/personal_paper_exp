# NeSy-RAG

Lightweight companion implementation for:

> Gann, J. & Gertz, M. “NeSy-RAG: Neuro-Symbolic RAG for Explainable Question Answering.” NeSy 2026 / PMLR 284. https://arxiv.org/abs/2608.06292

## Classification

This is a **methodological paper**, not a new dataset paper. It evaluates on the existing ShARC conversational question-answering benchmark. No official implementation link was identified in the paper or arXiv record.

## What is here

- `nesy_rag_toy_demo.ipynb`: a minimal Google Colab-compatible demonstration of the paper’s central neuro-symbolic pipeline.

The notebook demonstrates:

1. A flat collection of retrieved policy chunks.
2. One small symbolic module per chunk.
3. Zero-arity Boolean predicates that expose each module’s meaning.
4. Lightweight natural-language-to-predicate retrieval.
5. Composition of selected predicates into a Boolean query.
6. Dynamic user facts whose values may be missing at inference time.
7. Symbolic knowledge-gap detection by checking whether different assignments change the result.
8. A targeted follow-up question for an influential missing fact.
9. Deterministic re-execution and a trace linking every reasoning step to its source chunk.

## Intentional simplifications

The full system uses LLMs to classify chunks, synthesize Prolog modules, generate interaction methods, compose Prolog queries, and verbalize answers. It uses joint natural-language/code embeddings for predicate retrieval and SWI-Prolog through PySwip for execution.

This notebook replaces those components with hand-authored modules, lexical ranking, and a small Boolean evaluator written with Python’s standard library. It demonstrates the architecture, attribution, and knowledge-gap logic rather than reproducing the paper’s ShARC experiment.

## Official resources

- Paper: https://arxiv.org/abs/2608.06292
- PDF: https://arxiv.org/pdf/2608.06292

