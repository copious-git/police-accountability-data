# `us/police-killings-by-agency.csv`

**208 rows. One per department.** Same source and terms as the state file.

| Column | Type | Unit | Meaning |
|---|---|---|---|
| `agency_slug` | text  | n/a | Join key. Unique across all 208 rows |
| `agency` | text  | n/a | Department name. **207 unique across 208 rows**, two departments share a name in different states, so never join on this |
| `state` | text  | n/a | Full state name |
| `ori` | text  | n/a | FBI Originating Agency Identifier. **205 unique across 208 rows**; three are absent or shared |
| `killed_by_police` | integer | people | By any means, 2013 to 2026 |
| `bodycam_active_pct` | float | per cent | Computed only over completed records |
| `mental_illness_recorded_pct` | float | per cent | Computed only over completed records |
| `officers_charged` | integer | cases | Charge brought |
| `convicted_or_pleaded_guilty` | integer | cases | Conviction or guilty plea |
| `period` | text  | n/a | `2013 to 2026` |

## Two differences from the state file, both deliberate

**There is no `bodycam_denominator` here.** The per-agency counts are small enough that publishing a
denominator per row would identify individual cases. Treat `bodycam_active_pct` on this file as
directional only, and use the state file where a defensible rate is needed.

**There is no `acquitted` column here.** The state file carries one; this file does not, for the
same small-numbers reason.

## 208 departments is not every department

This file covers departments with enough records to be worth publishing individually. It is not a
census of US law enforcement, and a department's absence is not evidence that it has killed nobody.
Use `agencies_in_dataset` on the state file for the count that contributed to each state total.

## Browse this table without downloading it

[US police departments ranked by people killed by police](https://www.policecomplaint.com/states/agencies/) renders this file as a page, and names the source file it was computed from.
