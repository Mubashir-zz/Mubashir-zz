## Mubashir Ahmad Khan

MBBS. Clinical research in neuro-oncology, moving toward computational methods —
MS in Clinical & Epidemiological Research at UCSF, starting Fall 2026.

The work here follows one question: **oncology trials treat the brain, so how
often do they actually measure what happens to it?**

---

### [glioma-nco-registry-study](https://github.com/Mubashir-zz/glioma-nco-registry-study) · R

Cross-sectional registry analysis of 289 randomized glioblastoma and high-grade
glioma trials from ClinicalTrials.gov, ISRCTN, EU-CTR and the WHO ICTRP
registries.

Objective neurocognitive outcomes appear in **13.5%** of trials. Health-related
quality of life appears in **37.2%**. Paired discordance is 70 trials measuring
HRQoL alone against 4 measuring cognition alone (McNemar P<.001). Academic and
cooperative-group sponsors register cognition at roughly three times the
industry rate.

Firth penalized logistic regression rather than ordinary maximum likelihood,
because the international-registry term separates completely at 0/14 events and
ordinary GLM returns an odds ratio of 0.000 with an infinite interval. Bootstrap
optimism correction, E-values, and a sponsor-by-domain interaction test that
comes back at P=.389 — reported, because it limits the claim.

Every table and figure regenerates from one script; the run asserts cohort size
and event count before it estimates anything. Manuscript under revision for the
Journal of Neuro-Oncology.

### [neurocognitive-outcome-classifier](https://github.com/Mubashir-zz/neurocognitive-outcome-classifier) · R + Python

The same question at registry scale, across CNS, breast, lung and head & neck.

1,888 trials hand-labelled one at a time rather than keyword-matched, because
the distinctions that matter are not lexical: a cognitive instrument counts, the
NANO neurologic exam does not, Karnofsky performance status does not, and a
quality-of-life questionnaire's cognitive subscale does not.

A TF-IDF + LASSO baseline in R posts AUROC 0.971 and adds **zero lift** over a
naive keyword rule across all four cancer types. Fine-tuned Bio_ClinicalBERT
beats the baseline **only for CNS**, where the vocabulary is heterogeneous, and
not at all for the other three. Both negative results are the point.

### [cognitive-outcome-classifier-api](https://github.com/Mubashir-zz/cognitive-outcome-classifier-api) · Python

The classifier deployed and serving — hybrid routing, BERT for CNS and the
keyword rule elsewhere, because that is what the evidence supported.

[Live](https://cognitive-outcome-classifier-api.onrender.com/about) · FastAPI,
Docker, tests in CI. The model is int8-quantized to 169MB from 433MB to survive
a 512MB instance, and batches are capped at 3 after larger ones were
out-of-memory killed in production.

Every prediction carries a review flag. Text matching a documented failure
pattern is flagged even when the model is confident, because on those categories
confidence carries no information.

---

**Tools** — R (tidyverse, glmnet, logistf, ggplot2) · Python (PyTorch,
transformers, FastAPI, pandas) · Docker · registry APIs

khanmubashirahmad@gmail.com
