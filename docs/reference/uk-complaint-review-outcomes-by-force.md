# `uk/complaint-review-outcomes-by-force.csv`

**44 rows. One per force.** Source: Independent Office for Police Conduct, Open Government
Licence v3.0, year 2024/25.

| Column | Type | Unit | Meaning |
|---|---|---|---|
| `force_slug` | text  | n/a | Join key |
| `force_name` | text  | n/a | Publisher's name |
| `complaint_cases_logged`  | n/a |, | **EMPTY IN ALL 44 ROWS. See below.** |
| `reviews_completed` | integer | reviews | **The denominator.** Reviews completed, not complaints logged |
| `outcomes_overturned` | integer | reviews | Reviews finding the force's own handling was not reasonable and proportionate |
| `overturn_pct` | float | per cent | `outcomes_overturned / reviews_completed * 100` |
| `period` | text  | n/a | `2024/25` |

## `complaint_cases_logged` is empty and should not be relied on

The column ships with a header and no values in any row. It is retained because removing a column
from a dataset that already carries a DOI breaks every consumer, but **there is no complaints-logged
figure in this file, and you cannot compute complaints per force from it.**

## The denominator is reviews completed, not complaints made

Only a small minority of complaints reach a review. `overturn_pct` answers *"when someone asked for
a review, how often was the force's decision found wanting?"*, not *"how often do complaints
succeed?"* Those are different questions and the second one cannot be answered from this file.

## Small denominators

Two forces have denominators too small to rank: **City of London (1 of 3)** and
**Warwickshire (11 of 32)**. Exclude anything under about 30 completed reviews before ranking. Of
the 37 forces with 50 or more reviews the spread runs from **Devon and Cornwall at 40.1 per cent**
(69 of 172) down to **Leicestershire at 6.9 per cent** (14 of 203), a 5.8-fold spread between two
forces with comparable review volumes.

**A high overturn rate is not the same as a bad force.** It measures the quality of the force's own
complaint handling as judged on review, and recording practice varies.

## Browse this table without downloading it

[All 44 UK police forces ranked by complaints](https://www.policecomplaint.com/uk/forces/) renders this file as a page, and names the source file it was computed from.
