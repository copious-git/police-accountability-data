# `uk/stop-search-ethnic-disparity-by-force.csv`

**205 rows. One row per force per ethnic group** (41 forces x 5 groups). Sources: `data.police.uk`
joined to ONS Census 2021 table TS021 through the ONS local-authority to police-force-area lookup.
Both Open Government Licence v3.0.

| Column | Type | Unit | Meaning |
|---|---|---|---|
| `force_slug` | text  | n/a | Join key |
| `force_name` | text  | n/a | Publisher's name |
| `publishable` | `true`/`false`  | n/a | **Whether the ratio on this row can be trusted.** Filter on this before any analysis |
| `ethnic_group` | text  | n/a | One of Black, Asian, Mixed, White, Other. Census high-level groups |
| `searches_recorded_total` | integer | searches | Searches with a recorded ethnicity for the whole force. Repeats across that force's 5 rows |
| `searches_this_group_pct` | float | per cent | This group's share of searches with a recorded ethnicity |
| `residents_this_group_pct` | float | per cent | This group's share of the force area's resident population |
| `disparity_ratio` | float | ratio | `searches_this_group_pct / residents_this_group_pct`. **Blank where it could not be computed honestly** |
| `ethnicity_not_recorded_pct` | float | per cent | Force-level recording quality. Repeats across the force's rows |
| `period` | text  | n/a | `2023-07 to 2026-06` |
| `reason` | text  | n/a | **Why `disparity_ratio` is blank.** Populated on 143 of 205 rows |

## What the ratio means, and what it does not

A ratio of 4.5 means the group's share of searches is 4.5 times its share of residents. **It is a
measured difference in outcomes. It is not proof that anyone acted unlawfully and it does not
establish a cause.**

## The base mismatch, stated plainly

**The numerator and denominator use different definitions of ethnicity.** Searches carry
*officer-defined* ethnicity, recorded by the officer at the point of the stop. Census denominators
are *self-defined*. Officers barely record "Mixed" at all, **0.5 per cent of searches against
2.9 per cent of residents**, so people the Census counts as Mixed are recorded as something else at
the point of search, most often Black or White. That inflates whichever category absorbs them.

**Treat the direction as solid and the magnitude as uncertain.**

## Blanks are not zeros

`disparity_ratio` is blank on 62 rows and `reason` says which of these applies:

- the force records ethnicity on too few searches to support a ratio
- no searches were recorded for that group in the period
- no resident population figure exists for that group
- the group's resident share is **below the 0.5 per cent stability floor**, where a handful of
  searches produces an enormous and meaningless ratio

## Known artefact

**City of London Police returns the highest ratio in the file and should not be ranked against
territorial forces.** Roughly 8,600 residents against a very large daytime working population makes
a residence-based denominator the wrong denominator there. The row is published rather than deleted,
with the reason recorded.

## Browse this table without downloading it

[Who gets stopped and searched in England and Wales](https://www.policecomplaint.com/uk/reports/who-gets-stopped-and-searched/) renders this file as a page, and names the source file it was computed from.
