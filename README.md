# Predicting Market Salary from LinkedIn Job Posting Data

## Overview

This project develops a **machine learning-based salary benchmarking tool** using LinkedIn job posting data to estimate annual salaries for full-time roles in the United States.

Using a curated dataset of **17,892 full-time job postings**, the project compares multiple regression models, engineers features from job titles and descriptions, and uses **SHAP analysis** to understand the factors that drive salary predictions.

The final Decision Tree model achieved a **32.8% MAPE**, improving substantially over the **48.1% baseline** while providing interpretable insights into how experience, job category, skills, industry, and location influence compensation.

---

## Problem

Salary information in job postings is often missing or difficult to compare across roles, locations, and experience levels.

This creates challenges for:

- **Job seekers** trying to benchmark offers and negotiate compensation
- **Recruiters** evaluating whether offers are competitive
- **HR and compensation teams** developing market-aligned salary ranges

This project explores whether machine learning can transform job posting data into useful salary benchmarks while also identifying the factors that influence compensation.

---

## Dataset

The analysis uses the **LinkedIn Job Postings dataset**, containing more than **120,000 U.S. job postings** with structured and text-based information.

Available features include:

- Job title
- Job description
- Location
- Experience level
- Work type
- Remote eligibility
- Industry
- Company information
- Salary information
- Skills and job descriptions

After filtering and preprocessing, the final modeling dataset contained:

**17,892 full-time job postings with valid salary and location information.**

Salary values from the original 2023–2024 data were adjusted to approximate 2025–2026 compensation levels.

---

## Data Cleaning & Feature Engineering

The preprocessing pipeline included:

- Filtering for full-time positions
- Removing postings without valid salary or location information
- Correcting incorrectly labeled pay periods
- Removing unrealistic salary values
- Handling missing experience levels using job-title keywords
- Identifying remote roles using job-description keywords
- Incorporating company and industry information
- One-hot encoding categorical variables

### Job Categories

Job titles were grouped into **19 categories**, including:

- Engineering / Trades
- Management / Director
- Healthcare
- Finance / Accounting
- Sales
- Data / ML / Analyst
- Software / IT / DevOps
- Project Management
- Marketing
- Product / Design / UX
- Consulting

### Skill Extraction

Keyword-based feature engineering was used to identify **16 skills** directly from job descriptions, including:

- Management
- Communication
- Finance
- Sales
- Marketing
- Engineering
- Excel
- Project Management
- Data Analysis
- Cloud
- Machine Learning / AI
- SQL
- Python
- JavaScript
- Java

This allowed information contained in unstructured job descriptions to contribute directly to salary prediction.

---

## Models

Six approaches were evaluated:

1. **Median Baseline**
2. **OLS Linear Regression**
3. **Ridge Regression**
4. **Lasso Regression**
5. **Decision Tree**
6. **Random Forest**

The models were evaluated primarily using **Mean Absolute Percentage Error (MAPE)**, with MAE, RMSE, and R² used as complementary metrics.

MAPE was selected as the primary metric because it expresses prediction error relative to salary, making performance easier to interpret across different compensation levels.

---

## Model Training & Tuning

The dataset was divided into training and held-out test sets.

Hyperparameter tuning was performed using **5-fold cross-validation**.

- Ridge and Lasso were tuned using cross-validation across regularization parameters.
- Decision Tree was tuned across **900 hyperparameter combinations**.
- Random Forest was evaluated across **1,200 hyperparameter combinations**.
- The final test set remained held out during model selection.

---

## Results

All machine learning models substantially outperformed the median baseline.

| Model | Test MAPE |
|---|---:|
| Median Baseline | 48.1% |
| OLS Regression | 35.9% |
| Ridge Regression | 36.0% |
| Lasso Regression | 35.9% |
| **Decision Tree** | **32.8%** |
| Random Forest | 34.0% |

### Best Model: Decision Tree

The **Decision Tree achieved the lowest MAPE at 32.8%**, representing a **15.3 percentage-point improvement over the baseline**.

The results suggest that salary is influenced by nonlinear interactions between variables such as:

`Experience Level × Job Category × Location × Skills`

The Decision Tree also demonstrated strong cross-validation stability, with approximately **±0.6% standard deviation across folds**.

While Random Forest achieved a lower absolute error (MAE), the Decision Tree performed better on the project's primary relative-error metric.

---

## Model Interpretability with SHAP

**SHAP (SHapley Additive exPlanations)** was used to understand which features contributed most strongly to salary predictions.

### Top Salary Drivers

The analysis identified **experience level as the strongest predictor of salary**, with more than 2.5× the impact of the next most influential feature.

Other important factors included:

1. **Experience level**
2. **Job category**
3. **Engineering skills**
4. **Industry**
5. **Remote work eligibility**
6. **Project management skills**
7. **Finance skills**
8. **Machine Learning / AI skills**
9. **Cloud skills**

The analysis also showed that extracting skills from job descriptions added useful predictive information beyond job titles alone.

---

## Segment-Level Insights

Model accuracy was also evaluated across different experience levels and job categories.

### Experience Level

The model performed particularly well for **entry-level positions**, achieving approximately:

**29.4% MAPE**

Executive-level positions were more difficult to predict due to smaller sample sizes and greater variation in compensation.

### Job Category

Some of the strongest-performing categories included:

- **Data / ML / Analyst:** 26.0% MAPE
- **Hospitality / Food:** 26.1% MAPE

Categories with greater salary variation, including healthcare and legal roles, were more difficult to predict accurately.

---

## Business Applications

The salary prediction framework can support several decision-making use cases.

### Salary Benchmarking
Estimate a market salary range based on role, experience, location, and required skills.

### Job Seekers
Provide data-driven salary benchmarks for evaluating job opportunities and negotiating compensation.

### Recruiters & Hiring Managers
Compare proposed salaries against estimated market compensation.

### HR & Compensation Teams
Support compensation planning, market benchmarking, and pay-equity analysis.

### Workforce Planning
Estimate hiring costs across multiple roles and job categories.

---

## Limitations

The model should be treated as a **decision-support and benchmarking tool rather than a definitive salary calculator**.

Key limitations include:

- Only postings with disclosed salary information are included.
- Performance varies across job categories and experience levels.
- Executive and highly specialized positions have greater prediction uncertainty.
- Missing or incomplete job descriptions may affect feature extraction.
- Labor markets evolve over time, requiring periodic retraining.
- Historical compensation data may reflect existing structural inequities.

---

## Tech Stack

- **Python**
- **Pandas**
- **NumPy**
- **Scikit-learn**
- **SHAP**
- **Matplotlib**
- **Jupyter Notebook**
- **Machine Learning**
- **Feature Engineering**
- **Cross-Validation & Hyperparameter Tuning**

---

## Key Takeaway

The project demonstrates that salary prediction is fundamentally a **nonlinear problem** influenced by the interaction of seniority, role, skills, industry, and location.

By combining structured job-posting data with features extracted from unstructured job descriptions, the final model reduced MAPE from **48.1% to 32.8%** while also providing interpretable insights into the factors driving compensation.
