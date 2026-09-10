# insurance-claim-prediction
ML-powered insurance claim prediction and risk analytics dashboard built with React, TypeScript, and Logistic Regression &amp; Random Forest.
# Insurance Claim Risk Analytics & Prediction

An interactive **machine learning web application for insurance claim prediction, risk analytics, and model evaluation**.

The application processes historical insurance policy data, performs data cleaning and feature engineering, trains **Logistic Regression** and **Random Forest** classifiers directly in the browser, and provides an interactive dashboard for exploring claim patterns and predicting individual claim likelihood.

> **Disclaimer:** This project is intended for educational, analytical, and decision-support purposes only. Predictions should not be treated as actual underwriting, insurance, financial, or legal decisions.

---

##  Project Overview

Insurance companies need to understand which policyholders are more likely to file claims in order to analyze portfolio risk and improve decision-making.

This project demonstrates an end-to-end machine learning workflow:

**Raw Insurance Data → Data Cleaning → Feature Engineering → Encoding → Model Training → Model Evaluation → Risk Prediction → Interactive Analytics**

The application provides both **portfolio-level analysis** and **individual policy-level prediction** through a modern web dashboard.

---

##  Features

###  Interactive Dashboard

The dashboard provides an overview of the insurance portfolio, including:

* Total policies
* Total claims
* No-claim policies
* Overall claim rate
* Average annual premium
* Average customer age
* Average policy tenure
* Model performance summary

It also provides visualizations for:

* Claim vs. no-claim distribution
* Claims by policy type
* Claim rate by customer age group
* Claims by vehicle type
* Premium ranges
* Previous claim history
* Accident history

---

###  Machine Learning Models

Two classification algorithms are implemented from scratch in TypeScript:

#### Logistic Regression

A linear classification model used as an interpretable baseline for predicting claim probability.

#### Random Forest

An ensemble-based classification model designed to capture nonlinear relationships between policyholder and vehicle characteristics.

The application automatically compares both models using a weighted combination of:

* F1 Score
* ROC-AUC

The model with the higher combined score is selected as the **best-performing model**.

---

##  Individual Claim Prediction

The Claim Predictor allows users to enter policyholder information and estimate the probability of an insurance claim.

Prediction inputs include:

* Customer age
* Gender
* Policy type
* Vehicle type
* Vehicle age
* Annual income
* Policy tenure
* Premium amount
* Coverage amount
* Previous claims
* Accident history
* Driving experience
* Vehicle usage
* Claim history

The application returns:

* Claim probability
* No-claim probability
* Predicted class
* Prediction confidence
* Model used
* Classification threshold
* Key factors associated with the prediction

Users can select either **Logistic Regression** or **Random Forest** for prediction.

---

##  Model Evaluation

The Model Performance section provides detailed evaluation of both classifiers.

Metrics include:

* Accuracy
* Precision
* Recall
* F1 Score
* ROC-AUC
* Confusion Matrix

The application also provides an interactive **classification threshold slider**, allowing users to observe how changing the probability threshold affects model performance.

This makes it possible to explore the trade-off between false positives and false negatives.

---

##  Feature Engineering

The project creates additional features from the raw insurance data.

### Derived Features

#### Age Group

Customers are grouped into:

* Young Adult (<25)
* Adult (25-39)
* Middle Age (40-54)
* Senior (55+)

#### Vehicle Age Group

Vehicles are categorized as:

* New (0-2 years)
* Moderately Used (3-7 years)
* Older (8+ years)

#### Driving Experience Group

Drivers are categorized as:

* Novice (<3 years)
* Intermediate (3-7 years)
* Experienced (8+ years)

#### Premium-to-Coverage Ratio

A derived numerical feature:

`Premium Amount / Coverage Amount`

#### Binary Indicators

The pipeline also creates numerical indicators for:

* Accident history
* Claim history

---

##  Data Preprocessing

The application includes a complete preprocessing pipeline.

### Target Normalization

The target `claim` field supports multiple representations, including:

* `0`
* `1`
* `Yes`
* `No`
* `Claim`
* `No Claim`
* `True`
* `False`

These values are normalized into binary classes:

* `0` → No Claim
* `1` → Claim

### Categorical Normalization

The preprocessing pipeline also normalizes categorical fields such as:

