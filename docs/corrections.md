# Corrections

Every correction to a published figure is recorded here with the before and after values, so anyone
holding an older download can tell whether it affects them. GitHub cannot version-switch a README;
this page is versioned per release.

---

## 2026-08-31, two years of the UK deaths series were understated

**Affects:** `uk/deaths-following-police-contact-by-year.csv` and
`uk/deaths-following-police-contact-by-category.csv`, in every release before v1.2.

| Figure | Published until 2026-08-31 | Corrected |
|---|---|---|
| 2010/11 | 95 | **152** |
| 2015/16 | 99 | **205** |
| All years, all categories | 3,503 | **3,666** |
| "Deaths following other police contact", all years | 1,299 | **1,462** |

**Cause.** The IOPC footnotes individual year columns in its own time-series tables: `10/11*` and
`15/16**`. Our ingest matched year headers with a pattern that did not tolerate the footnote marker,
so both columns were dropped from the "other police contact" sheet alone and both years published a
category total of **zero**, a value the IOPC never recorded. Four of the five category sheets were
unaffected, which is why the fault looked like a finding rather than a bug: the missing 2015/16
created an apparent jump from 99 to 234 at 2016/17 that reads as a definitional change.

**No other year, category or file was affected.**

**What changed as a result.** `scripts/ingest_deaths.py` now fails loudly if any sheet yields other
than 21 year columns, and `scripts/export_opendata.py` regenerates both deaths files rather than
leaving them outside the reproducible build. Two separate faults in the same file were also fixed: a
Python import that had been pasted inside the module docstring, so the ingest could not run at all;
and an export script that claimed the dataset was reproducible from the repository while covering
only 2 of the 9 files.

**The general lesson, for anyone doing similar work:** a published zero sitting between non-zero
years is a parse failure until proven otherwise.

---

## 2026-08-31, a denominator bug in the UK disparity ratios

**Affects:** `uk/stop-search-ethnic-disparity-by-force.csv` before v1.1.

Ratios were computed against the wrong denominator, understating the disparity. Corrected in v1.1
and the national file was recomputed from the corrected per-force figures. If you are using v1.0,
replace it.

---

## Reporting an error

If something here is wrong, tell us and we will check it against the source and correct it: open an
issue on [the repository](https://github.com/copious-git/police-accountability-data), or email
`corrections@policecomplaint.com`. That applies to police forces and oversight bodies writing about
their own numbers as much as to anyone else.
