# Police accountability data

Column-level documentation for nine derived datasets covering police complaints, stop and search,
use of force and deaths following police contact in the **United Kingdom**, the **United States**
and **Australia**.

The data itself lives in the repository and on Zenodo. This site exists because the CSVs ship about
sixty columns, and several of them cannot be used correctly without knowing their denominator.
`no_further_action_n` against `_d` against `_pct`, the `publishable` flag and its `reason`,
`bodycam_denominator` which is **not** the row's `killed_by_police`, each of those is a trap for
anyone who opens the file and starts dividing.

- **Data and code:** [github.com/copious-git/police-accountability-data](https://github.com/copious-git/police-accountability-data)
- **Cite the concept DOI:** [10.5281/zenodo.22165476](https://doi.org/10.5281/zenodo.22165476)
- **Browsable versions of every table:** [policecomplaint.com/data](https://www.policecomplaint.com/data/)
- **Licence:** CC BY 4.0 on the derived data. Sources keep their own licences.

## Read this before you divide one column by another

- **A disparity ratio is a measured difference in outcomes.** It is not proof that anyone acted
  unlawfully and it does not establish a cause.
- **A recorded complaint is an allegation, not a finding.** A force that records complaints readily
  logs more of them.
- **The UK ethnicity figures use two different bases.** Searches carry *officer-defined* ethnicity;
  Census denominators are *self-defined*. Treat the direction as solid and the magnitude as
  uncertain. See [Method](method.md).
- **Where a rate could not be computed honestly, the row says why** rather than being dropped. Check
  `publishable` and `reason` before treating a blank as a zero.

## The nine files

| File | Rows | What one row is |
|---|---|---|
| `uk/stop-and-search-outcomes-by-force.csv` | 44 | One police force |
| `uk/stop-search-ethnic-disparity-by-force.csv` | 205 | One force and one ethnic group |
| `uk/stop-search-ethnic-disparity-national.csv` | 5 | One ethnic group, England and Wales |
| `uk/complaint-review-outcomes-by-force.csv` | 44 | One force |
| `uk/deaths-following-police-contact-by-year.csv` | 21 | One financial year |
| `uk/deaths-following-police-contact-by-category.csv` | 6 | One IOPC category, plus a TOTAL row |
| `us/police-killings-by-state.csv` | 51 | One state, including DC |
| `us/police-killings-by-agency.csv` | 208 | One department |
| `australia/complaints-and-deaths-in-custody-by-state.csv` | 144 | One state and one year |

## Coverage gaps that are real, not oversights

- **Scotland and Northern Ireland are absent from the UK files.** Police Scotland and the PSNI do
  not report into `data.police.uk`, and IOPC statistics cover England and Wales only.
- **Three forces publish no stop-and-search data at all** to `data.police.uk`: British Transport
  Police, Greater Manchester Police and Gwent Police. They are carried as rows with a `note`, not
  removed, so a count of 44 forces stays honest.
- **Five further forces record ethnicity on too few searches** to support a ratio and are marked
  `publishable=false` with the reason.
- **Ireland has no dataset.** Checked across all 12,985 Central Statistics Office tables.
