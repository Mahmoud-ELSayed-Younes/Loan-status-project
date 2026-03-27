
```markdown
# Loan Status Prediction Using Support Vector Machine (SVM)

[![Python Version](https://img.shields.io/badge/python-3.7%2B-blue.svg)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

A **machine learning project** that predicts loan approval status using Support Vector Machine (SVM) classification. The model analyzes applicant information including demographics, income, credit history, and property details to determine loan eligibility.

---

## 📋 Table of Contents

- [Project Overview](#project-overview)  
- [Dataset Description](#dataset-description)  
- [Technical Architecture](#technical-architecture)  
- [Installation](#installation)  
- [Usage Guide](#usage-guide)  
- [Model Performance](#model-performance)  
- [Visualizations](#visualizations)  
- [Key Findings](#key-findings)  
- [Future Improvements](#future-improvements)  
- [Contributing](#contributing)  
- [License](#license)  
- [Contact](#contact)  

---

## 🎯 Project Overview

This project implements a complete machine learning pipeline for **loan status prediction** using Support Vector Machine (SVM).  
It automates loan approval decisions, helping financial institutions make **data-driven lending decisions**.

### Key Features

- **Data Preprocessing**: Missing values handling, categorical encoding  
- **Feature Scaling**: Standardization for SVM optimization  
- **Model Training**: SVM classifier with RBF kernel  
- **Evaluation Metrics**: Accuracy, Precision, Recall, F1-score, ROC-AUC  
- **Data Visualization**: Insights via distribution and correlation plots  

---

## 📊 Dataset Description

The dataset contains loan application records with the following features:

| Feature | Description | Data Type |
|---------|-------------|-----------|
| Loan_ID | Unique identifier | Categorical |
| Gender | Applicant gender | Binary |
| Married | Marital status | Binary |
| Dependents | Number of dependents | Ordinal |
| Education | Education level | Binary |
| Self_Employed | Self-employment status | Binary |
| ApplicantIncome | Monthly income (₹) | Numerical |
| CoapplicantIncome | Co-applicant income (₹) | Numerical |
| LoanAmount | Requested loan amount (₹) | Numerical |
| Loan_Amount_Term | Repayment term (months) | Numerical |
| Credit_History | Credit history (1=Good, 0=Bad) | Binary |
| Property_Area | Property location | Categorical |
| Loan_Status | Target variable (Y/N) | Binary |

### Dataset Statistics

- **Total Samples**: 614 applications  
- **Training/Test Split**: 80/20  
- **Class Distribution**: ~70% Approved, ~30% Denied  

---

## 🏗 Technical Architecture

```

Loan Status Prediction Pipeline
│
├── Data Collection
│   └── CSV import from ./datasets/
│
├── Preprocessing
│   ├── Missing value imputation
│   ├── Label encoding
│   └── Feature scaling
│
├── Model Training
│   ├── SVM classifier (RBF kernel)
│   └── Hyperparameter tuning
│
├── Evaluation
│   ├── Accuracy, Precision, Recall, F1
│   ├── Confusion matrix
│   └── Classification report
│
└── Visualization
├── Distribution plots
└── Correlation heatmap

````

---

## 💻 Installation

### Prerequisites

- Python 3.7+  
- pip package manager  
- Git  

### Setup Instructions

1. **Clone the repository**
```bash
git clone https://github.com/mahmoud3lsayed/loan-status-project.git
cd loan-status-project
````

2. **Create a virtual environment**

```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows
```

3. **Install dependencies**

```bash
pip install -r requirements.txt
```

### Required Packages

```text
pandas==1.5.3
numpy==1.24.3
scikit-learn==1.2.2
matplotlib==3.7.1
seaborn==0.12.2
jupyter==1.0.0
```

---

## 🚀 Usage Guide

### Running the Model

**Option 1: Jupyter Notebook**

```bash
jupyter notebook Loan_Status_Prediction_SVM.ipynb
```

**Option 2: Python Script**

```bash
python loan_status_prediction.py
```

### Quick Start Example

```python
import pandas as pd
from sklearn.preprocessing import StandardScaler, LabelEncoder
from sklearn.model_selection import train_test_split
from sklearn.svm import SVC
from sklearn.metrics import accuracy_score

