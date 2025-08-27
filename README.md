# Energy Load Forecasting (Kaggle Competition Project)

This project demonstrates time-series forecasting approaches for electricity load management, 
comparing ARIMA and XGBoost on real-world energy data.

Forecasting hourly electricity load using **ARIMA** and **XGBoost**, based on the 
[Global Energy Forecasting Competition 2012 - Load Forecasting](https://www.kaggle.com/competitions/global-energy-forecasting-competition-2012-load-forecasting).

---

## Problem
Electric load forecasting is critical for power grid management and energy markets.  
The dataset contains **hourly load data across 15 zones** along with weather and calendar features.  
The objective is to forecast **168 hours (7 days)** ahead for each zone.

---

## Methods
- **ARIMA**
  - Iterated through candidate `(p,d,q)` parameters per zone.  
  - Fallback order `(1,1,1)` applied if optimal parameters not found.  
  - One-week-ahead forecasts generated per zone.  

- **XGBoost**
  - Gradient boosting with `n_estimators=100`, `objective='reg:squarederror'`.  
  - Train/test split performed per zone.  
  - Evaluation with RMSE, MAE, and R² metrics.  

---

## Results

| Model   | Avg RMSE | Avg MAE | Avg R²   |
|---------|----------|---------|----------|
| ARIMA   | 34.19    | 33.97   |-3.75e+24 |
| XGBoost | 3583.0   | 2642.6  | .9367    |

**Observations**:
- **ARIMA**:  
  - Captured local seasonal patterns with modest error.  
  - Some zones showed extreme variance, leading to very large negative R² (an artifact of poor fit in highly volatile regions).  

- **XGBoost**:  
  - Achieved a strong overall fit (Avg R² ≈ 0.94).  
  - RMSE/MAE values are higher in absolute terms due to scale of features, but relative fit was superior.  
  - Performed competitively without extensive feature engineering.
 
## Business Takeaways

- **Grid Reliability:** More accurate short-term load forecasts allow utilities to balance generation and demand, reducing the risk of blackouts or costly overproduction.  
- **Cost Savings:** Even a 1% improvement in forecast accuracy can translate into millions saved annually for energy providers due to optimized generation scheduling and reduced reliance on expensive reserve power.  
- **Market Impact:** Load forecasts feed into electricity market bidding. Better accuracy can improve pricing strategies and operational planning for power companies.  
- **Model Insight:** ARIMA captured local seasonal behavior but was unstable in highly volatile zones, while XGBoost demonstrated scalable performance across regions. This highlights the trade-off between interpretability (ARIMA) and predictive power (XGBoost).

## Future Work
This was completed as part of a **group project**. If revisited individually, I would explore advanced feature engineering and deployment in a Streamlit dashboard.
