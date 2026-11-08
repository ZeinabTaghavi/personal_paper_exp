# EnSIMem: Entity-Structured Indexing for Long-Term Agent Memory

Paper: [arXiv:2609.27279v2](https://arxiv.org/abs/2609.27279)  
Authors: Xuanyu Meng, Xing Fan, Xinyi Fan, Chenlei Guo, Yixuan Xie, and Jiawei Han (2026)

## What this paper contributes

EnSIMem separates long-term agent memory into two parts:

1. **Offline construction:** divide dialogue into coherent episodes, extract records shaped like `[entity][entity_type][property: value]`, and retain links to the original turns and timestamps.
2. **Online access:** decompose a query into evidence requirements, match entity/property records, retrieve enough episodes for the requested reasoning type, and answer from the original evidence rather than from the compressed index.

The index is therefore an address into evidence, not a replacement for evidence.

## Availability

- **Official EnSIMem code:** <https://github.com/RamonMeng/EnSIMem>
- **LoCoMo dataset:** <https://github.com/snap-research/locomo> (CC BY-NC 4.0)
- **LongMemEval dataset:** <https://github.com/xiaowu0162/LongMemEval> (MIT)

The EnSIMem repository includes complete LoCoMo and LongMemEval evaluation pipelines, but does not redistribute the datasets. Its documented reproduction setup requires Python 3.10, OpenAI access to `gpt-4.1-mini` and `gpt-4o-mini`, local embedding and cross-encoder downloads, and—on the reported LongMemEval setup—a separately served Qwen3-32B model.

## Colab demo

`demo.ipynb` is a small, API-free illustration. It:

- downloads the official LoCoMo JSON directly;
- displays two real QA examples and source dialogue turns;
- constructs two grounded entity/property records from the first conversation;
- plans a point query, performs structured lookup, and expands the matching source turn;
- prints an auditable query → record → source-evidence trace.

The two demonstration records are manually authored from the loaded dialogue so that the notebook remains deterministic. The full system uses language models for episode construction, entity/event extraction, property normalization, query planning, dense fallback, answer generation, and evaluation.

