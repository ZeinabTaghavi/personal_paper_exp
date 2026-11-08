# HolisQA

Companion materials for:

> Wang, N. et al. “CausalRAG2: Hierarchical Causal Knowledge Graph Design for RAG.” ICML 2026. https://arxiv.org/abs/2602.05143

## Access status

**Publicly available.** The authors release HolisQA in the public [CausalRAG2 GitHub repository](https://github.com/Pwnb/CausalRAG2/tree/main/data/holisqa) under the repository’s MIT license.

HolisQA contains approximately 2,200 multi-sentence question-answer pairs built from 2025 open-access paper abstracts. It covers five domains: biology, business, computer science, medicine, and psychology.

## What is here

- `holisqa_loader.ipynb`: a minimal Google Colab-compatible notebook that downloads one selected domain’s `qa.jsonl` directly from the authors’ repository, validates the documented schema, and displays two records.

The notebook defaults to the `medicine` domain. Change the `DOMAIN` variable to any of:

```python
biology
business
computer_science
medicine
psychology
```

Only Python’s standard library is needed. The notebook does not copy the complete dataset into this repository; it retrieves the current public file when executed.

## Record schema

Each `qa.jsonl` record contains:

- `qa_id`
- `category`
- `slice_id`
- `question`
- `answer`
- `context_sentence_ids`
- `context_text`

The released records may also contain metadata such as `created_at`.

## Method note

The paper also introduces the CausalRAG2 method: hierarchical graph construction, offline causal gates, multi-level seeding, gated traversal, causal-path filtering, and answer generation. That method is intentionally not reimplemented here because its desired scope has not yet been specified.

## Official resources

- Paper: https://arxiv.org/abs/2602.05143
- Code and dataset: https://github.com/Pwnb/CausalRAG2
- Dataset documentation: https://github.com/Pwnb/CausalRAG2/blob/main/data/holisqa/README.md

