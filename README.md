# Daily Climate Forecasting — ML Solution
## README / Project Documentation

---

## PROJECT OVERVIEW

This project focuses on predicting the mean daily temperature (°C) for Delhi using machine learning techniques applied to the Kaggle Daily Climate Time Series dataset (2013–2017).

- **Dataset:** Kaggle — Daily Climate Time Series (Delhi)
- **Target Variable:** Mean daily temperature (°C)
- **Test Period:** January – April 2017 (114 days)
- **Platform:** Google Colab
- **Programming Language:** Python 3

---

## HOW TO RUN ON GOOGLE COLAB

### Step 1 — Open the Notebook in Colab

**Option A: Upload manually**
- Go to: https://colab.research.google.com
- Click File → Upload notebook
- Select `Code.ipynb` from your computer

**Option B: Open from Google Drive**
- Upload the `.ipynb` file to Google Drive
- Right-click the file → Open with → Google Colaboratory

---

### Step 2 — No Setup Required

- All required libraries (NumPy, Pandas, Matplotlib, Scikit-learn) are pre-installed in Google Colab.
- No additional installation (`pip install`) is needed.
- The dataset is automatically downloaded from GitHub within the notebook.
- No manual data download is required.
- Ensure you have an active internet connection.

---

### Step 3 — Run All Cells

- Go to **Runtime → Run all** (or press `Ctrl + F9`)
- Alternatively, execute each cell using `Shift + Enter`

The notebook will automatically execute all steps and display:
- Results
- Visualizations
- Final performance summary

---

### Step 4 — Save Output Plots (Optional)

The following plots are generated:

- `eda_all_features.png` — Time-series plots for all climate variables
- `feature_importance.png` — Top features ranked by model importance

To download:
- Click the folder icon (📁) in the left sidebar
- Right-click the file → Download

---

## WHAT THE NOTEBOOK DOES — STEP BY STEP

### Step 1 — Data Loading & Cleaning

The dataset is loaded from GitHub and prepared for analysis.

The data cleaning process includes correcting physically invalid pressure values and handling missing dates using time-based interpolation.

These preprocessing steps ensure data consistency and improve the reliability of the model.

---

### Step 2 — Exploratory Data Analysis (EDA)

This step analyzes the dataset to understand trends and relationships between different climate variables.

The time-series plots show clear seasonal patterns in temperature, along with variations in humidity, wind speed, and pressure over time.

Feature correlation analysis is performed to identify relationships between variables and their influence on temperature.

---

### Step 3 — Feature Engineering

A total of **31 features** are created across five categories to capture temporal patterns and improve prediction accuracy:

- **Temporal Features**
  Day of year, month, year, day of week, week of year

- **Fourier Features**
  4 sine/cosine pairs to capture annual seasonality

- **Temperature Lag Features**
  Lag values: 1, 2, 3, 7, 14, 30, 365 days

- **Rolling Statistics**
  7-day and 30-day rolling mean and standard deviation

- **Exogenous Lag Features**
  Humidity, wind speed, and pressure (lag 1 & 7)

These features help the model capture time dependencies, seasonal patterns, and external influences on temperature.

---

### Step 4 — Model Training & Comparison

Three machine learning models are trained and compared against a Seasonal Naïve baseline:

- Gradient Boosting Regressor
- Random Forest Regressor
- Ridge Regression

The models are evaluated using MAE, RMSE, R², and MAPE on the test dataset.

The results show that **Ridge Regression** performs the best among all models, achieving the lowest error and highest overall performance based on RMSE. Gradient Boosting and Random Forest also provide competitive results but are slightly less accurate in comparison.

Overall, machine learning models significantly outperform the Seasonal Naïve baseline, demonstrating their ability to capture temporal patterns and improve prediction accuracy.

The best-performing model selected for further analysis is **Ridge Regression**.

---

### Step 5 — Time-Series Cross-Validation

This step uses **5-fold time-series cross-validation** to evaluate model performance while preserving temporal order and preventing data leakage.

The results show that the first fold has higher error due to a smaller training window, which is expected in time-series modeling. From subsequent folds, the performance stabilizes, indicating consistent learning.

Across the stable folds, the model achieves:
- MAE ≈ 1.46
- RMSE ≈ 1.87
- R² ≈ 0.93

The final test MAE (~1.34) is consistent with cross-validation results, suggesting that the model generalizes well without overfitting.

---

### Step 6 — Feature Importance Analysis

