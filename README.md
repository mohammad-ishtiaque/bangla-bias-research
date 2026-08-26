# Bangla Social Bias Research

Measuring and mitigating social bias in Bangla language models.

**Author:** Nazib
**Started:** August 2026
**Status:** Phase 0 — terminology & toolchain

---

## Goal

Bangla (Bengali) is the 6th most-spoken language in the world (230M+ speakers) yet remains
low-resource in NLP. Bias evaluation methods developed for English do not transfer directly:
they assume gendered pronouns, one-to-one gendered word pairs, and Western stereotype
inventories — none of which hold for Bangla.

This repo tracks a 20-week program to (1) understand the English bias-measurement literature,
(2) map what has already been done for Bangla, and (3) identify and execute a valid research
contribution.

---

## Repo structure

| Folder | Contents |
|---|---|
| `notebooks/` | Colab notebooks, one per study day (`dayNN_topic.ipynb`) |
| `src/` | Reusable implementations — WEAT, SEAT, LPBS, etc. |
| `data/` | Word lists, templates, annotated examples |
| `results/` | Output CSVs, figures, score tables |
| `notes/` | Per-paper and per-day notes (Markdown) |

---

## Environment

```bash
pip install transformers torch numpy scipy scikit-learn matplotlib pandas
```

Notebooks are written for Google Colab (T4 GPU). No local GPU required.

### Models used

| Model | HF id | Note |
|---|---|---|
| BanglaBERT | `csebuetnlp/banglabert` | ELECTRA discriminator — use for embeddings |
| BanglaBERT Generator | `csebuetnlp/banglabert_generator` | Use for `fill-mask` / MLM probability |
| mBERT | `bert-base-multilingual-cased` | Multilingual baseline |
| MuRIL | `google/muril-base-cased` | Indic multilingual baseline |

---

## Progress log

| Day | Topic | Output | Done |
|---|---|---|---|
| 1 | Vector & embedding basics | BanglaBERT loaded, first embedding extracted | ✅ |
| 2 | Cosine similarity | `cosine()` from scratch; first bias measurement | ⬜ |
| 3 | Direction & projection | Gender direction, RIPA scores | ⬜ |

*(extend as you go — one row per day)*

---

## Reference implementations

- [`csebuetnlp/BanglaContextualBias`](https://github.com/csebuetnlp/BanglaContextualBias) — code for
  *Characteristics of Bias upon Context Length Variation for Bangla* (Findings of ACL 2024).
  Closest prior work; primary reference.
- [`mcgill-nlp/bias-bench`](https://github.com/mcgill-nlp/bias-bench) — CDA, Dropout, INLP,
  SentenceDebias, Self-Debias in one place (Meade et al., ACL 2022).
- [`HerWILL-Inc/ACL-2025`](https://github.com/HerWILL-Inc/ACL-2025) — Pokkhopat dataset,
  WEAT/ECT/RND/RIPA for Bangla (GeBNLP 2025).

---

## Key prior work

**English foundations**
- Caliskan et al. 2017 — WEAT
- Zhao et al. 2018 — WinoBias (extrinsic)
- May et al. 2019 — SEAT
- Kurita et al. 2019 — Log Probability Bias Score
- Nangia et al. 2020 — CrowS-Pairs
- Nadeem et al. 2021 — StereoSet
- Blodgett et al. 2021 — *Stereotyping Norwegian Salmon* (benchmark validity critique)
- Goldfarb-Tarrant et al. 2021 — intrinsic metrics do not correlate with application bias
- Meade et al. 2022 — empirical survey of debiasing techniques

**Bangla**
- Sadhu et al. 2024 (Findings of ACL) — context length variation
- Sadhu et al. 2024 (GeBNLP) — gendered emotion attribution
- Sadhu et al. 2025 (LoResLM) — gender & religious bias, Disparate Impact
- Kamruzzaman et al. 2025 (Findings of ACL) — BanStereoSet
- Arnob et al. 2025 (GeBNLP) — Pokkhopat, STEM/SHAPE
- *Mitigating Extrinsic Gender Bias for Bangla Classification* (arXiv 2411.10636)

---

## License

Code: MIT. Data and annotations: to be determined at release.