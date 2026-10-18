# Related Work — Draft

**Status:** scaffold for Akhila to polish. ~1,350 words; a 4-page SRW
short paper needs roughly 600–800, so expect to cut Sections 2.1 and 2.2
hardest.

**Before sending:** read the "What you must verify yourself" section at
the bottom. Do not send this until you can defend every claim in it.

## 2 Related Work

### 2.1 Measuring bias inside the model

Work on social bias in language representations begins with the
observation that word embeddings encode stereotypical associations
geometrically. Bolukbasi et al. (2016) showed that embeddings trained on
Google News exhibit pronounced female/male stereotypes, that gender bias
is captured geometrically by a direction in the embedding space, and
that gender-neutral words are linearly separable from
gender-definitional ones. They defined metrics for both direct and
indirect gender bias and proposed algorithms for removing stereotypical
associations while preserving definitional ones. Gonen and Goldberg
(2019) later argued that this removal is superficial. Examining two
debiasing methods, they showed that gender information remains encoded
in the distances between the supposedly gender-neutralised words and can
be recovered from the debiased embeddings, so the procedure mostly hides
the bias from the metric rather than eliminating it, and should not be
relied on for gender-neutral modelling. This early exchange established
a pattern that recurs throughout the field, in which a measurement is
proposed, adopted, and subsequently shown to be weaker than assumed.

Caliskan et al. (2017) made the measurement statistical. Replicating a
spectrum of human biases documented by the Implicit Association Test
using GloVe embeddings trained on web text, they introduced the Word
Embedding Association Test (WEAT) together with the Word Embedding
Factual Association Test, and concluded that language itself carries
recoverable imprints of historical bias. WEAT remains the most widely
reported intrinsic metric, and a family of related measures operates on
the same geometry: Relative Norm Distance (Garg et al., 2018), the
Embedding Coherence Test (Dev and Phillips, 2019) and Relative Inner
Product Association (Ethayarajh et al., 2019) differ in whether they
compare distances, similarity rankings, or projections, but all
interrogate the position of a word relative to a group direction.
Ethayarajh et al. (2019) additionally argue that WEAT systematically
overestimates bias, showing that by contriving the attribute sets almost
any word can be made to appear gender-biased, a finding that bears
directly on how word lists are chosen.

The shift to contextual encoders complicated this picture, because a
model such as BERT assigns a different vector to a word in every
sentence. May et al. (2019) proposed the Sentence Encoder Association
Test (SEAT), which embeds target and attribute words in semantically
bleached templates and applies WEAT's arithmetic to the resulting
sentence representations; the authors report that the results are
inconsistent and sensitive to template choice. Kurita et al. (2019)
instead exploited the masked language modelling objective directly,
querying the model for the probability of a target token given an
attribute and dividing out the probability obtained when the attribute
is also masked. This prior correction separates stereotypical
association from mere corpus frequency, and the resulting Log
Probability Bias Score operates at a different level of the model than
the geometric family.

Dataset-driven measures followed. Nangia et al. (2020) released
CrowS-Pairs, a set of crowdsourced minimal pairs scored by
pseudo-log-likelihood, in which demographic tokens are never masked so
that their frequency does not enter the comparison. Nadeem et al. (2021)
introduced StereoSet, a large-scale natural English dataset covering
gender, profession, race and religion, and reported strong stereotypical
bias in BERT, GPT-2, RoBERTa and XLNet. Their scoring pairs a stereotype
score with a language modelling score, combining the two so that a model
cannot appear unbiased merely by becoming incoherent.

### 2.2 Measuring bias in what the model does

A parallel line measures bias in task output rather than representation.
Zhao et al. (2018) introduced WinoBias, a corpus of Winograd-schema
style sentences whose entities are people referred to by occupation, and
showed that rule-based, feature-rich and neural coreference systems
alike resolve gendered pronouns to pro-stereotypical entities more
accurately than to anti-stereotypical ones, by an average of 21.1 F1.
They further demonstrated that a data augmentation approach, combined
with existing word-embedding debiasing, removes the measured bias
without substantially harming performance on standard coreference
benchmarks; this augmentation strategy is now generally referred to as
counterfactual data augmentation. Rudinger et al. (2018) independently
introduced Winogender schemas, minimal pairs differing only in pronoun
gender, confirmed systematic bias in three publicly available
coreference systems, and correlated that bias with real-world and
textual gender statistics. Meade et al. (2022) compared five mitigation
techniques under a single protocol and found that Self-Debias performed
most consistently, that methods transferred poorly from gender to other
bias dimensions, and, most relevant here, that improvements on intrinsic
benchmarks were frequently accompanied by degraded language modelling
ability, making it difficult to establish whether bias had been reduced
at all.