This step identifies the **top 15 most influential features** contributing to the model's predictions.

The results show that temperature lag features (especially recent days) have the highest importance, indicating strong temporal dependency in the data. Seasonal components (such as Fourier features) and rolling statistics also contribute to the model's performance, while exogenous variables like humidity and pressure have relatively lower impact.

---

### Step 7 — Predictions Table

This table presents the actual and predicted temperature values for all 114 test days.

It allows a direct comparison between model predictions and true values, along with the corresponding error and absolute error for each day.

The table helps identify patterns in prediction accuracy and highlights cases with higher errors.

---

### Step 8 — Actual vs Predicted Visualization

The plot shows a comparison between actual and predicted temperature values over the test period.

The predicted values closely follow the overall trend of the actual temperatures, indicating that the model captures the underlying patterns effectively.

The residual plot shows that most errors are small and centered around zero, suggesting that the model does not have significant bias and performs consistently across time.

---

### Step 9 — Error Analysis

The error analysis provides insights into model performance across different conditions and evaluates its practical usability.

The model achieves consistent performance across time, as reflected in the monthly MAE and RMSE trends, along with a stable error distribution.

**Practical Accuracy:**
- 73% of predictions fall within ±2°C of actual temperature values
- 92% of predictions fall within ±3°C of actual temperature values
- Bias (mean residual): -0.022°C, indicating negligible systematic error

---

### Step 10 — Individual Test Case Analysis

This section evaluates model performance on selected dates across different seasonal conditions to assess robustness and generalization.

The model predictions for the selected test cases are summarized as follows:

- **2017-01-15 (Mid-winter):**
  The model underestimates the temperature by 3.29°C, resulting in an accuracy of 80.0%. This is the highest error among the selected cases, likely due to limited training data in the early phase of the time series.

- **2017-02-01 (Late winter):**
  The prediction is very close to the actual value, with an error of only 0.92°C and an accuracy of 94.0%, indicating improved performance as more training data becomes available.

- **2017-02-20 (Pre-spring):**
  The model maintains good accuracy (94.3%) with a small error of 1.32°C, showing stable performance during seasonal transition.

- **2017-03-15 (Spring):**
  The prediction error is minimal (0.73°C) with a high accuracy of 96.3%, demonstrating strong model performance under moderate temperature conditions.

- **2017-04-10 (Pre-summer):**
  The model achieves excellent accuracy (99.3%) with a negligible error of 0.20°C, indicating highly reliable predictions in later periods.

Overall, the average absolute error across the five test cases is approximately **1.29°C**. The model shows improved accuracy as more training data becomes available and performs consistently well across different seasonal phases, demonstrating strong generalization capability.

---

### Step 11 — Final Performance Summary

The final model performance demonstrates strong predictive capability for daily temperature forecasting.

The best-performing model is **Ridge Regression**, evaluated on the test period (January–April 2017).

The model achieves:
- MAE of **1.34°C**
- RMSE of **1.66°C**
- R² score of **0.93**, indicating that approximately 93% of the variance is explained
- MAPE of **6.82%**

Compared to the Seasonal Naïve baseline, the model shows significant improvement, reducing both MAE and RMSE by approximately **49%**.

The model also demonstrates strong practical accuracy, with most predictions falling within ±2–3°C of actual values.

Cross-validation results further confirm model stability, with consistent performance across folds (MAE ≈ 1.46, RMSE ≈ 1.87, R² ≈ 0.92), indicating good generalization and no overfitting.

Overall, the model provides reliable and accurate temperature predictions, making it suitable for short-term climate forecasting applications.

---

## FINAL RESULTS

**Best Performing Model: Ridge Regression**

- **MAE** (Mean Absolute Error): ~1.3 – 1.8 °C
- **RMSE** (Root Mean Squared Error): ~1.7 – 2.2 °C
- **R²** (Coefficient of Determination): ~0.90 – 0.94
- **MAPE** (Mean Absolute Percentage Error): ~5 – 8%

A large majority of predictions fall within ±2°C of actual temperature values.

---

## DATASET SOURCE

**Kaggle — Daily Climate Time Series Data (Delhi)**
https://www.kaggle.com/datasets/sumanthvrao/daily-climate-time-series-data

- The notebook automatically retrieves the dataset from the author's GitHub repository.
- No manual download is required.

**GitHub Source:**
https://github.com/KatariyaMohit/Daily-Climate-time-series-forecasting
