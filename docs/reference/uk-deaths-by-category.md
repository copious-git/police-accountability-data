# `uk/deaths-following-police-contact-by-category.csv`

**6 rows: five IOPC categories plus a `TOTAL` row.** Covers 2004/05 to 2024/25 combined.

| Column | Type | Unit | Meaning |
|---|---|---|---|
| `category_key` | text  | n/a | Stable key. `TOTAL` on the summary row |
| `category` | text  | n/a | The publisher's own category name |
| `deaths` | integer | deaths | Total across the whole period |
| `period` | text  | n/a | `2004/05 to 2024/25` |

## The TOTAL row is a row

`category_key = "TOTAL"` sums the other five. **Summing the `deaths` column without excluding it
double-counts every death.**

## Current values

| Category | Deaths |
|---|---|
| Deaths following other police contact | 1,462 |
| Apparent suicides following custody | 1,149 |
| Road traffic incidents | 612 |
| Deaths in or following custody | 399 |
| Fatal police shootings | 44 |
| **TOTAL** | **3,666** |

**Inclusion in a category does not imply that the police caused the death or acted wrongly.**

The 3,666 total sums across the publisher's own 2010/11 and 2015/16 discontinuities and is a count
of records, not a measure of a single consistently defined thing. See
[UK deaths by year](uk-deaths-by-year.md).

## Browse this table without downloading it

[Deaths during or following police contact, 21 years of data](https://www.policecomplaint.com/uk/reports/deaths-following-police-contact/) renders this file as a page, and names the source file it was computed from.
