# Demand Forecasting and Inventory Policy Simulation

## Project Overview

This project analyzes how demand forecasting can be connected with inventory replenishment decisions for a retail product-store combination.

The main research question is:

**How can demand forecasting be integrated with inventory policies to improve replenishment decisions under demand uncertainty?**

The project follows a practical operations analytics workflow:

1. Prepare item-store level daily demand data
2. Explore demand patterns
3. Build and compare forecasting models
4. Select the best demand forecast
5. Simulate inventory replenishment policies
6. Recommend a safety stock level based on total cost and service level

## Dataset

The project uses the M5 Forecasting dataset.

Selected item-store combination:

- **FOODS_3_586 at TX_2**
- Forecast horizon: **56 days**

The processed dataset contains daily demand, selling price, calendar variables, and revenue-related fields for the selected item-store pair.

## Methodology

### 1. Data Preparation

The raw M5 data was transformed from wide daily sales format into a clean daily time-series dataset for one item-store combination.

### 2. Exploratory Data Analysis

The exploratory analysis examined:

- Historical demand trend
- Demand distribution and outliers
- Weekday demand patterns
- Monthly demand patterns
- Price-demand patterns
- Yearly demand and price trends

### 3. Demand Forecasting

Several forecasting approaches were compared:

- Naive forecast
- 7-day moving average forecast
- 28-day moving average forecast
- Weekday-adjusted moving average forecast
- Calendar-feature linear regression forecast

The best forecasting model was:

**Calendar-feature linear regression forecast**

Forecasting performance:

- MAE: **9.84**
- RMSE: **12.45**
- MAPE: **13.45%**
- MAE reduction from naive baseline: **59.05%**

### 4. Inventory Policy Simulation

The selected forecast was used as an input to simulate forecast-based replenishment policies.

The inventory policy tested different safety stock levels:

- 0 units
- 5 units
- 10 units
- 15 units
- 20 units
- 25 units
- 30 units

The simulation evaluated each policy using:

- Total lost sales
- Service level
- Stockout days
- Average ending inventory
- Holding cost
- Stockout cost
- Total cost

## Key Results

The recommended safety stock level was:

**15 units**

Compared with the base policy without safety stock:

- Total cost decreased from **1685.0** to **953.0**
- Total cost reduction: **732.0**
- Total cost reduction percent: **43.44%**
- Service level improvement: **0.0594**
- Lost sales reduction: **262 units**

## Repository Structure

```text
portfolio1_demand_inventory/
├── data/
│   ├── raw/
│   └── processed/
├── notebooks/
│   ├── 01_data_preparation.ipynb
│   ├── 02_exploratory_analysis.ipynb
│   ├── 03_demand_forecasting.ipynb
│   └── 04_inventory_policy_simulation.ipynb
├── outputs/
│   ├── figures/
│   └── tables/
├── report/
└── README.md
```

## Key Output Files

Important tables:

- `outputs/tables/final_model_comparison_metrics_FOODS_3_586_TX_2.csv`
- `outputs/tables/selected_forecast_for_inventory_FOODS_3_586_TX_2.csv`
- `outputs/tables/safety_stock_policy_comparison_FOODS_3_586_TX_2.csv`
- `outputs/tables/final_inventory_policy_recommendation_FOODS_3_586_TX_2.csv`
- `outputs/tables/final_project_summary_FOODS_3_586_TX_2.csv`

Important figures:

- `outputs/figures/forecast_model_comparison_MAE_FOODS_3_586_TX_2.png`
- `outputs/figures/forecast_model_comparison_RMSE_FOODS_3_586_TX_2.png`
- `outputs/figures/forecast_model_comparison_MAPE_FOODS_3_586_TX_2.png`
- `outputs/figures/safety_stock_vs_total_cost_FOODS_3_586_TX_2.png`
- `outputs/figures/safety_stock_vs_service_level_FOODS_3_586_TX_2.png`
- `outputs/figures/safety_stock_cost_breakdown_FOODS_3_586_TX_2.png`
- `outputs/figures/base_vs_optimal_total_cost_FOODS_3_586_TX_2.png`
- `outputs/figures/base_vs_optimal_service_level_FOODS_3_586_TX_2.png`

## Interpretation

The results show that a calendar-feature forecasting model improved short-term demand forecasting accuracy compared with simple baseline models.

The inventory simulation further showed that adding safety stock can reduce stockout risk and total cost. In this case, a safety stock level of **15 units** achieved the lowest total cost among the tested policies.

## Limitations

This project focuses on one item-store combination. The results should be interpreted as a case study rather than a universal policy for all products or stores.

The inventory simulation uses simplified assumptions, including:

- Daily replenishment
- Immediate replenishment before demand occurs
- Fixed holding cost
- Fixed stockout cost
- No supplier lead time uncertainty

Future extensions could test multiple item-store pairs, include lead time, compare additional forecasting models, and evaluate more advanced replenishment policies.

## Tools Used

- Python
- pandas
- NumPy
- matplotlib
- scikit-learn
- Jupyter Notebook

## Project Summary

This project demonstrates an end-to-end operations analytics workflow that connects demand forecasting with inventory replenishment decisions.
