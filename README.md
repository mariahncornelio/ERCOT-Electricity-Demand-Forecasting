# ERCOT Electricity Demand Forecasting & Modeling (2023–2026)

## OVERVIEW

This project forecasts daily ERCOT (Electric Reliability Council of Texas) electricity demand (MWh) using historical load and weather data. Two modeling approaches were implemented and compared:
- XGBoost (Machine Learning)
- Prophet (Time-Series Forecasting)
The objective is to evaluate predictive performance and understand how weather and historical demand patterns influence grid load.
This project demonstrates time-series forecasting, feature engineering, model comparison, and dashboard deployment for infrastructure analytics.

## DATA

Time Range: Jan 1, 2023 – Feb 8, 2026

**Sources:**
- U.S. Energy Information Administration API: https://www.eia.gov/opendata/
- NOAA Climate Data Online (DALLAS FAA AIRPORT, TX US station used as temperature proxy): https://www.ncei.noaa.gov/cdo-web/search?datasetid=GHCND

Key Features:
- Temperature (TAVG, TAVG²)
- Weather (PRCP, AWND)
- Calendar (month, day_of_week)
- Lag features (lag_1, lag_7)

Dallas weather was used as a proxy for statewide demand trends due to data accessibility constraints.

## MODELS AND RESULTS

XGBoost was used to capture nonlinear relationships between demand, weather, and recent load patterns. Prophet was used to model long-term trends and seasonal cycles in the time series.

Comparing both helps determine whether electricity demand is driven more by external features or by underlying time-based patterns.
| Model   | MAE (MWh) | RMSE (MWh) | R²   |
| ------- | --------- | ---------- | ---- |
| XGBoost | 88,464    | 130,193    | 0.61 |
| Prophet | 79,432    | 117,496    | 0.72 |

**XGBoost:**
- Captures nonlinear relationships, most important drivers are lag_1 (previous day demand), TAVG² (extreme temperature effect), TAVG, and day_of_week

**Prophet:**
- Decomposes demand into long-term trend, weekly seasonality, yearly seasonality, and reveals steady demand growth from 2023-2026

## DASHBOARD
Power BI dashboard includes:
- ERCOT KPIs
- Actual vs Predicted (XGBoost & Prophet)
- Feature Importance (XGBoost)
- Trend & Seasonality Decomposition (Prophet)

<img width="2456" height="1382" alt="image" src="https://github.com/user-attachments/assets/2714e06b-2638-4358-8e9f-fa788d8243f3" />

<img width="2458" height="1372" alt="image" src="https://github.com/user-attachments/assets/6286e6a9-2525-4004-b9f5-341945e23923" />

## KEY INSIGHTS
- Electricity demand is strongly influenced by recent demand patterns.
- Temperature has a nonlinear impact, especially during extreme heat/cold.
- Seasonal cycles explain a large portion of demand variation.
- Prophet outperformed XGBoost in this dataset, suggesting time-based patterns dominate.

## FUTURE WORK AND IMPROVEMENTS
- Incorporate multiple Texas weather stations instead of using just a Dallas proxy
- Add holiday indicators
- Test SARIMAX or LSTM models
- Perform rolling time-series cross-validation