* Gender
* Vehicle usage
* Accident history
* Claim history

For example, different capitalization formats such as `male`, `Male`, and `MALE` are normalized to a consistent representation.

### Missing Values

The application handles missing numerical values using **median imputation** and missing categorical values using **mode-based imputation**.

### Data Validation

The preprocessing pipeline also:

* Removes records without a valid policy ID
* Removes duplicate policy IDs
* Removes records with an invalid claim target
* Applies sensible value boundaries to numerical fields

---

##  Feature Encoding

Before model training:

### Numerical Features

Numerical variables are standardized using Z-score normalization:

`z = (x - μ) / σ`

### Categorical Features

Categorical variables are transformed using **one-hot encoding**.

The resulting feature vector combines:

* Standardized numerical variables
* One-hot encoded categorical variables

This allows both machine learning models to operate on a consistent numerical feature space.

---

##  Model Training

The dataset is divided using a **stratified 80/20 train-test split**.

* **80%** → Training data
* **20%** → Testing data

Stratification ensures that the relative distribution of claim and no-claim records is maintained across the training and testing partitions.

The test set is kept separate for model evaluation.

---

##  Dataset

The project contains an insurance claims dataset located at:

```text
public/data/insurance_claims.csv
```

The dataset contains **650 policy records** and 16 columns.

### Dataset Features

| Feature              | Description                                |
| -------------------- | ------------------------------------------ |
| `policy_id`          | Unique policy identifier                   |
| `customer_age`       | Age of the customer                        |
| `gender`             | Customer gender                            |
| `policy_type`        | Type of insurance policy                   |
| `vehicle_type`       | Type of vehicle                            |
| `vehicle_age`        | Age of the vehicle                         |
| `annual_income`      | Customer annual income                     |
| `policy_tenure`      | Number of years the policy has been active |
| `premium_amount`     | Annual insurance premium                   |
| `coverage_amount`    | Insurance coverage amount                  |
| `previous_claims`    | Number of previous claims                  |
| `accident_history`   | Previous accident history                  |
| `driving_experience` | Years of driving experience                |
| `vehicle_usage`      | Personal, Commercial, or Mixed usage       |
| `claim_history`      | Historical claim indicator                 |
| `claim`              | Target variable                            |

The target variable is converted into a binary classification problem:

```text
0 = No Claim
1 = Claim
```

---

##  Project Architecture

```text
insurance-claim-prediction/
│
├── public/
│   └── data/
│       └── insurance_claims.csv
│
├── src/
│   ├── components/
│   │   ├── ClaimPredictionForm.tsx
│   │   ├── PredictionResult.tsx
│   │   ├── ModelMetricsTable.tsx
│   │   ├── ConfusionMatrix.tsx
│   │   ├── FeatureImportanceChart.tsx
│   │   ├── ProbabilityDistributionChart.tsx
│   │   ├── ThresholdSlider.tsx
│   │   ├── PolicyTable.tsx
│   │   └── ...
│   │
│   ├── ml/
│   │   ├── logisticRegression.ts
│   │   ├── randomForest.ts
│   │   ├── modelTraining.ts
│   │   ├── preprocessing.ts
│   │   ├── featureEngineering.ts
│   │   ├── encoding.ts
│   │   └── metrics.ts
│   │
│   ├── pages/
│   │   ├── Dashboard.tsx
│   │   ├── ClaimPredictor.tsx
│   │   ├── InsuranceAnalysis.tsx
│   │   └── ModelPerformance.tsx
│   │
│   ├── utils/
│   │   ├── insuranceAnalysis.ts
│   │   ├── insights.ts
│   │   └── reportGenerator.ts
│   │
│   ├── App.tsx
│   ├── main.tsx
│   ├── types.ts
│   └── index.css
│
├── package.json
├── tsconfig.json
├── vite.config.ts
└── README.md
```

---

##  Tech Stack

### Frontend

* React
* TypeScript
* Vite
* Tailwind CSS

### Machine Learning

* Logistic Regression
* Random Forest
* Custom TypeScript ML implementations
* Feature engineering
* One-hot encoding
* Numerical standardization
* Stratified train/test split

### Data Processing

* Papa Parse
* CSV-based dataset processing

### Visualization

* Recharts

### UI & Utilities

* Lucide React
* Motion
* jsPDF
* html2canvas

