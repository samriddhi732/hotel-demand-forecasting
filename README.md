# Hotel Demand Forecasting using ARIMA in R

#Project Overview
This project applies Time Series Analysis and
ARIMA modelling to forecast monthly hotel bookings
Demand using a real-world dataset of 119,390
hotel booking records from 2015 to 2017.

#Objective
To build a reliable forecasting model that
predicts future hotel demand, helping hotel
management with staffing, pricing, and
inventory planning decisions.

#Dataset
- Total Records: 119,390 bookings
- Period: July 2015 to August 2017
- Variables: 32 columns including hotel type,
  arrival date, cancellation status, ADR, etc.
- Target Variable: Monthly confirmed bookings
  (excluding cancellations)

#Tools & Technologies
- Language: R Programming
- IDE: RStudio
- Libraries:
  - tidyverse - data manipulation
  - ggplot2 - data visualization
  - forecast - ARIMA modelling
  - tseries - stationarity testing

#Methodology
1. Data Import & Inspection
2. Data Cleaning & Preprocessing
3. Exploratory Data Analysis (EDA)
4. Time Series Object Creation
5. ADF Stationarity Test
6. ACF & PACF Analysis
7. Auto ARIMA Model Building
8. 12-Month Forecasting
9. Residual Diagnostics

#Model Results
| Metric | Value |
|--------|-------|
| Best Model | ARIMA(0,1,1)(0,1,0)[12] |
| MAPE | 5.97% |
| Forecast Accuracy | ~94% |
| AIC | 210.2 |
| Ljung-Box p-value | 0.3849 |

#Key Findings
- Hotel demand follows a strong monthly
  seasonality (period = 12)
- Peak demand occurs during May-August
- Lowest demand observed in
  November-January
- Model successfully captured seasonal
  patterns with high accuracy

#Files in Repository
- hotel_demand_forecasting.R - Main R script
- hotel_forecast_results.csv - Forecast values
- hotel_forecast.png - Forecast plot
- README.md - Project documentation
