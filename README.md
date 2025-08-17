# AIML_24.1 Capstone Project
## Project Title - *Predicting Air Quality Index (AQI) Category in Delhi Using Machine Learning*

**Author:** Amit Kumar

#### Executive Summary
Delhi continues to face severe air pollution, with levels of harmful particles (PM2.5, PM10) and gases (NO₂, SO₂, CO) often exceeding safe limits. These conditions affect public health, daily life, and economic productivity. While citizens and authorities receive air quality alerts, they are often reactive rather than predictive. Our project explores how machine learning can forecast the Air Quality Index (AQI) category—ranging from Good to Severe—so that preventive actions can be taken in time.

Accurate classification of air quality levels enables early warnings, public health interventions and environmental policy decisions. After extensive exploratory data analysis and model experimentation, the project identifies the **XGBoost Classifier** as the most reliable model for predicting AQI categories with over **85.8% accuracy**.

#### Rationale
Air pollution is a persistent public health and environmental crisis in Delhi. Given the complex interactions between pollutants and weather variables, manual forecasting is inadequate. Predictive modeling offers a scalable, data-driven alternative. This project seeks to empower authorities and citizens with **category-level AQI predictions** (e.g., "Poor", "Severe") using **historical pollutant and weather data**.

---

## Research Question

> **Can we develop a robust machine learning model that accurately predicts the Air Quality Index (AQI) category — Good, Satisfactory, Moderate, Poor, Very Poor, Severe — for Delhi using pollutant concentration levels and weather data?**

---

## Data Sources

1. **Delhi Pollution Dataset**  
   Daily concentration values for pollutants (PM2.5, PM10, NO2, SO2, CO, NH3, O3, etc.)  
   [Source: Tumidata](https://hub.tumidata.org/dataset/air_quality_analysis_of_delhi_delhi)

2. **Delhi Weather Dataset**  
   Meteorological data including temperature, humidity, wind speed, pressure, etc.  
   [Source: Visual Crossing Weather Data](https://www.visualcrossing.com/weather-query-builder/)

3. **Changes in Dataset Identified During Assignment 16.1**  
   Kaggle – Air Quality Analysis of Delhi dataset mentioned in submission for Assignement 16.1 has not been used as the requirement of pollution and weather dataset has been met from the above sources.     

  
---

## Methodology

### 1. **Data Cleaning & Merging**
- Removed irrelevant columns (e.g., station codes)
- Converted timestamps and aligned formats
- Merged pollution and weather datasets on `datetime`
- Interpolated missing values and ensured temporal consistency

### 2. **Exploratory Data Analysis (EDA)**
- Visualized seasonal, daily and category-wise AQI variations
- Boxplots, KDEs and scatter matrices analyzed pollutant distributions
- Outlier detection via boxplots and value thresholds

### 3. **Feature Engineering**
- Extracted `month`, `weekday`, `hour` from datetime
- Converted AQI values to categories using CPCB thresholds
- Encoded categorical AQI labels using `LabelEncoder`

### 4. Baseline Modeling  
- **Logistic Regression (baseline):** Accuracy 0.62, Macro-F1 0.64.  
- **Balanced Logistic Regression:** No major gains (F1 0.61).  
- **Dummy Classifier:** Useless baseline (F1 ~0.07). 

### 5. Tuned Modeling & Selection  
| Model                     | Accuracy (CV) | Macro-F1 (CV) | Kappa (CV) | Notes |
|----------------------------|---------------|---------------|------------|-------|
| **XGBoost (tuned)**        | 0.827 | 0.853 | 0.777 | Best overall |
| HistGradientBoosting (tuned)| 0.822 | 0.848 | 0.770 | Strong, slightly behind XGB |
| Random Forest (tuned)      | 0.794 | 0.823 | 0.733 | Good robustness |
| Logistic Regression (base) | 0.621 | 0.636 | 0.508 | Weak baseline |
| Dummy (Most Frequent)      | 0.259 | 0.069 | 0.000 | Trivial baseline |  

### 6. **Final Selection:**  
- **XGBoost (grid-tuned)** → Accuracy 0.8582, Macro-F1 0.8772, Kappa 0.817, Quadratic Weighted Kappa (QWK) 0.8697.  
- **Per-class metrics:** Excellent precision/recall for *Good, Moderate, Very Poor, Severe*, though some overlap remained between *Poor* and *Very Poor*.  
---

## Findings  

1. **Feasibility Proven:** AQI category prediction is realistic with ~86% accuracy using daily pollution + weather data.  
2. **XGBoost Emerges Best:** Outperforms Random Forest and Logistic Regression across accuracy and F1.  
3. **Critical Features:** PM2.5, PM10, NO₂ and CO dominate predictive power.  
4. **Policy Relevance:** Model outputs can directly inform **public health warnings, urban planning and emergency responses**.  

---
## Business and Policy Implications  

The model has wide-ranging practical value:  

- **Public:** Enables timely advisories (mask usage, limiting outdoor activities, using air purifiers).  
- **Government:** Supports dynamic enforcement of pollution control (e.g., construction bans, traffic regulations).  
- **Schools & Workplaces:** Provides evidence for closures or online operations during severe days.  
- **Traffic Authorities:** Can trigger “odd-even” road rationing or limit heavy vehicle entry.  
- **Construction Activity:** Alerts can enforce dust-control and suspension of high-emission activities.  
- **Hospitals & Medical Agencies:** Forecasts allow stockpiling of emergency medicines, oxygen support and respiratory care facilities.  
- **Supplies & Retail:** Demand spikes in masks, air purifiers, filters and essential drugs can be anticipated, avoiding shortages.  

In short, **predictive AQI models bridge science and policy**, allowing targeted, timely and resource-efficient responses.  


---

## Next Steps

- Extend dataset with real-time streaming sources (CPCB, SAFAR, OpenAQ).  
- Deploy model as a **public dashboard / API** for continuous advisories.  
- Explore **deep learning (LSTM, GRU)** for temporal forecasting.  
- Integrate economic and health cost data to link AQI predictions with **policy impact modeling**.  
- Fine-tune thresholds to minimize confusion between *Poor* and *Very Poor*.  

---

## Project Structure and Notebooks

| Notebook | Description |
|----------|-------------|
| [Link to Notebook](https://github.com/amitkushwaha2000/AIML_20.1_Capstone/blob/main/20.1%20Capstone_AK_AQI%20Prediction.ipynb) | Jupyter Notebook for Assignment 20.1 Capstone Project |
| [Link to Datasets](https://github.com/amitkushwaha2000/AIML_20.1_Capstone/tree/main/data) | delhi_pollution.csv and delhi_weather.csv |

---

## Contact and Further Information

For feedback, collaboration, or deployment queries, feel free to reach out at:  
**[amitkushwaha2000@gmail.com]**

---
