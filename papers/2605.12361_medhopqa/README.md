# MedHopQA: A Disease-Centered Multi-Hop Reasoning Benchmark

Paper: [arXiv:2605.12361v1](https://arxiv.org/abs/2605.12361)  
Official project page: [NLM BioNLP — MedHopQA](https://www.ncbi.nlm.nih.gov/research/bionlp/medhopqa)  
Competition: [CodaBench](https://www.codabench.org/competitions/7609/)  
Metadata record: [Zenodo DOI 10.5281/zenodo.16992154](https://doi.org/10.5281/zenodo.16992154)

## Classification

This is a **dataset and evaluation paper**. MedHopQA contains 1,000 expert-curated, open-ended biomedical questions. Each question is designed to require evidence from two Wikipedia articles. The authors place those scored questions inside a public pool of 10,000 questions and withhold their answers to reduce benchmark gaming and contamination.

## Availability

- The official NLM page publishes **15 question–answer examples** directly and links to the benchmark.
- The 10,000-question competition package is distributed through CodaBench; the 1,000 scored items are concealed inside it and their answers are intentionally withheld.
- The linked Zenodo deposit provides metadata and project links, not an anonymous raw copy of the complete answer key.

Therefore, this folder does **not** pretend that the hidden labels are public. The notebook downloads the 15 official examples from the NLM page. If the page is temporarily unavailable, it falls back to two of those same published examples so the tutorial still runs.

## JSON shape used in the notebook

The official web examples do not provide stable IDs, so the notebook adds deterministic local IDs:

```json
{
  "id": "official_example_01",
  "question": "Which benign, autosomal recessive hyperbilirubinemia syndrome is caused by a mutation in the UGT1A1 gene on chromosome 2?",
  "answer": "Gilbert syndrome",
  "source": "NLM MedHopQA public examples"
}
```

This is a transparent teaching representation, not a claim about CodaBench's upload-file schema.

## Colab demo

`demo.ipynb` is a small tutorial that:

1. downloads and parses all 15 official public examples with Python's standard library;
2. displays the records as JSON;
3. explains the two-hop reasoning shape with a simplified evidence chain;
4. implements normalized exact match plus curated answer aliases;
5. evaluates a few predictions and shows why synonym handling matters; and
6. creates a prediction-only JSON object without exposing hidden labels.

No API key, GPU, or package installation is needed. The notebook is an educational benchmark demo, not a clinical decision-support system and not a reproduction of the paper's full expert curation or MedCPT-based concept evaluation.

## Run

Open `demo.ipynb` in Google Colab and run all cells. Internet access is used to fetch the official NLM examples; the two-example fallback supports offline execution.
