# LongHealth

Companion materials for:

> Adams, L. et al. “LongHealth: A Question Answering Benchmark with Long Clinical Documents.” arXiv:2401.14490 (2024). https://arxiv.org/abs/2401.14490

## Access status

**Publicly available.** The benchmark and evaluation code are hosted in the authors’ [LongHealth GitHub repository](https://github.com/kbressem/LongHealth) under the Apache 2.0 license.

LongHealth contains 20 entirely fictional patient cases and 400 multiple-choice questions. Each case includes multiple long clinical documents and 20 questions covering information extraction, negation or missing information, and temporal ordering.

## Author request about benchmark contamination

The dataset authors ask users not to publicly reproduce benchmark examples, because copied narratives and questions may enter future model-training corpora. They include a canary string to help detect or exclude such contamination.

For that reason, this folder does **not** contain copied patient narratives, questions, answer options, or labels. The notebook downloads the official JSON only when run and displays schema information plus aggregate or redacted case metadata.

## What is here

- `longhealth_loader.ipynb`: a minimal Google Colab-compatible loader for the official `benchmark_v5.json` file.

The notebook:

- downloads the public benchmark directly from the authors’ repository;
- validates the documented case and question fields;
- reports case, document, and question counts;
- displays two safe summaries without names, birthdays, narratives, questions, answers, or labels;
- checks that annotated answer spans use valid normalized document positions without printing their contents.

Only Python’s standard library is required.

## Official resources

- Paper: https://arxiv.org/abs/2401.14490
- Dataset and evaluation code: https://github.com/kbressem/LongHealth
- Dataset schema: https://github.com/kbressem/LongHealth/tree/main/data

The benchmark is for research and evaluation only and must not be used for clinical decision-making.

