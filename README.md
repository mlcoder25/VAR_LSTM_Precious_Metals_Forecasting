# 📈 Multivariate Precious Metals Forecasting  
### VAR, LSTM & Hybrid Residual Learning

## 📌 Project Overview
This project implements a **real-world multivariate time-series forecasting pipeline** to predict prices of precious metals using:

- **Vector Autoregression (VAR)** — statistical baseline
- **Multivariate LSTM** — deep learning model
- **Hybrid VAR + LSTM (Residual Learning)** — combined approach

The objective is to evaluate whether combining **classical econometric models** with **deep learning** improves forecasting accuracy for correlated financial assets.

---

## 🎯 Problem Statement
**Can we improve precious metals price forecasting by combining linear multivariate time-series models with non-linear neural networks?**

Accurate commodity price forecasting is critical for:
- Investment decision-making  
- Risk management  
- Portfolio allocation  
- Financial planning  

---

## 📂 Dataset
Two CSV files are used:

1. **Historical Prices**
   - Daily historical prices of precious metals
   - Key columns:
     - `Silver_Price`
     - `Gold_Price`
     - `Platinum_Price`

2. **Extended / Feature Dataset**
   - Additional engineered features and future rows

⚠️ **Data Leakage Prevention:**  
Only rows containing **true historical prices** are used for training and evaluation.

---

## 🧠 Methodology

### 1️⃣ Data Preprocessing
- Robust date parsing and merging
- Safe numeric conversion (handles commas, currency symbols, spaces)
- Forward-fill and backward-fill for missing values
- Time-based train/test split (last 20% as test)

---

### 2️⃣ Stationarity & Transformations
- Augmented Dickey-Fuller (ADF) test
- Optional log transformation (for strictly positive prices)
- First-order differencing for VAR compatibility
- Inverse transformations applied after forecasting

---

### 3️⃣ VAR (Vector Autoregression)
- Captures **linear interdependencies** between multiple metal prices
- Lag order selected using **AIC**
- Provides an interpretable statistical baseline

---

### 4️⃣ Multivariate LSTM
- Learns **non-linear temporal patterns**
- Sliding window sequence modeling
- Standardized inputs
- Regularization techniques:
  - Dropout
  - Early stopping
  - Learning rate reduction

---

### 5️⃣ Hybrid VAR + LSTM (Residual Learning)
**Core idea:**
- VAR models linear structure
- LSTM models remaining non-linear residuals

**Process:**
1. Train VAR on differenced series
2. Compute residuals:  
   `residual = actual − VAR_prediction`
3. Train LSTM on residuals
4. Final forecast:  
   `Hybrid = VAR_forecast + LSTM_residual_forecast`

This hybrid strategy reflects **industry-grade forecasting approaches** used in quantitative finance.

---

## 📏 Evaluation Metrics
Models are evaluated on the **original price scale** using:

- **MAE** — Mean Absolute Error  
- **RMSE** — Root Mean Squared Error  
- **MAPE** — Mean Absolute Percentage Error  

---

## 📊 Results Summary
| Model | Key Characteristics |
|-----|--------------------|
| VAR | Stable, interpretable linear baseline |
| LSTM | Captures non-linear trends and volatility |
| VAR + LSTM (Hybrid) | Best overall performance in most cases |

**Observation:**  
The hybrid model generally reduces error during volatile periods, demonstrating the benefit of combining statistical and deep learning methods.

---

## 🧪 Reproducibility
- Random seeds fixed
- Version-agnostic evaluation logic
- Recommended execution order:
