# Patient Mobility Forecasting using Time Series and Clinical Data

The objective of this project is to forecast daily patient step counts by integrating high-frequency mobility data with longitudinal clinical information, while maintaining interpretability of the model predictions.

---

## 1. Problem Statement

Patient mobility, measured through daily step counts, is an important indicator of health, recovery, and overall well-being.  
However, raw mobility data is collected at very high frequency and is influenced by several clinical factors such as therapies, side effects, and medical events.

The goal of this project is to:
- Aggregate raw step-count data into meaningful daily metrics
- Integrate clinical data with mobility data on a unified timeline
- Forecast daily step counts for the next **365 days**
- Explain how health-related factors impact patient activity

---

## 2. Dataset Description

This project uses two JSON datasets:

### a) Time Series Data (`timeseries-data.json`)
- Contains high-frequency step-count intervals collected from mobile devices
- Each record includes step count and start/end timestamps
- This data is aggregated into **daily step counts**

### b) Clinical Data (`categorical-data.json`)
- Contains patient demographic information (gender, birth year, disease)
- Includes interval-based clinical events such as:
  - Therapies
  - Side effects with intensity levels
  - Other medical events

---

## 3. Data Preprocessing and Feature Engineering

The following preprocessing steps were performed:

- Converted all timestamps into Python datetime format
- Standardized timezone handling to avoid comparison issues
- Aggregated granular step data into daily totals
- Created a continuous daily timeline with no missing dates

### Engineered Features
- **Static features:** age, gender
- **Therapy features:** daily binary indicators for active therapies
- **Side effect features:** 
  - Number of active side effects per day
  - Maximum side-effect intensity per day
- **Time-series features:**
  - Day of week
  - Week of year
  - Lag features (t-1, t-7, t-30)

---

## 4. Modeling Approach

### Baseline Model
A **SARIMA** (Seasonal ARIMA) model was used as a baseline:
- Uses only historical daily step counts
- Captures trend and weekly seasonality
- Provides a benchmark for comparison

### Machine Learning Model
An **Explainable Boosting Machine (EBM)** was used as the primary model:
- Uses both time-series and clinical features
- Provides strong predictive performance
- Offers built-in explainability, which is important for healthcare applications

---

## 5. Model Evaluation

Models were evaluated using:
- **RMSE (Root Mean Squared Error)**
- **MAE (Mean Absolute Error)**

The dataset was split using a time-based approach:
- Training data: historical records
- Test data: last 365 days

The multivariate ML model outperformed the baseline model.

---

## 6. Explainability

To understand model behavior, global explainability techniques were applied using EBM:
- Lagged step counts were the strongest predictors
- Therapy periods were generally associated with increased activity
- Side effects and clinical events were linked to reduced mobility

This helped validate that the model learned meaningful, real-world patterns.

---

## 7. Forecast Output

The final output is a 365-day forecast with the following structure:
- Date
- Predicted step count
- Baseline trend component
- Exogenous (clinical) impact

This format makes the predictions easy to interpret and integrate into downstream systems.

---

## 8. Scalability Considerations

A scalable design was proposed to support up to 100,000 patients:
- Cloud-based data storage (Amazon S3)
- Distributed data processing using Spark
- Global modeling strategy with normalization
- Batch prediction pipelines for large-scale inference

Details are provided in the Scalability Document.

---

## 9. Technologies Used

- Python
- Pandas, NumPy
- Scikit-learn
- Statsmodels (SARIMA)
- InterpretML (Explainable Boosting Machine)
- Google Colab

---

## 10. Repository Structure

- `Liberdat_Assignment_Anushikagupta.ipynb` – Main implementation notebook
- `Scalability_Document_Liberdat.pdf` – Scalability and architecture design
- `Supporting_Document_Liberdat.pdf` – Project explanation, challenges, and learnings
- `README.md` – Project documentation

---

## 11. Author

**Anushika Gupta**  

