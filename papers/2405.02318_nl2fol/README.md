# Autoformalizing Natural Language to First-Order Logic

Paper: [arXiv:2405.02318v3](https://arxiv.org/abs/2405.02318)  
Authors: Abhinav Lalwani et al. (2024; revised 2025)

## What this paper contributes

NL2FOL is a neurosymbolic pipeline for translating a natural-language argument into first-order logic and testing its validity with an SMT solver. Its main stages are:

1. split the argument into claims and an implication;
2. extract entities, predicates, and their relationships;
3. add relevant background relations, including relations proposed through natural-language inference;
4. compose a first-order logical formula;
5. ask a solver whether the premises together with the **negated conclusion** are satisfiable;
6. interpret a satisfying countermodel as an explanation of the fallacy.

If the negated conclusion is satisfiable, at least one counterexample is compatible with the premises, so the argument is not logically valid. If it is unsatisfiable, the conclusion follows under the supplied formalization and background assumptions.

## Availability

- **Official implementation:** <https://github.com/lovishchopra/NL2FOL> (MIT)
- **Public data used by that implementation:** `data/fallacies.csv` and `data/fallacies_climate.csv`
- **Original LOGIC and LOGICCLIMATE release:** <https://github.com/causalNLP/logical-fallacy>

This is primarily a method paper, not a new dataset release. It evaluates on the previously published LOGIC and LOGICCLIMATE datasets. The authors' repository publicly includes prepared CSV files, prompts, source code, evaluation scripts, and results.

## Colab demo

`demo.ipynb` is a compact, API-free illustration. It:

- downloads the public `fallacies.csv` file from the official repository;
- displays two real rows in a compact JSON shape;
- installs the lightweight `z3-solver` package;
- manually formalizes one invalid generalization and one valid implication;
- checks `premises AND NOT(conclusion)` and prints a countermodel for the fallacy.

The manual formalizations replace the paper's LLM and NLI translation stages. This keeps the notebook deterministic and small while preserving the central symbolic validity test.

## Full reproduction

The complete repository requires language and NLI models for natural-language decomposition, relation discovery, FOL construction, and countermodel interpretation. Its documented entry point is `src/nl_to_fol.py`, followed by FOL-to-SMT conversion and metric scripts. Those stages are intentionally outside this minimal Colab.
