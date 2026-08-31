# Worked examples

Run these against the published CSVs, or against the Datasette image
(`docker run -p 8001:8001 copiousltd/police-accountability-data`).

## Rates, with the correct denominator

```python
import csv

rows = list(csv.DictReader(open("uk/stop-and-search-outcomes-by-force.csv")))

for r in rows:
    if not r["searches_total"]:
        continue                      # 3 forces publish nothing; not a zero

    n = int(r["no_further_action_n"])
    d = int(r["no_further_action_d"])  # NOT searches_total
    print(f"{r['force_name']:34} {n / d * 100:.1f}%")
```

Guard the strip-search field separately, because **four forces publish a denominator of zero**:

```python
    dm = int(r["more_than_outer_clothing_d"])
    if dm:                            # Lancashire, Essex, Cleveland, Surrey are 0
        print(int(r["more_than_outer_clothing_n"]) / dm * 100)
```

## Disparity, filtered and de-artefacted

```python
rows = list(csv.DictReader(open("uk/stop-search-ethnic-disparity-by-force.csv")))

black = [
    r for r in rows
    if r["ethnic_group"] == "Black"
    and r["publishable"].lower() == "true"
    and r["disparity_ratio"]
    and r["force_slug"] != "city-of-london"   # residence denominator is wrong here
]
black.sort(key=lambda r: -float(r["disparity_ratio"]))
```

Without the last filter, City of London tops the ranking at 10.6 and the result is an artefact.

## US body-camera rate

```python
rows = list(csv.DictReader(open("us/police-killings-by-state.csv")))
ca = next(r for r in rows if r["state"] == "California")

correct = int(ca["bodycam_denominator"])   # 1,444
wrong   = int(ca["killed_by_police"])      # 2,118 - understates by 32%
```

## SQL, against the Datasette image

```sql
select force_name,
       round(100.0 * no_further_action_n / no_further_action_d, 1) as nfa_pct
from   stop_and_search_outcomes_by_force
where  no_further_action_d > 0
order  by nfa_pct desc;
```

## Before you publish anything from this

* A disparity ratio is a measured difference in outcomes, not proof of unlawful conduct.
* The UK ethnicity figures use two bases: searches carry *officer-defined* ethnicity, Census
  denominators are *self-defined*. Direction solid, magnitude uncertain.
* Scotland and Northern Ireland are absent because Police Scotland and the PSNI do not report into
  these datasets, not because they were overlooked.
* Check [corrections](https://police-accountability-data.readthedocs.io/en/latest/corrections/)
  before relying on an older download.
