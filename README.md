# Heart Disease Risk Prediction & Patient Segmentation

A portfolio machine-learning project using the **Framingham Heart Study teaching dataset**. The project combines **Logistic Regression** for 10-year coronary heart disease (CHD) risk classification with **K-Means clustering** for exploratory patient segmentation.

> **Important:** This is an educational machine-learning project, not a clinical diagnostic system.

## Project highlights

- 4,240 observations and 15 predictor variables
- CHD-positive class: **15.2%**
- Leakage-safe preprocessing with median imputation and standardization
- Stratified train/validation/test workflow
- Class-balanced Logistic Regression
- Cross-validated hyperparameter tuning
- Validation-based decision-threshold optimization using F2
- ROC-AUC, PR-AUC, sensitivity, specificity, balanced accuracy and confusion-matrix evaluation
- Standardized coefficient / odds-ratio interpretation
- K-Means cluster selection using silhouette score
- PCA visualization and patient cluster profiling
- Reproducible model artifact saving

## Classification results

| Metric | Baseline Logistic Regression | Balanced + tuned threshold |
|---|---:|---:|
| Decision threshold | 0.50 | **0.36** |
| Accuracy | 0.852 | 0.502 |
| Balanced accuracy | 0.532 | **0.642** |
| Precision | 0.583 | 0.211 |
| Recall / sensitivity | 0.073 | **0.844** |
| Specificity | 0.991 | 0.441 |
| F1 | 0.130 | 0.338 |
| F2 | 0.088 | **0.528** |
| ROC-AUC | 0.699 | **0.701** |
| PR-AUC | 0.328 | **0.339** |

### Why the lower accuracy is not automatically worse

The baseline model achieved **85.2% accuracy**, but because the dataset is imbalanced it detected only **7.3% of CHD-positive cases**.

The final screening-oriented operating point uses a validation-selected threshold of **0.36**, increasing CHD recall to **84.4%**. The trade-off is lower precision (**21.1%**) and specificity (**44.1%**), meaning more false positives.

Importantly, ROC-AUC changed only slightly from **0.699 to 0.701**. The project therefore demonstrates a key machine-learning lesson: **threshold selection changes the operating behavior of a classifier even when its underlying ranking ability changes very little**.

## Important model associations

The largest positive standardized Logistic Regression coefficients were:

1. **Age** — standardized odds ratio ≈ **1.69**
2. **Cigarettes per day** — ≈ **1.26**
3. **Systolic blood pressure** — ≈ **1.25**
4. **Male sex** — ≈ **1.20**
5. **Glucose** — ≈ **1.13**

These are predictive associations in this teaching dataset and are **not causal estimates**.

## K-Means patient segmentation

Silhouette analysis selected **k = 3** with a best silhouette score of approximately **0.215**.

| Cluster | Patients | Observed CHD prevalence | Main profile |
|---|---:|---:|---|
| 0 | 2,392 | 10.5% | Comparatively lower BP/glucose profile |
| 1 | 1,116 | 23.6% | Hypertension-heavy; mean systolic BP ≈ 154.8 |
| 2 | 96 | **36.5%** | Diabetes/metabolic-risk group; mean glucose ≈ 167.1 |

The modest silhouette score means the clusters overlap and should be interpreted as **exploratory patient segments**, not definitive clinical phenotypes.

## Repository structure

```text
heart-disease-ml-portfolio/
├── HEART_DISEASE_PREDICTION_PORTFOLIO_FINAL.ipynb
├── README.md
├── requirements.txt
├── .gitignore
├── GITHUB_UPLOAD_CHECKLIST.md
└── data/
    └── README.md
```

## How to run

1. Clone or download the repository.
2. Optionally place `framingham.csv` inside the `data/` folder.
3. Install dependencies:

```bash
pip install -r requirements.txt
```

4. Open the notebook in Jupyter, VS Code, or Google Colab.
5. Run all cells from top to bottom.

The notebook also contains a public fallback dataset URL if a local CSV is not present.

## Technologies

Python · pandas · NumPy · Matplotlib · Seaborn · scikit-learn · Jupyter · joblib

## Responsible use

This notebook is for learning and portfolio demonstration. It has not been clinically validated and must not be used for diagnosis, treatment, or patient-level medical decisions.
