# Satellite Telemetry Anomaly Detection Using Machine Learning in R

## 1. Project Overview

This coursework case study analyzes satellite telemetry data and uses machine learning to classify telemetry segments as **Nominal** or **Anomalous**.

**Project title:** Satellite Telemetry Anomaly Detection Using Machine Learning in R

**Problem statement:**
To identify anomalous satellite telemetry segments from nominal telemetry using machine learning in R.

**Modeling scope:** This project treats anomaly detection as **supervised binary classification** because the official OPSSAT-AD dataset provides ground-truth anomaly labels. The project is a telemetry-segment classifier; it is **not future satellite-failure forecasting**.

## 2. Official Dataset

This project uses **only the official OPSSAT-AD dataset**.

**Dataset source:**
> OPSSAT-AD – anomaly detection dataset for satellite telemetry, Zenodo Record 12588359, Version 1.

**DOI:** https://doi.org/10.5281/zenodo.12588359

The dataset contains telemetry acquired on board ESA's OPS-SAT CubeSat and includes ground-truth anomaly labels and an official train/test split.

### Dataset summary

- **Rows:** 2,123 labeled telemetry segments
- **Columns:** 23
- **Channels:** 9
- **Training segments:** 1,594
- **Test segments:** 529
- **Nominal segments:** 1,689
- **Anomalous segments:** 434
- **Telemetry-derived features:** 18
- **Target variable:** `anomaly`
  - `0` = Nominal
  - `1` = Anomalous

The tabular dataset contains metadata, the anomaly label, and 18 supplied telemetry-derived features.

## 3. Google Colab – R Runtime

The main implementation is designed to run in **Google Colab using the R runtime**.

### Steps

1. Open `Satellite_Telemetry_Anomaly_Detection_Colab_R.ipynb` in Google Colab.
2. Select **Runtime → Change runtime type → R**.
3. Upload your official OPSSAT-AD `dataset.csv` to Colab, or place it in Google Drive.
4. In the notebook, set the path in the dataset-path cell, for example:

```r
dataset_path <- "/content/dataset.csv"
```

or

```r
dataset_path <- "/content/drive/MyDrive/OPSSAT-AD/dataset.csv"
```

5. Run the notebook from top to bottom.

**Important:** The notebook does **not** download the dataset. It reads the official CSV from the path that you provide.

## 4. Project Workflow

```text
Official OPSSAT-AD dataset
            ↓
Data understanding
            ↓
Data quality checks
            ↓
Data preprocessing
            ↓
Exploratory data analysis
            ↓
Visualization
            ↓
Official train/test split
            ↓
Random Forest + Logistic Regression
            ↓
Prediction
            ↓
Model evaluation
            ↓
Feature importance
            ↓
Findings and conclusion
```

## 5. Data Preparation

The R implementation performs the following checks and preprocessing steps:

- Inspects dimensions and column names.
- Checks data types.
- Checks missing values.
- Checks duplicate rows.
- Checks non-finite numeric values.
- Converts `anomaly` and `channel` to suitable factors.
- Uses the supplied `train` variable for the official train/test split.
- Excludes `segment` and `train` from the machine-learning predictors to avoid identifier/split leakage.
- Applies median imputation to predictor values only when missing values are present, using medians calculated from the training data.

The cleaning steps are evidence-based; the notebook does not claim that a problem exists unless the data check finds it.

## 6. Exploratory Data Analysis and Visualization

The notebook generates relevant visualizations such as:

- Nominal vs anomalous class distribution.
- Anomaly rate by telemetry channel.
- Feature distributions and boxplots, including `mean` and `std`.
- Other supporting plots where useful for interpretation.

Every important graph includes a meaningful title and axis labels, and the generated results are used for interpretation.

## 7. Machine Learning Models

### Primary model: Random Forest

Random Forest is used as the primary model because it can capture nonlinear relationships and interactions among telemetry features and provides feature-importance information.

### Comparison model: Logistic Regression

Logistic Regression is used as an interpretable baseline for binary classification.

## 8. Model Evaluation

The models are evaluated using:

- Accuracy
- Precision
- Recall
- F1-score
- Matthews Correlation Coefficient (MCC)
- ROC-AUC
- PR-AUC

The confusion matrix, ROC curve, PR curve, and feature-importance results are generated from the executed R notebook.

**Important:** Final numerical results in the PPT and final report must be taken from the notebook after it is executed on the official dataset. Do not enter guessed or manually invented metrics.

## 9. R Markdown and Final Documentation

`Satellite_Telemetry_Anomaly_Detection_Final_Report.Rmd` is the R Markdown source for the final documentation.

The final document is organized around:

1. Title
2. Introduction / Problem
3. Objectives
4. Dataset
5. Data Preparation
6. Data Analysis
7. Visualization
8. Prediction / Model
9. Results
10. Conclusion
11. References

The final documentation should be kept within the college requirement of **5–10 pages** and should contain only relevant code, tables, graphs, interpretations, and results.

## 10. Presentation

`PPT_PROMPT_FOR_CLAUDE.txt` contains the prompt for generating a **10–12 slide college-level presentation** in Claude.

The presentation covers:

- Title
- Background
- Problem statement
- Objectives
- Dataset
- Important variables
- Data preparation in R
- Analysis and visualization
- Machine-learning methods
- Model evaluation
- Feature importance and findings
- Conclusion and references

Use the actual plots and model results generated by the R notebook. Do not manufacture statistics, screenshots, confusion-matrix counts, or feature rankings.

## 11. Version Control

Use simple version control through Git/GitHub or clearly named project versions.

Recommended milestones:

```text
v1_initial_dataset_and_problem
v2_preprocessing_and_eda
v3_model_development
v4_final_results
```

`version_history.csv` records the major stages of the case study.

## 12. Suggested Final Project Folder

```text
Satellite_Telemetry_Anomaly_Detection/
│
├── dataset.csv
├── Satellite_Telemetry_Anomaly_Detection_Colab_R.ipynb
├── Satellite_Telemetry_Anomaly_Detection_Final_Report.Rmd
├── Satellite_Telemetry_Anomaly_Detection_Final_Report.pdf
├── Satellite_Telemetry_Anomaly_Detection_Presentation.pptx
├── PPT_PROMPT_FOR_CLAUDE.txt
├── version_history.csv
└── README.md
```

The PDF report and PPTX should be created after executing the R notebook so that all documented results match the actual outputs.

## 13. References

1. Ruszczak, B., Kotowski, K., Evans, D., & Nalepa, J. (2025). *The OPS-SAT benchmark for detecting anomalies in satellite telemetry*. Scientific Data. DOI: https://doi.org/10.1038/s41597-025-05035-3
2. OPSSAT-AD – anomaly detection dataset for satellite telemetry. Zenodo Record 12588359, Version 1. DOI: https://doi.org/10.5281/zenodo.12588359
3. KP Labs. OPS-SAT-AD GitHub repository.

## 14. Important Project Rules

- Use **only the official OPSSAT-AD dataset** for this project.
- Do not describe the dataset as synthetic, self-generated, simulated, toy, or fabricated.
- Do not use the earlier synthetic dataset.
- Do not claim that the model predicts future satellite failures.
- Describe the task as **supervised binary classification of telemetry segments into Nominal and Anomalous classes**.
- Do not invent model metrics or analytical findings; use the values produced by the executed R notebook.
