# Using this data without getting it wrong

A short handbook for anyone analysing the nine open datasets on police complaints, stop and search
and deaths following police contact published by
[PoliceComplaint.com](https://www.policecomplaint.com/data/).

This is deliberately **not** a column reference. That already exists at
[the data dictionary](https://police-accountability-data.readthedocs.io/) and documents what every
column is. This handbook covers the different question: **which calculations are wrong**, with the
numbers to show it.

Every figure below is re-derived from the shipped CSVs. Nothing here is asserted.

* **Data and code:** [github.com/copious-git/police-accountability-data](https://github.com/copious-git/police-accountability-data)
* **Cite the concept DOI:** [10.5281/zenodo.22165476](https://doi.org/10.5281/zenodo.22165476)
* **Licence:** CC BY 4.0 on the derived data. Sources keep their own.

## The three mistakes that actually happen

1. **Dividing by `searches_total`.** Every rate in the stop-and-search file ships with its own
   `_n` and `_d` pair. Using the row total instead understates the rate on **21 of 41 forces**, by
   up to **24.5 percentage points**. See [The denominator traps](denominators.md).
2. **Assuming `publishable` catches every problem.** It does not catch the City of London artefact,
   which is flagged `publishable=true` and still should not be ranked. See
   [Filtering](filtering.md).
3. **Reading a per-agency US rate as comparable.** `bodycam_active_pct` is computed over a
   *different, smaller* denominator than `killed_by_police`. In California that is 1,444 against
   2,118 — using the wrong one understates by **32%**.

## One caveat that outranks all of the above

**A disparity ratio is a measured difference in outcomes.** It is not proof that anyone acted
unlawfully and it does not establish a cause. **A recorded complaint is an allegation, not a
finding.** A force that records complaints readily logs more of them.
