# A Neurosymbolic Approach to Natural Language Formalization and Verification

Paper: [arXiv:2511.09008v1](https://arxiv.org/abs/2511.09008v1)  
Authors: Bayless et al. (2025)

## What this paper contributes

The paper presents **Automated Reasoning Checks (ARC)**, a two-stage system:

1. A Policy Model Creator translates natural-language policies into a typed SMT-LIB policy model.
2. An Answer Verifier translates claims into premise/conclusion formulas and asks an SMT solver whether each conclusion follows from the policy.

The full ARC implementation is not released with the paper. In particular, its LLM prompts, generated policy models, and redundant-translation pipeline are not available.

## Dataset availability

| Dataset | Status | Notes |
| --- | --- | --- |
| ConditionalQA | Public | The source dataset is released under CC BY-SA 4.0 at <https://github.com/haitian-sun/ConditionalQA>. |
| CONDITIONALQA-LOGIC | Not publicly located | The paper derives 522 examples from ConditionalQA: 349 Valid, 103 Invalid, 52 Satisfiable, 4 Impossible, and 14 NoTranslations. It describes the transformations, but does not link to a release. |
| Six-business policy dataset | Not publicly located | The paper describes customer-facing policies collected from six businesses and a manually labelled RyanAir case study, but provides no artifact link or schema release. |

`examples.json` therefore contains **synthetic schema examples**, not rows claimed to come from the unreleased datasets.

## Colab demo

Open `demo.ipynb` in Google Colab. It:

- downloads the public ConditionalQA development split directly from the official repository;
- prints two source examples;
- loads the local synthetic JSON examples when the repository is cloned, with an embedded fallback for a standalone Colab upload;
- implements a small, deterministic version of ARC's symbolic verification stage with Z3.

The demo deliberately omits natural-language-to-logic translation, ensemble agreement, policy vetting, and feedback generation. Those components require unreleased implementation details and LLM calls.

## Files

- `demo.ipynb` — minimal Colab-compatible loader and method demonstration
- `examples.json` — two synthetic examples matching a practical reconstruction of the paper's evaluation format

