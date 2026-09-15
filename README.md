## Mubashir Ahmad Khan

MBBS. Clinical research in neuro-oncology, moving toward computational methods.

The work here follows one question: **oncology trials treat the brain, so how
often do they actually measure what happens to it?**

---

### [ctgov-functional-outcomes](https://github.com/Mubashir-zz/ctgov-functional-outcomes) · Python

Registration is where a trial declares what it intends to measure. Across 93,371
outcome-bearing ClinicalTrials.gov cancer records and 14 functional domains, this asks
whether the outcome matching a drug's best-documented toxicity is among them. The
anchor is cisplatin, which causes permanent hearing loss in a large share of the
patients who receive it.

Of 2,189 modern therapeutic cisplatin trials, **27** register a hearing outcome.
1.72% after direct standardisation for cancer site, phase and era, against 0.15% in
matched comparator strata — rate ratio **11.88 (95% CI 6.34–21.92)**. Corrected for
classification error the corpus-wide rate is **0.12% (0.06–0.17)** against an observed
0.21%. Relative enrichment and an absolute rate under 2% are both true at once.

The ground truth is 7,966 paired domain labels from two independent clinician passes,
97.21% raw agreement, all 222 disagreements resolved by documented human adjudication.
No model output enters it.

Accuracy uncertainty comes from a cluster bootstrap of the validation design rather
than independent Beta approximations per cell — sensitivity and specificity are drawn
from the same resample, so their dependence survives, and prevalence stays inside
[0,1] by construction instead of hitting the boundary the Rogan–Gladen plug-in
produces. Rate ratios use BCa intervals; switching from percentile intervals moved
two secondary pairs across the null, which is reported rather than smoothed.

One arm is deliberately unweighted. The enrichment sample drew 40 records from a
stratum of 71 for hearing, but which records belonged to which stratum lived only in a
sampling key that no longer exists. Assigning those records a probability from the
wider frame is wrong by three orders of magnitude, so they carry no weight and are
reported as an unweighted audit of the predicted-negative space instead.

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
naive keyword rule. A fine-tuned Bio_ClinicalBERT appeared to beat that rule for
CNS — the one cancer type where the vocabulary is heterogeneous.

Then I checked the input. The outcome text I had trained on was truncated at a
median of 400 characters against ~1,760 in the registry, and for most positive
trials it no longer contained the instrument. The test is the 113 trials I had
labelled positive that keyword flagging missed — the ones that made the task look
hard. On the truncated text the keyword rule recovers **1 of 113**. On complete
registry text, the same unchanged list recovers **113 of 113**, and neither model
improves on it: the deployed BERT gets 72% recall on CNS where the rule gets 100%.

The transformer was solving a problem my own text pipeline had created. That
correction is written into the repository against the original claim rather than
edited out of it.

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
