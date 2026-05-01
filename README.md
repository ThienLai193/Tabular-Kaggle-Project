# American Express Default Prediction

* **One Sentence Summary**  
This project builds a machine learning pipeline to predict customer default using aggregated time-series features from the American Express dataset.

---

## Overview

* **Task**  
Predict whether a customer will default (target = 1) or not (target = 0).

* **Approach**  
- Convert time-series → customer-level data  
- Clean + preprocess  
- Handle imbalance  
- Train Gradient Boosting  
- Evaluate with ROC-AUC  

---

## Summary of Workdone

### Data

* Input: customer monthly records (CSV)  
* Output: binary label (default / no default)  

---

## Preprocessing / Clean up (WITH OUTPUTS)

### Step 1 – Data Inspection

**What was done:**
- Checked dataset shape and previewed data

**Output:**
- Data contains **multiple rows per customer**
- Confirmed dataset is **time-series structure**

---

### Step 2 – Customer Analysis

**What was done:**
- Counted unique customers
- Checked rows per customer

**Output:**
- Each customer has **multiple monthly records**
- Confirms need for aggregation

---

### Step 3 – Missing Values

**What was done:**
- Calculated missing values per column

**Output:**
- Several features contain **missing values (some high %)**
- Requires imputation before modeling

---

### Step 4 – Feature Split

**What was done:**
- Split into numerical and categorical features

**Output:**
- Two groups created:
  - Numerical → continuous values
  - Categorical → encoded later

---

### Step 5 – Target Distribution

**What was done:**
- Checked class distribution

**Output:**
- Dataset is **imbalanced**
- Negative class (0) is **subsampled to 5%**
- Each class 0 sample represents ~20 real samples
<img width="597" height="455" alt="image" src="https://github.com/user-attachments/assets/3b484606-68f4-4b56-b0c6-41f3b55751b3" />

---

### Step 6 – Aggregation (Critical Step)

**What was done:**
- Grouped by customer_ID
- Numerical → mean, std, min, max, last
- Categorical → last, nunique

**Output:**
- Data transformed from:
  - many rows per customer → **1 row per customer**
- Dataset becomes **ML-ready**

---

### Step 7 – Numerical Visualization

**What was done:**
- Plotted histograms for selected features

**Output:**
- Some features show **clear separation between classes**
- Indicates strong predictive features
<img width="803" height="1490" alt="image" src="https://github.com/user-attachments/assets/837de22d-805e-4e63-a8ff-46aea836a268" />

---

### Step 8 – Categorical Visualization

**What was done:**
- Plotted category distributions

**Output:**
- Certain categories have **higher default rates**
- Confirms categorical features are useful
<img width="1189" height="889" alt="image" src="https://github.com/user-attachments/assets/52bdbb69-d5a0-408a-bc12-2f04f6c2d396" />

---

### Step 9 – Correlation Analysis

**What was done:**
- Generated correlation heatmap

**Output:**
- Some features show **moderate correlation with target**
- Some features are correlated with each other → possible redundancy
<img width="579" height="490" alt="image" src="https://github.com/user-attachments/assets/7dd6fb0b-7bac-4f43-8d0c-2c7bbafadf0a" />

---

### Step 10 – Missing Value Handling

**What was done:**
- Numerical → filled with median
- Categorical → filled with mode

**Output:**
- Dataset has **0 missing values after processing**
<img width="1189" height="390" alt="image" src="https://github.com/user-attachments/assets/4a545b57-4e50-4594-b2f1-7f0b2eebdc08" />

---

### Step 11 – Scaling

**What was done:**
- Applied StandardScaler

**Output:**
- Numerical features transformed:
  - mean ≈ 0
  - std ≈ 1

---

### Step 12 – Encoding

**What was done:**
- Applied one-hot encoding

**Output:**
- All categorical features converted to numeric
- Final dataset is **fully numeric**

---

### Step 13 – Train/Test Split

**What was done:**
- Split data (60/20/20)
- Used stratify

**Output:**
- Class distribution preserved across splits

---

## Problem Formulation

* Input: aggregated features  
* Output: default prediction  

---

## Training

**What was done:**
- Trained GradientBoostingClassifier
- Used sample weights (20x for class 0)

**Output:**
- Model trained successfully
- Handles imbalance properly

---

## Performance Comparison

**Metrics:**
- ROC-AUC
- Precision / Recall
- Confusion Matrix
<img width="505" height="219" alt="image" src="https://github.com/user-attachments/assets/6cb8bbc3-93ca-4e67-915b-e80acffb4cba" />
<img width="567" height="490" alt="image" src="https://github.com/user-attachments/assets/55175544-a558-4fd3-9463-beaffcfa6cc5" />

**Output:**
- ROC-AUC ≈ 0.89  
- Model separates classes well  
- Good recall for default class  

---

## Conclusions

- Aggregation is essential for time-series data  
- Handling imbalance improves model performance  
- Feature engineering is critical  

---

## Future Work

- Try XGBoost / LightGBM  
- Add time-based features  
- Use full dataset  

---

## How to reproduce results

Run:

```bash
jupyter notebook final.ipynb
