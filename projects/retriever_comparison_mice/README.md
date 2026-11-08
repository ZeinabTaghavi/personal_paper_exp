# Retriever Architecture Tutorial: ColBERT, Cross-Encoder, and MICE-P

Paper anchor: [MICE to Meet You: From Re-ranking Only to End-to-End Retrieval](https://arxiv.org/abs/2610.31932)  
Official code: <https://github.com/xpmir/mice>

## Goal

This project explains and runs three different relevance-scoring architectures:

- **ColBERTv2:** encode the query and document independently into one vector per token, then use MaxSim to match every query token to its best document token.
- **Cross-encoder:** concatenate the query and document and run all transformer layers jointly, allowing full token-to-token interaction but requiring a new forward pass for every pair.
- **MICE-P:** independently contextualize the document in lower layers, store a compressed token representation, then restore it and use learned transformer interaction layers with the query at scoring time.

The central question is not simply “which model is best?” It is: **where does query–document interaction happen, what can be precomputed, and what must be recomputed for every query?**

## Project files

- `retriever_tutorial.ipynb` — a Colab-oriented tutorial using real public checkpoints.
- `requirements.txt` — the same core dependencies installed by the notebook setup cell.

## Models used

- ColBERT: [`lightonai/colbertv2.0`](https://huggingface.co/lightonai/colbertv2.0)
- Cross-encoder: [`cross-encoder/ettin-reranker-68m-v1`](https://huggingface.co/cross-encoder/ettin-reranker-68m-v1)
- MICE-P: [`xpmir/Mice-P-61m`](https://huggingface.co/xpmir/Mice-P-61m)

The cross-encoder and MICE-P checkpoints use the same 68M Ettin backbone family, which makes their architectural contrast especially useful. The public ColBERTv2 checkpoint uses a different BERT backbone, so the notebook is a **learning comparison**, not a controlled reproduction of the paper's matched training experiment.

## What the notebook teaches

1. Build a small corpus with known relevant documents.
2. Inspect how a cross-encoder tokenizes a query–document pair.
3. Score all pairs with the cross-encoder.
4. precompute ColBERT document-token matrices and inspect MaxSim directly.
5. Score the same pairs with the released MICE-P checkpoint and inspect its split-layer configuration.
6. Compare rankings, reciprocal rank, and timing components.
7. Run a custom query through all three scorers.

Raw scores are not compared across models because their numerical scales are not calibrated to one another. Rankings are the meaningful comparison.

## Important production distinction

The toy corpus is small enough that every scorer can inspect every document. At large scale:

- ColBERT can use PLAID as its first-stage index and scorer.
- A cross-encoder normally reranks candidates retrieved by BM25, a dense retriever, or SPLADE.
- The paper's MICE-P pipeline retrieves top candidates with DistilBERT-SPLADEv3, stores compressed document-token states using FastPLAID, decompresses candidate states, and scores them with MICE interaction layers. It uses PLAID's storage format, but does not use PLAID's MaxSim candidate-generation procedure.

Therefore the notebook faithfully compares the three **scorers** and their data flow, but it does not build the paper's full million-document SPLADE/FastPLAID infrastructure.

## Colab expectations

The first run downloads roughly a few hundred million model parameters in total. A GPU runtime is helpful but not required for the tiny corpus. The MICE checkpoint uses trusted remote model code published with the checkpoint; the notebook calls this out before loading it.
