# 🏨 Hotel Booking Demand Forecasting

> **Time series forecasting of monthly hotel booking demand using ARIMA in R**

---

## 📌 Project Summary

This project builds a monthly demand forecasting model for hotel bookings using the [Hotel Booking Demand dataset](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand) from Kaggle.

The full pipeline covers data cleaning, time series construction, stationarity testing, ARIMA model fitting, residual diagnostics, accuracy evaluation, and a 12-month future forecast — implemented entirely in R.

---

## 📊 Key Results

| Metric | Value |
|--------|-------|
| Best Model | ARIMA(0,1,1)(0,1,0)[12] |
| RMSE | *[update after running script]* |
| MAE | *[update after running script]* |
| MAPE | *[update after running script]* |
| Forecast Horizon | 12 months |

---

## 🗂️ Repository Structure

```
hotel-demand-forecasting/
│
├── hotel_demand_forecasting.Rmd      # Full analysis as R Markdown report
├── hotel_forecasting_improved.R      # Standalone R script
│
├── hotel_bookings.csv                # Dataset (from Kaggle)
│
├── plots/
│   ├── 01_raw_time_series.png        # Monthly demand over time
│   ├── 02_decomposition.png          # Trend + Seasonal + Residual
│   ├── 03_acf_pacf.png              # Autocorrelation plots
│   ├── 04_residual_diagnostics.png  # Model residual checks
│   ├── 05_actual_vs_predicted.png   # Test set evaluation
│   └── 06_12month_forecast.png      # Future forecast with CI
│
└── outputs/
    └── forecast_12months.csv         # Forecast values + confidence intervals
```

---

## 📁 Dataset

- **Source:** [Kaggle — Hotel Booking Demand](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand)
- **Original paper:** Antonio, Almeida & Nunes (2019), *Data in Brief*, Vol. 22
- **Size:** 119,390 rows × 32 columns
- **Period:** July 2015 – August 2017
- **Hotels:** City Hotel + Resort Hotel (Portugal)

---

## 🔧 Methodology

### Pipeline

```
Raw Data → Clean (remove cancellations) → Monthly Aggregation
→ Time Series Object → ADF Stationarity Test → ACF/PACF
→ Train/Test Split (80/20) → auto.arima() → Residual Diagnostics
→ Accuracy Metrics (RMSE, MAE, MAPE) → 12-Month Forecast
```

### Techniques Used

- **ADF Test** — Augmented Dickey-Fuller for stationarity
- **ACF/PACF** — Identify AR/MA order candidates
- **auto.arima()** — Exhaustive AIC-based model selection (stepwise = FALSE)
- **Ljung-Box Test** — Verify white noise residuals
- **80/20 Train-Test Split** — Evaluate out-of-sample accuracy
- **Confidence Intervals** — 80% and 95% for forecast uncertainty

---

## 📦 R Packages Required

```r
install.packages(c("tidyverse", "forecast", "tseries", "Metrics", "lubridate"))
```

| Package | Purpose |
|---------|---------|
| `tidyverse` | Data manipulation & ggplot2 visualization |
| `forecast` | ARIMA modeling, forecasting, auto.arima() |
| `tseries` | ADF stationarity test |
| `Metrics` | RMSE, MAE calculation |
| `lubridate` | Date parsing and manipulation |

---

## ▶️ How to Run

### Option 1: R Markdown Report (Recommended)

```r
# In RStudio — opens a fully rendered HTML report
rmarkdown::render("hotel_demand_forecasting.Rmd")
```

### Option 2: R Script

```r
# Ensure hotel_bookings.csv is in your working directory
# Create folders first:
dir.create("plots")
dir.create("outputs")

source("hotel_forecasting_improved.R")
```

> **Dataset:** Download `hotel_bookings.csv` from [Kaggle](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand) and place it in the project root.

---

## 📈 Sample Output

### Monthly Demand (2015–2017)
![Raw Time Series](plots/01_raw_time_series.png)

### 12-Month Forecast
![Forecast](plots/06_12month_forecast.png)

### Actual vs Predicted (Test Set)
![Actual vs Predicted](plots/05_actual_vs_predicted.png)

---

## 💡 Business Insights

- Booking demand shows strong **annual seasonality** — peaks consistently in summer months (June–August)
- Clear **upward trend** from 2015 to 2017 indicating growing demand
- The model can support hotel management in:
  - 📅 **Staffing** — anticipate high-demand periods
  - 💰 **Dynamic Pricing** — raise rates ahead of demand peaks
  - 🛏️ **Inventory Planning** — optimize room availability

---

## 👩‍💻 Author

**Samriddhi**
M.Sc. Statistics — Punjabi University

[![GitHub](https://img.shields.io/badge/GitHub-samriddhi732-black?logo=github)](https://github.com/samriddhi732)

---

## 📄 License

This project uses publicly available data under the original dataset's license.
Reference: Antonio, N., Almeida, A., & Nunes, L. (2019). Hotel booking demand datasets. *Data in Brief*, 22, 41–49.
