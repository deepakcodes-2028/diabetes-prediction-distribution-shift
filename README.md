# Diabetes Prediction Under Population Distribution Shift Using ANN

An AI/ML research project that investigates how changes in population characteristics over time affect diabetes prediction performance. The project trains and evaluates machine learning models using CDC Behavioral Risk Factor Surveillance System (BRFSS) data from 2015 and 2021.

## Overview

Machine learning models may perform differently when evaluated on data collected from a different population or time period. This project studies **temporal population distribution shift** by developing a diabetes prediction model using BRFSS 2015 data and evaluating its performance on BRFSS 2021 data.

The project includes an Artificial Neural Network (ANN), Logistic Regression, and Random Forest for comparative evaluation, along with an interactive Streamlit application for exploring predictions and research results.

## Objectives

- Develop an ANN-based diabetes prediction model.
- Train and evaluate models using BRFSS 2015 data.
- Assess temporal generalization using BRFSS 2021 data.
- Compare ANN, Logistic Regression, and Random Forest.
- Evaluate performance using accuracy, precision, recall, F1-score, and ROC-AUC.
- Examine differences in feature distributions between the two datasets.
- Present model predictions and research findings through a Streamlit web interface.

## Dataset

The project uses data from the **CDC Behavioral Risk Factor Surveillance System (BRFSS)**.

| Dataset | Purpose | Processed records |
|---|---|---:|
| BRFSS 2015 | Model training, validation, and testing | 364,815 |
| BRFSS 2021 | Temporal evaluation | 368,974 |

The processed datasets contain selected health and demographic features. The project uses the following input variables:

- General health
- Sex
- Age group
- Exercise
- Smoking history
- Body Mass Index (BMI)

The target variable represents diabetes status as defined by the project's data-processing pipeline.

**Dataset source:** [CDC BRFSS](https://www.cdc.gov/brfss/)

Note: Processed record counts reflect the project's filtering and preprocessing. They should not be interpreted as official CDC population prevalence estimates.

## Methodology

1. **Data preprocessing:** Extract relevant variables, clean records, handle missing or invalid values, and prepare the datasets.
2. **Feature preparation:** Select six health and demographic input features.
3. **Model development:** Train an ANN using BRFSS 2015 data and compare it with Logistic Regression and Random Forest.
4. **Validation and threshold selection:** Use validation data to select classification thresholds for the model comparison.
5. **Temporal evaluation:** Evaluate the trained models on BRFSS 2021 data.
6. **Performance analysis:** Compare classification metrics and investigate differences in feature distributions.
7. **Web application:** Use Streamlit to provide an interactive interface for predictions and research results.

## Results

### Baseline ANN: 2015 vs. 2021

The following results are from the baseline ANN evaluation at its default classification threshold.

| Metric | BRFSS 2015 test | BRFSS 2021 evaluation |
|---|---:|---:|
| Accuracy | 86.88% | 86.54% |
| Precision | 55.90% | 54.07% |
| Recall | 10.50% | 10.15% |
| F1-score | 17.68% | 17.09% |
| ROC-AUC | 81.90% | 80.78% |

The baseline ANN shows a small decrease in ROC-AUC from 2015 to 2021. However, its low recall at the default threshold means that many diabetes-positive cases are missed. Accuracy alone is therefore insufficient to assess its usefulness.

### Three-model comparison on BRFSS 2021

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| ANN | 78.97% | 34.33% | 59.00% | 43.41% | 80.60% |
| Logistic Regression | 77.41% | 32.58% | 60.99% | 42.48% | 79.97% |
| Random Forest | 76.30% | 30.64% | 58.03% | 40.10% | 77.10% |

These comparison results use validation-selected classification thresholds and are separate from the baseline ANN results above. The ANN achieved the highest F1-score and ROC-AUC among the three models in this comparison.

Differences in these results should be interpreted in the context of the chosen threshold, class imbalance, preprocessing, and evaluation design. Observed feature distribution differences do not, by themselves, prove that distribution shift caused a performance change.

## Web Application

The Streamlit application provides:

- An interactive diabetes prediction interface.
- A research novelty and methodology section.
- Model performance comparisons and result visualizations.
- Input fields for selected health and demographic features.

The predictions are research outputs, not medical diagnoses.

## Tech Stack

- **Language:** Python
- **Machine learning:** scikit-learn, Artificial Neural Networks
- **Data processing:** pandas, NumPy
- **Web application:** Streamlit
- **Visualization:** Matplotlib, Plotly
- **Model persistence:** joblib

## Project Structure

```text
diabetes-prediction-distribution-shift/
├── app/
│   └── app.py
├── models/
│   ├── ann_comparison.joblib
│   ├── logistic_regression_comparison.joblib
│   └── random_forest_comparison.joblib
├── results/
│   ├── model_comparison_all.csv
│   ├── final_model_comparison.csv
│   └── population_distribution_comparison.csv
├── requirements.txt
├── README.md
└── .gitignore
```

*Adjust this structure to match the files actually included in your repository. Model and results filenames may differ in your local version.*

## Installation and Setup

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/diabetes-prediction-distribution-shift.git
cd diabetes-prediction-distribution-shift
```

Replace `YOUR-USERNAME` with your GitHub username.

### 2. Create a virtual environment

Windows PowerShell:

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install streamlit pandas numpy scikit-learn matplotlib plotly joblib
```

Alternatively, if the repository includes a complete and tested `requirements.txt`:

```bash
pip install -r requirements.txt
```

### 4. Run the application

If the Streamlit entry point is `app/app.py`:

```bash
streamlit run app/app.py
```

If `app.py` is located in the repository root:

```bash
streamlit run app.py
```

Open the local URL displayed in your terminal, usually `http://localhost:8501`.

**Important:** Ensure the required trained model files and result CSV files exist at the paths expected by the application. The raw BRFSS datasets may need to be downloaded separately.

## Limitations

- The study evaluates temporal generalization between two survey years; it does not establish causal relationships.
- Results depend on preprocessing, selected features, class balance, and classification thresholds.
- Low recall in the baseline ANN indicates that many positive cases are missed at its default threshold.
- Survey sampling, weighting, missing-data handling, and target-label definitions can affect the interpretation of results.
- The application is intended for educational and research purposes and is not a clinically validated diagnostic tool.

## Future Scope

- Evaluate additional BRFSS years and external datasets.
- Investigate class imbalance and threshold-selection strategies.
- Conduct feature ablation and calibration experiments.
- Explore explainability techniques such as SHAP.
- Assess survey-weighted evaluation and subgroup performance.
- Improve model monitoring and reproducibility.

## Acknowledgements

The project uses public health survey data provided by the U.S. Centers for Disease Control and Prevention (CDC).

## Disclaimer

This project is for academic research and educational purposes only. It is not intended to diagnose diabetes, replace professional medical advice, or guide treatment decisions.

## License

Choose a license before publishing. The MIT License is a common option for open-source software, provided you have the rights to distribute all included code and artifacts.
