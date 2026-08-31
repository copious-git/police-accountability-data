# `australia/complaints-and-deaths-in-custody-by-state.csv`

**144 rows. One per state per year**, 8 jurisdictions x 18 years, 2007-08 to 2024-25. Source:
Productivity Commission, Report on Government Services 2026, Part C Section 6, tables 6A.11 and
6A.5. CC BY 4.0.

| Column | Type | Unit | Meaning |
|---|---|---|---|
| `state_slug` | text  | n/a | Join key |
| `state` | text  | n/a | Full jurisdiction name |
| `police_service` | text  | n/a | The force, e.g. ACT Policing |
| `year` | text  | n/a | Australian financial year, `YYYY-YY` |
| `complaints_per_100k_people` | float | rate | **Published by the Productivity Commission, not computed by us.** Blank on 64 of 144 rows |
| `complaints_per_100_sworn_staff` | float | rate | Also the publisher's own. Blank on the same 64 rows |
| `deaths_in_police_custody` | integer | deaths | Count as published |
| `deaths_indigenous` | integer | deaths | Of which the person was recorded as Aboriginal or Torres Strait Islander |
| `oversight_body` | text  | n/a | The jurisdiction's police oversight body |

## The rates are the publisher's, and 64 rows have none

Both complaint rate columns are blank for 64 of 144 rows, because the Productivity Commission did
not publish a comparable rate for those jurisdiction-years. **A blank is missing, not zero.** The
deaths columns are complete.

## The 15-fold spread is about recording, not conduct

In 2024-25 the rate ran from **6.3 per 100,000 in Victoria** to **97.6 in the Northern Territory**.
That gap is far too large to be a difference in police behaviour. It very largely reflects what each
jurisdiction records as a complaint and how easy it is to make one. **A high figure can indicate a
system that captures complaints well.**

## Indigenous deaths are counts and a share, deliberately not a rate

`deaths_indigenous` is a count. It is **not** expressed as a rate, because that would need a
population series by Indigenous status that we do not hold in a form we can recompute and verify.
Across the whole period: **445 deaths in police custody, 93 of them of a person recorded as
Aboriginal or Torres Strait Islander.**

## Browse this table without downloading it

[Police complaints and deaths in custody in Australia, by state](https://www.policecomplaint.com/australia/) renders this file as a page, and names the source file it was computed from.
