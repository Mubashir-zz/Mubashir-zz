# Mubashir Ahmad Khan, MBBS

Clinical researcher working at the intersection of neuroscience, clinical outcomes research, and biomedical informatics. I completed my medical degree at Zhengzhou University in 2025. My work uses clinical and trial-registry data to study how neurological and functional outcomes are defined, measured, and sometimes lost in research pipelines.

My current interests include cognitive and functional recovery after brain injury and disease, neuroinflammation and blood-brain barrier injury after stroke, hippocampal memory, clinical outcome measurement, and reproducible analysis in R and Python.

## Research

### [Objective neurocognitive endpoints in randomized glioma trials](https://github.com/Mubashir-zz/glioma-nco-registry-study)

First-author registry study of 289 randomized phase II-III glioblastoma and high-grade glioma trials. I led the protocol development, trial reconciliation, screening, endpoint adjudication, R analysis, and preparation of the reproducible research files. The analysis uses paired within-trial outcome comparisons and Firth penalized regression to handle sparse strata and separation. The manuscript is under review at *Supportive Care in Cancer*.

### [Neurocognitive outcome ascertainment in oncology trials](https://github.com/Mubashir-zz/neurocognitive-outcome-classifier)

A human-adjudicated reference set of 1,888 oncology trials, including 1,804 records used for classifier development and stratified evaluation. I compared a deterministic rule, TF-IDF with LASSO, and Bio_ClinicalBERT. The central result was methodological: an apparent advantage of contextual modeling arose because the stored registry text was truncated. Restoring complete outcome text changed the conclusion and showed why input provenance must be audited before model performance is interpreted.

### [Neurocognitive outcome classifier API](https://github.com/Mubashir-zz/cognitive-outcome-classifier-api)

A FastAPI and Docker serving implementation with explicit uncertainty flags, automated decision-logic tests, and a model card documenting known errors. The public v1 endpoint preserves the original hybrid routing for reproducibility, but its CNS BERT route is now treated as legacy because complete-text validation favored the deterministic rule. A corrected, versioned routing decision is required before this system should be used beyond research screening.

### [Functional-outcome registration in oncology trials](https://github.com/Mubashir-zz/ctgov-functional-outcomes)

Reproducible analysis of 93,371 outcome-bearing ClinicalTrials.gov cancer records across 14 functional domains. The project combines deterministic extraction, a human reference standard, design weights, misclassification correction, direct standardization, cluster bootstrap uncertainty, and BCa intervals. Its purpose is to distinguish relative enrichment from adequate absolute measurement rather than treating either as sufficient alone.

## Research background

- MBBS, Zhengzhou University, 2025.
- Neurosurgical clinical and laboratory research training at the First Affiliated Hospital of Zhengzhou University, including a Chiari I outcomes study and assisting work in a rodent intracerebral hemorrhage laboratory.
- Clinical internship at Henan Provincial People's Hospital of Zhengzhou University.
- Two peer-reviewed articles, one book chapter in neurointerventional history, and a conference poster on outcomes after Chiari decompression.
- Current protocol collaboration on retrospective peripheral-nerve recovery studies.

## Methods

**R:** tidyverse, readxl, logistf, glmnet, ggplot2, boot; registry reconciliation, endpoint adjudication, Wilson intervals, McNemar tests, bootstrap estimation, penalized regression, and reproducible figures.

**Python:** pandas, NumPy, scikit-learn, PyTorch, Transformers, FastAPI, automated testing, GitHub Actions, Docker, model cards, codebooks, and provenance records.

## Contact

- [ORCID 0009-0003-9842-4513](https://orcid.org/0009-0003-9842-4513)
- [khanmubashirahmad@gmail.com](mailto:khanmubashirahmad@gmail.com)
