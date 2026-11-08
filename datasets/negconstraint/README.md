# NegConstraint

Dataset companion for:

> Ganlin Xu, Zhoujia Zhang, Wangyi Mei, Jiaqing Liang, Weijia Lu, Xiaodong Zhang, Zhifei Yang, Xiaofeng Ma, Yanghua Xiao, and Deqing Yang. **Logical Consistency is Vital: Neural-Symbolic Information Retrieval for Negative-Constraint Queries.** Findings of ACL 2025.

- Paper: https://aclanthology.org/2025.findings-acl.92/
- PDF: https://aclanthology.org/2025.findings-acl.92.pdf
- Authors' repository: https://github.com/xgl-git/NS-IR-main
- Dataset archive: https://raw.githubusercontent.com/xgl-git/NS-IR-main/main/NegConstraint.zip

## What it contains

NegConstraint evaluates retrieval for queries that include explicit exclusions, such as asking about an author's work while excluding one title. The paper defines three formulations:

- `A - a`
- `(A - a) ∪ B`
- `(A - a) ∪ (B - b)`

The released archive uses the familiar BEIR-style layout:

- `corpus.jsonl`: 3,946 documents with `_id` and `text`;
- `queries.jsonl`: 366 queries with `_id` and `text`;
- `test.tsv`: tab-separated `query-id`, `corpus-id`, and relevance `score`.

## Release audit

The paper reports 366 queries: 136 + 123 + 107 across its three formulations. The current public archive indeed contains 366 query records. However, `test.tsv` contains only 198 relevance judgments, covering query IDs `0` through `197`; 168 released queries have no qrel in the archive. This was verified against the public ZIP on 2026-11-08.

Consequently, evaluations using the repository as released should either:

- restrict evaluation to the 198 judged queries; or
- obtain the missing relevance judgments from the authors.

Do not silently interpret an absent qrel as a negative label.

## Notebook

[`negconstraint_loader.ipynb`](negconstraint_loader.ipynb) uses only Python's standard library. It:

1. downloads the public 1 MB ZIP directly from the authors' repository;
2. reads its JSONL and TSV files in memory;
3. validates identifiers and relevance targets;
4. reports the missing-qrel discrepancy; and
5. displays two joined query/positive-document examples.

Upload it to Google Colab and choose **Runtime → Run all**.

## Format example

[`examples.json`](examples.json) contains two synthetic examples of a convenient joined representation. These are structural examples, not records copied from Wikipedia or the released dataset.

## Method note

The accompanying NS-IR method initially retrieves documents with BGE, translates the query and candidate documents to first-order logic using an LLM, and reranks them using logic alignment and connective constraints. Reproducing the full method is intentionally outside this loader: the paper reports GPT-4o translation and an NVIDIA A800 80 GB GPU, while this project artifact is meant to stay small and Colab-friendly.

## License note

The repository makes the archive publicly downloadable, but no explicit `LICENSE` file or dataset license was visible in the repository when checked on 2026-11-08. Confirm permitted reuse with the authors/repository before redistribution or commercial use, and cite the paper.
