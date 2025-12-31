## **Walmart Weekly Sales Regression Analysis**

**Overview**

This project analyzes the drivers of Walmart’s weekly store-level sales using linear regression and predictive modeling in R. The analysis progresses from simple linear models to more robust multivariate and log-linear specifications, with an emphasis on both explanatory insight and predictive performance.

The final model demonstrates that store characteristics and seasonality dominate sales outcomes, while macroeconomic indicators such as inflation and unemployment play smaller but statistically meaningful roles.

**Dataset**

The dataset contains weekly observations for multiple Walmart stores and includes the following variables:

weekly_sales – Weekly sales revenue (USD)

store – Store identifier

date – Week of observation

size – Store size

temperature – Average weekly temperature

fuel_price – Fuel price

cpi – Consumer Price Index (regional)

unemployment – Unemployment rate

isholiday – Holiday week indicator

CPI is measured at the CBSA/MSA level, introducing regional clustering effects explored during the analysis.

**Modeling Approach**

The analysis follows a structured modeling workflow:

Simple linear regression to assess CPI’s standalone effect

Store-level visualizations to explore regional heterogeneity

Multivariate regression incorporating store size and economic variables

Interaction and nonlinear terms to test behavioral hypotheses

Train/test split for out-of-sample prediction

Log transformation of weekly sales to address scale and heteroskedasticity

Models are evaluated using Adjusted R², RMSE, and MAE, with careful distinction between explanatory fit and predictive accuracy.

**Final Model Summary**

The final specification uses a log-linear regression with weekly sales transformed to their natural logarithm. This model achieves an Adjusted R² of approximately 0.71, substantially improving fit and stabilizing variance across stores with widely differing revenue levels.

Key findings include:

+ Store size is the strongest predictor of weekly sales

+ Holiday weeks increase sales by roughly 6–7%

+ CPI has a statistically significant negative relationship with sales

T+ emperature and unemployment have modest, intuitive effects

+ Fuel prices do not meaningfully impact sales once other factors are controlled for

+ This model provides a strong balance of interpretability, robustness, and practical relevance.

**Predictive Performance**

Using a 75/25 train-test split, the final predictive model achieves:

RMSE: ≈ $240,000

MAE: ≈ $179,000

Given that weekly store sales range from approximately $70K to $2.8M, these error levels are considered reasonable.

**Tools & Libraries**

tidyverse – Data manipulation and visualization

tidymodels – Modeling framework

tidylog – Pipeline transparency

ggplot2 / plotly – Visualization

gganimate – Animated store-level analysis

lubridate – Date handling

Repository Structure
├── data/
│   └── walmart.csv
├── walmart_sales_analysis.Rmd
├── README.md
├── .gitignore
└── outputs/
    └── walmart_sales_analysis.html

**How to Run**

Clone the repository

Ensure walmart.csv is located in the data/ directory

Open walmart_sales_analysis.Rmd in RStudio

Knit to HTML or PDF

**Limitations**

Store-level fixed effects are not explicitly modeled

Temporal autocorrelation and seasonality are not directly addressed

Some economic indicators are measured at broader geographic levels

Linear assumptions may obscure more complex nonlinear dynamics

**Next Steps**

Implement mixed-effects models to capture store-specific variation

Explore time-series methods for improved short-term forecasting

Apply regularization (LASSO/Ridge) for feature selection

Incorporate promotional or demographic data if available

**Author**

Eric Frederic
