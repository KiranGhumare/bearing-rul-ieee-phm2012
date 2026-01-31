# 📦 Bearing Remaining Useful Life (RUL) Prediction  
### IEEE PHM 2012 Prognostics Dataset

This repository presents a complete **feature-based prognostics pipeline** for predicting the Remaining Useful Life (RUL) of rolling element bearings using the **IEEE PHM 2012 Ball Bearing Dataset**.

The project focuses on **signal processing, health indicator construction, and degradation modeling**, with strong emphasis on interpretability, data correctness, and realistic evaluation — making it suitable for predictive maintenance and industrial reliability applications.

---

## 🚀 Project Highlights

- End-to-end RUL prediction pipeline from raw vibration signals
- Extensive time-domain feature extraction
- Feature selection based on degradation behavior
- PCA-based Health Indicator (HI) construction
- HI smoothing and monotonicity analysis
- Polynomial degradation modeling for RUL estimation
- Realistic test evaluation using partial life observation (25%, 50%, 75%)
- Careful handling of timestamp inconsistencies and data leakage

---


---

## 🧠 Problem Statement

Rolling bearings are critical components in rotating machinery. Unexpected bearing failures can lead to costly downtime and safety risks.

The objective of this project is to **estimate the Remaining Useful Life (RUL)** of bearings using vibration measurements, enabling **predictive maintenance** before catastrophic failure occurs.

---

## ⚙️ Methodology

### 1️⃣ Feature Extraction

Time-domain vibration features are extracted from horizontal and vertical acceleration signals, including:

- RMS
- Variance
- Crest Factor
- Impulse Factor
- Clearance Factor
- Kurtosis Factor
- Statistical moments

Each feature is computed over fixed time windows and stored in structured CSV files.

---

### 2️⃣ Feature Selection

Based on trend analysis and degradation sensitivity, the following features were selected for Health Indicator construction:

rms_ver
variance_ver
crest_factor_ver
impulse_factor_ver
clearance_factor_ver
kurtosis_factor_ver


Vertical vibration features were found to be more informative for fault progression.

---

### 3️⃣ Health Indicator (HI) Construction

A **Principal Component Analysis (PCA)** approach is used to combine selected features into a single scalar Health Indicator.

- Features are normalized using Min-Max scaling
- First principal component is used as the HI
- HI is smoothed using a rolling mean to reduce noise

The resulting HI shows clear degradation behavior as the bearing approaches failure.

---

### 4️⃣ Degradation Modeling & RUL Estimation

Bearing degradation is modeled by fitting a **polynomial trend** to the Health Indicator:

- Polynomial fitting is performed using only observed data
- A failure threshold is defined based on end-of-life HI values
- Failure time is estimated from the trend intersection
- RUL is computed as the difference between estimated failure time and current time

---

### 5️⃣ Evaluation Strategy

To simulate real-world prognostics scenarios, test bearings are evaluated at partial life stages:

- **25% of life**
- **50% of life**
- **75% of life**

At each stage:
- Only data up to that point is used
- No future information is leaked
- RUL predictions are compared against ground truth

This setup reflects early-warning and mid-life prediction use cases.

---

## 📊 Results & Observations

- Health Indicator exhibits stable behavior in early life and accelerates near failure
- Polynomial trend captures the general degradation trajectory
- RUL predictions improve as more operational data becomes available
- Data quality issues (timestamp resets, sensor spikes) significantly impact HI construction and must be handled carefully

---

## 🧪 How to Run

### 1️⃣ Install Dependencies

```bash
pip install -r requirements.txt
```
