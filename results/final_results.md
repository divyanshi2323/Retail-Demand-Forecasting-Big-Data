\# Final Results – Retail Demand Forecasting



\## Dataset Validation



\- Total records: 76,000

\- Total columns: 16

\- Date range: 2022-01-01 to 2024-01-30

\- Null values: 0

\- Full duplicate records: 0

\- Duplicate (date, store\_id, product\_id) keys: 0

\- Negative demand/units: 0

\- Non-positive prices: 0

\- Invalid promotion/epidemic flags: 0



\## Store-Level Demand



| Store | Region | Total Demand | Average Demand |

|---|---|---:|---:|

| S001 | North | 1,547,573 | 101.81 |

| S002 | South | 1,625,471 | 106.94 |

| S003 | East | 1,618,324 | 106.47 |

| S004 | West | 1,529,651 | 100.63 |

| S005 | North | 1,607,085 | 105.73 |



\### Key Finding



S002 (South) recorded the highest total demand at 1,625,471.



\## Demand Patterns



\- Highest average-demand quarter: 2023 Q3 — 115.50

\- 2022 Q1 average demand: 112.73

\- Demand was approximately 29–31% higher during promotions across categories.

\- Average demand during epidemic periods: 70.16.

\- Average demand without epidemic conditions: 112.86.

\- Demand during epidemic periods was approximately 38% lower.



\## Discount Analysis



| Discount | Average Demand |

|---:|---:|

| 0% | 94.75 |

| 5% | 94.94 |

| 10% | 102.77 |

| 15% | 123.58 |

| 20% | 124.07 |

| 25% | 122.97 |



Demand increased with higher discounts up to around 15–20%, after which the gains began to level off.



\## Unmet Demand Gap



| Category | Average Demand Gap |

|---|---:|

| Groceries | 18.10 |

| Clothing | 17.98 |

| Electronics | 14.44 |

| Toys | 14.16 |

| Furniture | 9.21 |



Groceries had the highest average unmet-demand gap.



\## Weather Analysis



| Weather | Average Demand |

|---|---:|

| Sunny | 115.17 |

| Cloudy | 105.40 |

| Rainy | 95.11 |

| Snowy | 94.05 |



Average demand was highest during Sunny weather conditions.



\## Forecasting Model Results



| Model | RMSE | MAE | R² |

|---|---:|---:|---:|

| Lag-1 Baseline | 51.465 | 39.671 | -0.312 |

| Linear Regression | 32.790 | 25.374 | 0.467 |

| Random Forest | 31.931 | 24.715 | 0.495 |



\### Best Model



Random Forest produced the best performance among the tested models:



\- RMSE: 31.931

\- MAE: 24.715

\- R²: 0.495



\## Important Note



The observed relationships between demand and factors such as promotions, discounts, weather, and epidemic conditions are associations in the analysed data. They should not be interpreted as proof of causation.

