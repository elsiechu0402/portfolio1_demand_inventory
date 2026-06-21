# Final Project Summary: Demand Forecasting and Inventory Policy Simulation

## Project Scope

- Selected item-store: FOODS_3_586 at TX_2
- Forecast horizon: 56 days
- Main workflow: demand forecasting followed by inventory policy simulation

## Forecasting Result

The best forecasting model was **Calendar-feature linear regression forecast**.

- MAE: 9.84
- RMSE: 12.45
- MAPE: 13.45%
- MAE reduction from naive baseline: 59.05%

## Inventory Policy Recommendation

The recommended safety stock level was **15 units**.

Compared with the base policy without safety stock:

- Total cost decreased from 1685.00 to 953.00
- Total cost reduction: 732.00 (43.44%)
- Service level improved from 0.9354 to 0.9948
- Lost sales decreased by 262 units
- Stockout days decreased by 25 days

## Interpretation

The results suggest that combining calendar-feature demand forecasting with a safety-stock-based replenishment policy can reduce stockout risk while lowering total inventory-related cost.
