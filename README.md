# Retail Promotion Strategy

## When and Where Do Retail Promotions Work Best?

A business-focused analysis of promotion-associated sales differences using the Rossmann Store Sales dataset. The project examines how promotion patterns vary across timing, store characteristics, assortment, and competitor proximity, then benchmarks predictive models using a temporal holdout.

## Business Questions

1. Under what conditions are promotions associated with the largest sales differences?
2. Does competitor proximity change the observed promotion pattern?
3. Which timing and store characteristics should be prioritized for further controlled testing?

## Dataset

The analysis uses the **Rossmann Store Sales** dataset from Kaggle.

- 1,017,209 daily store observations
- 1,115 stores
- Historical coverage: January 2013 to July 2015
- Daily sales, customer counts, promotion status, store format, assortment, holidays, and competitor information

Raw data are **not included** in this repository. Download the competition data from Kaggle and place `train.csv` and `store.csv` in a local `data/` directory before running the notebook.

Dataset: https://www.kaggle.com/competitions/rossmann-store-sales/data

## Approach

The project combines descriptive matching and predictive modeling:

- Data quality and coverage checks
- Matched comparisons within store × year-month × weekday
- Separate analysis of sales, customers, and sales per customer
- Promotion patterns by weekday, store type, assortment, and competitor distance
- Temporal train/validation/test design
- Ridge regression as an interpretable baseline
- Histogram Gradient Boosting as the nonlinear benchmark
- Scenario comparisons using `Promo = 0` and `Promo = 1` while holding other pre-outcome features fixed
- Robustness checks across years and alternative sample definitions

## Key Findings

- The matched sales difference is approximately **39.6%** between promotion and non-promotion days within comparable store-calendar groups.
- Timing is the strongest recurring pattern: the matched difference is highest on **Monday (64.3%)** and lowest on **Friday (21.3%)**.
- Customer traffic and sales per customer both move with promotion status, suggesting that sales-only monitoring misses useful business context.
- Competitor proximity shows a smaller and less stable relationship than weekday timing.
- Histogram Gradient Boosting achieves a final holdout **MAE of 797.7** and **R² of 0.874**, outperforming the Ridge baseline.

These are descriptive and model-implied differences, **not causal estimates of promotion uplift or profit impact**.

## Repository Structure

```text
retail-promotion-strategy/
├── README.md
├── notebooks/
│   └── promotion_strategy.ipynb
└── report/
    └── promotion_strategy_report.pdf
```

## Reproducing the Analysis

1. Download the Rossmann Store Sales data from Kaggle.
2. Create a local `data/` directory.
3. Place `train.csv` and `store.csv` inside it.
4. Open and run `notebooks/promotion_strategy.ipynb` from top to bottom.

The notebook also supports a configurable Rossmann data directory through the project code.

## Practical Interpretation

The analysis supports a clear next step: test weekday timing first in a controlled promotion pilot, stratify by store format and competitor proximity, and evaluate **incremental gross margin**, promotion cost, and post-promotion demand rather than sales alone.

## Limitations

The historical data do not contain gross margin, promotion cost, discount depth, product mix, competitor prices, or customer identities. Promotion timing is not randomly assigned, so the results should not be interpreted as causal effects or profit-maximizing rules.

## Author

**Mahmood Mohammadi Nezhad**  
M.Sc. in Economics & E-Commerce, University of Tehran

- GitHub: https://github.com/DataMahmood
- LinkedIn: https://www.linkedin.com/in/mahmood-mohammadi-nezhad-a477881b4/

## Full Report

See: [Promotion Strategy Report](report/promotion_strategy_report.pdf)
