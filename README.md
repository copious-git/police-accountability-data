# Police accountability data

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22165476.svg)](https://doi.org/10.5281/zenodo.22165476)
[![Licence: CC BY 4.0](https://img.shields.io/badge/Licence-CC%20BY%204.0-blue.svg)](https://creativecommons.org/licenses/by/4.0/)

Open, machine-readable datasets on police complaints, stop and search, use of force and
deaths following police contact, for the **United Kingdom**, the **United States** and
**Australia**.

> **Correction, 2026-08-30 (v1.1).** The UK disparity figures in v1.0.0 were computed on an
> incomplete denominator. Census 2021 uses 2021 local-authority codes, and the local-authority
> to police-force lookup we joined against uses 2024 codes, so the 17 districts abolished in
> the April 2023 local government reorganisation matched nothing and **1,686,893 residents were
> silently dropped**. Cumbria and North Yorkshire lost most or all of their populations; Avon
> and Somerset lost the whole of Somerset. A partial denominator produces a wrong ratio rather
> than a blank one, so the affected figures were understated. Corrected values: Avon and
> Somerset Black **4.3x → 5.9x**, North Yorkshire Black **4.0x → 5.6x**, North Yorkshire Asian
> **1.3x → 2.6x**, national Black **4.4x → 4.5x**, and Cumbria is computable for the first
> time. The build now fails loudly on any unmatched local authority instead of continuing.

> **Correction, 2026-08-31 (v1.1.1).** The UK deaths series was understated by **163 deaths**.
> The IOPC footnotes two of its year column headers, and our ingest matched year headers on a
> pattern that did not allow for a trailing footnote marker, so **2010/11 and 2015/16 were dropped
> silently** and published as zero rather than failing. All of the difference falls in one
> category: deaths following other police contact, **1,299 to 1,462**. The corrected all-category
> total is **3,666, not 3,503**. The parser now asserts that exactly 21 year columns are found and
> aborts otherwise. The correction table is in `METHOD.md`. Versions of this dataset published
> before 2026-08-31, including Zenodo v1.1.0, carry the understated figure and should not be used.

Everything here is **derived** data: computed from official open sources by code, then
published with the source, the period and the denominator attached. No figure in this
repository was written, estimated or rounded by a language model.

Published by [PoliceComplaint.com](https://www.policecomplaint.com/), which presents the
same figures as readable pages. This repository is the underlying data.

---

## What is actually new here

Most of the inputs are already public. Two of these outputs are not published in this form
anywhere we could find, and one is a straightforward tidying of a source that is otherwise
only available as a spreadsheet.

| Dataset | What it adds |
|---|---|
| `uk/stop-search-ethnic-disparity-by-force.csv` and `-national.csv` | Each force's stop-and-search **shares by ethnicity divided by that ethnic group's share of that force area's own resident population**, built by joining data.police.uk to Census 2021 via the ONS local-authority-to-police-force-area lookup |
| `uk/complaint-review-outcomes-by-force.csv` | Every force ranked on how often its own complaint decisions were **overturned on review** |
| `us/police-killings-by-state.csv` | Per-state aggregates including **whether any officer was criminally charged, and how the prosecution ended** |
| `australia/complaints-and-deaths-in-custody-by-state.csv` | The Report on Government Services police tables as tidy per-state rows rather than a 3,328-row wide spreadsheet |

### Where this overlaps something official — read this before citing it

**The UK government already publishes per-force stop-and-search rates by ethnicity.**
[Ethnicity Facts and Figures](https://www.ethnicity-facts-figures.service.gov.uk/)
publishes "stop and search rate for every 1,000 people, by ethnicity and area", by police
force area, using the same 2021 Census.

This dataset differs in two ways, and neither is "they don't publish it":

1. **Recency.** Their most recent published year ends 31 March 2023. This covers rolling
   36-month windows running to mid-2026.
2. **Measure and granularity.** They publish a *rate per 1,000 people*. This publishes a
   *ratio of shares*: a group's share of recorded searches divided by its share of
   residents, alongside outcome data on the same rows.

Both are legitimate measures and they answer slightly different questions. If you need the
official statistic, use theirs. If you need something more current, or you need outcome and
ethnicity on the same row, use this.

---

## Headline figures

All verified against the files in this repository at the commit you are reading.

**United Kingdom**
- **1,397,874** stop and search records across **41** of 44 forces. Three forces published
  no stop-and-search data at all and are named in the file rather than dropped.
- Nationally, Black people accounted for **18.2%** of searches with a recorded ethnicity
  against **4.0%** of residents, a ratio of **4.5x**. That national figure is computed over
  **1,151,285** searches across the 36 forces with a publishable denominator, and is in
  `uk/stop-search-ethnic-disparity-national.csv` with the shares it is derived from.
- **24.5%** of completed complaint reviews found the force's own handling was not reasonable
  and proportionate. The highest was **Devon & Cornwall at 40.1%**; the Metropolitan Police
  was **36.0%**.
- Disparity ratios are published for **36 forces**. Five forces have search data but no
  publishable denominator and are marked `publishable=false` with the reason.

**United States**
- **15,550** people killed by police, 2013 to 2026, across 51 states and 208 departments.
- **267** of those cases (**1.7%**) led to a criminal charge against an officer.
- **91** ended in a conviction or a guilty plea. **40** ended in acquittal.

**Australia**
- Complaints per 100,000 people in 2024-25 ranged from **6.3 in Victoria** to
  **97.6 in the Northern Territory**.
- **445** deaths in police custody, 2007-08 to 2024-25. **93** involved a person recorded as
  Aboriginal or Torres Strait Islander.

---

## Caveats that matter

**Read these before drawing a conclusion from any file here.**

- **A disparity ratio is not proof of unlawful conduct.** It is a measured difference in
  outcomes. It does not establish a cause and it does not identify anyone's behaviour.
- **The numerator and denominator use different bases.** Searches carry *officer-defined*
  ethnicity; the Census records *self-defined* ethnicity. Nationally, people recorded as
  Mixed are 0.5% of searches against 2.9% of residents, a gap too large to be real:
  officers rarely record "Mixed", so those people are recorded as something else at the
  point of search, which inflates whichever category absorbs them. **The direction of the
  finding is solid; the magnitude is uncertain.** See `METHOD.md`, which sets out the test
  we ran against the government's own published rates.
- **City of London is an artefact, not an outlier.** Its ratio is the highest in the UK file
  at **10.6x**, because the City has roughly 8,600 residents and several hundred thousand
  daily workers and visitors. A residence-based denominator is the wrong denominator there.
  The figure is published because dropping inconvenient rows is worse, but do not rank it
  against territorial forces.
- **Complaint counts reflect recording practice.** A force that records complaints readily
  logs more of them. That is not the same as a force whose officers behave worse. This is
  most visible in the Australian file, where the 15x spread between Victoria and the
  Northern Territory is far too large to be conduct and is very largely definitional.
- **Denominators are smaller than totals wherever a field is often blank.** Body-camera and
  mental-health shares are computed only over records where the field was completed, and the
  denominator is published in its own column so you can see it.
- **Periods differ by force.** data.police.uk coverage is not uniform; each row carries its
  own `period`.
- **A recorded complaint is an allegation, not a finding.** A death recorded as following
  police contact is categorised that way by the publisher and does not imply the police
  caused it or acted wrongly.
- **Scotland and Northern Ireland are absent** from the UK files. Police Scotland and the
  PSNI do not report into these datasets and the IOPC's statistics cover England and Wales
  only. There is no Scottish or Northern Irish data here because there is none to compute
  from, not because it was overlooked.
- **Ireland has no dataset at all.** We checked all 12,985 tables in the Central Statistics
  Office catalogue. No Irish police complaints, use-of-force or death-following-contact data
  exists in machine-readable form.

---

## Sources

| Source | Covers | Licence |
|---|---|---|
| [data.police.uk](https://data.police.uk/) | Stop and search with outcomes, England, Wales, Northern Ireland | Open Government Licence v3.0 |
| [Independent Office for Police Conduct](https://www.policeconduct.gov.uk/) | Complaints and review outcomes, England and Wales | Open Government Licence v3.0 |
| [Home Office use of force statistics](https://www.gov.uk/government/collections/police-use-of-force-statistics) | Use of force reports | Open Government Licence v3.0 |
| [ONS Census 2021 (TS021)](https://www.ons.gov.uk/) and the LAD-to-PFA lookup | Population denominators by ethnic group | Open Government Licence v3.0 |
| [Mapping Police Violence](https://mappingpoliceviolence.us/) | People killed by US police, 2013 onwards | Per the publisher's terms; aggregates only here |
| [US Census Bureau](https://www.census.gov/) NST-EST2024 | State population denominators | Public domain |
| [Report on Government Services 2026](https://www.pc.gov.au/ongoing/report-on-government-services), Part C Section 6 | Australian complaints and deaths in custody | CC BY 4.0 |

Only **aggregates** are redistributed here. No source's record-level data is republished.

---

## Method

See [`METHOD.md`](METHOD.md) for how each figure is computed, including the exact joins,
the publishability thresholds and the rounding.

The pipeline is deliberately boring: Python reads the source files, counts, divides, and
writes. Where a rate cannot be computed honestly, the row is marked unpublishable and the
reason is recorded rather than the row being dropped.

## Related resources

Every file here is also rendered as a browsable page, so a reader can check a figure without
downloading a CSV. Each page names the source file it was computed from.

| Page | Renders |
|---|---|
| [Open data downloads and methodology](https://www.policecomplaint.com/data/) | All nine files, with per-column notes and the publishability thresholds |
| [Who gets stopped and searched in England and Wales](https://www.policecomplaint.com/uk/reports/who-gets-stopped-and-searched/) | `uk/stop-search-ethnic-disparity-by-force.csv` and the national file |
| [All 44 UK police forces ranked by complaints](https://www.policecomplaint.com/uk/forces/) | `uk/complaint-review-outcomes-by-force.csv` and `uk/stop-and-search-outcomes-by-force.csv` |
| [Deaths during or following police contact, 21 years of data](https://www.policecomplaint.com/uk/reports/deaths-following-police-contact/) | Both deaths files |
| [US police departments ranked by people killed by police](https://www.policecomplaint.com/states/agencies/) | `us/police-killings-by-agency.csv` |
| [The US state index](https://www.policecomplaint.com/states/) | `us/police-killings-by-state.csv` |
| [Police complaints and deaths in custody in Australia, by state](https://www.policecomplaint.com/australia/) | `australia/complaints-and-deaths-in-custody-by-state.csv` |
| [Compare two UK police forces side by side](https://www.policecomplaint.com/uk/tools/compare/) | A tool built on the UK files |
| [Press and media](https://www.policecomplaint.com/press/) | Who publishes this, what may be reused, and the commercial interest disclosed in full |

## How to cite

Cite the **concept DOI**, which always resolves to the most recent version:

> PoliceComplaint.com. (2026). *Police accountability data: United Kingdom, United States
> and Australia* [Data set]. Zenodo. https://doi.org/10.5281/zenodo.22165476

To cite this specific release, use `10.5281/zenodo.22165477`.

If you rely on an underlying figure rather than our calculation, please cite the original
publisher as well. Each dataset names its sources.

## Licence

Derived data in this repository: [CC BY 4.0](LICENSE). Attribute to
PoliceComplaint.com and, where you rely on an underlying figure, to the original publisher
named in the table above.

## Corrections

If anything here is wrong, tell us and we will check it against the source and correct it:
open an issue, or email info@policecomplaint.com. That applies to police forces and
oversight bodies writing about their own numbers as much as to anyone else.