### 2.3 Whether these measurements are valid

A third line questions the measurements themselves. Blodgett et al.
(2020) surveyed 146 papers analysing bias in NLP and found their
motivations vague, inconsistent and lacking normative reasoning, and
their quantitative techniques poorly matched to those motivations. They
recommend that researchers articulate explicitly what system behaviours
are harmful, in what ways, to whom and why. Blodgett et al. (2021)
applied a measurement modelling framework from the social sciences to
StereoSet and CrowS-Pairs and documented pervasive construction faults,
including perturbations that alter more than the demographic term, pairs
with no stereotypical content, and disagreement over which member of a
pair is the stereotype.

Most directly relevant to the present work, Goldfarb-Tarrant et al.
(2021) tested whether intrinsic metrics predict application-level bias.
Correlating intrinsic scores against extrinsic bias on downstream tasks
across many embedding variants, they found no reliable relationship, and
recommended that work on debiasing be evaluated extrinsically. Delobelle
et al. (2022) reached a compatible conclusion from a different
direction. Combining a survey of existing fairness metrics with
correlation analysis and their own empirical evaluation, they report
that many metrics are mutually incompatible and depend heavily on three
arbitrary choices, namely the templates used, the attribute and target
seed words, and the embeddings selected. They conclude by recommending
that practitioners avoid embedding-based metrics and evaluate fairness
on downstream tasks instead.

### 2.4 Bias in Bangla

Bangla has over 230 million speakers but remains under-resourced in NLP
(Joshi et al., 2020), and work on bias in Bangla is recent and
concentrated on measurement.

Sadhu et al. (2024a) provide the first systematic intrinsic study for
Bangla. They adapt WEAT, SEAT, CEAT and the Log Probability Bias Score
to Bangla, noting that word lists require cultural adaptation rather
than direct translation, and show that bias scores vary systematically
with the context length of the templates used, identifying roughly
twenty tokens as the most stable setting. They further separate a prior
bias component, attributable to inherent corpus imbalance, from the
corrected score. Sadhu et al. (2024b) extend bias evaluation to a new
axis, gendered attribution of emotion, and show that attribution shifts
when models are assigned gendered personas. Sadhu et al. (2025) probe
multilingual LLMs in Bangla for gender and religious bias using
template-based and naturally sourced prompts derived from BIBED (Das et
al., 2023), reporting Disparate Impact scores and finding that negative
traits are consistently associated with one religious community across
models.

Two resources target stereotype content directly. Kamruzzaman et al.
(2025) release BanStereoSet, 1,194 sentences across nine bias categories
localised from StereoSet, IndiBias and prior work, including categories
such as caste, region and beauty that are absent or weakly represented
in English benchmarks. Arnob et al. (2025) introduce Pokkhopat, a
curated list of gendered terms and profession words spanning STEM and
SHAPE disciplines, and evaluate eleven Bangla models using WEAT, ECT,
RND and RIPA. They additionally observe that many profession terms are
absent from the vocabularies of the models tested, which complicates
measurement and may amplify measured bias, although they do not quantify
this effect.

Extrinsic work in Bangla is limited to a single study. \[CITATION: arXiv
2411.10636\] construct counterfactual test sets for four classification
tasks using a hand-built lexicon of 573 Bangla gendered word pairs
together with named entity substitution, define bias as the proportion
of predictions that change under swapping, and report rates between 0.46
and 7.48 percent across tasks. They compare counterfactual augmentation,
token masking and a proposed joint loss that aligns the representations
of original and swapped inputs.

### 2.5 The gap

