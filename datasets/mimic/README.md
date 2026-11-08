# MIMIC

Companion artifact for:

> Roger Mark. **The Story of MIMIC.** In *Secondary Analysis of Electronic Health Records*, pp. 43–49. Springer, 2016.

- Chapter: https://doi.org/10.1007/978-3-319-43742-2_5
- Open chapter copy: https://www.ncbi.nlm.nih.gov/books/NBK543645/
- MIMIC-III demo: https://physionet.org/content/mimiciii-demo/1.4/

## Availability

The chapter recounts the creation of MIMIC-II and its evolution into MIMIC-III. The full clinical MIMIC databases contain deidentified real patient data but are **credentialed resources**, not anonymous downloads. PhysioNet currently requires an approved account, human-subjects training, and acceptance of the relevant Data Use Agreement.

An official **open MIMIC-III Clinical Database Demo v1.4** is available without credentialing. It contains all ICU stays for 100 patients and follows the full database's 26-table relational schema, except that free-text notes are removed. The demo patients were sampled from patients who eventually died, so the demo is not representative of the full MIMIC-III population.

## Notebook

[`mimic_demo_loader.ipynb`](mimic_demo_loader.ipynb) loads three small tables directly from the official open demo:

- `PATIENTS.csv` — patient-level demographics and mortality fields;
- `ADMISSIONS.csv` — hospital admissions;
- `ICUSTAYS.csv` — ICU stays and lengths of stay.

It validates the relational keys, joins the tables, displays two rows, and converts two joined records to nested JSON. It does not download the 103 MB full demo or any free-text clinical notes.

Upload the notebook to Google Colab and choose **Runtime → Run all**. Only `pandas`, already available in Colab, is required.

## JSON example

[`examples.json`](examples.json) contains two **synthetic** records matching the nested structure produced by the notebook. The values are illustrative and are not patient records.

## Important use restriction

PhysioNet states that credentialed MIMIC data must not be shared with third parties or services that retain it. Researchers using the full database must follow the current agreement and PhysioNet's guidance on LLMs and online services:

- https://physionet.org/about/faqs/
- https://physionet.org/news/post/llm-responsible-use/

The open demo has its own Open Database License, but it still contains deidentified clinical records and should be handled responsibly.
