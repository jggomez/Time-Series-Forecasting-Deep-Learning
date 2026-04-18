# Time Series Forecasting Deep Learning

## **Authors:**
- Alejandra Valle Fernandez
- [Juan Guillermo Gómez](https://www.linkedin.com/in/jggomezt/)

## Notebook

- [Notebook Link](https://colab.research.google.com/drive/11okJNvpVdrMaUCeFV2JvLmhKk9n9LAoU?usp=sharing)

## **1. Project Overview**

This project aims to implement a time series model to forecast daily PM2.5 levels in Bogotá for the next 7 days. PM2.5 was chosen due to its direct impact on public health and its strong correlation with the Air Quality Index (AQI). The analysis covers data selection, exploratory data analysis, stationarity transformations, autocorrelation analysis, and baseline model validation.

## **2. Dataset Selection and Characterization**

**Latin America Weather and Air Quality Data**

- **Source**: Kaggle (https://www.kaggle.com/datasets/anycaroliny/latin-america-weather-and-air-quality-data)
- **Content**: Two CSV files from the Open-Meteo API with weather and air quality data for various Latin American cities.
- **Frequency**: Daily data.
- **Parameters**: Country/city names, latitude/longitude, PM10, PM2.5, Carbon monoxide, Nitrogen dioxide, Sulphur dioxide, Ozone levels.

### **Key Characteristics (Bogotá PM2.5)**

| Characteristic | Description |
|---|---|
| Frequency | Daily |
| Main Variable | PM2.5 Concentration (µg/m³) |
| Observation Period | Continuous (August 2022 - April 2024), no missing data |
| Data Quality | No null values, few outliers after capping |

## **3. Phase 1 Objectives**

Upon completion of this phase, the student will demonstrate the ability to:

*   Conduct a comprehensive exploratory analysis of time series.
*   Identify fundamental patterns (trend, seasonality, cycles).
*   Apply transformations to achieve stationarity.
*   Implement and validate reference models.
*   Establish benchmark metrics for future phases.

## **4. Exploratory Data Analysis (EDA)**

### **Summary Statistics for PM2.5 (Bogotá)**

| Statistic | Value |
|---|---|
| Count | 626.00 |
| Mean | 21.55 µg/m³ |
| Std Dev | 9.06 µg/m³ |
| Min | 0.70 µg/m³ |
| 25% | 14.85 µg/m³ |
| 50% (Median)| 20.10 µg/m³ |
| 75% | 27.58 µg/m³ |
| Max (Capped)| 46.66 µg/m³ |
| Skewness | 0.61 (Right-skewed) |
| Kurtosis | 0.00 (Mesokurtic) |
| CV | 42.07% (Significant variability)|

## 5. The Solution
The project followed a structured approach:
- **Data Acquisition**: Using Latin America Weather and Air Quality data (Open-Meteo API).
- **Preprocessing**: Handling outliers via IQR capping and achieving stationarity using **Logarithmic Transformation + Differencing**.
- **Modeling Strategy**:
    - **Baselines**: Naive, Seasonal Naive, SMA, and Drift models.
    - **Deep Learning**: Conv1D (Temporal feature extraction), RNN-LSTM (Sequential dependency modeling), and Transformers (Self-attention mechanism).
- **Validation**: Temporal Cross-Validation and residual analysis to ensure model robustness.

## 6. Results
Through extensive testing, the following performance metrics were observed:
- **Baseline Winner**: The Drift model combined with Log-Differencing showed the best performance among classical methods.
- **Deep Learning Comparison**: 
    - **RNN (LSTM)**: Achieved the lowest error metrics (RMSE ~0.19, MAE ~0.16 in standardized scale), proving most effective for sequential air quality data.
    - **Conv1D**: Followed closely, offering a balance between computational efficiency and accuracy.
    - **Transformer**: Showed higher variance and underfitting, likely due to the limited dataset size relative to the model's complexity.
 
## 7. Architectures and Weights

### **Conv1D Network**

<img width="705" height="340" alt="Conv1d-DL drawio" src="https://github.com/user-attachments/assets/05d34bd9-0c76-4d5c-8649-b91ebfbbb71e" />

### **RNN (LSTM)**

<img width="531" height="267" alt="time-series-rnn drawio" src="https://github.com/user-attachments/assets/4a31133d-b85f-4744-b145-07beee4e54eb" />

### **Transformer**

<img width="2572" height="822" alt="red-transformers drawio" src="https://github.com/user-attachments/assets/c8a3b3ee-ed47-4e28-a003-19f28048d30c" />


## 8. Conclusions
- **Sequential Modeling**: RNNs remain superior for medium-sized environmental time series due to their ability to retain long-term dependencies.
- **Stationarity**: Variance stabilization (Log) and trend removal (Diff) are non-negotiable steps for accurate forecasting.
- **The Data Gap**: While Deep Learning models are powerful, the "performance ceiling" observed suggests that future improvements require incorporating **exogenous variables** (like wind speed, humidity, or traffic data) rather than just increasing model depth.

<img width="1000" height="700" alt="newplot" src="https://github.com/user-attachments/assets/de440a5a-acd0-4f25-8c38-1be25377cc3a" />

## 9. References
- **Conv1D for Time Series**: LeCun, Y., et al. "Convolutional networks for images, speech, and time series."
- **RNN/LSTM**: Hochreiter, S., & Schmidhuber, J. "Long Short-Term Memory." Neural Computation.
- **Transformers**: Vaswani, A., et al. "Attention is All You Need." (NIPS 2017).
- **Time Series Analysis**: Hyndman, R.J., & Athanasopoulos, G. "Forecasting: Principles and Practice."
