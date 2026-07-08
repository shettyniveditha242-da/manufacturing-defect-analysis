# Manufacturing Quality Analysis: What Drives Phone-Case Drop-Test Failures?

Exploratory data analysis of a cell-phone-case manufacturing process, using Python (pandas, seaborn) to find out **why roughly 1 in 3 cases fails its drop test** — and which factor the business should act on first.

> *Note: this analysis was originally built as a graduate data science project (Master of Data Science). The dataset was provided as part of the course.*

## The problem

A manufacturer produces phone cases on **three injection-molding machines**, using plastic pellets from **two suppliers**. Every finished case goes through a **drop test** it either passes or fails. About 30% fail, and the goal is to identify what's associated with failure so the business can target the right machine, supplier, or process setting instead of guessing.

## The data

I combined four separate sources into one analytical dataset:

| Source | Rows | Contents |
|---|---|---|
| Machine logs (×3) | ~14,300 combined | Per-unit operating variables `x1`–`x4`, batch, sequence id |
| Supplier / material file | 50 batches | Supplier for each batch and its plastic **density** |
| Drop-test results | 1,412 tests | Pass / fail outcome (`Result`; 1 = fail) per unit |

## Approach

1. Validated each source (shape, data types, unique values, missing values).
2. Concatenated the three machine logs and merged in supplier/material data, then joined the drop-test results — producing a single table linking every tested unit to its machine, supplier, material density, and operating conditions.
3. Explored each factor's relationship to the pass/fail outcome using grouped failure rates and boxplots.

## Key findings

- **Supplier is the strongest lever.** Supplier A's cases fail **33%** of the time vs **25%** for Supplier B — the biggest gap of any factor.
- **Material density matters.** Failed cases have lower average density (9.61 vs 9.78), and Supplier A's material is both lower-density and less consistent.
- **Machines are roughly equivalent.** Failure rates sit in a tight 28–32% band, so the machines themselves aren't the primary driver.
- **One process setting stands out.** Operating variable `x4` runs higher on failed cases — the most promising parameter to investigate.

## Recommendations

- Audit Supplier A on density consistency (or shift volume to Supplier B) and re-test the failure rate.
- Add an incoming-material minimum density spec, since low density tracks with failure.
- Investigate the `x4` machine setting with process engineers.
- Deprioritize machine-level changes — the machines perform equivalently.

## Tools & skills

Python · pandas · seaborn / matplotlib · data validation & cleaning · multi-source joins/merges · grouped aggregation · choosing visualizations by data type · turning exploratory findings into business recommendations.

## How to view

Open [`phone_case_quality_analysis.ipynb`](phone_case_quality_analysis.ipynb) — GitHub renders it directly in the browser. If it doesn't load, paste the notebook URL into [nbviewer.org](https://nbviewer.org).
