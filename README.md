<p align="center">
  <img src="assets/banner.png" alt="Predicting Diabetes Banner" width="100%">
</p>
# Predicting Diabetes with Feature Engineering & Model Evaluation

This project builds and evaluates machine-learning models to predict diabetes based on clinical patient data.  
It demonstrates a full **end-to-end ML workflow** including: data exploration, preprocessing pipelines, modeling, hyperparameter tuning, and feature engineering improvements.

---

## 📊 Project Overview

- **Goal:** Classify whether a patient has diabetes based on medical measurements  
- **Dataset:** 403 records with 15 clinical features (`data/diabetes.csv`)  
- **Target Variable:** `has_diabetes` created using medical threshold: HbA1c (glyhb) ≥ 6.5%  
- **Challenge:** Imbalanced dataset → handled with class weighting & threshold tuning  

---

## 🔍 Exploratory Data Analysis

The notebook includes:

- Summary statistics and distributions of key variables  
- Missing value analysis  
- Class imbalance analysis  
- Visualizations: histograms, boxplots, correlation heatmap  
- Insights on which features are most associated with diabetes risk (e.g. glucose, HbA1c, age, obesity-related measures)

---

## 🧠 Modeling Approach

### Preprocessing & Pipeline

A Scikit-learn `Pipeline` is used to keep preprocessing and modeling together:

- **Numeric features:**
  - Median imputation
  - Standard scaling
- **Categorical features:**
  - Most-frequent imputation
  - One-Hot Encoding
- **Classifier:**
  - Logistic Regression with `class_weight="balanced"` to handle class imbalance

### Baseline Model Performance (Logistic Regression)

- Accuracy: ~0.79  
- ROC AUC: ~0.88  
- Recall for diabetic class: ~0.68  

The baseline model is clearly better than random and already has good discrimination, but recall for diabetic patients can be improved.

---

## 🔧 Hyperparameter Tuning

`GridSearchCV` is used to tune:

- Regularization strength (`C`)
- Penalty type
- Solver
- Class weighting

Tuning improves:

- ROC AUC
- Sensitivity (recall) for the diabetic class
- Generalization (similar CV vs test scores)

---

## ✨ Feature Engineering

Clinically meaningful features are engineered to improve both performance and interpretability:

- **BMI**  
- **Waist-to-Height Ratio**  
- **Cholesterol Ratio** (Chol/HDL)  
- **Blood Pressure Categories**  
- **Age Groups**

After feature engineering:

- ROC AUC increases to ~0.90  
- Recall for the diabetic class improves  
- Coefficients align with known medical risk factors (obesity, high cholesterol, high blood pressure)

The final model is more interpretable and better at identifying diabetic patients.

---

## 🆚 Model Comparison

A **Random Forest** classifier is also trained for comparison.

- Higher overall accuracy and AUC in some settings  
- But less interpretable than Logistic Regression  

For this problem, Logistic Regression with feature engineering is preferred due to:

- Good performance
- Clear, clinically meaningful coefficients

---

## 📈 Final Results (Summary)

| Model                                   | ROC AUC (approx.) | Notes                                      |
|----------------------------------------|-------------------|--------------------------------------------|
| Logistic Regression (baseline)         | ~0.88             | Solid baseline, reasonable recall          |
| Logistic Regression (tuned + features) | **~0.90**         | Best recall & interpretability             |
| Random Forest                          | ~0.89             | Strong, but less interpretable             |

In a medical screening context, **recall (sensitivity)** for diabetic patients is especially important.  
The tuned Logistic Regression with feature engineering provides a good balance between performance and interpretability.

---

## 📂 Repository Structure

```text
.
├─ notebook/
│   └─ diabetes_model.ipynb        # Full code: EDA, modeling, tuning, feature engineering
├─ data/
│   └─ diabetes.csv                # Dataset used in the project
├─ presentation/
│   └─ Diabetes_Presentation.pdf   # Slide deck summarizing the project
├─ requirements.txt                # Python dependencies
└─ README.md                       # Project overview (this file)
