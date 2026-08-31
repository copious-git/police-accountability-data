# The denominator traps

## Never divide by `searches_total`

`uk/stop-and-search-outcomes-by-force.csv` publishes each rate as an explicit numerator and
denominator pair, precisely so nobody has to guess. `searches_total` is **not** the denominator for
any of them: some records carry no recorded outcome, and the fields are completed on different
subsets.

Measured across all 41 publishing forces, the gap between the correct rate and the one you get by
dividing by `searches_total`:

| Force | `n` | correct `d` | `searches_total` | Error if you use the total |
|---|---|---|---|---|
| Dorset Police | 1,187 | 2,634 | 5,765 | **24.5 points** |
| Dyfed-Powys Police | 4,508 | 6,644 | 8,883 | 17.1 points |
| Leicestershire Police | 7,734 | 11,550 | 15,064 | 15.6 points |
| North Yorkshire Police | 44 | 218 | 960 | 15.6 points |
| Merseyside Police | 116,719 | 150,950 | 182,231 | 13.3 points |

**The gap exceeds one percentage point on 21 of 41 forces.**

### Why sampling one force will mislead you

On the Metropolitan Police the two denominators are 373,321 and 373,367, a difference of 46
records, and the rate is 67.5% either way. **Checking the Met alone would tell you the trap does not
exist.** It exists on half the forces.

## The two denominators are not the same denominator

`no_further_action_d` and `more_than_outer_clothing_d` are different numbers on **35 of 41 forces**.

| Force | NFA denominator | Strip-search denominator |
|---|---|---|
| Metropolitan Police Service | 373,321 | 294,543 |
| Lancashire Constabulary | 73,486 | **0** |
| Essex Police | 44,362 | **0** |
| Cleveland Police | 17,595 | **0** |
| Surrey Police | 17,066 | **0** |

**Four forces publish a strip-search denominator of zero.** Dividing by it raises `ZeroDivisionError`
if you are lucky and produces silent nonsense if you are not. Guard for it.

You can check any of these against the rendered page for that force at
[All 44 UK police forces](https://www.policecomplaint.com/uk/forces/), which shows the same
numerator and denominator pairs.

## The US file has the same shape

`us/police-killings-by-state.csv` carries `bodycam_denominator` as its own column because
`bodycam_active_pct` is computed **only** over records where the field was completed yes or no.
"Unclear" is excluded.

California: `bodycam_denominator` 1,444 against `killed_by_police` 2,118. **Using the wrong one
understates the rate by 32%.**

`mental_illness_recorded_pct` has the same construction and **no published denominator column**.
Read it as directional only.

The state figures are rendered at
[the US state index](https://www.policecomplaint.com/states/), and the per-department ones at
[US police departments ranked by people killed by police](https://www.policecomplaint.com/states/agencies/).

`us/police-killings-by-agency.csv` deliberately publishes **no** `bodycam_denominator` and no
`acquitted` column: the per-agency counts are small enough that publishing them would identify
individual cases. Use the state file where a defensible rate is needed.
