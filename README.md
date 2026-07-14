# 🩺 Autoimmune Disease ML Prediction System

A clinical decision-support tool that predicts autoimmune disease diagnoses from lab, vitals, demographic, and autoantibody-panel data — built with clinical advisors, evaluated to clinical-grade rigor, and **selected for IEEE Conference presentation**.

*Sep 2025 – Jan 2026 · Stevens Institute of Technology*

## The problem

General practitioners need a pre-referral triage signal for autoimmune conditions — a category that's notoriously hard to diagnose early because symptoms overlap across dozens of conditions. This project scopes the problem around that real user (GPs, not specialists) and that real decision moment (before a costly specialist referral).

## Approach

- **Dataset:** 11,712 patient records × 79 features — labs (RBC, hemoglobin, hematocrit, MCV/MCH), vitals, demographics, and a full autoantibody panel (ANA-related markers: Anti-Sm, anti-Scl-70, pANCA, and others)
- **Success criteria, set with 2 clinical advisors:** sensitivity ≥ 90%, false positive rate < 15% — thresholds chosen for a pre-referral triage tool, not a final diagnosis
- **Feature selection:** deliberately kept to a simple, low-cardinality set of labs/vitals/demographics to avoid overfitting to a synthetic-feeling signal
- **Model comparison:** XGBoost, Random Forest, Gradient Boosting, AdaBoost, SVC, and Naive Bayes evaluated before selecting an **XGBoost + Random Forest ensemble**
- **Validation:** 10-fold CV, Leave-One-Out, Leave-One-Group-Out, and Repeated Stratified K-Fold — deliberately over-validated to catch overfitting before trusting the numbers
- **Tuning:** mild GridSearchCV, tuned for generalization rather than squeezing out a "too perfect" score
- **Interpretability:** SHAP values to explain individual predictions and identify which lab markers drive risk
- **Class imbalance:** handled with SMOTE and stratified sampling

## Results

| Metric | Score |
|---|---|
| Diagnostic accuracy | 89% |
| Sensitivity | 91% |
| AUC | 0.93 |

Paper selected for **IEEE Conference presentation** — validated for real-world clinical relevance and methodological rigor.

## Making it usable, not just accurate

A model with good metrics is only useful if a clinician will actually use it. This project shipped a **Streamlit prototype** so non-technical clinical reviewers could probe the model with real-world scenarios — feedback from those sessions drove 2 rounds of feature iteration.

## Team & role

Led a 4-person team across data, modeling, and evaluation — ran weekly syncs, owned the experiment tracking sheet, and drove the collaboration with clinical advisors that shaped the success criteria.

## Repo contents

| File | What it is |
|---|---|
| `ML_Pipeline.ipynb` | Full pipeline: preprocessing, feature selection, model comparison, cross-validation, tuning, SHAP, ROC/confusion matrix |
| `DEPLOYMENT_.ipynb` | Streamlit deployment notebook for the clinical-reviewer prototype |
| `Final_Balanced_Autoimmune_Disorder_Dataset.csv` | Balanced dataset used for training/evaluation |

## Stack

`XGBoost` · `Random Forest` · `scikit-learn` · `SHAP` · `Streamlit` · `SMOTE`

## Run it

```bash
pip install xgboost shap scikit-learn pandas numpy streamlit
jupyter notebook ML_Pipeline.ipynb
```

---

Part of my AI/ML product work — see my [portfolio](https://render-reflection-relay.lovable.app) for the product-management framing of this project, including the requirements process with clinical advisors.
