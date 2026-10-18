# Bangla Bias Research — Full History (consolidated 18 Oct 2026)

Sources: Google Drive folder "Bangla Bias Research" (00-INDEX + Day 1–28 notes), `literature-review-draft.md` (18 Oct),
sheet "Bangla Social Bias", and this repo (`main` @ 1074858).

## Timeline
| Date | Event |
|---|---|
| 28 Jul 2026 | "Bias and Fairness" doc started |
| 27 Aug 2026 | Day 1 (vector & embedding). Day 2 done, then a long gap |
| 13 Sep 2026 | Restarted from Day 3 |
| 26–27 Sep | Revision notes rebuilt; Drive folder created (Days 1–4) |
| 10 Oct | Notes for Days 5–28 + 00-INDEX uploaded |
| 15 Oct | `beginners-guide.pdf` added |
| 16 Oct, 18 Oct | Related Work drafts (v1, v2) — for Akhila to polish, SRW short paper target |
| 18 Oct | Lit-matrix sheet "Bangla Social Bias" (Das 2023, Sadhu 2024a/b, Kamruzzaman 2025) |
| repo | Day 1 notebook; Day 3 notebook + 4 result CSVs across 8 models |

## Curriculum (Day 1–31)
**Phase 0 – Toolchain (1–12):** vectors, cosine, direction/projection/RIPA, PCA, Cohen's d, permutation test,
Review 1, tokenizer/OOV, MLM log-prob, bias vocabulary 1–2, Review 2 + first supervisor report.
**Phase 1 – English foundations (13–31):** Bolukbasi (13–14), Gonen & Goldberg (15), WEAT (16–19),
WinoBias + Bangla wall (20–21), intrinsic vs extrinsic (22), SEAT + template sensitivity (23–25),
Kurita LPBS + prior confound + BanglaBERT impl + 20 professions (26–29), CrowS-Pairs/PLL (30–31).
**Next:** StereoSet (34–37), Blodgett *Norwegian Salmon* (38–40), Goldfarb-Tarrant (41–43). Dataset is off-limits before Day 90.

## Research question (from Related Work §2.5)
> Do intrinsic bias metrics computed on Bangla LMs predict extrinsic, task-level gender bias in those same models?
(Goldfarb-Tarrant 2021 answered "no" for English; never tested for Bangla.)

## Six results that are yours
1. **OOV/fragmentation** — high-status professions (প্রকৌশলী, স্থপতি, পদার্থবিজ্ঞানী) split into subwords → scores pulled to zero.
2. **PC1 explained variance** — is gender one linear direction in BanglaBERT?
3. **Minimal-pair impossibility** — genderless Bangla pronouns make WinoBias *undefined*, not just hard.
4. **Prior confound** — three incompatible definitions of the LPBS prior.
5. **Template/pooling sensitivity** — watch উনি vs সে (honorific axis).
6. **Cost estimate** for a 1k Bangla sentence-pair dataset.

## Results already in repo (8 models: banglabert, banglishbert, bangla-bert-base, kowsher-bangla, sahajbert, mbert, muril, xlm-r)
- `results_fragmentation.csv`: % words intact — banglabert 65.9, sahajbert 62.0, muril 51.2, banglishbert 51.0,
  bangla-bert-base 35.6, xlm-r 15.4, mbert 7.2.
- `results_normalization.csv`: bangla-bert-base / kowsher-bangla **drop the virama (্)** — সম্পদ → সমপদ. Tokenizer bug, not bias.
- `results_weat.csv`: 48 gender tests → 18 positive, 30 negative, only 4 significant.
- `results_seat.csv`: 56 gender tests → 34 positive, 22 negative, 19 significant.
- Controls (weat1/2, seat1/2) are mostly significant, so the pipeline detects *something*.

## Open items
1. PCA rerun with 12+ matched pairs; confirm no pair word fragments.
2. Verify পুরুষ / নারী are single tokens (else recompute Day 3–4).
3. Neutralise-then-cluster probe (Gonen & Goldberg on Bangla).
4. Log template → number provenance from now on.
5. Check BBS labour-force data has occupation breakdown (Day 29 validity).
6. Keep `notes/lineage.md` current (doesn't exist yet).
7. Related Work: verify Garg 2018 & Dev–Phillips 2019 at source; fill arXiv 2411.10636 authors.
8. README progress log is stale (Day 2/3 unchecked); `src/` is empty — all code lives in notebooks.
