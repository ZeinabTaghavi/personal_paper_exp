# Logic-LM

Lightweight companion implementation for:

> Pan, L., Albalak, A., Wang, X. & Wang, W. “Logic-LM: Empowering Large Language Models with Symbolic Solvers for Faithful Logical Reasoning.” Findings of EMNLP 2023, pp. 3806–3824. https://doi.org/10.18653/v1/2023.findings-emnlp.248

## Classification

This is a **methodological paper**, not a new dataset paper. Logic-LM is evaluated on five existing benchmarks: ProofWriter, PrOntoQA, FOLIO, LogicalDeduction, and AR-LSAT. The authors provide public code and preprocessed benchmark files in their [GitHub repository](https://github.com/teacherpeterpan/Logic-LLM).

## What is here

- `logic_lm_toy_demo.ipynb`: a minimal Google Colab-compatible implementation of the method’s central pipeline.

The notebook demonstrates:

1. A natural-language problem paired with a symbolic formulation.
2. Facts, explicit negation, and implication rules in a small JSON-like schema.
3. Deterministic forward-chaining inference.
4. Interpretation of a query as `true`, `false`, or `unknown`.
5. A malformed symbolic program that triggers a solver validation error.
6. A small self-refinement step that uses the error to repair a misspelled predicate before retrying.

## Intentional simplifications

The full paper uses an LLM to produce symbolic programs and supports several solver families, including logic programming, first-order logic, constraint optimization, and SAT/SMT solving. This notebook uses a hand-authored formulation and a compact unary-rule engine written with Python’s standard library.

It illustrates the architecture and the faithfulness benefit of deterministic inference; it does not reproduce the paper’s prompts, datasets, models, or reported results.

## Official resources

- Paper: https://aclanthology.org/2023.findings-emnlp.248/
- PDF: https://aclanthology.org/2023.findings-emnlp.248.pdf
- Authors’ code and preprocessed data: https://github.com/teacherpeterpan/Logic-LLM