Bangla bias research is therefore almost entirely intrinsic. Of the work
surveyed above, four studies measure bias inside the model, two
contribute resources, one addresses mitigation extrinsically, and none
assess whether the intrinsic metrics in use have predictive validity.
Sadhu et al. (2024a) already show that these scores are unstable with
respect to an arbitrary design choice, which raises but does not answer
the question of whether they correspond to anything observable in
deployment. For English, Goldfarb-Tarrant et al. (2021) answered that
question negatively. The equivalent experiment has not been conducted
for Bangla, and the conclusion cannot simply be assumed to transfer,
since Bangla differs from English in ways that bear directly on both
halves of the comparison: pronouns are not gender-marked, gendered
vocabulary does not map one-to-one, and vocabulary coverage in available
models is incomplete.

We therefore ask whether intrinsic bias metrics computed on Bangla
language models predict extrinsic, task-level gender bias in those same
models.

## Verification status

Every claim above has now been checked against the paper's own abstract
or metadata. Sources used for each:

| **Claim about**                   | **Verified from**                             | **Status**   |
|-----------------------------------|-----------------------------------------------|--------------|
| Bolukbasi et al. 2016             | arXiv 1607.06520 abstract                     | ✅ corrected |
| Caliskan et al. 2017              | arXiv 1608.07187 abstract                     | ✅ corrected |
| Gonen and Goldberg 2019           | arXiv 1903.03862 abstract                     | ✅ corrected |
| Garg et al. 2018 (RND)            | PNAS 115(16) E3635–E3644, via secondary       | ⚠️ see below |
| Dev and Phillips 2019 (ECT)       | AISTATS 2019, arXiv 1901.07656, via secondary | ⚠️ see below |
| Ethayarajh et al. 2019 (RIPA)     | ACL P19-1166 / arXiv 1908.06361               | ✅ added     |
| May et al. 2019 (SEAT)            | ACL N19-1063 listing                          | ✅           |
| Kurita et al. 2019 (LPBS)         | ACL W19-3823 listing                          | ✅           |
| Nangia et al. 2020 (CrowS-Pairs)  | ACL 2020.emnlp-main.154                       | ✅           |
| Nadeem et al. 2021 (StereoSet)    | arXiv 2004.09456 abstract                     | ✅ corrected |
| Zhao et al. 2018 (WinoBias)       | arXiv 1804.06876 abstract                     | ✅ corrected |
| Rudinger et al. 2018 (Winogender) | arXiv 1804.09301 abstract                     | ✅ corrected |
| Blodgett et al. 2020              | arXiv 2005.14050 abstract                     | ✅ corrected |
| Blodgett et al. 2021              | ACL 2021.acl-long.81                          | ✅           |
| Goldfarb-Tarrant et al. 2021      | ACL 2021.acl-long.150                         | ✅           |
| Delobelle et al. 2022             | arXiv 2112.07447 abstract                     | ✅ corrected |
| Meade et al. 2022                 | ACL 2022.acl-long.132                         | ✅           |
| Joshi et al. 2020                 | ACL 2020.acl-main.560 abstract                | ✅           |
| All six Bangla works              | ACL Anthology pages and arXiv full texts      | ✅           |

### Two items still at second-hand

Garg et al. (2018) and Dev and Phillips (2019) were confirmed only
through secondary documentation, not from the papers' own abstracts. The
citations and the direction of each metric are consistent across
sources, but if you want the Related Work to be airtight, open these two
and confirm:

- Garg et al., PNAS 2018, 115(16), E3635–E3644 — Relative Norm Distance

- Dev and Phillips, AISTATS 2019, arXiv 1901.07656 — Embedding Coherence
  > Test

If you would rather not, remove the two parenthetical citations and
write the sentence without attributing those metrics to specific papers.

### Still to fix

The arXiv 2411.10636 citation is a placeholder. Get the author names
from the PDF and check whether it has since appeared at a venue.

### How to use this

**Rewrite every paragraph in your own words before sending.** Not
because of plagiarism — this summarises public literature — but because
you have to own the argument. Akhila already told you not to copy-paste,
and if she or your supervisor asks you to explain a sentence you cannot
explain, that costs you more than submitting nothing.

**Tell Akhila honestly what state this is in.** Something like: *"Ei ta
first draft, ami je paper gula porechi oigula theke likhechi. Koyekta
claim ekhono verify kora baki, oigula mark kore rekhechi."* Being
upfront about what is unverified is what a researcher does, and she will
trust the next draft more.
