# Explicit Alignment and Many-to-many Entailment Based Reasoning for Conversational Machine Reading

Paper: [ACL Anthology 2023.findings-emnlp.866](https://aclanthology.org/2023.findings-emnlp.866/)  
Authors: Yangyang Luo, Shiyu Tian, Caixia Yuan, and Xiaojie Wang (2023)

## What this paper contributes

The paper presents **BiAE**, a pipeline for conversational machine reading over policy-like rules:

1. split the document into hypotheses and the user information into premises;
2. explicitly align every document hypothesis with the relevant user premises;
3. predict many-to-many entailment states (entailment, contradiction, or neutral);
4. classify the next action as `YES`, `NO`, `MORE`, or `IRRELEVANT`;
5. use a fine-tuned T5 model to generate a follow-up question for `MORE` cases.

## Availability

- **Dataset: public.** The paper uses the ShARC dataset. Its official site distributes the data under CC BY-SA 3.0: <https://sharc-data.github.io/data.html>.
- **Dataset download:** <https://sharc-data.github.io/data/sharc1-official.zip>.
- **Paper repository: incomplete.** The paper links to <https://github.com/AidenYo/BiAE>, but as checked on 2026-11-08 it contains only a one-line README and no implementation, model weights, requirements, or preprocessing scripts.

## Colab demo

`demo.ipynb` is intentionally small. It:

- downloads the official ShARC archive;
- loads the development split and displays two real records;
- summarizes the output-label distribution;
- demonstrates the paper's explicit-alignment idea with a lightweight TF-IDF cosine-similarity matrix.

The alignment cell is a **conceptual demonstration**, not a reproduction of BiAE. The paper uses trainable DeBERTaV3 encodings, Sentence-BERT-derived weak alignment supervision, a learned many-to-many entailment module, and a fine-tuned T5 generator. A faithful run would require the missing official preprocessing/training code and substantial GPU training.

