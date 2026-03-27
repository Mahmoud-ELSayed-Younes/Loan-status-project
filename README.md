````markdown
# Loan Prediction Using SVM

## Overview
This project predicts whether a loan will be approved or denied based on applicant information using a **Support Vector Machine (SVM)** classifier.  
The dataset includes applicant demographics, employment, income, and property area information.  

The workflow includes:
1. Data collection & preprocessing
2. Handling missing values
3. Label encoding categorical features
4. Feature scaling
5. Training an SVM classifier
6. Evaluating the model on train & test sets
7. Data visualization

---

## Dataset
- **Source:** The dataset is in `./datasets/train_u6lujuX_CVtuZ9i (1).csv`
- **Columns:**
  - `Loan_ID` : Unique loan identifier
  - `Gender` : Male / Female
  - `Married` : Yes / No
  - `Dependents` : Number of dependents (0,1,2,3+)
  - `Education` : Graduate / Not Graduate
  - `Self_Employed` : Yes / No
  - `ApplicantIncome` : Applicant income
  - `CoapplicantIncome` : Co-applicant income
  - `LoanAmount` : Loan amount
  - `Loan_Amount_Term` : Term of loan in months
  - `Credit_History` : 1 / 0
  - `Property_Area` : Urban / Semiurban / Rural
  - `Loan_Status` : Target variable (Y / N)

---

## Installation

Clone this repository:

```bash
git clone https://github.com/your-username/loan-prediction-svm.git
cd loan-prediction-svm
````

Create a virtual environment and install dependencies:

```bash
python -m venv venv
source venv/bin/activate   # Linux/Mac
venv\Scripts\activate      # Windows

pip install -r requirements.txt
```

**requirements.txt** should include:

```
numpy
pandas
scikit-learn
matplotlib
seaborn
```

---

## Data Preprocessing

* Drop rows with missing values.
* Convert categorical features to numeric using **label encoding**:

  * `Loan_Status`: Y → 1, N → 0
  * `Married`: Yes → 1, No → 0
  * `Education`: Graduate → 1, Not Graduate → 0
  * `Gender`: Male → 1, Female → 0
  * `Self_Employed`: Yes → 1, No → 0
  * `Property_Area`: Rural → 0, Urban → 1, Semiurban → 2
* Replace `3+` in `Dependents` with 4 and convert to numeric.
* Separate features (`X`) and target (`y`).

---

## Model Training

1. **Train-test split:** 90% training, 10% testing, stratified by `Loan_Status`.
2. **Scaling features:** StandardScaler used to normalize numeric features.
3. **Model:** SVM classifier with linear kernel.
4. **Evaluation:** Accuracy, precision, recall, F1-score.

```python
from sklearn.preprocessing import StandardScaler
from sklearn.svm import SVC
from sklearn.metrics import accuracy_score, classification_report

scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

model = SVC(kernel="linear", random_state=42)
model.fit(X_train_scaled, y_train)

y_pred = model.predict(X_test_scaled)
print("Accuracy:", accuracy_score(y_test, y_pred))
print(classification_report(y_test, y_pred))
```

---

## Data Visualization

Some visualizations of features vs `Loan_Status`:

![Loan Status by Education](plots/loan_status_by_education.png)
![Loan Status by Marital Status](plots/loan_status_by_married.png)
![Loan Status by Property Area](plots/loan_status_by_property_area.png)

---

## Model Performance

| Dataset | Accuracy |
| ------- | -------- |
| Train   | 0.84     |
| Test    | 0.79     |

**Classification Report (Test set):**

* **Class 0 (Loan Denied):** Precision 0.86, Recall 0.40, F1-score 0.55
* **Class 1 (Loan Approved):** Precision 0.78, Recall 0.97, F1-score 0.86

**Insights:**

* The model is better at predicting approved loans than denied loans.
* Can improve minority class prediction with **class balancing** or oversampling techniques.

---

## Future Improvements

* Handle missing values more intelligently instead of dropping rows.
* Use **SMOTE** or class weights to improve minority class prediction.
* Try other classifiers like **Random Forest** or **XGBoost**.
* Hyperparameter tuning using **GridSearchCV** for SVM.
* Feature engineering (e.g., income ratios, loan-to-income ratios).

---

## License

This project is licensed under the MIT License.

---



---
