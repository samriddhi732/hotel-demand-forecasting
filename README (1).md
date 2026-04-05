# 🏨 Hotel Booking Demand Forecasting

> Time series forecasting of hotel booking demand using ARIMA and SARIMA models in Python — M.Sc. Statistics Final Year Project

---

## 📌 Project Overview

Hotel businesses depend heavily on accurate demand forecasting to manage staffing, pricing, and inventory. This project applies classical time series models to forecast monthly hotel booking demand using real-world reservation data from Portuguese hotels (2015–2017).

The project covers the complete data science workflow — from raw data ingestion and cleaning, through exploratory data analysis, stationarity testing, model building, and performance evaluation — concluding with a comparison between ARIMA and SARIMA models.

---

## 📊 Dataset

| Attribute | Details |
|-----------|---------|
| Source | [Kaggle — Hotel Booking Demand](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand) |
| Original size | 119,390 rows × 32 columns |
| Date range | July 2015 – August 2017 |
| Hotel types | City Hotel, Resort Hotel |
| After cleaning | 73,388 rows × 20 columns |

**Key cleaning steps performed:**
- Removed 44,224 cancelled bookings (retained confirmed stays only)
- Handled missing values in `country`, `agent`, `company`, and `children`
- Removed entries with invalid ADR (average daily rate) and zero-guest records
- Merged `babies` into `children` column
- Dropped redundant and low-information columns
- Constructed a proper datetime index for time series aggregation

---

## 🔍 Exploratory Data Analysis

The EDA phase investigated booking patterns across multiple dimensions:

- **Bookings by hotel type** — City Hotel accounted for ~61% of confirmed bookings vs Resort Hotel (~39%)
- **Monthly booking trend (2015–2017)** — Clear seasonal peaks in summer months; upward trend over the observation period
- **Lead time distribution** — Right-skewed; majority of bookings made within 0–50 days of arrival, indicating predominantly short-notice demand
- **Top 10 guest nationalities** — Portugal (PRT) dominates, followed by UK (GBR), France (FRA), Spain (ESP), Germany (DEU)
- **Customer type breakdown** — Transient customers form ~71% of bookings; Transient-Party ~25%; Contract and Group together less than 5%

---

## 📈 Time Series Methodology

### Stationarity Testing
Applied the **Augmented Dickey-Fuller (ADF) test** to check for stationarity before modelling.

| ADF Statistic | p-value | Result |
|---------------|---------|--------|
| -2.2964 | 0.1731 | ❌ Non-stationary (p > 0.05) |

First-order differencing (d=1) was applied to achieve stationarity.

### ACF and PACF Analysis
- **ACF (Autocorrelation Function):** Showed gradual decay — indicating the presence of autocorrelation across multiple lags and guiding the MA (q) parameter selection
- **PACF (Partial Autocorrelation Function):** Showed sharp cutoff after lag 1–2 — guiding the AR (p) parameter selection

### Train-Test Split

| Split | Period | Months |
|-------|--------|--------|
| Training | July 2015 – February 2017 | 20 months |
| Test | March 2017 – August 2017 | 6 months |

---

## 🤖 Models Built

### Model 1 — ARIMA(1,1,1)
A standard AutoRegressive Integrated Moving Average model capturing trend and short-term autocorrelation. Does not account for seasonal patterns.

- **p = 1** → Uses 1 lagged value (AR component)
- **d = 1** → First-order differencing for stationarity
- **q = 1** → 1 lagged forecast error (MA component)

### Model 2 — SARIMA(1,1,1)(1,1,1,12)
Extends ARIMA with an additional seasonal component (period = 12 months), allowing the model to capture recurring yearly patterns in booking demand.

- Non-seasonal: (1,1,1)
- Seasonal: (1,1,1,12) — looks back 12 months to model yearly seasonality

---

## 📉 Model Performance

| Model | MAE | RMSE | MAPE |
|-------|-----|------|------|
| ARIMA(1,1,1) | 525.48 | 541.27 | 16.12% |
| **SARIMA(1,1,1)(1,1,1,12)** | **332.47** | **497.60** | **10.58%** |

**✅ Best Model: SARIMA(1,1,1)(1,1,1,12)**

SARIMA outperformed ARIMA across all three metrics. The MAPE improvement from 16.12% to 10.58% confirms that capturing the 12-month seasonal cycle significantly improves forecast accuracy for hotel booking demand.

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Python 3 | Core programming language |
| Pandas | Data manipulation and time series aggregation |
| Matplotlib | Data visualization and plot generation |
| Statsmodels | ADF test, ACF/PACF plots, ARIMA/SARIMA modelling |
| Jupyter Notebook | Interactive development environment |

---

## 📁 Project Structure

```
hotel-demand-forecasting/
│
├── Hotel_Demand_Forecast.ipynb   # Main Jupyter notebook (full workflow)
├── plot_monthly_trend.png         # Monthly bookings time series plot
└── README.md                      # Project documentation
```

---

## 🚀 How to Run

1. Clone the repository
   ```bash
   git clone https://github.com/samriddhi732/hotel-demand-forecasting.git
   ```

2. Install required libraries
   ```bash
   pip install pandas matplotlib statsmodels jupyter
   ```

3. Download the dataset from [Kaggle](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand) and place `hotel_bookings.csv` in the project folder

4. Open and run the notebook
   ```bash
   jupyter notebook Hotel_Demand_Forecast.ipynb
   ```

---

## 📚 Key Learnings

- Real-world hotel booking data requires substantial cleaning before analysis — over 38% of records were either cancelled or invalid
- Lead time distribution reveals that most demand is short-notice, making near-term forecasting especially valuable
- ARIMA alone is insufficient for data with strong seasonal patterns; SARIMA's seasonal component is essential
- A MAPE of ~10.6% on a 6-month test horizon is a practically meaningful result for hospitality demand planning

---

## 👩‍💻 Author

**Samriddhi**
M.Sc. Statistics — Punjabi University (2024–2026)
Aspiring Data Analyst | R · Python · SQL · Excel · Power BI

[![GitHub](https://img.shields.io/badge/GitHub-samriddhi732-181717?style=flat&logo=github)](https://github.com/samriddhi732)

---

## 📄 License

This project is intended for academic and portfolio purposes.
Dataset credit: [Antonio, Almeida & Nunes (2019)](https://www.sciencedirect.com/science/article/pii/S2352340918315191) via Kaggle.
