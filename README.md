# Walmart Weekly Sales: Regression Analysis in R

**Author:** Eric A. Frederic, MBA  
**Tools:** R | tidymodels | ggplot2 | tidyverse  
**Full Notebook:** [View on Kaggle](https://www.kaggle.com/code/ericfrederic/analyzing-drivers-of-walmart-weekly-sales-regress)

---

## Business Problem

What actually drives weekly sales at a large retail chain? This project uses linear regression and predictive modeling to identify the key drivers of Walmart's weekly store-level sales revenue, progressing from simple single-variable models to a robust log-linear specification that explains 71% of the variance in sales outcomes.

The analysis distinguishes between explanatory fit and predictive accuracy throughout — two related but distinct analytical goals that require different evaluation criteria.

---

## Dataset

Weekly observations for 45 Walmart store locations. Key variables:

| Variable | Description |
|----------|-------------|
| `weekly_sales` | Weekly sales revenue (USD) — target variable |
| `store` | Store identifier |
| `date` | Week of observation |
| `size` | Store square footage |
| `temperature` | Average weekly temperature |
| `fuel_price` | Regional fuel price |
| `cpi` | Consumer Price Index (CBSA/MSA level) |
| `unemployment` | Regional unemployment rate |
| `isholiday` | Holiday week indicator (TRUE/FALSE) |

**Note:** CPI is measured at the Core Based Statistical Area level, introducing regional clustering effects explored during the analysis.

---

## Modeling Approach

The analysis follows a structured progression from simple to complex:

1. **Simple linear regression** — CPI as standalone predictor (Adjusted R² ≈ 0.005)
2. **Store-level visualization** — Regional heterogeneity in CPI effects
3. **Multivariate regression** — Adding store size as predictor (Adjusted R² ≈ 0.62)
4. **Interaction and nonlinear terms** — Holiday × temperature interaction; temperature²
5. **Train/test split** — 75/25 split for out-of-sample predictive evaluation
6. **Log-linear transformation** — Log(weekly_sales) to address scale and heteroskedasticity (Adjusted R² ≈ 0.71)

Models are evaluated using Adjusted R², RMSE, and MAE with careful distinction between explanatory and predictive performance.

---

## Key Findings

<img width="349" height="322" alt="log_bar" src="https://github.com/user-attachments/assets/b2bd85ed-19dd-4d3c-82d6-5e82b0c0ce6f" />


Weekly sales vary significantly across store locations, motivating the log transformation that becomes the core modeling decision.

<img width="342" height="324" alt="CPI" src="https://github.com/user-attachments/assets/1c92264a-c435-434a-82a3-b004ff34e64c" />

The relationship between CPI and sales varies by region and reverses sign across store clusters — a finding that explains why CPI alone accounts for less than 1% of sales variance.

<img width="353" height="326" alt="temp_curve" src="https://github.com/user-attachments/assets/2cd3f6ef-63f3-43e5-b060-a3fdca88dc14" />

Temperature has a curvilinear effect on sales — an inverted U-shape consistent with consumer behavior. Neither extreme cold nor extreme heat is good for foot traffic.

**Final model findings:**

- **Store size** is the dominant predictor of weekly sales, dwarfing all macroeconomic variables
- **Holiday weeks** are associated with a 6–7% increase in sales
- **CPI** has a statistically significant negative relationship with sales after controlling for store characteristics
- **Temperature and unemployment** exhibit modest, intuitive effects
- **Fuel prices** do not meaningfully impact sales once other factors are controlled

---

## Predictive Performance

Using a 75/25 train/test split, the final log-linear model achieves:

| Metric | Value |
|--------|-------|
| RMSE | ≈ $240,000 |
| MAE | ≈ $179,000 |

Given that weekly store sales range from approximately $70K to $2.8M with a mean of $740K, these error levels are considered reasonable for a model of this specification.

---

## Limitations

| Limitation | Notes |
|------------|-------|
| No store fixed effects | Store-level idiosyncrasies are not explicitly modeled |
| Temporal structure | Autocorrelation and seasonality are handled implicitly, not directly |
| Geographic aggregation | CPI and unemployment measured at broader levels than individual stores |
| Linear assumptions | Nonlinear and interaction effects beyond those tested may exist |

---

## Next Steps

- Implement mixed-effects (hierarchical) models to capture store-specific variation
- Explore time-series methods for improved short-term forecasting
- Apply regularization (LASSO/Ridge) for feature selection
- Incorporate promotional, demographic, or foot traffic data if available

---

## Tools & Libraries

| Package | Purpose |
|---------|---------|
| `tidyverse` | Data manipulation and visualization |
| `tidymodels` | Modeling framework |
| `tidylog` | Pipeline transparency |
| `ggplot2` / `plotly` | Static and interactive visualization |
| `gganimate` | Animated store-level analysis |
| `lubridate` | Date handling |

---

## How to Run

1. Clone the repository
2. Place `walmart.csv` in the `data/` directory
3. Open `walmart_sales_analysis.Rmd` in RStudio
4. Knit to HTML or PDF

Or view the fully rendered notebook directly on [Kaggle](https://www.kaggle.com/code/ericfrederic/analyzing-drivers-of-walmart-weekly-sales-regress).

---

*MIT License — see LICENSE for details*
