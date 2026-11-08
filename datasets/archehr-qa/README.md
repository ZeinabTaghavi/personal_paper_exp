# ArchEHR-QA

Companion materials for:

> Soni, S. & Demner-Fushman, D. “A Dataset for Addressing Patient’s Information Needs related to Clinical Course of Hospitalization.” *Scientific Data* 13, 523 (2026). https://doi.org/10.1038/s41597-026-06639-z

## Access status

The dataset is hosted on [PhysioNet](https://physionet.org/content/archehr-qa-bionlp-task-2025/) but is **not anonymously/publicly downloadable**. PhysioNet requires a credentialed account, completion of the CITI “Data or Specimens Only Research” training, and acceptance of the project data-use agreement.

The paper describes 134 cases. The current PhysioNet v1.4 release notes report 167 cases, so results should record the downloaded dataset version.

## What is here

- `archehr_qa_demo.ipynb`: a small Google Colab-compatible notebook with two fully synthetic examples, schema inspection, and a tiny relevance-label summary.
- `examples.json`: the same synthetic examples as a standalone JSON file.

No real patient record or restricted PhysioNet content is included. The examples reproduce the documented logical structure: patient narrative and focal phrases, clinician question, sentence-indexed note excerpt, clinical specialty, clinician answer with citations, sentence-level answer decomposition, and relevance labels (`essential`, `supplementary`, `not-relevant`).

The official release uses XML for case text and JSON for keys/answers/mappings. For convenience, these examples combine those components into one JSON object per case. This makes the examples easy to inspect while retaining the field relationships and ID references needed to write a real XML/JSON loader later.

## Use in Colab

Upload `archehr_qa_demo.ipynb` to [Google Colab](https://colab.research.google.com/) and run all cells. It uses only Python’s standard library and does not require the restricted dataset.

## Official resources

- Paper: https://doi.org/10.1038/s41597-026-06639-z
- Dataset (latest): https://doi.org/10.13026/zzax-sy62
- Authors’ code: https://github.com/soni-sarvesh/archehr-qa

