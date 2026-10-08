# COMP90049 Assignment 2 — Bank Marketing

## Project Overview

This project investigates the use of machine learning to predict whether a bank client will subscribe to a term deposit.

We use the **Bank Marketing** dataset from the **UCI Machine Learning Repository**, which contains data collected from direct marketing campaigns conducted by a Portuguese banking institution through phone calls.

The project focuses on two research questions:

1. How effectively can different machine learning models predict whether a client will subscribe to a term deposit?
2. How much does previous campaign history contribute to subscription prediction beyond customer demographic and financial information?

---

## Dataset

- **Dataset:** Bank Marketing
- **Source:** UCI Machine Learning Repository
- **Dataset page:** https://archive.ics.uci.edu/dataset/222/bank+marketing
- **Dataset DOI:** 10.24432/C5K306
- **File used:** `bank-additional-full.csv`
- **Original number of instances:** 41,188
- **Input features:** 20
- **Target variable:** `y`
  - `yes`: the client subscribed to a term deposit
  - `no`: the client did not subscribe

The dataset contains demographic, financial, campaign-related, previous campaign, and socio-economic information.

The `duration` feature is excluded from the main RQ1 prediction feature set because it is only known after the phone call has ended and is therefore unsuitable for a realistic pre-outcome prediction setting.

---

## Research Questions

### RQ1

**How effectively can different machine learning models predict whether a client will subscribe to a term deposit?**

RQ1 compares multiple machine learning models using a broad feature set containing:

- demographic information
- financial information
- current campaign information
- previous campaign history
- socio-economic information

Classical machine learning models and a neural network will be evaluated using the same train/test observations and evaluation framework.

### RQ2

**How much does previous campaign history contribute to subscription prediction beyond customer demographic and financial information?**

RQ2 uses a feature ablation experiment with two feature sets:

- **Set A:** Customer demographic and financial information only
- **Set B:** Set A plus previous campaign history

The difference in predictive performance between Set A and Set B is used to estimate the additional predictive value of previous campaign history.

---

## Data Preparation

The shared preprocessing workflow includes:

- checking dataset structure and target distribution
- identifying `unknown` categorical values
- checking duplicate observations
- analysing the special `pdays` value
- removing exact duplicate rows
- engineering `pdays_recorded` and `pdays_clean`
- encoding the target as:
  - `no = 0`
  - `yes = 1`
- using an 80/20 stratified train/test split
- one-hot encoding categorical features
- standardising numerical features

All preprocessing transformations are fitted on the training data only and then applied to the test data.

RQ1, RQ2 Set A, and RQ2 Set B use the same train/test observations.

---

## Feature Sets

### RQ1 Feature Set

RQ1 uses a broader feature set for overall prediction.

The feature groups include:

- demographic and financial features
- current campaign features
- previous campaign history
- socio-economic context

The `duration` feature is excluded.

The original `pdays` variable is replaced by the engineered features:

- `pdays_recorded`
- `pdays_clean`

### RQ2 Feature Sets

#### Set A — Without Previous Campaign History

Set A contains customer demographic and financial information only.

#### Set B — With Previous Campaign History

Set B contains all Set A features plus:

- `previous`
- `poutcome`
- `pdays_recorded`
- `pdays_clean`

---

## Experimental Setup

The following setup is shared across the project:

- 80% training data
- 20% test data
- stratified splitting based on the target variable
- fixed random state for reproducibility
- the same train/test observations for RQ1 and RQ2
- categorical features are one-hot encoded
- numerical features are standardised
- preprocessing is fitted on training data only

For RQ2, Set A and Set B are compared under the same experimental conditions.

For the same model type, both feature sets should use:

- the same hyperparameter search space
- the same cross-validation strategy
- the same scoring metric
- the same train/test split

Set A and Set B may obtain different best hyperparameters through the same tuning procedure.

---

## Evaluation

Because the target classes are imbalanced, model performance is not evaluated using accuracy alone.

The main evaluation metrics include:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- Confusion Matrix

For RQ1, the main goal is to compare the predictive performance of different machine learning models.

For RQ2, the main comparison is the performance difference between Set A and Set B for the same model type.

---

## Team Members and Responsibilities

| Team Member | Role | Main Responsibilities |
|---|---|---|
| **Yuxin Qi (Person A)** | Data, Literature Review & RQ2 Lead | Dataset selection and inspection, data preprocessing, feature engineering, train/test split, RQ1 and RQ2 feature preparation, literature review, RQ2 experimental design, RQ2 result integration and analysis |
| **Feize Zhao (Person B)** | Classical ML, Evaluation & RQ1 Lead | Classical ML model implementation, hyperparameter tuning, validation and evaluation, RQ1 model comparison, classical ML experiments for RQ2, notebook integration |
| **Yan Le (Person C)** | Neural Network & Report Integration | Neural network implementation and tuning, neural network evaluation for RQ1 and RQ2, bibliography and Generative AI disclosure, final report integration and editing |

---

## Literature Review Collaboration

### Person A — Yuxin Qi

Responsible for:

- leading the Literature Review
- finding and reviewing the dataset source paper
- finding literature related to RQ2
- finding literature related to feature contribution and previous campaign history
- integrating literature contributed by the other team members

### Person B — Feize Zhao

Responsible for contributing literature related to:

- classical machine learning
- model comparison
- customer response prediction
- model evaluation

### Person C — Yan Le

Responsible for contributing literature related to:

- neural networks
- deep learning
- neural network applications in bank marketing prediction

---

## RQ1 Responsibilities

### Person A

- prepares the unified RQ1 dataset
- defines the RQ1 feature set
- provides the shared train/test split
- provides the preprocessing setup

### Person B

- leads RQ1
- trains classical machine learning models
- performs hyperparameter tuning
- evaluates classical models
- compares model performance
- integrates the neural network results into the final RQ1 comparison

### Person C

- trains and tunes the neural network
- evaluates the neural network using the same train/test observations
- provides neural network results for the RQ1 comparison

---

## RQ2 Responsibilities

### Person A

- leads RQ2
- defines Set A and Set B
- prepares the shared preprocessing setup
- collects model results from Person B and Person C
- compares Set A and Set B
- analyses the additional predictive value of previous campaign history
- leads the final RQ2 interpretation

### Person B

- runs classical ML models on Set A
- runs the same classical ML model types on Set B
- performs hyperparameter tuning for both feature sets using the same tuning procedure
- provides evaluation results to Person A

### Person C

- runs the neural network on Set A
- runs the neural network on Set B
- tunes the neural network under a consistent setup
- provides evaluation results to Person A

---

## Report Responsibilities

| Report Section | Lead |
|---|---|
| Introduction | Person B, with support from Person A and Person C |
| Literature Review | Person A |
| Dataset Description | Person A |
| Data Preprocessing & Feature Engineering | Person A |
| Classical ML Methodology | Person B |
| Neural Network Methodology | Person C |
| Validation & Evaluation Setup | Person B |
| RQ1 Results & Discussion | Person B |
| RQ2 Results & Discussion | Person A |
| Conclusion | All team members |
| Generative AI Disclosure | Person C |
| Bibliography & Citation Formatting | Person C |
| Final Report Integration & Editing | Person C |
| Final Notebook Integration | Person B |

---

## Repository Structure

```text
COMP90049-Project2/
├── README.md
├── A2_Bank_Marketing.ipynb
└── data/
    └── bank-additional-full.csv
