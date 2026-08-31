# Filtering: `publishable`, `reason`, and what they do not catch

## What the flag does

`uk/stop-search-ethnic-disparity-by-force.csv` carries `publishable` and, where a ratio is absent,
a `reason`. Filter on `publishable` before any analysis. `disparity_ratio` is blank on 62 of 205
rows and `reason` says which of these applies:

* the force records ethnicity on too few searches to support a ratio
* no searches were recorded for that group in the period
* no resident population figure exists for that group
* the group's resident share is below the **0.5% stability floor**, where a handful of searches
  produces an enormous and meaningless ratio

**A blank is not a zero.** Treating it as one silently drops the forces with the worst recording,
which biases the result in the least helpful direction.

## What the flag does NOT catch, and this is the important part

**The City of London artefact is flagged `publishable=true`.**

Filtering on `publishable` and then ranking Black disparity ratios puts **City of London Police top
at 10.6**, ahead of Norfolk at 9.2 and Dorset at 9.1. That ranking is wrong, and the flag will not
stop you producing it.

The City has roughly 8,600 residents against a very large daytime working population. A
residence-based denominator is simply the wrong denominator there. The row is published rather than
deleted because deleting it hides the problem, but **it must not be ranked against territorial
forces.**

Exclude City of London explicitly. The flag is about whether a ratio could be *computed* honestly,
not about whether it is *comparable*.

The filtered ranking is rendered at
[Who gets stopped and searched in England and Wales](https://www.policecomplaint.com/uk/reports/who-gets-stopped-and-searched/),
with City of London excluded for the reason above.

## Small denominators in the complaints file

`uk/complaint-review-outcomes-by-force.csv` has one force under 30 completed reviews:
**City of London, 1 of 3, which renders as 33.3%.** Warwickshire is also thin at 11 of 32.

Exclude anything under about 30 completed reviews before ranking. Of the 37 forces with 50 or more,
the spread runs from **Devon and Cornwall at 40.1%** (69 of 172) down to **Leicestershire at 6.9%**
(14 of 203).

**A high overturn rate is not the same as a bad force.** It measures how often that force's own
complaint handling was found wanting on review, and recording practice varies between forces.
