# **Assignment 2: Time Series Analysis**

## **Overview**
This project explores the **Metro Interstate Traffic Volume** dataset to analyze traffic patterns using univariate and multivariate time-series modeling. The goal is to forecast future traffic volumes and gain insights into seasonal and trend-based variations. The project includes exploratory data analysis, ARIMA and SARIMA modeling for univariate time series, and VAR modeling for multivariate time series forecasting.

---

## **Table of Contents**
1. [Introduction](#introduction)  
   - 1.1 [Dataset Description](#dataset-description)  
   - 1.2 [Objectives](#objectives)  

2. [Task 1: Time Series Exploration](#task-1-time-series-exploration)  
   - 2.1 [Data Cleaning & Encoding](#data-cleaning--encoding)  
   - 2.2 [Descriptive Statistics & Visualization](#descriptive-statistics--visualization)  
   - 2.3 [Time Series Decomposition](#time-series-decomposition)  
   - 2.4 [Stationarity Check](#stationarity-check)  

3. [Task 2: Univariate Time-Series Models](#task-2-univariate-time-series-models)  
   - 3.1 [ARIMA Model](#arima-model)  
   - 3.2 [SARIMA Model](#sarima-model)  
   - 3.3 [Forecasting & Model Comparison](#forecasting--model-comparison)  

4. [Task 3: Multivariate Time-Series Models](#task-3-multivariate-time-series-models)  
   - 4.1 [Vector Autoregression (VAR) Model](#vector-autoregression-var-model)  
   - 4.2 [AIC & BIC Model Selection](#aic--bic-model-selection)  
   - 4.3 [VAR Forecasting](#var-forecasting)  

5. [Comparison of Univariate & Multivariate Models](#comparison-of-univariate--multivariate-models)  

6. [Procedure to Run](#procedure-to-run)  

---

## **Introduction**

### **Dataset Description**
The **Metro Interstate Traffic Volume** dataset includes **48,204** observations with **9** key variables:
- **date_time** (timestamp)
- **traffic_volume** (number of vehicles)
- **weather_main, weather_description** (weather conditions)
- **holiday** (whether the date is a holiday)
- **temp, rain_1h, snow_1h, clouds_all** (weather-related attributes)

The dataset records hourly traffic volume on Interstate I-94, covering multiple years.

### **Objectives**
- Explore traffic volume trends and seasonality.
- Build **univariate time-series models** (ARIMA, SARIMA) to forecast traffic.
- Develop a **multivariate time-series model** (VAR) incorporating weather and holidays.
- Compare **forecasting performance** of univariate vs. multivariate models.

---

## **Task 1: Time Series Exploration**

### **Data Cleaning & Encoding**
- Converted `date_time` to **POSIXct** format for time-based operations.
- Encoded categorical variables (e.g., `holiday`, `weather_main`) into numeric factors.
- Checked and removed any missing values to ensure data integrity.

### **Descriptive Statistics & Visualization**
- **Summary statistics**:
  - **Traffic volume ranges** from **0 to 7,280**.
  - Median: **3,380**, Mean: **3,260** (indicating slight skewness).
- **Time-series visualization**:
  - Traffic volume **fluctuates cyclically**.
  - Gaps in data (e.g., **mid-2014 to mid-2015**) indicate missing periods.

### **Time Series Decomposition**
- Applied **STL decomposition**:
  - **Trend**: Captures long-term variations in traffic volume.
  - **Seasonality**: Identifies daily/weekly cycles.
  - **Residuals**: Unexplained noise in the data.

### **Stationarity Check**
- **Augmented Dickey-Fuller (ADF) test**:
  - **p-value < 0.01** → Rejects null hypothesis → **Data is stationary**.
- **Autocorrelation Function (ACF) & Partial ACF (PACF) plots**:
  - Significant **autocorrelation at lag 1** suggests the need for differencing.

---

## **Task 2: Univariate Time-Series Models**

### **ARIMA Model**
- **Best ARIMA model selected**: **ARIMA(5,1,2)**
- **Evaluation metrics**:
  - **MSE = 138252284**
  - **R² = 0.0187**
- **Residual analysis** shows minimal autocorrelation, confirming a good fit.

### **SARIMA Model**
- **Best SARIMA model selected**: **ARIMA(2,1,3)(1,0,2)[24] with drift**
- **Evaluation metrics**:
  - **MSE = 132155**
  - **AIC = 932327.1 (lower than ARIMA)**
- Captures both **seasonality** and **trend components** better than ARIMA.

### **Forecasting & Model Comparison**
- **ARIMA forecast** shows **steady increase** in traffic volume but lacks seasonality.
- **SARIMA forecast** captures **cyclical fluctuations** better.
- **SARIMA outperforms ARIMA** based on **AIC and RMSE**.

---

## **Task 3: Multivariate Time-Series Models**

### **Vector Autoregression (VAR) Model**
- Selected **4 key predictors**:
  - **Traffic Volume, Temperature, Holiday, Weather Condition**
- Preprocessed missing values using **interpolation**.

### **AIC & BIC Model Selection**
- **VAR(2) selected** based on lowest **AIC = 25805.35** and **BIC = 26071.52**.
- Lag **2** captures short-term dependencies in traffic volume effectively.

### **VAR Forecasting**
- **24-hour forecast** shows:
  - **Peak traffic between 9 AM – 12 PM** (morning rush hour).
  - **Gradual decline in afternoon/evening**.
- **Better fit than univariate models** due to inclusion of multiple influencing factors.

---

## **Comparison of Univariate & Multivariate Models**
| Model  | AIC Score | Forecast Accuracy | Seasonality Capture | Complexity |
|--------|-----------|------------------|---------------------|------------|
| **ARIMA(5,1,2)** | 935211.45 | Moderate | ❌ Poor | Low |
| **SARIMA(2,1,3)(1,0,2)[24]** | **932327.1** | **Good** | ✅ Strong | Medium |
| **VAR(2)** | **25805.35** | **Best** | ✅ Captures External Factors | High |

- **SARIMA performs better than ARIMA** by capturing seasonal trends.
- **VAR model significantly outperforms both**, incorporating external factors (weather, holidays).

---

## **Procedure to Run**
1. **Modify CSV path**:
   - Update the file path **twice** (Task 1 & Task 3).
2. **Run the script**:
   - **Execution time:** ~2-3 minutes (large dataset).
3. **Generate Knit file**:
   - **Output will be produced automatically**.

> ⚠ **Note:** A full dataset run (without sampling) takes **15-20 minutes**.

---

## **Key Findings & Conclusion**
✔ **Traffic volume exhibits strong seasonality and trend components.**  
✔ **SARIMA outperforms ARIMA in capturing seasonal fluctuations.**  
✔ **Multivariate VAR model is the best choice**, integrating external predictors (weather, holidays).  
✔ **Forecasting shows peak morning traffic (9 AM - 12 PM) and lower evening traffic.**  

This analysis provides **actionable insights** for traffic forecasting and urban planning.

---

## **Author**
This project was implemented by **[Your Name]** as part of **Assignment 2: Time Series Analysis**.

---

## **License**
This project is licensed under the **MIT License**.
