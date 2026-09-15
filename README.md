# insurance-claim-prediction
Interactive insurance claim prediction and risk analytics dashboard using Logistic Regression and Random Forest with React, TypeScript, and in-browser machine learning.
#  Insurance Claim Prediction & Risk Analytics

An interactive **Insurance Claim Prediction and Risk Analytics** web application built with **React, TypeScript, and Vite**.

The application loads historical insurance policy data, preprocesses and engineers features, trains **Logistic Regression** and **Random Forest** classification models directly in the browser, evaluates their performance, and provides an interactive interface for predicting the probability of an insurance claim.

##  Features

*  Interactive insurance analytics dashboard
*  Logistic Regression classification
*  Random Forest classification
*  Individual insurance claim prediction
*  Model performance comparison
*  claim probability and risk prediction
*  Feature importance analysis
*  Confusion matrix visualization
*  ROC-AUC, Accuracy, Precision, Recall, and F1-score
*  Adjustable prediction threshold
*  Insurance CSV dataset processing
*  Policy and claim analysis
*  PDF insurance analytics report generation
*  Machine learning executed directly in the browser
*  Responsive React interface

##  Machine Learning

The project performs binary classification:

```text
0 → No Claim
1 → Claim
```

Two classification models are implemented and compared:

### Logistic Regression

A custom Logistic Regression implementation is used to estimate the probability of an insurance claim.

The model uses:

* Gradient-based optimization
* Sigmoid probability calculation
* L2 regularization
* Feature coefficients for importance analysis

### Random Forest

A custom Random Forest implementation is included using multiple decision trees.

The implementation uses:

* Bootstrap sampling
* Random feature selection
* Decision trees
* Gini impurity
* Maximum tree depth
* Aggregated tree probabilities
* Gini-based feature importance

The application automatically selects the better-performing model based on a weighted combination of:

```text
F1 Score × 60%
ROC-AUC × 40%
```

##  Dataset

The project includes an insurance claims dataset containing **650 policy records** and **16 columns**.

### Dataset Features

| Feature              | Description                                  |
| -------------------- | -------------------------------------------- |
| `policy_id`          | Unique insurance policy identifier           |
| `customer_age`       | Age of the policyholder                      |
| `gender`             | Customer gender                              |
| `policy_type`        | Type of insurance policy                     |
| `vehicle_type`       | Type of insured vehicle                      |
| `vehicle_age`        | Age of the vehicle                           |
| `annual_income`      | Customer's annual income                     |
| `policy_tenure`      | Duration of the policy                       |
| `premium_amount`     | Insurance premium amount                     |
| `coverage_amount`    | Policy coverage amount                       |
| `previous_claims`    | Number of previous claims                    |
| `accident_history`   | Whether the customer has an accident history |
| `driving_experience` | Years of driving experience                  |
| `vehicle_usage`      | Personal, commercial, or mixed usage         |
| `claim_history`      | Previous claim history                       |
| `claim`              | Target variable                              |

### Target Variable

```text
0 = No Claim
1 = Claim
```

The preprocessing pipeline also supports common textual representations such as `Yes`, `No`, `Claim`, and `No Claim`.

##  Data Preprocessing

Before model training, the application performs several preprocessing steps:

1. Parses the CSV dataset using Papa Parse
2. Removes invalid records
3. Removes duplicate policy IDs
4. Normalizes categorical values
5. Handles missing numerical values using median imputation
6. Handles missing categorical values using mode imputation
7. Normalizes the target claim variable
8. Applies reasonable value boundaries
9. Engineers additional features
10. Encodes categorical variables
11. Standardizes numerical features

##  Feature Engineering

Additional features are derived from the original policy information.

### Age Group

```text
Young Adult (<25)
Adult (25-39)
Middle Age (40-54)
Senior (55+)
```

### Vehicle Age Group

```text
New (0-2 yrs)
Moderately Used (3-7 yrs)
Older (8+ yrs)
```

### Driving Experience Group

```text
Novice (<3 yrs)
Intermediate (3-7 yrs)
Experienced (8+ yrs)
```

### Additional Numerical Features

* `premium_to_coverage_ratio`
* `accident_indicator`
* `claim_history_indicator`

These engineered features help the models capture additional relationships within the insurance data.

##  Model Training Pipeline

The overall machine learning workflow is:

```text
Insurance CSV
      ↓
Data Validation
      ↓
Cleaning & Normalization
      ↓
Feature Engineering
      ↓
Categorical Encoding
      ↓
Numerical Standardization
      ↓
Stratified 80/20 Train-Test Split
      ↓
┌──────────────────────┐
│ Logistic Regression  │
└──────────────────────┘
      ↓
Model Evaluation

┌──────────────────────┐
│ Random Forest        │
└──────────────────────┘
      ↓
Model Evaluation
      ↓
Model Comparison
      ↓
Best Model Selection
      ↓
Claim Prediction
```

