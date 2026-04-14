# 🌤️ Daily Climate Forecasting — Delhi
### Machine Learning Solution for Mean Temperature Prediction

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Platform-Google%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white"/>
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white"/>
  <img src="https://img.shields.io/badge/Model-Ridge%20Regression-success?style=for-the-badge"/>
</p>

---

## 📌 Project Overview

This project predicts the **mean daily temperature (°C)** for Delhi using machine learning applied to the [Kaggle Daily Climate Time Series Dataset (2013–2017)](https://www.kaggle.com/datasets/sumanthvrao/daily-climate-time-series-data).

| Detail | Value |
|---|---|
| 🎯 **Target Variable** | Mean Daily Temperature (°C) |
| 📅 **Test Period** | January – April 2017 (114 days) |
| 🏆 **Best Model** | Ridge Regression |
| 📊 **R² Score** | ~0.93 |
| 📉 **MAE** | ~1.34°C |

---

## 🚀 How to Run (Google Colab)

### Step 1 — Open the Notebook

**Option A — Upload manually:**
1. Go to [colab.research.google.com](https://colab.research.google.com)
2. Click **File → Upload notebook**
3. Select `Delhi_Climate_Forecasting_FINAL_V2.ipynb`

**Option B — Open from Google Drive:**
1. Upload the `.ipynb` file to Google Drive
2. Right-click → **Open with → Google Colaboratory**

### Step 2 — No Setup Required ✅

> All required libraries (**NumPy, Pandas, Matplotlib, Scikit-learn**) come pre-installed in Colab.
> The dataset is **automatically downloaded from GitHub** — no manual download needed.
> Just ensure you have an **active internet connection**.

### Step 3 — Run All Cells

```
Runtime → Run all   (or press Ctrl + F9)
```
Or execute cells one-by-one with `Shift + Enter`.

### Step 4 — Download Output Plots (Optional)

| Plot File | Description |
|---|---|
| `eda_all_features.png` | Time-series plots for all climate variables |
| `feature_importance.png` | Top features ranked by model importance |

To download: click the **📁 folder icon** in the sidebar → right-click file → **Download**

---

## 🔬 What the Notebook Does — Step by Step

<details>
<summary><b>Step 1 — Data Loading & Cleaning</b></summary>

- Loads dataset directly from GitHub
- Corrects physically invalid pressure values
- Handles missing dates via time-based interpolation
</details>

<details>
<summary><b>Step 2 — Exploratory Data Analysis (EDA)</b></summary>

- Time-series plots revealing seasonal temperature patterns
- Variation analysis across humidity, wind speed, and pressure
- Feature correlation analysis to identify influential variables
</details>

<details>
<summary><b>Step 3 — Feature Engineering (31 Features)</b></summary>

| Category | Features |
|---|---|
| 🕐 Temporal | Day of year, month, year, day of week, week of year |
| 🌊 Fourier | 4 sine/cosine pairs for annual seasonality |
| 🌡️ Temperature Lags | Lag 1, 2, 3, 7, 14, 30, 365 days |
| 📈 Rolling Statistics | 7-day & 30-day rolling mean and std |
| 💨 Exogenous Lags | Humidity, wind speed, pressure (lag 1 & 7) |
</details>

<details>
<summary><b>Step 4 — Model Training & Comparison</b></summary>

Three models trained and compared against a **Seasonal Naïve baseline**:
- ✅ **Ridge Regression** ← Best performer
- 🌲 Random Forest Regressor
- 📈 Gradient Boosting Regressor
</details>

<details>
<summary><b>Step 5 — Time-Series Cross-Validation</b></summary>

- 5-fold time-series CV (temporal order preserved, no data leakage)
- Stable folds achieve: MAE ≈ 1.46, RMSE ≈ 1.87, R² ≈ 0.93
</details>

<details>
<summary><b>Step 6 — Feature Importance Analysis</b></summary>

- Top 15 most influential features identified
- Temperature lag features (recent days) rank highest
- Fourier/seasonal features and rolling stats also contribute
</details>

<details>
<summary><b>Steps 7–11 — Evaluation & Error Analysis</b></summary>

- Predictions table: actual vs predicted for all 114 test days
- Actual vs Predicted visualization with residual plot
- Monthly MAE/RMSE trends and error distribution
- Individual test case analysis across seasonal phases
</details>

---

## 📊 Final Results

| Metric | Score |
|---|---|
| **MAE** | ~1.3 – 1.8°C |
| **RMSE** | ~1.7 – 2.2°C |
| **R²** | ~0.90 – 0.94 |
| **MAPE** | ~5 – 8% |
| **Bias** | -0.022°C (negligible) |

### ✅ Practical Accuracy
- **73%** of predictions fall within **±2°C**
- **92%** of predictions fall within **±3°C**
- **~49% reduction** in MAE & RMSE vs Seasonal Naïve baseline

---

## 🗂️ Dataset Source

- **Kaggle:** [Daily Climate Time Series Data (Delhi)](https://www.kaggle.com/datasets/sumanthvrao/daily-climate-time-series-data)
- **GitHub (auto-loaded in notebook):** [KatariyaMohit/Daily-Climate-time-series-forecasting](https://github.com/KatariyaMohit/Daily-Climate-time-series-forecasting)

> The notebook automatically retrieves the dataset from GitHub. No manual download required.

---

## 🛠️ Tech Stack

```
Python 3  |  NumPy  |  Pandas  |  Matplotlib  |  Scikit-learn  |  Google Colab
```

---

<p align="center">Made with ☀️ for short-term climate forecasting</p>
