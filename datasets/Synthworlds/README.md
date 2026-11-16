# SynthWorlds: Controlled Parallel Worlds for Disentangling Reasoning and Knowledge in Language Models

Paper: [arXiv:2510.24427](https://arxiv.org/abs/2510.24427) — ICLR 2026  
Official dataset: [Hugging Face — kenqgu/SynthWorlds](https://huggingface.co/datasets/kenqgu/SynthWorlds)  
Official code: [behavioral-data/synthworlds](https://github.com/behavioral-data/synthworlds)

## Classification

This is both a **dataset/framework paper** and an evaluation study. SynthWorlds builds two structurally parallel worlds:

- **RM (real-mapped):** familiar real-world entity names, where a language model may use memorized facts.
- **SM (synthetic-mapped):** type-consistent invented entity names, where the same reasoning structure remains but memorized entity facts are not useful.

The paired design supports a controlled quantity called the **knowledge advantage gap**:

`KA = performance(RM) - performance(SM)`

A large positive gap suggests that the evaluated system benefits from familiar factual knowledge, not only from the reasoning structure shared by both worlds.

## Public data

The complete benchmark is publicly available under CC BY 4.0. The current Hugging Face release contains:

- `qa-rm` and `qa-sm`: 1,200 paired multi-hop QA instances per world;
- `qa-*-docs`: 6,290 generated documents per world;
- `qa-*-facts`: the underlying facts;
- `wikinav-rm` and `wikinav-sm`: 1,000 paired page-navigation tasks per world; and
- `wikinav-*-pages`: the corresponding page collections.

The QA schema includes `instance_id`, `query`, `gold_answers`, `gold_docs`, `question_graph_type`, `expected_output_is_time`, `gold_qids`, and `mhop_qa`. The last field is itself a JSON string containing the graph template, decomposed questions, and real-to-synthetic entity map.

## Colab demo

`demo.ipynb` is a small, tutorial-style notebook that:

1. fetches two RM rows and their two SM counterparts from the official Hugging Face dataset server;
2. prints compact examples in the actual released schema;
3. pairs records and parses the nested `mhop_qa` metadata;
4. applies the released entity-renaming map to show how reasoning structure is preserved;
5. displays the two supporting documents for one multi-hop question; and
6. implements token F1 and the paper's `KA = F1_RM - F1_SM` calculation using clearly labeled toy predictions.

The notebook downloads only a few sample rows, needs no API key or GPU, and installs no packages. It does not run an LLM or reproduce the paper's full closed-book, HippoRAG, IRCoT, or page-navigation experiments.

## Run

Open `demo.ipynb` in Google Colab and run all cells. Internet access is required to read the public dataset sample.

For the full release, use the official `datasets` loader, for example:

```python
from datasets import load_dataset

qa_rm = load_dataset("kenqgu/SynthWorlds", "qa-rm", split="test")
qa_sm = load_dataset("kenqgu/SynthWorlds", "qa-sm", split="test")
```
