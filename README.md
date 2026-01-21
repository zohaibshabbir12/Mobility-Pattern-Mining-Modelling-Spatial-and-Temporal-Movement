## Mobility Pattern Analysis and Urban Development Insights in Beijing

**Author:** Zohaib Shabbir
**Date:** January 2026

---

##  Introduction

This project analyzes large-scale GPS trajectory data to understand human mobility patterns and the factors influencing urban development in Beijing. Completed as part of the **Winter Data Competition 2025–2026**, the work combines spatial clustering, feature engineering, and predictive modeling to explain population density across urban zones.

---

##  Project Goal and Research Question

The primary objectives of this project were to:

* Extract and preprocess raw GPS trajectory data
* Engineer meaningful spatiotemporal features
* Investigate factors influencing urban population density
* Build and evaluate predictive models for population density

**Research Question:**
*What factors, particularly transportation modes and activity patterns, influence the population density of urban zones in Beijing, and how can these factors be used to explain urban development?*

---

##  Data Overview and Preprocessing

The dataset consists of:

* Raw GPS trajectory files (`.plt`)
* Transportation mode labels (`labels.txt`)

### Preprocessing Steps

* Organized data by individual users
* Standardized date and time formats
* Removed irrelevant columns
* Merged individual datasets into unified DataFrames
* Filtered invalid latitude values
* Restricted data to Beijing’s geographic boundaries
* Converted time fields to datetime objects
* Extracted hourly activity features
* Computed trip durations and route-level data

---

## Methodologies

### 1. Spatial Clustering (K-Means)

* Applied K-Means clustering to GPS coordinates
* Partitioned Beijing into **200 urban zones**
* Assigned each GPS point to a spatial zone

### 2. Feature Engineering for Population Density

For each zone, the following features were computed:

* Number of unique users
* Average activity hour
* Estimated zone area (km²)

**Population Density Formula:**

```
Population Density = Number of Users / Area (km²)
```

Transportation modes were accurately assigned using a **time-aware merge** between GPS points and labeled trips. Predominant modes per zone were identified and one-hot encoded.

### 3. Custom Linear Regression Model

* Implemented from scratch using gradient descent
* L2 loss function
* Feature standardization using `StandardScaler`
* Train-test split applied
* Gradient computation corrected using vectorized operations

### 4. XGBoost Regressor

* Implemented to capture non-linear relationships
* Used as a performance benchmark
* Demonstrated superior predictive capability

---

##  Issues Identified and Solutions

* **SettingWithCopyWarning:** Fixed using explicit `.loc` assignments
* **Incorrect Gradient Descent:** Replaced scalar gradients with vectorized matrix operations
* **Random Transportation Mode Assignment:** Corrected using merge-as-of strategy
* **KeyError in Mode Columns:** Resolved by dynamic column selection

---

##  Model Performance

### Custom Linear Regression

* Training MSE improved: **~1.04 → ~0.51**
* Test MSE slightly worsened: **~0.25 → ~0.27**
* R² score decreased: **~−0.74 → ~−0.87**

 Indicates potential overfitting and limitations of linear modeling.

### XGBoost Regressor

* **MSE:** 0.1122
* **RMSE:** 0.3350
* **R² Score:** 0.2349

 Explained ~23.5% of the variance in population density.

---

##  Business and Policy Relevance

* **Urban Planning:** Infrastructure investment and land-use planning
* **Public Transportation:** Route and schedule optimization
* **Retail & Commercial Strategy:** Location intelligence and zoning
* **Logistics:** Route optimization and warehouse placement

Understanding mobility patterns enables smarter, data-driven urban decision-making.

---

##  Conclusion and Next Steps

### Conclusion

The project successfully established a full pipeline for analyzing mobility data and predicting population density. After resolving key data and modeling issues, **XGBoost emerged as the most effective model**.

### Future Work

* Hyperparameter tuning for XGBoost
* Feature importance analysis
* Advanced models (e.g., neural networks)
* Enhanced temporal and geographic features
* Improved area estimation methods
* Model interpretability tools (SHAP, LIME)

---

##  Repository Structure (Suggested)

```
├── data/
├── notebooks/
├── src/
├── README.md
└── requirements.txt
```

---

This repository demonstrates the value of mobility data in understanding urban dynamics and provides a foundation for future data-driven urban analytics.
