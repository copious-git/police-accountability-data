# `uk/stop-and-search-outcomes-by-force.csv`

**44 rows. One row per police force.** Source: `data.police.uk`, Open Government Licence v3.0.

Three forces publish nothing to this dataset and appear as rows with every numeric column blank and
a `note` explaining why. **Do not read those blanks as zeros.**

| Column | Type | Unit | Meaning |
|---|---|---|---|
| `force_slug` | text  | n/a | Stable identifier. Use this to join, not `force_name` |
| `force_name` | text  | n/a | Publisher's name for the force |
| `searches_total` | integer | searches | All recorded stop and searches in `period`. Blank for the 3 non-publishing forces |
| `months_with_data` | integer | months | How many months of the window the force actually published. **Ranges 34 to 36. A force with 34 months is not comparable on raw counts to one with 36** |
| `no_further_action_n` | integer | searches | Numerator: searches ending in no further action |
| `no_further_action_d` | integer | searches | **Denominator: searches with a recorded outcome.** This is smaller than `searches_total`, because some records carry no outcome |
| `no_further_action_pct` | float | per cent | `n / d * 100`, one decimal place |
| `more_than_outer_clothing_n` | integer | searches | Numerator: searches where more than outer clothing was removed |
| `more_than_outer_clothing_d` | integer | searches | **Its own denominator**, and not equal to `no_further_action_d`. The field is completed on a different subset |
| `ethnicity_not_recorded_n` | integer | searches | Searches with no officer-defined ethnicity recorded |
| `ethnicity_not_recorded_pct` | float | per cent | Share of `searches_total` with no ethnicity recorded |
| `period` | text  | n/a | Coverage window, `YYYY-MM to YYYY-MM`. **Varies by force**; it is not one shared window |
| `note` | text  | n/a | Populated only where data is absent, and says why |

## Traps

**Every `_n` has its own `_d`.** They are published as pairs precisely so nobody divides by
`searches_total`. Using `searches_total` as the denominator understates every rate on this file.

**`period` is per row.** Eight distinct windows exist across the 44 forces. Comparing raw
`searches_total` between two forces with different `months_with_data` compares different amounts of
time. Normalise, or compare rates rather than counts.

**`ethnicity_not_recorded_pct` is the quality flag for the disparity file.** A force above roughly
20 per cent here cannot support a trustworthy ratio, which is why five forces are marked
unpublishable in `stop-search-ethnic-disparity-by-force.csv`.

## Browse this table without downloading it

[All 44 UK police forces ranked by complaints](https://www.policecomplaint.com/uk/forces/) renders this file as a page, and names the source file it was computed from.
