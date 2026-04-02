# Predicting Diabetes: Identifying Key Risk Factors Using Machine Learning

**Module:** CSC3031 — Applied Data Science  
**Degree:** BSc Computer Science, University of Exeter  
**Student Number:** 720017170

---

## Overview

This project investigates which clinical factors are the strongest predictors of diabetes, and how accurately machine learning models can classify diabetes outcomes. The analysis is implemented **twice** — once in **R** and once in **Python** — allowing a direct comparison of approaches and outputs across both ecosystems.

**Research Questions:**
1. Which factors are the strongest predictors of diabetes?
2. How accurately can these factors classify diabetes status?
3. Which machine learning model most accurately classifies diabetes status?

---

## Repository Structure

```
.
├── README.md
├── .gitignore
├── data/
│   └── diabetes.csv                  # Pima Indians Diabetes dataset (768 records)
├── analysis/
│   ├── Coursework.Rmd                # Full analysis in R (knit to PDF)
│   ├── Project.qmd                   # Full analysis in Python via Quarto (render to PDF)
│   ├── references.bib                # BibTeX bibliography
│   └── harvard-exeter.csl            # Harvard (Exeter) citation style
├── outputs/
│   ├── Coursework.pdf                # Compiled R report
│   ├── Project.pdf                   # Compiled Python report
│   ├── summary_table.tex             # LaTeX summary statistics table
│   └── performance_table.tex         # LaTeX model performance table
└── docs/
```

---

## Dataset

**File:** [data/diabetes.csv](data/diabetes.csv)  
**Source:** Pima Indians Diabetes Dataset via [Kaggle](https://www.kaggle.com/)  
**Scope:** 768 female patients; binary outcome (diabetic / non-diabetic)

| Variable | Description |
|---|---|
| `Pregnancies` | Number of times pregnant |
| `Glucose` | Plasma glucose concentration (2-hr oral glucose tolerance test), mg/dL |
| `BloodPressure` | Diastolic blood pressure, mm Hg |
| `SkinThickness` | Triceps skinfold thickness, mm |
| `Insulin` | 2-hour serum insulin, μU/mL |
| `BMI` | Body Mass Index |
| `DiabetesPedigreeFunction` | Genetic diabetes risk score based on family history |
| `Age` | Age in years |
| `Outcome` | Target variable — `1` = Diabetic, `0` = Non-Diabetic |

**Data quality note:** ~49% of rows contain physiologically impossible zero values in fields such as Glucose, BloodPressure, and BMI. Both analyses handle this by replacing zeros with the column mean (excluding zeros from the mean calculation), except for `Pregnancies` and `Outcome` where zero is a valid value.

---

## Methods

Both analyses follow an identical methodology:

1. **Data Preprocessing** — Replace zero-value placeholders with column means; z-score normalise continuous features.
2. **Exploratory Data Analysis (EDA)** — Descriptive statistics, correlation heatmap, and distribution plots grouped by outcome.
3. **Modelling** — Train/test split (80/20). Three models trained and evaluated:
   - **Logistic Regression (LR)** — Odds ratios to quantify predictor-outcome relationships.
   - **Random Forest (RF)** — Feature importance scores to rank predictors.
   - **Support Vector Machine (SVM)** — Non-linear classification boundary evaluation.
4. **Evaluation** — Accuracy, Precision, Recall, F1-Score, and AUC-ROC for each model.

---

## Results Summary

| Model | Accuracy | Precision | Recall | F1-Score | AUC |
|---|---|---|---|---|---|
| Logistic Regression | 80.5% | 81.8% | 62.1% | 0.706 | 0.848 |
| Random Forest | 77.9% | 72.2% | 67.2% | 0.696 | 0.856 |
| SVM | 76.6% | 75.0% | 56.9% | 0.647 | 0.863 |

**Key findings:**
- **Glucose** and **BMI** are consistently the strongest predictors across all three models.
- **Logistic Regression** achieves the highest overall accuracy (80.5%) and precision.
- **SVM** achieves the highest AUC (0.863), suggesting strong rank-ordering of risk even where point accuracy is lower.

---

## Reproducing the Analysis

### R Analysis (`analysis/Coursework.Rmd`)

**Requirements:** R >= 4.0, RStudio (recommended)

Install dependencies:
```r
install.packages(c("tidyverse", "gridExtra", "caret", "randomForest", "e1071", "vtable"))
```

Render to PDF from RStudio using **Knit**, or from the terminal:
```bash
Rscript -e "rmarkdown::render('analysis/Coursework.Rmd')"
```

### Python Analysis (`analysis/Project.qmd`)

**Requirements:** Python >= 3.9, [Quarto](https://quarto.org/) >= 1.3

Install Python dependencies:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn statsmodels
```

Render to PDF:
```bash
quarto render analysis/Project.qmd
```

> **Note:** Both files reference the dataset as `../data/diabetes.csv` (relative to the `analysis/` directory). Run render commands from the project root or ensure the working directory is set to `analysis/`.

---

## Technologies

| Tool | Purpose |
|---|---|
| R / RMarkdown | Primary statistical analysis and report generation |
| Python / Quarto | Alternative analysis and report generation |
| scikit-learn | ML models (RF, SVM, LR) in Python |
| caret / randomForest / e1071 | ML models in R |
| LaTeX | Table formatting embedded in PDF output |
| BibTeX + Harvard CSL | Academic referencing |

---

## GitHub Repository

[https://github.com/JoshLG18/Diabetes-Prediction](https://github.com/JoshLG18/Diabetes-Prediction)