---

##  Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/insurance-claim-prediction.git
```

Navigate into the project:

```bash
cd insurance-claim-prediction
```

### 2. Install dependencies

Using npm:

```bash
npm install
```

Or using Bun:

```bash
bun install
```

### 3. Start the development server

```bash
npm run dev
```

The application will be available through the Vite development server.

---

##  Available Scripts

### Development

```bash
npm run dev
```

Starts the Vite development server.

### Production Build

```bash
npm run build
```

Creates an optimized production build.

### Preview

```bash
npm run preview
```

Previews the production build locally.

### Type Checking

```bash
npm run lint
```

Runs TypeScript type checking without emitting files.

### Clean

```bash
npm run clean
```

Removes generated build/server artifacts.

---

##  Application Workflow

```text
                ┌─────────────────────┐
                │ Insurance CSV Data  │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │ Data Preprocessing   │
                │ & Validation         │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │ Feature Engineering  │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │ Encoding & Scaling   │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │ Stratified 80/20     │
                │ Train/Test Split     │
                └──────────┬──────────┘
                           │
                ┌──────────┴──────────┐
                ▼                     ▼
       ┌─────────────────┐   ┌─────────────────┐
       │ Logistic        │   │ Random Forest   │
       │ Regression      │   │ Classifier      │
       └────────┬────────┘   └────────┬────────┘
                │                     │
                └──────────┬──────────┘
                           ▼
                ┌─────────────────────┐
                │ Model Evaluation     │
                │ F1 / ROC-AUC / etc. │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │ Risk Prediction &    │
                │ Analytics Dashboard  │
                └─────────────────────┘
```

---

##  Main Application Sections

### 1. Dashboard

Provides a high-level overview of the insurance portfolio and historical claim behavior.

### 2. Claim Predictor

Allows users to enter individual policyholder information and generate a claim likelihood prediction.

### 3. Insurance Analysis

Provides deeper statistical analysis of claims across:

* Policy types
* Vehicle types
* Customer age groups
* Premium ranges
* Previous claim counts
* Accident history
* Vehicle age
* Policy tenure

### 4. Model Performance

Provides model benchmarking and diagnostics, including:

* Model comparison
* Classification metrics
* Confusion matrices
* Probability distributions
* Feature importance
* Threshold sensitivity
* Dynamic model insights

---

##  PDF Reporting

The application includes a PDF report generator that summarizes:

* Portfolio statistics
* Dataset information
* Data preprocessing
* Claim patterns
* Model performance
* Analytical insights
* Prediction information

This allows users to export the results of the analysis into a structured report.

---

##  Key Learning Outcomes

This project demonstrates practical implementation of:

* End-to-end machine learning workflows
* Binary classification
* Data preprocessing
* Handling inconsistent categorical data
* Missing-value imputation
* Feature engineering
* Feature scaling
* One-hot encoding
* Stratified sampling
* Logistic Regression
* Random Forest
* Classification metrics
* Threshold optimization
* Feature importance analysis
* Interactive data visualization
* Client-side machine learning
* React + TypeScript application development

---

##  Limitations

This project is primarily designed as a **machine learning demonstration and analytical dashboard**.

Important limitations include:

* The dataset is relatively small.
* Model training occurs in the browser.
* Results depend on the provided historical dataset.
* The train/test split uses randomized shuffling.
* Prediction probabilities should not be interpreted as guaranteed outcomes.
* The model does not represent a production insurance underwriting system.
* Additional validation and monitoring would be required for real-world deployment.

---

##  Future Improvements

Potential improvements include:

* Cross-validation
* Hyperparameter optimization
* Additional classification algorithms
* XGBoost/Gradient Boosting comparison
* ROC and Precision-Recall curves
* Calibration analysis
* SHAP-style explainability
* Model persistence and versioning
* Backend model serving
* Database integration
* Authentication and user management
* Automated model retraining
* Production monitoring
* Fairness and bias evaluation
* Larger real-world datasets

---

##  Author

**Chaithanya**

This project was developed as a machine learning and frontend analytics application demonstrating how predictive modeling can be integrated into an interactive web interface.

---

##  License

Add your preferred license here, for example:

```text
MIT License
```

If you plan to make the repository public, adding an explicit `LICENSE` file is recommended.
