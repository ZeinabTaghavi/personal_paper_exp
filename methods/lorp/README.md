# LoRP: LLM-based Logical Reasoning via Prolog

Minimal, Colab-ready demonstration inspired by:

> Zhengkun Di, Chaoli Zhang, Hongtao Lv, Lizhen Cui, and Lei Liu. **LoRP: LLM-based Logical Reasoning via Prolog.** *Knowledge-Based Systems* 327 (2025), 114140.

- Article: https://www.sciencedirect.com/science/article/pii/S0950705125011815
- DOI: https://doi.org/10.1016/j.knosys.2025.114140

## Availability

This is a methodological paper, not a dataset release. No public author repository or downloadable implementation was found through the article metadata and targeted web/GitHub searches on 2026-11-08. The publisher offers an article preview, while the full PDF requires institutional or purchased access.

## What the notebook demonstrates

The article describes four LoRP stages:

1. **Translation:** an LLM converts a natural-language reasoning problem to Prolog.
2. **Validation:** candidate Prolog programs are checked before execution.
3. **Proving:** SWI-Prolog executes the query.
4. **Voting:** three independently generated programs are run and their Boolean answers are combined by majority vote.

[`lorp_toy_demo.ipynb`](lorp_toy_demo.ipynb) implements a transparent toy version of those four stages. Three candidate translations are supplied directly so that the notebook needs no paid LLM API. Two preserve the intended rules and one contains a plausible semantic translation error. The notebook validates their syntax, runs each candidate in SWI-Prolog, and returns the majority result.

## Run in Google Colab

Upload the notebook and select **Runtime → Run all**. Its setup cell installs the Ubuntu `swi-prolog-nox` package. No model weights or API key are required.

## Scope and limitations

- This is an educational reconstruction from the accessible article description, not the authors' code.
- Natural-language-to-Prolog translation is represented by three prewritten candidates.
- Validation checks syntax/executability, not whether a candidate preserves the input's meaning.
- The example uses ordinary Horn clauses and does not reproduce the paper's full FOL-to-extended-Prolog mechanism.
- Majority voting can tolerate an occasional bad translation, but it cannot guarantee correctness when correlated translation errors win the vote.
