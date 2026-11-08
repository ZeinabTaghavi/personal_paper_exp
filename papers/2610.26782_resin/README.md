# RESIN: Multi-Chain Reasoning with Entity-Structured Indexing

Paper: [arXiv:2610.26782v1](https://arxiv.org/abs/2610.26782)  
Authors: Xuanyu Meng, Jash Rajesh Parekh, and Jiawei Han (2026)

## What this paper contributes

RESIN separates evidence organization from final reasoning:

1. **Offline:** convert source passages into typed, entity-centered reasoning units. Each unit retains an exact pointer to its source evidence.
2. **Plan:** decompose a multi-chain question into focused one-hop evidence needs, with targets, bridge terms, and dependencies.
3. **Retrieve:** independently retrieve a small candidate set for every hop instead of forcing one early reasoning path.
4. **Buffer:** keep the candidates and their alternatives together in a bounded reasoning buffer.
5. **Compose:** recover the original source passages and answer the full question only after all evidence needs are visible.

The index is used as an address into evidence, not as a substitute for the evidence. Delaying final selection helps avoid losing a chain that appears unimportant before the other chains are assembled.

## Availability

- **Official RESIN code:** <https://github.com/RamonMeng/RESIN>
- **HolisQA release:** <https://github.com/Pwnb/CausalRAG2/tree/main/data/holisqa> (five domains, approximately 2,200 QA pairs; repository released under MIT)
- **QASC:** <https://huggingface.co/datasets/allenai/qasc> (CC BY 4.0)
- **MS MARCO:** <https://huggingface.co/datasets/microsoft/ms_marco>

This is a method paper rather than a new dataset paper. Its main evaluation uses the previously released HolisQA benchmark, with additional QASC and MS MARCO experiments. Full RESIN runs require model credentials and the benchmark preparation/indexing pipeline.

## Colab demo

`demo.ipynb` is small, deterministic, and API-free. It:

- streams only the first two public HolisQA biology records from the official JSONL file;
- constructs a tiny typed reasoning-unit store for a route-comparison example;
- plans separate bus and metro evidence needs;
- retrieves candidates independently and retains them in a reasoning buffer;
- follows provenance pointers back to the original passages;
- computes the answer from those source passages after both chains are available.

The unit extraction, planning, retrieval scoring, and final composition are deliberately simplified. The full implementation uses language models, embeddings, top-k retrieval, and benchmark-specific generation and evaluation.

## Full reproduction

The official guide uses `gpt-5-nano` for generation and separate RAGAS evaluation. HolisQA must be copied from the CausalRAG2 release, while the provided scripts can download selected QASC and MS MARCO validation examples from Hugging Face. API credentials and substantially more computation are required for the reported experiments.
