# Safety-First Risk Stratification for ICU Length of Stay Prediction

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Library](https://img.shields.io/badge/Library-Scikit--Learn%20|%20XGBoost%20|%20LightGBM-orange)
![Dataset](https://img.shields.io/badge/Dataset-MIMIC--III-red)
![Status](https://img.shields.io/badge/Status-Research-green)

## Overview
This repository contains the implementation of the term project: **"Safety-First Risk Stratification for ICU Length of Stay: An Ensemble Learning Approach with Missing and Imbalanced Data Management."**

The goal of this project is to predict whether an ICU patient requires a **Long Stay (>5 days)** or a **Short Stay**. Unlike traditional regression models that focus on average accuracy, this project adopts a **"Safety-First"** strategy, optimizing the model to maximize **Sensitivity (Recall)**. This ensures that high-risk patients who need extended care are correctly identified, minimizing dangerous "false negatives."

## Key Features
* **Ensemble Modeling:** Combines **XGBoost**, **LightGBM**, and **Random Forest** in a Voting Classifier for robust predictions
* **Disease-Aware Feature Engineering:** Incorporates specific disease flags (Pneumonia, Heart Failure, Sepsis, etc.) derived from ICD-9 codes, alongside physiological indicators like Shock Index and GCS
* **Advanced Data Handling:**
    * **Missing Data:** Uses **MICE** (Multivariate Imputation by Chained Equations) to preserve statistical relationships
    * **Imbalance:** Implements **SMOTE** (Synthetic Minority Over-sampling Technique) to prevent bias towards the majority class
* **Explainable AI:** Uses **SHAP** (SHapley Additive exPlanations) to interpret model decisions and validate clinical relevance

## Performance
The model was evaluated on a held-out test set from the MIMIC-III database with a custom decision threshold of **0.38**:

| Metric | Value | Note |
| :--- | :--- | :--- |
| **Sensitivity (Recall)** | **90.73%** | Maximized for patient safety  |
| **ROC-AUC** | 0.77 | Good discrimination capability|
| **Specificity** | 39.61% |Trade-off accepted for higher safety|

> **Key Insight:** SHAP analysis revealed that specific disease etiologies (e.g., **Pneumonia**) are stronger predictors of long stays than general vital signs alone.

## Dataset Access (MIMIC-III)
**Important Note regarding Data Availability:**

This project utilizes the **MIMIC-III (Medical Information Mart for Intensive Care III)** database, version 1.4.

> **Due to the sensitive nature of the data (Protected Health Information - PHI) and the data use agreement (DUA), the dataset files are NOT included in this repository.**

To reproduce the results or use the code:
1.  You must complete the CITI "Data or Specimens Only Research" training.
2.  Request access to MIMIC-III via [PhysioNet](https://physionet.org/content/mimiciii/).
3.  Once approved, download the CSV files and place them in the `data/` directory (or adjust the paths in the config).
