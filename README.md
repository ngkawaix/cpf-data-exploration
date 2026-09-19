# CPF Contribution Rates: Who Bears the Cost, 1955-2026

Who bears the cost when CPF contribution rates go up, employers or employees?

## Overview

An analysis of Singapore's CPF contribution rate history, pulled live from data.gov.sg, split by who pays (employer vs employee) and by age band, going back to 1955.

## Data Source

Pulled live via the data.gov.sg datastore API:

- **CPF Contribution Rates**: [dataset d_98ffa142ae0dec40391f78f81d26aca9](https://data.gov.sg/datasets/d_98ffa142ae0dec40391f78f81d26aca9/view)
- **CPF Allocation Rates**: [dataset d_97ec9a2ce15cbf253128e48779a3fba0](https://data.gov.sg/datasets/d_97ec9a2ce15cbf253128e48779a3fba0/view)

## Method

1. Fetch both datasets in full via a paginated API wrapper (`fetch_full_dataset()`)
2. Pivot into employer and employee contribution tables by age band
3. Empirically test whether the three sub-50 age bands ("35 and below," "35-45," "45-50") actually differ, before merging them. They matched on every one of 48 recorded rate revisions since 1955, for both employer and employee rates, so they were collapsed into a single "Below 50" band
4. Recompute the employer-employee spread and total contribution rate from the merged bands
5. Plot four views: employer rate, employee rate, total rate, and spread, each by age group over time

## Findings

From 2000 to 2016, every age band trended toward employers carrying more of each contribution rate increase.

From 2022 onward, that trend reversed for older workers, in the 55-60 and 60-65 age bands specifically. For the 55-60 band, the spread moved from even in 2022 to employees contributing 2 percentage points more by 2026. The 60-65 band shows the same shift, moving from employer-loaded by 1.5pp to break even over the same window.

The bands outside this middle range didn't follow the shift. The youngest bands (below 50, and 50-55) have held a spread of employees contributing 3 percentage points more, unchanged since 2015. The newest oldest bands (65-70 and 70+, introduced in 2022) have stayed employer-loaded, with the spread holding at 1.5pp for the 65-70 band and 2.5pp for the 70+ band.

## Caveats

- CPF Board's current contribution rate tables (as of July 2026) report a single "55 and below" band. This analysis keeps "50-55" separate from the merged "Below 50" group, because between 2005 and 2016 the total contribution rate for the 50-55 band differed from the "Below 50" group, even though the employer-employee spread between them had already converged by 2015.
- CPF only began tracking workers above 65 as two separate bands ("65-70" and "70+") from 2022. Before that, it was a single "above 65" band that stopped being revised in 2016. Charts spanning the full history will show this as a definitional break around 2016-2022 but it is not a data gap.
- CPF contribution rates in this dataset apply to the highest wage band. CPF uses graduated phase-in rates for lower monthly wages that aren't captured here.
- Some age bands have fewer recorded revisions than others, since the dataset logs a new row only when a band's rate actually changes. This can produce short visual gaps in step-plotted lines for bands that went several years without a change.

## Repo Structure

```
.
├── cpf_allocation_rates.ipynb   # full analysis notebook
├── charts/                      # generated PNGs
│   ├── employer_contribution_by_age_group.png
│   ├── employee_contribution_by_age_group.png
│   ├── contribution_rate_spread.png
│   └── total_contribution_rate.png
├── requirements.txt
└── README.md
```

## Running Locally

```bash
pip install -r requirements.txt
jupyter notebook cpf_allocation_rates.ipynb
```

## Author

Ng Ka Wai
