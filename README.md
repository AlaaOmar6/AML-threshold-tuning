<div align="center">

# 💰 AML Threshold Tuning & Fraud Detection

### *Anti-Money Laundering Transaction Analysis with Machine Learning*

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://python.org)
[![Pandas](https://img.shields.io/badge/Pandas-1.3+-green.svg)](https://pandas.pydata.org)
[![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-1.0+-orange.svg)](https://scikit-learn.org)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Completed-success.svg)]()

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Dataset](#-dataset)
- [Methodology](#-methodology)
- [Installation](#-installation)
- [Usage](#-usage)
- [Results](#-results)
- [Model Comparison](#-model-comparison)
- [Project Structure](#-project-structure)
- [Acknowledgments](#-acknowledgments)

---

## 🎯 Overview

This project implements a comprehensive **Anti-Money Laundering (AML) detection system** that analyzes financial transactions to identify suspicious activity. The approach combines:

- 📊 **Statistical threshold tuning** using percentile-based simulation
- 📈 **ROC curve analysis** with AUC evaluation
- 🤖 **Machine Learning models**: Random Forest & Neural Network
- ⚖️ **J-Statistic & F1-Score optimization** for threshold selection

> **Dataset:** [IBM AMLSim Example Dataset](https://www.kaggle.com/datasets/anshankul/ibm-amlsim-example-dataset)

---

## 📊 Dataset

### Source
- **Platform:** Kaggle
- **URL:** https://www.kaggle.com/datasets/anshankul/ibm-amlsim-example-dataset
- **Type:** Synthetic banking transaction data

### Files
| File | Description | Records |
|------|-------------|---------|
| `accounts.csv` | Account information with fraud labels | ~1,000 |
| `transactions.csv` | Transaction records (sender, receiver, amount) | ~100,000 |

### Features Engineered

| Feature | Description |
|---------|-------------|
| `CREDIT_AMT` | Total amount received |
| `CREDIT_COUNT` | Number of incoming transactions |
| `CREDIT_CTPY` | Number of unique senders |
| `DEBIT_AMT` | Total amount sent |
| `DEBIT_COUNT` | Number of outgoing transactions |
| `DEBIT_CTPY` | Number of unique receivers |
| `SUSPICIOUS` | Target variable (0=Legitimate, 1=Fraud) |

---

## 🔬 Methodology

### 1. Data Preprocessing
- Merge account and transaction data
- Aggregate transactions per account (credit & debit summaries)
- Handle missing values (fill with 0)

### 2. Exploratory Data Analysis
- Statistical distribution analysis
- Skewness measurement per class
- Visualization of feature distributions

### 3. Threshold Simulation
- Simulate thresholds from 1st to 99th percentile
- Calculate confusion matrix components (TP, FP, TN, FN)
- Evaluate using J-Statistic and F1-Score

### 4. Model Training
- **Random Forest** with balanced class weights
- **Neural Network (MLP)** with hidden layers (64, 32)
- Feature scaling with StandardScaler
- Stratified train-test split

### 5. Evaluation
- ROC curves with AUC
- Precision, Recall, F1-Score
- Confusion matrices
- Feature importance analysis

---

## ⚙️ Installation

### Prerequisites

- Python 3.8 or higher

### Setup

```bash
# Clone the repository
git clone https://github.com/yourusername/aml-threshold-tuning.git
cd aml-threshold-tuning

# Install dependencies
pip install -r requirements.txt
```

### requirements.txt

```
pandas>=1.3.0
numpy>=1.21.0
matplotlib>=3.5.0
seaborn>=0.11.0
scikit-learn>=1.0.0
joblib>=1.1.0
```

---

## 🚀 Usage

### 1. Prepare Data

Place the dataset files in the project root:
```
aml-threshold-tuning/
├── accounts.csv
├── transactions.csv
└── money_laundry.py
```

### 2. Run the Analysis

```bash
python money_laundry.py
```

This executes the complete pipeline:

1. **Data Loading** — reads accounts.csv and transactions.csv
2. **Feature Engineering** — aggregates credit/debit summaries per account
3. **EDA** — distribution analysis and visualization
4. **Threshold Simulation** — tests 99 percentile thresholds
5. **J-Statistic Optimization** — finds best threshold via Youden's Index
6. **F1-Score Optimization** — finds best threshold via F1-Score
7. **Test Validation** — validates chosen threshold on test set
8. **ROC Analysis** — compares all features with AUC
9. **ML Models** — trains Random Forest and Neural Network
10. **Model Comparison** — side-by-side evaluation

---

## 📈 Results

### Threshold Optimization

| Metric | Best Percentile | Threshold | TPR | FPR | F1-Score |
|--------|-----------------|-----------|-----|-----|----------|
| **J-Statistic** | ~85th | Variable | ~0.75 | ~0.15 | ~0.70 |
| **F1-Score** | ~90th | $12,412,189 | ~0.80 | ~0.20 | ~0.75 |

> **Final Recommendation:** F1-Score threshold adopted to minimize false negatives (missed fraud).

### Model Performance Comparison

| Model | Precision | Recall | F1-Score | ROC-AUC |
|-------|-----------|--------|----------|---------|
| **Random Forest** | ~0.85 | ~0.78 | ~0.81 | ~0.92 |
| **Neural Network** | ~0.82 | ~0.75 | ~0.78 | ~0.89 |

### Key Insights

- **CREDIT_AMT** is the most predictive feature for detecting suspicious accounts
- **Mean + 3SD threshold** is a fallacy for non-normal distributions
- **Random Forest** outperforms Neural Network on this tabular dataset
- **Class imbalance** requires careful threshold selection (not just accuracy)

---

## 🤖 Model Comparison

### Random Forest
- Handles non-linear relationships well
- Provides feature importance
- Robust to outliers
- Better for tabular data

### Neural Network (MLP)
- Learns complex patterns
- Requires more data
- Sensitive to feature scaling
- Good for high-dimensional data

### Threshold-Based (Baseline)
- Simple and interpretable
- No training required
- Fast inference
- Good starting point

---

## 📁 Project Structure

```
aml-threshold-tuning/
├── money_laundry.py              # Main implementation
├── README.md                      # This file
├── requirements.txt               # Python dependencies
├── .gitignore                     # Git ignore rules
├── .gitattributes                 # GitHub language detection
├── accounts.csv                   # Dataset (not in repo)
├── transactions.csv               # Dataset (not in repo)
├── rf_aml_model.pkl               # Saved Random Forest model
├── scaler.pkl                     # Saved StandardScaler
├── rf_roc_curve.png               # ROC curve visualization
├── feature_importance.png         # Feature importance plot
└── outputs/                       # Generated visualizations
```

---

## 🎓 Acknowledgments

- **Dataset:** [IBM AMLSim](https://www.kaggle.com/datasets/anshankul/ibm-amlsim-example-dataset) — Synthetic AML dataset
- **Libraries:** Pandas, Scikit-Learn, Matplotlib, Seaborn
- **Techniques:** Youden's J-Statistic, ROC Analysis, Threshold Optimization

---

<div align="center">

**⭐ Star this repo if you found it helpful!**

</div>
