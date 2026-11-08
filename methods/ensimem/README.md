# EnSIMem

Lightweight companion implementation for:

> Meng, X. et al. “EnSIMem: Entity-Structured Indexing for Long-Term Agent Memory.” arXiv:2609.27279 (2026). https://arxiv.org/abs/2609.27279

## Classification

This is a **methodological paper**, not a dataset paper. It evaluates on existing long-term-memory benchmarks, including LoCoMo and LongMemEval, and provides an official implementation at https://github.com/RamonMeng/EnSIMem.

## What is here

- `ensimem_toy_demo.ipynb`: a minimal Google Colab-compatible demonstration of the paper’s central design principle.

The notebook shows:

1. Theme-coherent episodes containing original dialogue turns.
2. Compact records of the form `[entity][entity_type][property:value]`.
3. Provenance links from each index record back to source turns.
4. Query requirements aligned with entity and property fields.
5. Query-type-aware retrieval for point, temporal, and aggregation requests.
6. Expansion of selected records into an evidence buffer containing original dialogue rather than a lossy summary.

## Intentional simplifications

The paper uses language models for episode partitioning, index extraction, query planning, dense fallback retrieval, and answer generation. The notebook replaces those components with small, inspectable examples and deterministic Python. It demonstrates the information flow and data structures, not the full reported system or its accuracy.

The notebook requires only Python’s standard library, no model download, and no API key.

## Official resources

- Paper: https://arxiv.org/abs/2609.27279
- Authors’ code: https://github.com/RamonMeng/EnSIMem

