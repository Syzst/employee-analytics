# 🧠 Employee Segmentation Model Usage Guide

This guide explains how to use the KMeans clustering model for employee segmentation using two different script modes: from **Google Drive** or from **local file upload**.

---

## 📁 Project Directory Structure
```
employee-analytics/
├── model/                   # Folder for model files
├── notebook.ipynb           # Notebook for exploration and model training
├── prediction.py            # Prediction script (uses Google Drive paths)
├── prediction_local.py      # Local prediction script (manual file upload)
├── README.md                # This documentation file
├── metabase.db.mv.db        # Metabase database file
└── requirements.txt         # List of Python dependencies
```
---

## 🧠 Model Overview

The model uses **K-Means clustering (K=3)** to segment employees based on attributes such as job role, department, salary, work-life balance, performance rating, etc.

---

## ✅ Requirements

- Python 3.6+
- Required packages: `pandas`, `numpy`, `scikit-learn`, `joblib`, `etc`

Install dependencies using:

```

pip install -r requirements.txt

```
📂 Files Included

- model/kmeans_clustering_model.joblib – Trained KMeans model

- prediction.py – Script using Google Drive path

- prediction_local.py – Script for local CSV file upload



⚙️ Option 1: Prediction from Google Drive (prediction.py) 

Step 1: Mount Google Drive

```

from google.colab import drive
drive.mount('/content/drive')

```
Step 2: Update Paths
Edit the file paths in prediction.py to match your own Drive structure:
```
model_path = "/content/drive/MyDrive/.../model/kmeans_clustering_model.joblib"
data_path = "/content/drive/MyDrive/.../df_final.csv"

```
Step 3: Run the Script
```
python prediction.py

```
📥 Option 2: Local File Upload (prediction_local.py)
This script works in environments like Jupyter or Colab with file upload.

Step 1: Run the Script
```
python prediction_local.py

```
The script will:

- Ask you to upload a CSV file

- Load and preprocess the data

- Predict clusters

- Save results to employee_segments_results.csv
  
<br> 

📊 Expected Input Format

Your CSV should include these features:


- **Categorical**:
business_travel, department, education_field, gender, job_role, marital_status, over_time


- **Numerical**:
age, daily_rate, distance_from_home, education, environment_satisfaction, hourly_rate, job_involvement, job_level, job_satisfaction, monthly_income, monthly_rate, num_companies_worked, percent_salary_hike, performance_rating, relationship_satisfaction, stock_option_level, total_working_years, training_times_last_year, work_life_balance, years_at_company, years_in_current_role, years_since_last_promotion, years_with_curr_manager


Note: Extra columns like employee_id will be dropped automatically.

<br> 

📈 Output
The output CSV employee_segments_results.csv will include:

All input data

A new column: employee_segment with values: 0, 1, or 2

Example:
```
| Job Role         | Monthly Income | Gender | ... | Employee Segment |
|------------------|----------------|--------|-----|------------------|
| Sales Executive  | 4200           | Male   | ... | 1                |
| Human Resource   | 7200           | Female | ... | 0                |
```

<br> 

🔍 Cluster Interpretations
- Cluster 0: High-performing, low attrition risk employees

- Cluster 1: Moderate performance, mid-level attrition risk

- Cluster 2: High attrition risk or dissatisfied employees

<br> 

🛠 Troubleshooting
Model not found?
Ensure the model file exists at the specified path.
<br> 

Column issues?
Make sure your CSV contains the expected raw features. The script handles renaming and transformation.

<br> 

📬 Contact
Have questions? Reach out via ilhamaji2001@gmail.com or open a GitHub issue.