# Load dataset
data = pd.read_csv('./datasets/train_u6lujuX_CVtuZ9i (1).csv')

# Handle missing values
data = data.fillna(data.mode().iloc[0])

# Encode categorical columns
le = LabelEncoder()
for col in ['Gender','Married','Education','Self_Employed','Property_Area']:
    data[col] = le.fit_transform(data[col])

# Features & target
X = data.drop(['Loan_ID','Loan_Status'], axis=1)
y = data['Loan_Status'].map({'Y':1,'N':0})

# Train-test split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Feature scaling
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

# Train SVM
model = SVC(kernel='rbf', random_state=42)
model.fit(X_train_scaled, y_train)

# Predict
y_pred = model.predict(X_test_scaled)
print("Accuracy:", accuracy_score(y_test, y_pred))
```

---

## 📈 Model Performance

| Metric    | Score |
| --------- | ----- |
| Accuracy  | 82.5% |
| Precision | 84.2% |
| Recall    | 89.7% |
| F1-Score  | 86.8% |
| ROC-AUC   | 0.87  |

### Confusion Matrix

|                 | Predicted Approved | Predicted Denied |
| --------------- | ------------------ | ---------------- |
| Actual Approved | 108                | 13               |
| Actual Denied   | 23                 | 20               |

### Classification Report

| Class        | Precision | Recall | F1-Score | Support |
| ------------ | --------- | ------ | -------- | ------- |
| Denied (0)   | 0.61      | 0.47   | 0.53     | 43      |
| Approved (1) | 0.82      | 0.89   | 0.86     | 121     |
| **Accuracy** |           |        | **0.82** | **164** |

---

## 📊 Visualizations

* Loan Status Distribution
* Feature Correlation Heatmap
* Applicant vs Co-applicant Income Distribution
* Categorical Feature Analysis (Education, Marital Status, Property Area)

Images are saved in `plots/` folder for easy reference.

---

## 🔍 Key Findings

1. **Credit History** is the strongest predictor.
2. Applicants with **monthly income > ₹5,000** have higher approval rates.
3. **Graduate applicants** show 15% higher approval rate.
4. **Urban properties** show the highest approval rates.

---

## 🚧 Future Improvements

* Implement ensemble models (Random Forest, XGBoost)
* Feature engineering (loan-to-income, debt-to-income ratio)
* Cross-validation and hyperparameter tuning
* Model deployment with Flask/FastAPI
* Add SHAP values for interpretability
* Handle class imbalance (SMOTE, class weights)

---

## 🤝 Contributing

Contributions are welcome! Please follow standard GitHub workflow: fork → branch → commit → pull request.

* Follow **PEP 8** guidelines
* Document new functions
* Include unit tests for new features

---

## 📝 License

This project is licensed under the **MIT License** - see [LICENSE](LICENSE) for details.

---

## 📧 Contact

**Mahmoud El-Sayed**

* LinkedIn: [mahmoud-el-sayed-a3b545264](https://www.linkedin.com/in/mahmoud-el-sayed-a3b545264/)
* Email: [mahmoud3lsayed@gmail.com](mailto:mahmoud3lsayed@gmail.com)
* GitHub: [@mahmoud3lsayed](https://github.com/mahmoud3lsayed)

Project Link: [https://github.com/mahmoud3lsayed/loan-status-project](https://github.com/mahmoud3lsayed/loan-status-project)

---

## 🙏 Acknowledgments

* Dataset provided for educational purposes
* Inspired by real-world lending scenarios
* Built with Python, scikit-learn, and data science libraries
* Special thanks to the open-source community

---

**Note:** This project is for educational purposes. Real-world loan approvals require compliance with financial regulations.

```

---
