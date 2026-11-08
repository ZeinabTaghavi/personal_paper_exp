# Retriever-Free Retrieval: Navigating Documents with Decision Models

Paper: [arXiv:2610.35868v1](https://arxiv.org/abs/2610.35868)  
Authors: Chao Wan, Paul Jünger, Beixi Du, Bodong Liu, Navaneetha Krishnan, and Kilian Q. Weinberger (2026)

## What this paper contributes

The paper presents **DecisionRAG**, which retrieves passages by navigating a corpus hierarchy rather than running a conventional first-stage search:

1. jointly score candidate branches with binary relevance decisions;
2. retain the highest-scoring branches and discard the others;
3. expand the retained branches and repeat until reaching passages;
4. optionally rerank a short passage list with a multiple-choice decision.

The paper's main decision model, Jev 1.13, is accessed through a hosted API. The paper also experiments with trained Qwen3-based decision models.

## Availability

The paper does not introduce a new public dataset. It evaluates on four existing public resources:

- MultiDoc2Dial: <https://huggingface.co/datasets/IBM/multidoc2dial>
- ConditionalQA and its DAPR retrieval version: <https://huggingface.co/datasets/UKPLab/dapr>
- MTRAG: <https://github.com/IBM/mt-rag-benchmark>
- Natural Questions in DAPR: <https://huggingface.co/datasets/UKPLab/dapr>

The exact experimental artifacts were not publicly located as of 2026-11-08. This includes the DecisionRAG implementation, the paper's processed hierarchies and routing metadata, the 500 sampled Natural Questions IDs, generated cluster summaries, trained decision-model checkpoints, and expanded MTRAG relevance judgments.

## Colab demo

`demo.ipynb`:

- loads the small public `ConditionalQA-queries` split from DAPR and displays two records;
- creates a tiny three-level corpus tree;
- implements the paper's irreversible top-k navigation loop;
- uses token-overlap similarity as a transparent stand-in for a decision model, requiring no API key or GPU.

The stand-in scorer does **not** reproduce the paper's shared-context decision probabilities. It exists only to make the tree traversal and pruning algorithm runnable and easy to inspect. Reproducing the reported benchmarks would require the missing preprocessing artifacts plus either Jev API access or training an open-weight decision model.

