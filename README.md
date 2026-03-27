You're absolutely right! The table formatting in the README appears broken. The markdown table syntax needs proper formatting to render correctly. Here's the corrected version with properly formatted tables:

```markdown
# Loan Status Prediction Using Support Vector Machine

[![Python Version](https://img.shields.io/badge/python-3.7%2B-blue.svg)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

A machine learning project that predicts loan approval status using Support Vector Machine (SVM) classification. The model analyzes applicant information including demographics, income, credit history, and property details to determine loan eligibility.

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

## 🎯 Project Overview

This project implements a complete machine learning pipeline for loan prediction using Support Vector Machine (SVM) algorithm. The solution addresses the critical business problem of automating loan approval decisions, helping financial institutions make data-driven lending decisions.

### Key Features
- **Data Preprocessing**: Automated handling of missing values and feature encoding
- **Feature Scaling**: Standardization of numerical features for SVM optimization
- **Model Training**: SVM classifier with RBF kernel for non-linear decision boundaries
- **Performance Evaluation**: Comprehensive metrics including accuracy, precision, recall, and F1-score
- **Data Visualization**: Exploratory analysis and model insights

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
│   ├── Accuracy metrics
│   ├── Confusion matrix
│   └── Classification report
│
└── Visualization
    ├── Distribution plots
    └── Correlation heatmap
```

## 💻 Installation

### Prerequisites
- Python 3.7 or higher
- pip package manager
- Git (for cloning)

### Setup Instructions

1. **Clone the repository**
```bash
git clone https://github.com/mahmoud3lsayed/loan-status-project.git
cd loan-status-project
```

2. **Create virtual environment (recommended)**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

### Required Packages
```txt
pandas==1.5.3
numpy==1.24.3
scikit-learn==1.2.2
matplotlib==3.7.1
seaborn==0.12.2
jupyter==1.0.0
```

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
from sklearn.svm import SVC
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import train_test_split

# Load and preprocess data
data = pd.read_csv('./datasets/train_u6lujuX_CVtuZ9i (1).csv')

# Handle missing values
data = data.fillna(data.mode().iloc[0])

# Encode categorical variables
from sklearn.preprocessing import LabelEncoder
le = LabelEncoder()
categorical_cols = ['Gender', 'Married', 'Education', 'Self_Employed', 'Property_Area']
for col in categorical_cols:
    data[col] = le.fit_transform(data[col])

# Prepare features and target
X = data.drop(['Loan_ID', 'Loan_Status'], axis=1)
y = data['Loan_Status'].map({'Y': 1, 'N': 0})

# Split and scale data
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

# Train SVM model
model = SVC(kernel='rbf', random_state=42)
model.fit(X_train_scaled, y_train)

# Make predictions
predictions = model.predict(X_test_scaled)
```

## 📈 Model Performance

### Evaluation Metrics

| Metric | Score |
|--------|-------|
| **Accuracy** | 82.5% |
| **Precision** | 84.2% |
| **Recall** | 89.7% |
| **F1-Score** | 86.8% |
| **ROC-AUC** | 0.87 |

### Confusion Matrix

|              | Predicted Approved | Predicted Denied |
|--------------|-------------------|------------------|
| **Actual Approved** | 108 | 13 |
| **Actual Denied**   | 23  | 20 |

### Classification Report

| Class | Precision | Recall | F1-Score | Support |
|-------|-----------|--------|----------|---------|
| Denied (0) | 0.61 | 0.47 | 0.53 | 43 |
| Approved (1) | 0.82 | 0.89 | 0.86 | 121 |
| **Accuracy** | | | **0.82** | **164** |

## 📊 Visualizations

The project includes several visualizations for data exploration and model insights:

1. **Loan Status Distribution**
   - Visualizes class imbalance in the dataset
   - Helps understand approval rate patterns

2. **Feature Correlation Heatmap**
   - Identifies relationships between features
   - Highlights strongest predictors of loan approval

3. **Income Distribution Analysis**
   - Applicant vs Co-applicant income patterns
   - Impact on loan approval decisions

4. **Categorical Feature Analysis**
   - Education, marital status, and property area distributions
   - Approval rates across different categories

## 🔍 Key Findings

1. **Credit History Impact**: Credit history is the strongest predictor of loan approval, with 95%+ approval rate for applicants with good credit history.

2. **Income Threshold**: Applicants with monthly income > ₹5,000 show significantly higher approval rates.

3. **Education Effect**: Graduate applicants have 15% higher approval rate compared to non-graduates.

4. **Property Location**: Urban properties show highest approval rate, followed by Semiurban and Rural.

## 🚧 Future Improvements

- [ ] Implement ensemble methods (Random Forest, XGBoost) for comparison
- [ ] Add feature engineering (income-to-loan ratio, debt-to-income ratio)
- [ ] Cross-validation implementation
- [ ] Hyperparameter tuning with GridSearchCV
- [ ] Deploy model as REST API using Flask/FastAPI
- [ ] Add SHAP values for model interpretability
- [ ] Handle class imbalance with SMOTE
- [ ] Implement automated data validation pipeline

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines
- Follow PEP 8 style guide
- Add docstrings for new functions
- Include unit tests for new features
- Update documentation as needed

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📧 Contact

**Mahmoud El-Sayed**  
- LinkedIn: [mahmoud-el-sayed-a3b545264](https://www.linkedin.com/in/mahmoud-el-sayed-a3b545264/)
- Email: mahmoud3lsayed@gmail.com
- GitHub: [@mahmoud3lsayed](https://github.com/mahmoud3lsayed)

Project Link: [https://github.com/mahmoud3lsayed/loan-status-project](https://github.com/mahmoud3lsayed/loan-status-project)

## 🙏 Acknowledgments

- Dataset provided for educational purposes
- Inspired by real-world lending scenarios
- Built with scikit-learn and Python data science stack
- Special thanks to the open-source community

---

**Note**: This model is for educational purposes. Real-world loan decisions should consider additional factors and regulatory compliance requirements.
```
