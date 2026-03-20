# Project Title: Multidimensional Analysis and Predictive Forecasting of the Olist E-Commerce Ecosystem

## Abstract
This repository contains an end-to-end analytical framework and predictive pipeline developed for the **Olist Brazilian E-Commerce** dataset. Utilizing a relational database of over **100,000 orders**, this study implements a dual-track approach: a **strategic business diagnostic** (RFM Segmentation, Geospatial Analysis) and a **predictive modeling engine** to forecast transaction volumes. The project specifically addresses the **extrapolation challenges** inherent in high-growth e-commerce environments.

---

## Theoretical Framework: The Extrapolation Paradox
The predictive component of this study explores the tension between **Stochastic Gradient Boosting** and **Ordinary Least Squares (OLS)** regression in the context of non-stationary time series. 

While ensemble methods like **XGBoost** and **Random Forest** excel at capturing non-linear local dependencies, they inherently suffer from a "ceiling effect" when forecasting record-breaking growth. This project demonstrates that in presence of a strong linear trend, the **Bias-Variance tradeoff** favors global linear estimators. 

The optimization was guided by the **Root Mean Square Error (RMSE)**:
$$\text{RMSE} = \sqrt{\frac{1}{n}\sum_{i=1}^{n}(y_i - \hat{y}_i)^2}$$
where $\hat{y}_i$ represents the forecasted order volume, emphasizing the penalty for large residuals during peak promotional periods (e.g., Black Friday).

---

## Methodology and Technical Workflow

### 1. Relational Data Engineering
The raw data was ingested via an **SQLite** environment to maintain relational integrity across nine interconnected tables. 
* **ETL Pipeline:** Implemented SQL-based joins to synthesize customer behavior with logistics performance.
* **Feature Engineering:** Developed a **7-day Moving Average (Momentum)** and **Active Seller Regressors**, which proved to be the most significant predictors of sales velocity.

### 2. Strategic Segmentation (RFM Model)
To address the identified **96.6% Churn Risk**, I implemented a **Recency, Frequency, and Monetary (RFM)** model. By applying **Quantile-based binning**, customers were categorized into actionable segments:
* **Champions:** High-velocity, high-value users requiring loyalty preservation.
* **At Risk / Sleepers:** High-historical value users with declining recency, requiring targeted win-back interventions.

### 3. Geospatial Optimization
Using **Folium-based Heatmaps**, I mapped revenue density across 27 Brazilian states. The findings revealed a heavy concentration in the **Southeast (SP, RJ, MG)**, providing a data-driven justification for regional warehouse decentralization to reduce the identified **average delivery lead time of 12.5 days**.

---

## Predictive Modeling Performance

I evaluated four distinct architectures to forecast daily order counts:

| Model | Test RMSE | Technical Evaluation |
| :--- | :--- | :--- |
| **Multivariate Linear Regression** | **28.72** | **Winner:** Successfully extrapolated the linear growth trend beyond training boundaries. |
| **Lasso Regression (L1)** | 29.73 | Successfully performed feature selection, removing redundant weekend indicators. |
| **XGBoost** | 30.63 | Captured local volatility but struggled with trend-based extrapolation. |
| **Random Forest** | 43.05 | Suffered from "Extrapolation Failure," hitting a prediction ceiling. |

---

## Installation and Environment Setup
Ensure **Python 3.9+** and a local **SQLite** environment are configured.

### Dependencies
* **Core:** `Pandas`, `NumPy`, `SciPy`
* **ML:** `Scikit-Learn`, `XGBoost`
* **Visuals:** `Seaborn`, `Plotly`, `Folium`

### Execution
Clone the repository:
`git clone https://github.com/arzuunr/brazilian-ecommerce-analytics.git`

Install dependencies:
`pip install -r requirements.txt`

Run the diagnostic and model:
`python main.py`

---

## Conclusion and Future Scalability
The analysis exposes a **"Leaky Bucket" syndrome**: while acquisition and daily growth are robust, the **3.01% retention rate** represents a critical operational bottleneck. 

To transition this project to a **Google-scale production environment**, future development will focus on:
* **Modularization:** Refactoring the procedural script into a **Class-based Pipeline Architecture**.
* **Containerization:** Packaging the environment via **Docker** for cross-platform deployment.
* **MLOps:** Implementing **Walk-Forward Validation** triggers to handle future non-linear shifts in e-commerce trends.


