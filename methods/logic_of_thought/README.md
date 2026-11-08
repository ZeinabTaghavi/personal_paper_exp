# Logic-of-Thought (LoT)

Minimal, Colab-ready demonstration of **Logic-of-Thought: Injecting Logic into Contexts for Full Reasoning in Large Language Models** (Liu et al., NAACL 2025).

- Paper: https://aclanthology.org/2025.naacl-long.510/
- PDF: https://aclanthology.org/2025.naacl-long.510.pdf
- DOI: https://doi.org/10.18653/v1/2025.naacl-long.510
- Code URL printed in the paper: https://github.com/HEA10R/lot (returned 404 when checked on 2026-11-08)

## What the notebook implements

The paper's pipeline has three phases:

1. **Logic extraction** — an LLM maps natural-language statements to propositions and implications.
2. **Logic extension** — Python expands the implications using double negation, contraposition, and transitivity.
3. **Logic translation** — an LLM translates new implications back to natural language and appends them to the original context.

[`logic_of_thought_demo.ipynb`](logic_of_thought_demo.ipynb) is a deliberately small educational implementation. It reproduces the symbolic extension step with standard Python only and demonstrates the paper's keyboard-skills example. To keep it free and immediately runnable in Colab, the extraction is supplied as a small structured object and the translation is template-based rather than performed by an LLM.

## Run

Upload the notebook to Google Colab and select **Runtime → Run all**. It has no dependencies, downloads, model weights, or API keys.

## Scope and limitations

This is not the authors' full experimental code and does not reproduce their benchmark results. In particular:

- proposition extraction is the most error-prone stage in the paper and is not automated here;
- the translator is intentionally simple and may produce awkward English;
- the demo handles implications between single literals, not conjunctions, quantifiers, or full first-order logic;
- logical equivalences can generate redundant but valid implications.

The notebook is intended to make the central mechanism inspectable and easy to modify before adding an LLM-based extractor or benchmark dataset.
