# Demand Forecasting and Inventory Policy Simulation

## 1. Project Overview

This project connects demand forecasting with inventory replenishment decisions for a retail product-store combination.

**Research question:**

> How can demand forecasting be integrated with inventory policies to improve replenishment decisions under demand uncertainty?

The project follows an end-to-end operations analytics workflow:

1. Prepare item-store level daily demand data
2. Analyze demand patterns
3. Build and compare forecasting models
4. Select the best demand forecast
5. Simulate inventory replenishment policies
6. Recommend a safety stock level based on total cost and service level

## 2. Data

The project uses the M5 Forecasting dataset and focuses on one product-store combination.

- Selected item-store: **FOODS_3_586 at TX_2**
- Forecast horizon: **56 days**

The processed dataset contains daily demand, selling price, calendar variables, and revenue-related fields.

## 3. Demand Forecasting

The following forecasting models were compared:

- Naive forecast
- 7-day moving average forecast
- 28-day moving average forecast
- Weekday-adjusted moving average forecast
- Calendar-feature linear regression forecast

The calendar-feature linear regression model used selling price, time trend, weekday indicators, and monthly indicators as forecasting features.

### Forecasting model comparison

| model_short         |     MAE |    RMSE |   MAPE_percent |
|:--------------------|--------:|--------:|---------------:|
| Calendar regression |  9.8362 | 12.4503 |        13.4506 |
| Weekday-adjusted MA | 12.8884 | 16.8554 |        19.4382 |
| 7-day MA            | 16.2526 | 19.5498 |        23.897  |
| 28-day MA           | 17.0893 | 20.2939 |        25.3874 |
| Naive               | 24.0179 | 27.9595 |        36.7765 |

The best forecasting model was **Calendar-feature linear regression forecast**.

Key forecasting results:

- MAE: **9.84**
- RMSE: **12.45**
- MAPE: **13.45%**
- MAE reduction from naive baseline: **59.05%**

![Forecast Model Comparison by MAE](assets/figures/forecast_model_comparison_MAE_FOODS_3_586_TX_2.png)

![Forecast Model Comparison by RMSE](assets/figures/forecast_model_comparison_RMSE_FOODS_3_586_TX_2.png)

![Forecast Model Comparison by MAPE](assets/figures/forecast_model_comparison_MAPE_FOODS_3_586_TX_2.png)

## 4. Inventory Policy Simulation

The selected forecast was used as an input to simulate forecast-based replenishment policies.

The simulation tested safety stock levels of 0, 5, 10, 15, 20, 25, and 30 units.

Each policy was evaluated using lost sales, service level, stockout days, holding cost, stockout cost, and total cost.

### Safety stock policy comparison

|   safety_stock_units |   total_lost_sales |   service_level |   stockout_days |   total_holding_cost |   total_stockout_cost |   total_cost |
|---------------------:|-------------------:|----------------:|----------------:|---------------------:|----------------------:|-------------:|
|                    0 |                285 |        0.935418 |              30 |                  260 |                  1425 |         1685 |
|                    5 |                159 |        0.96397  |              22 |                  414 |                   795 |         1209 |
|                   10 |                 74 |        0.983231 |              13 |                  609 |                   370 |          979 |
|                   15 |                 23 |        0.994788 |               5 |                  838 |                   115 |          953 |
|                   20 |                  6 |        0.99864  |               2 |                 1101 |                    30 |         1131 |
|                   25 |                  0 |        1        |               0 |                 1375 |                     0 |         1375 |
|                   30 |                  0 |        1        |               0 |                 1655 |                     0 |         1655 |

![Safety Stock vs Total Cost](assets/figures/safety_stock_vs_total_cost_FOODS_3_586_TX_2.png)

![Safety Stock vs Service Level](assets/figures/safety_stock_vs_service_level_FOODS_3_586_TX_2.png)

![Safety Stock Cost Trade-off](assets/figures/safety_stock_cost_breakdown_FOODS_3_586_TX_2.png)

## 5. Recommended Inventory Policy

The recommended safety stock level is **15 units**.

This policy achieved the lowest total cost among the tested safety stock levels.

### Base policy vs optimal policy

| policy_type    |   safety_stock_units |   total_lost_sales |   service_level |   stockout_days |   average_ending_inventory |   total_holding_cost |   total_stockout_cost |   total_cost |
|:---------------|---------------------:|-------------------:|----------------:|----------------:|---------------------------:|---------------------:|----------------------:|-------------:|
| Base policy    |                    0 |                285 |        0.935418 |              30 |                    4.64286 |                  260 |                  1425 |         1685 |
| Optimal policy |                   15 |                 23 |        0.994788 |               5 |                   14.9643  |                  838 |                   115 |          953 |

Compared with the base policy without safety stock:

- Total cost decreased from **1685.0** to **953.0**
- Total cost reduction: **732.0**
- Total cost reduction percent: **43.44%**
- Service level improvement: **0.0594**
- Lost sales reduction: **262 units**

![Base vs Optimal Total Cost](assets/figures/base_vs_optimal_total_cost_FOODS_3_586_TX_2.png)

![Base vs Optimal Service Level](assets/figures/base_vs_optimal_service_level_FOODS_3_586_TX_2.png)

## 6. Interpretation

The results show that demand forecasting can support inventory replenishment decisions by providing a data-driven estimate of future demand.

The calendar-feature regression model improved forecasting accuracy compared with simpler baselines. The inventory simulation then showed that adding safety stock reduced stockout risk and lowered total inventory-related cost.

The results also show a clear trade-off: increasing safety stock reduces stockout cost but increases holding cost. The optimal policy balances these two costs.

## 7. Limitations

This project is a case study based on one item-store combination. The results should not be interpreted as a universal inventory policy for all products or stores.

The inventory simulation uses simplified assumptions:

- Daily replenishment
- Replenishment arrives before daily demand occurs
- Fixed holding cost
- Fixed stockout cost
- No supplier lead time uncertainty

Future extensions could evaluate multiple products and stores, include lead time uncertainty, and compare additional forecasting and replenishment methods.

## 8. Conclusion

This project demonstrates a practical operations analytics workflow that connects demand forecasting with inventory policy simulation.

The best forecasting model was **Calendar-feature linear regression forecast**, and the recommended safety stock level was **15 units**. This reduced total cost by **43.44%** compared with the base policy without safety stock.
