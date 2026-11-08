# Memory Tax: Dissecting the Net Value of Agent Memory

Paper: [arXiv:2610.34073v1](https://arxiv.org/abs/2610.34073)  
Authors: Xuan He et al. (2026)

## What this paper contributes

The paper argues that an agent-memory system should be compared query by query with a simple retrieval-augmented generation (RAG) baseline. It separates disagreements into:

- **memory benefit:** memory is correct and RAG is wrong;
- **memory tax:** RAG is correct and memory is wrong;
- **net value:** benefit minus tax.

For the same evaluated questions, the normalized net value is exactly the memory system's accuracy change relative to RAG. The paper uses this accounting to study whether memory construction improves access to useful evidence or instead loses, distorts, or hides it.

## Availability

- **Official code:** <https://github.com/hexuan21/MemoryTax> (MIT)
- **Official project page:** <https://hexuan21.github.io/MemoryTax/>
- **Released result repositories:** <https://huggingface.co/datasets/hexuan21/MemoryTax-Res>
- **Public benchmarks:** [LongMemEval](https://huggingface.co/datasets/xiaowu0162/longmemeval), [PersonaMem-v2](https://huggingface.co/datasets/bowen-upenn/PersonaMem-v2), and [MINT-Eval](https://huggingface.co/datasets/dinobby/MINTEval)

The paper introduces an evaluation framework rather than a new dataset. Its official downloader pins the exact benchmark revisions used in the experiments. The released model-result repositories are public but collectively large, so this compact package does not download them.

## Colab demo

`demo.ipynb` is deliberately small and API-free. It:

1. downloads the public PersonaMem-v2 benchmark CSV at the exact revision pinned by the authors;
2. prints two real benchmark rows as JSON-like dictionaries;
3. computes benefit, tax, net value, both-correct, and both-wrong sets from a tiny synthetic paired evaluation;
4. checks that normalized net value equals the accuracy difference.

Only the paired correctness records are synthetic. They make the paper's accounting executable without running multiple expensive memory systems and language models.

## Full reproduction

For the complete benchmark preparation, clone the official repository and run `python common/bench/download.py` followed by `python common/bench/prepare.py`. Full model evaluation additionally needs the relevant memory-system setup and model credentials or endpoints.