##  Model Evaluation

The application evaluates both models using:

* Accuracy
* Precision
* Recall
* F1 Score
* Macro Precision
* Macro Recall
* Macro F1
* ROC-AUC
* Confusion Matrix

The prediction threshold defaults to:

```text
0.5
```

Users can also adjust the threshold through the application's threshold control to explore different classification trade-offs.

##  Claim Prediction

The **Claim Predictor** allows users to enter policyholder information and estimate claim risk.

Inputs include:

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

* Predicted class
* Claim probability
* No-claim probability
* Prediction confidence
* Selected model
* Prediction threshold
* Important risk factors

##  Analytics Dashboard

The dashboard provides an overview of the insurance dataset, including:

* Total policies
* Total claims
* No-claim policies
* Overall claim rate
* Average premium
* Average customer age
* Average policy tenure
* Claims by policy type
* Claims by vehicle type
* Claims by age group
* Claims by premium range
* Claims by previous claims
* Claims by accident history

Interactive charts are implemented using **Recharts**.

## Model Performance Dashboard

The Model Performance section allows users to compare Logistic Regression and Random Forest using:

* Accuracy
* Precision
* Recall
* F1 Score
* ROC-AUC
* Confusion Matrix
* Feature Importance
* Probability Distribution
* Training time

This makes it possible to understand not only which model performs better, but also which features contribute most to predictions.

##  PDF Reports

The application can generate an **Insurance Analytics PDF Report** containing relevant dataset and model information.

PDF generation uses:

* `html2canvas`
* `jsPDF`

##  Technology Stack

### Frontend

* React 19
* TypeScript
* Vite
* Tailwind CSS
* Lucide React

### Machine Learning

* Custom Logistic Regression
* Custom Random Forest
* Feature engineering
* Categorical encoding
* Numerical standardization
* Classification metrics

### Data Processing

* Papa Parse
* JavaScript/TypeScript data processing

### Visualization

* Recharts

### Reporting

* jsPDF
* html2canvas

### AI Integration

* Google Gemini API support through `@google/genai`

##  Project Structure

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
│   │   ├── PolicyTable.tsx
│   │   ├── ModelMetricsTable.tsx
│   │   ├── ConfusionMatrix.tsx
│   │   ├── FeatureImportanceChart.tsx
│   │   ├── ProbabilityDistributionChart.tsx
│   │   └── ...
│   │
│   ├── ml/
│   │   ├── encoding.ts
│   │   ├── featureEngineering.ts
│   │   ├── logisticRegression.ts
│   │   ├── randomForest.ts
│   │   ├── metrics.ts
│   │   ├── modelTraining.ts
│   │   └── preprocessing.ts
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
├── .env.example
├── package.json
├── tsconfig.json
├── vite.config.ts
└── README.md
```

##  Getting Started

### Prerequisites

Make sure you have installed:

* Node.js
* npm

### 1. Clone the Repository

```bash
git clone <your-repository-url>
cd insurance-claim-prediction
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment Variables

Create a `.env.local` file if you want to use the Gemini integration:

```env
GEMINI_API_KEY=your_gemini_api_key
```

Refer to `.env.example` for the available environment variables.

### 4. Start the Development Server

```bash
npm run dev
```

The application will start using Vite.

### 5. Build for Production

```bash
npm run build
```

### 6. Preview the Production Build

```bash
npm run preview
```

##  Type Checking

Run the TypeScript compiler without generating output:

```bash
npm run lint
```

##  Key Highlights

* **650 insurance policy records**
* **16 original dataset columns**
* **Binary claim prediction**
* **Two ML classification algorithms**
* **80/20 stratified train-test split**
* **Custom ML implementations in TypeScript**
* **Feature engineering pipeline**
* **Interactive prediction interface**
* **Model performance comparison**
* **Risk factor visualization**
* **PDF report generation**
* **Responsive web dashboard**

##  Disclaimer

This project is intended for **educational, demonstration, and portfolio purposes**.

Predictions generated by the application should not be treated as professional insurance underwriting decisions or financial advice. Real-world insurance applications require validated datasets, rigorous model validation, fairness analysis, calibration, regulatory compliance, security controls, and domain-expert review.

##  Future Improvements

Possible improvements include:

* Hyperparameter optimization
* Cross-validation
* Model calibration
* Class imbalance handling
* More advanced ensemble methods
* Additional insurance and customer features
* Explainable AI techniques such as SHAP
* Persistent model storage
* Backend API for production inference
* Authentication and authorization
* Model monitoring and drift detection
* Automated model retraining
* Cloud deployment
* Comprehensive unit and integration testing

##  License

Add your preferred license before publishing the repository.
