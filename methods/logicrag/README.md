# LogicRAG

Lightweight companion implementation for:

> Chen, S. et al. “You Don’t Need Pre-built Graphs for RAG: Retrieval Augmented Generation with Adaptive Reasoning Structures.” AAAI 2026. https://arxiv.org/abs/2508.06105

## Classification

This is a **methodological paper**, not a new dataset paper. It evaluates on existing multi-hop question-answering benchmarks. The authors’ implementation is publicly available at https://github.com/chensyCN/LogicRAG.

## What is here

- `logicrag_toy_demo.ipynb`: a minimal Google Colab-compatible demonstration of LogicRAG’s query-time reasoning structure.

The notebook demonstrates:

1. Decomposing one multi-hop question into interdependent subproblems.
2. Representing those dependencies as a directed acyclic graph (DAG).
3. Validating and linearizing the DAG with topological sorting.
4. Resolving subproblems sequentially, with earlier answers inserted into later retrieval queries.
5. Retrieving from a flat text corpus without constructing a corpus-level knowledge graph.
6. Maintaining a compact rolling memory containing only the supporting evidence.
7. Preserving a trace from each subproblem to its retrieved document and intermediate answer.

## Intentional simplifications

The full system uses LLMs for query decomposition, dependency prediction, subproblem resolution, dynamic DAG expansion, graph pruning, context summarization, self-reflection, and final answer generation. This notebook uses a hand-authored DAG, lexical retrieval, and deterministic regular-expression extraction so that the information flow is transparent and runnable without an API key.

It demonstrates the architecture rather than reproducing the paper’s experiments or performance.

## Official resources

- Paper: https://arxiv.org/abs/2508.06105
- Version used here: https://arxiv.org/pdf/2508.06105v2
- Authors’ code: https://github.com/chensyCN/LogicRAG

