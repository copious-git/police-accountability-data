# `us/police-killings-by-state.csv`

**51 rows: 50 states plus the District of Columbia.** Source: Mapping Police Violence, 2013 to 2026,
used per the publisher's own terms; aggregates only. State populations from US Census Bureau
NST-EST2024 (public domain).

| Column | Type | Unit | Meaning |
|---|---|---|---|
| `state_slug` | text  | n/a | Join key |
| `state` | text  | n/a | Full name |
| `state_code` | text  | n/a | Two-letter postal code |
| `killed_by_police` | integer | people | Killed **by any means**, see below |
| `population` | integer | people | NST-EST2024 estimate |
| `per_million_per_year` | float | rate | `killed / years covered / (population / 1,000,000)` |
| `agencies_in_dataset` | integer | agencies | Departments with at least one record |
| `bodycam_active_pct` | float | per cent | Share with a body camera recorded active |
| `bodycam_denominator` | integer | records | **The denominator for the line above. NOT `killed_by_police`** |
| `mental_illness_recorded_pct` | float | per cent | Computed only where the field was completed yes or no |
| `officers_charged` | integer | cases | Records where the charges field begins "Charged" |
| `officers_charged_pct` | float | per cent | `officers_charged / killed_by_police * 100` |
| `convicted_or_pleaded_guilty` | integer | cases | Ended in conviction or guilty plea |
| `acquitted` | integer | cases | Ended in acquittal |
| `period` | text  | n/a | `2013 to 2026` |

## `bodycam_denominator` is the single most misread column here

`bodycam_active_pct` is computed **only over records where the body-camera field was completed as
yes or no**. "Unclear" is excluded. `bodycam_denominator` is that count, and it is always smaller
than `killed_by_police`. Dividing by `killed_by_police` understates the rate on every row.

The same applies to `mental_illness_recorded_pct`, which has no published denominator column and
should be read as directional.

## "Killed by police" means by any means

Gunshot, Taser, physical restraint, police vehicle and beating are all included, not fatal
shootings only. Combination causes such as "Gunshot, Taser" are normalised so that ordering does not
split one category into two.

## Charges are not convictions

`officers_charged` counts records where a charge was brought. Nationally that is **267 of 15,550
cases, 1.7 per cent**, of which **91** ended in a conviction or guilty plea and **40** in acquittal.
The remainder were pending or otherwise resolved at the time of extraction.

## Source currency

Mapping Police Violence is current to 2026. An earlier version of this dataset used the Washington
Post police-shootings dataset, which is **frozen**, its last record is 31 December 2024. Every US
page on the site discloses which source it uses.

## Browse this table without downloading it

[The US state index](https://www.policecomplaint.com/states/) renders this file as a page, and names the source file it was computed from.
