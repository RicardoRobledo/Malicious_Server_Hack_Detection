# 🛡️ Malicious Server Hack Prediction

## 📋 Project Description

This project develops a predictive model to identify patterns that indicate the probability of malicious server hacks. With the exponential growth of digital payments globally, cyberattacks have become increasingly frequent, where hackers can compromise data using only phone numbers linked to bank accounts.

**Objective:** Build an early detection system that allows cybersecurity teams to prevent attacks before they actually happen.

## 🎯 Target Variable

- **`MALICIOUS_OFFENSE`**: Indicates whether a server will be victim of a malicious hack

## 🗂️ Dataset

- **Source:** [Malicious Server Hack Dataset](https://www.kaggle.com/datasets/lplenka/malicious-server-hack)
- **Automatic download:** Using `kagglehub` for reproducibility
- **Variables:** Set of anonymous features that enable prediction

## 🔧 Methodology and Pipeline

### 1. Data Preprocessing
- **Missing value imputation:** `SimpleImputer` (median for numerical, mode for categorical)
- **Numerical variable scaling:** `StandardScaler`
- **Categorical encoding:** `OneHotEncoder` with unknown category handling
- **Modular architecture:** `ColumnTransformer` for parallel processing

### 2. Class Balancing
Exhaustive evaluation of balancing techniques:

**Undersampling Techniques:**
- TomekLinks
- EditedNearestNeighbours (ENN)
- RepeatedEditedNearestNeighbours (RENN)
- OneSidedSelection (OSS)
- NeighbourhoodCleaningRule (NCR)

**Oversampling Techniques:**
- RandomOverSampler
- **SMOTE** (Synthetic Minority Oversampling Technique)
- BorderlineSMOTE
- **ADASYN** (Adaptive Synthetic Sampling)

### 3. Models Evaluated
- **Logistic Regression (LR)**
- **Linear Discriminant Analysis (LDA)**
- **Random Forest (RF)**
- **Gradient Boosting (GB)** ⭐ *Best performance*
- **Support Vector Classifier (SVC)**
- **Gaussian Naive Bayes (NB)**

### 4. Probability Calibration
- **CalibratedClassifierCV** with isotonic method to obtain well-calibrated probabilities

## 📊 Main Results

### Model Performance (G-Mean):
| Model | Mean | Std. Deviation |
|-------|------|----------------|
| Gradient Boosting | **0.989** | 0.003 |
| Random Forest | 0.928 | 0.015 |
| SVC | 0.730 | 0.017 |
| LDA | 0.583 | 0.016 |
| Logistic Regression | 0.546 | 0.009 |
| Naive Bayes | 0.559 | 0.014 |

### Performance by Balancing Technique:
| Technique | G-Mean | Std. Deviation |
|-----------|--------|----------------|
| **RandomOverSampler** | **0.995** | 0.002 |
| SMOTE | 0.994 | 0.003 |
| BorderlineSMOTE | 0.994 | 0.003 |
| ADASYN | 0.994 | 0.003 |
| RENN | 0.992 | 0.003 |

### Final Model: Gradient Boosting + ADASYN + Calibration
- **Prediction distribution on test set:**
  - Class 0 (No hack): 8,004 instances (33.55%)
  - Class 1 (Hack): 7,899 instances (33.11%)

## 🛠️ Technologies and Libraries

```python
# Core ML
scikit-learn
imbalanced-learn
numpy
pandas

# Specific models
RandomForestClassifier
GradientBoostingClassifier
SVM, Logistic Regression, etc.

# Class balancing
SMOTE, ADASYN, TomekLinks, etc.

# Evaluation
RepeatedStratifiedKFold
geometric_mean_score
CalibratedClassifierCV
```

## 🎯 Evaluation Metrics

- **Main metric:** G-Mean (Geometric Mean Score)
- **Rationale:** Ideal for imbalanced classification problems
- **Validation:** Repeated stratified cross-validation (5 folds, 3 repeats)
- **Robustness:** Stability analysis across multiple runs

## 📈 Key Conclusions

1. **Gradient Boosting** proved to be the most effective model for this problem
2. **Oversampling** techniques consistently outperformed undersampling
3. **RandomOverSampler** achieved the best performance (G-Mean: 0.995)
4. **Probability calibration** improves prediction reliability
5. Pipeline is robust and generalizable for production data

## 🔮 Practical Applications

- **Preventive detection** of hacking attempts
- **Early alerts** for cybersecurity teams
- **Continuous monitoring** of server security
- **Risk-based optimization** of security resources

## 📝 Technical Notes

- Fully automated pipeline with `ColumnTransformer` and `imblearn.Pipeline`
- Robust handling of categorical and numerical data
- Exhaustive comparative evaluation of balancing techniques
- Modular and reusable code for different datasets

---

*This project is part of a comprehensive predictive cybersecurity system, designed to anticipate and prevent malicious attacks on critical infrastructure.*
