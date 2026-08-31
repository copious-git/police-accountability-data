# `uk/stop-search-ethnic-disparity-national.csv`

**5 rows. One per ethnic group, England and Wales.**

| Column | Type | Unit | Meaning |
|---|---|---|---|
| `ethnic_group` | text  | n/a | Black, Asian, Mixed, White, Other |
| `searches_this_group_pct` | float | per cent | Share of in-scope searches with a recorded ethnicity |
| `residents_this_group_pct` | float | per cent | Share of the in-scope resident population |
| `disparity_ratio` | float | ratio | Shares divided, to one decimal place |
| `searches_in_scope` | integer | searches | **1,151,285.** The denominator behind every row |
| `forces_publishable` | integer | forces | **36.** Forces contributing to the national figure |
| `forces_total` | integer | forces | **41.** Forces publishing any stop-and-search data |
| `period` | text  | n/a | `2023-07 to 2026-06` |

## The national figure is computed over 36 forces, not 44

Three forces publish nothing, five more cannot support a ratio. `searches_in_scope` (1,151,285) is
therefore smaller than the 1,397,874 total searches in the outcomes file. **Both numbers are correct
and they answer different questions.** Quoting the larger one alongside the national ratio is wrong.

## How it compares to the official statistic

Recomputing our data as a rate per 1,000 people, the all-ethnicities figure comes out at
**8.5 per 1,000 per year** against the government's **8.9** for year ending March 2023, close,
which suggests the overall method is sound. But **Black** comes out at **37.4** against the
government's **24.5**, and **Mixed** at **9.3** against **9.9**. The divergence is concentrated
exactly where the officer-defined versus self-defined mismatch predicts it would be.

**Do not present these ratios as a corrected or updated version of the official statistic.** The UK
government's Ethnicity Facts and Figures service already publishes per-force stop-and-search rates
by ethnicity from the same Census. This dataset differs in recency, and in publishing a ratio of
shares alongside outcome data on the same row rather than a rate per 1,000. For the official
statistic, use theirs.

## Browse this table without downloading it

[Who gets stopped and searched in England and Wales](https://www.policecomplaint.com/uk/reports/who-gets-stopped-and-searched/) renders this file as a page, and names the source file it was computed from.
