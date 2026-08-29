# Method

Every figure is computed in Python from the source files. Nothing is generated, estimated or
rounded by a language model. Where a figure cannot be computed honestly, the row is marked
unpublishable and the reason recorded, rather than the row being quietly dropped.

## The rule that governs everything here

**A rate is published only with its denominator.** Every percentage in these files has the
numerator and the denominator on the same row, because a rate without its denominator is the
easiest way for a reader to draw a wrong conclusion from correct data.

Where a source field is frequently blank, the rate is computed **only over records where the
field was completed**. The denominator column then differs from the total column, deliberately.

---

## UK: stop-and-search ethnic disparity

`uk/stop-search-ethnic-disparity-by-force.csv`

1. Pull every stop-and-search record published to data.police.uk for each force, for the
   rolling window in the `period` column. Coverage is not uniform: `months_with_data` in
   `stop-and-search-outcomes-by-force.csv` records how many months each force actually
   published.
2. Count searches by officer-defined ethnicity. Records with no ethnicity recorded are
   **excluded from the denominator**, so shares sum to 100% of *recorded* searches, not of
   all searches. The excluded count is published as `ethnicity_not_recorded_pct`.
3. Build the population denominator: take Census 2021 table TS021 (ethnic group by local
   authority), map each local authority to its police force area using the ONS LAD-to-PFA
   lookup, and sum.
4. `disparity_ratio = searches_this_group_pct / residents_this_group_pct`.

A ratio of 1.0 means searches match population share exactly. Above 1.0 means the group is
searched more often than its population share alone would produce.

**Publishability.** A force is marked `publishable=false` where the LAD-to-PFA mapping cannot
be resolved cleanly enough for the denominator to be trustworthy. Five forces are excluded on
that basis and are listed in the file with `reason`. A further three forces published no
stop-and-search data at all and appear in the outcomes file with a `note`.

**The two halves of the ratio are not recorded the same way.** This is the most important
limitation on the dataset and it cuts against the headline figure, not for it.

The numerator is **officer-defined** ethnicity: what the officer recorded at the time,
without asking. The denominator is the **self-defined** ethnicity people gave the 2021
Census about themselves. Those are different measurements and in practice they do not use
the same categories.

The evidence is in the data itself. Nationally, people recorded as **Mixed** account for
**0.5%** of searches against **2.9%** of residents. That gap is far too large to be real.
Officers rarely record "Mixed" at all, so people the Census counts as Mixed are recorded as
something else at the point of search, most often Black or White. That inflates whichever
category absorbs them, and on these figures it inflates the Black ratio.

**Treat the direction as solid and the magnitude as uncertain.** A disparity exists on any
reasonable measure. The exact multiple depends on a recording practice the forces control.

We tested this. Recomputing our data as a rate per 1,000 people, the all-ethnicities figure
comes out at **8.5 per 1,000 per year** against the government's **8.9** for year ending
March 2023 — close, which suggests the overall method is sound. But **Black** comes out at
**37.4** against the government's **24.5**, and **Mixed** at **9.3** against **9.9**. The
divergence is concentrated exactly where the category mismatch predicts it would be.

**Do not present these ratios as a corrected or updated version of the official statistic.**
They are computed on a different basis and answer a related but different question.

**Known artefact.** City of London Police returns the highest ratio in the file. The City has
roughly 8,600 residents against a very large daytime working population, so a residence-based
denominator materially overstates disparity there. The row is published rather than deleted,
with this caveat, because removing inconvenient rows is a worse failure than publishing one
that needs explaining.

---

## UK: complaint review outcomes

`uk/complaint-review-outcomes-by-force.csv`

From the IOPC's published complaints and reviews statistics. `overturn_pct` is
`outcomes_overturned / reviews_completed`.

The denominator is **reviews completed**, not complaints logged. Only a small minority of
complaints go to review, so this is not "a quarter of all complaints were wrong". It is
"a quarter of the decisions someone challenged did not survive that challenge".

---

## UK: deaths following police contact

`uk/deaths-following-police-contact-by-category.csv` and `-by-year.csv`

The IOPC's own categories, kept separate rather than collapsed into a single figure. The
category names are the publisher's. Inclusion in a category does not imply that the police
caused the death or acted wrongly.

---

## United States

`us/police-killings-by-state.csv`, `us/police-killings-by-agency.csv`

Source: Mapping Police Violence, 2013 to 2026. This counts people killed by police **by any
means** — gunshot, Taser, physical restraint, police vehicle, beating — not fatal shootings
only. Combination causes ("Gunshot, Taser") are normalised so that ordering does not split
one category into two.

- `per_million_per_year` = killings / years covered / (state population / 1,000,000), using
  US Census Bureau NST-EST2024.
- `bodycam_active_pct` and `mental_illness_recorded_pct` are computed **only over records
  where the field was completed as yes or no**. "Unclear" is excluded from the denominator,
  and the denominator is published.
- `officers_charged` counts records where the charges field begins "Charged".
- `convicted_or_pleaded_guilty` counts records recording a conviction **or a guilty or
  no-contest plea**. Counting only the literal word "convicted" would understate it: across
  the whole dataset that is 77 against 91.

**Agency threshold.** An agency appears only where it has **12 or more records**. Below that
a per-agency rate is noise. 208 of 4,641 agencies in the source meet it. Agencies below the
threshold are not in the file; their absence is not evidence of anything.

---

## Australia

`australia/complaints-and-deaths-in-custody-by-state.csv`

Source: Report on Government Services 2026, Part C Section 6, tables 6A.11 (complaints) and
6A.5 (deaths in police custody). Licensed CC BY 4.0.

**The rates are the publisher's own, not ours.** Complaints per 100,000 people and per 100
sworn staff are published by the Productivity Commission; this file reshapes them from a wide
spreadsheet into tidy rows. Deaths are counts as published.

The 15x spread between Victoria (6.3 per 100,000) and the Northern Territory (97.6) is far
too large to be a difference in conduct. It very largely reflects what each jurisdiction
records as a complaint and how easy it is to make one. A high figure can indicate a system
that captures complaints well.

The Aboriginal and Torres Strait Islander figures are **counts, and a share of deaths**. They
are deliberately **not** expressed as a rate, because that would need a population series by
Indigenous status that we do not hold in a form we can recompute and verify.

---

## What we do not do

- We do not estimate a missing value.
- We do not impute a denominator.
- We do not carry a figure forward from a previous period and present it as current.
- We do not publish a rate whose denominator we cannot state.
