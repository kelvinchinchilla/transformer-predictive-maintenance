# Transformer Predictive Maintenance: Anomaly Detection Analysis

**Author:** Kelvin Chinchilla
**Date:** October 23, 2025

---

## 1. Project Summary

This project demonstrates an end-to-end workflow for analyzing electrical transformer monitoring data to identify operational anomalies, serving as a foundation for predictive maintenance strategies. Using time-series data from Kaggle's "Distributed Transformer Monitoring" dataset, this analysis focuses on data cleaning, exploratory visualization, and applying unsupervised machine learning for anomaly detection. The goal is to identify deviations from normal operating behavior that could indicate potential faults or maintenance needs.

---

## 2. Data Source & Preparation

* **Dataset:** Kaggle's "Distributed Transformer Monitoring" dataset, containing time-series readings (Power, Voltage, Current, Power Factor) from multiple sensors.
* **Tools:** Python, Pandas
* **Process:**
    * Loaded data from multiple CSV files (`Power.csv`, `CurrentVoltage.csv`, `PowerFactor.csv`).
    * **Cleaned and standardized** column names for programmatic access.
    * Converted timestamp columns to a **`datetime` index**, enabling time-series analysis.
    * **Merged** disparate data sources into a single, comprehensive DataFrame aligned by timestamp.
    * Handled potential inconsistencies and verified data integrity using `.info()` and `.describe()`.

---

## 3. Exploratory Data Analysis (EDA) & Visualization

* **Tools:** Matplotlib, Pandas
* **Key Findings:**
    * Visual analysis of key variables (`WL1`, `VL1`, `PFL1`) revealed distinct operational patterns and **identified periods of interest**, such as intervals with zero power (`WL1`) despite stable voltage (`VL1`).
    * Analysis of Power Factor (`PFL1`) indicated generally efficient operation (PF close to 1.0) during high load periods but potentially unreliable readings during near-zero power flow.
    * Identified a specific period (late Feb/early Mar 2020) with a noticeable dip in Power Factor, prompting further investigation.


    ![Power vs Power Factor Plot] (power_vrs_power_factor_plot.png)
    

---

## 4. Anomaly Detection using Machine Learning

* **Goal:** Automatically identify statistically significant deviations from normal operating conditions.
* **Model:** Scikit-learn's **`IsolationForest`**, an unsupervised algorithm effective for identifying outliers in multivariate data.
* **Features Used:** `WL1` (Power), `VL1` (Voltage), `PFL1` (Power Factor).
* **Process:**
    * Trained the `IsolationForest` model on the combined dataset.
    * Initially observed high sensitivity; **tuned the `contamination` hyperparameter** (e.g., to `0.01`) to refine detection and focus on more significant anomalies.
    * Visualized the detected anomalies (marked points) overlaid on the `WL1` time-series plot.
    * Performed **contextual analysis** by zooming into specific time windows to correlate flagged anomalies with the behavior of other variables (`VL1`, `PFL1`), aiding interpretation.

---

## 5. Conclusion & Key Skills Demonstrated

This project successfully applied data science techniques to raw transformer monitoring data to extract actionable insights relevant to predictive maintenance. While the `IsolationForest` flagged statistically unusual points, the analysis emphasized the need for **engineering context** to interpret whether these anomalies represent critical issues.

**Skills Demonstrated:**
* **Data Wrangling:** Handling multiple data sources, cleaning time-series data, merging datasets (Pandas).
* **Exploratory Data Analysis (EDA):** Time-series visualization, pattern identification (Matplotlib).
* **Machine Learning:** Unsupervised Anomaly Detection (`IsolationForest`), hyperparameter tuning, model interpretation (Scikit-learn).
* **Domain Application:** Applying data science to a core electrical engineering problem (Transformer Monitoring / Predictive Maintenance).
* **Problem Solving:** Iteratively refining the analysis based on results (adjusting model sensitivity, contextual investigation).
