Employee Segmentation Model Usage Guide
This guide explains how to use the KMeans clustering model for employee segmentation using two different script modes: from Google Drive or from local file upload.

📁 Project Directory Structure
nginx
Copy
Edit
submission
├───model                         # Folder for model files
├───notebook.ipynb                # Notebook for exploration and model training
├───prediction.py                 # Main prediction script (uses Drive paths)
├───prediction_local.py          # Alternative script (uses local file upload)
├───README.md                     # This documentation
├───<@ilhamaji-dashboard          # Folder for dashboard artifacts
├───@ilhamaji-video               # Folder for video documentation
├───metabase.db.mv.db             # Metabase database file
└───requirements.txt              # Python dependencies
🧠 Model Overview
The model uses K-Means clustering (K=3) to segment employees based on attributes such as role, department, salary, work-life balance, and performance.

✅ Requirements
Python 3.6+

Required packages: pandas, numpy, scikit-learn, joblib

Install dependencies via:

bash
Copy
Edit
pip install -r requirements.txt
📂 Files Included
kmeans_clustering_model.joblib - The trained KMeans model

prediction.py - Script using Google Drive path

prediction_local.py - Script for uploading local CSV files

⚙️ Option 1: Use Prediction from Google Drive (prediction.py)
Step 1: Mount Google Drive (in Google Colab)
python
Copy
Edit
from google.colab import drive
drive.mount('/content/drive')
Step 2: Check and Update File Paths
Open prediction.py, and make sure to update these two lines if your file is stored in a different folder:

python
Copy
Edit
model_path = "/content/drive/MyDrive/Colab Notebooks/Dicoding Penerapan Data Science/Submission/kmeans_clustering_model.joblib"
data_path = "/content/drive/MyDrive/Colab Notebooks/Dicoding Penerapan Data Science/Submission/df_final.csv"
Step 3: Run the Script
bash
Copy
Edit
python prediction.py
The script will:

Load the model from your Drive

Load the dataset

Preprocess data (drop unnecessary columns, transform numerics, encode categoricals)

Predict cluster labels

Save results as employee_segments_results.csv

📥 Option 2: Use Prediction with Local File Upload (prediction_local.py)
This version is suitable when you're working locally or in environments that support manual file uploads (like Colab or Jupyter).

Step 1: Run the Script
bash
Copy
Edit
python prediction_local.py
The script will prompt you to upload your CSV file manually. After upload:

The model is loaded from the current folder (model/kmeans_clustering_model.joblib)

Data is preprocessed (standardized columns, encoded categoricals)

Segmentation prediction is applied

Results are saved to employee_segments_results.csv

📊 Expected Input Format
Your input CSV should include these raw features. The script will handle column formatting and transformation automatically:

Categorical Features:
business_travel

department

education_field

gender

job_role

marital_status

over_time

Numerical Features:
age

daily_rate

distance_from_home

education

environment_satisfaction

hourly_rate

job_involvement

job_level

job_satisfaction

monthly_income

monthly_rate

num_companies_worked

percent_salary_hike

performance_rating

relationship_satisfaction

stock_option_level

total_working_years

training_times_last_year

work_life_balance

years_at_company

years_in_current_role

years_since_last_promotion

years_with_curr_manager

Columns not required (e.g., employee_id) will be dropped automatically during preprocessing.

🧩 Interpreting the Output
The output CSV (employee_segments_results.csv) will contain your input data along with a new column:

employee_segment: Cluster label (0, 1, or 2)

Example:

job_role	monthly_income	gender	...	employee_segment
Sales Exec	4200	Male	...	1
Data Scientist	7200	Female	...	0
🔍 Understanding the Clusters
Each cluster represents a group of employees with similar patterns. You can interpret the clusters based on:

Attrition risk

Salary patterns

Satisfaction and performance

Work-life balance and tenure

You may replace the following with your actual interpretation:

Cluster 0: High-performing, satisfied employees with low attrition risk

Cluster 1: Moderate satisfaction, younger or mid-level staff

Cluster 2: Dissatisfied or high-risk employees

🛠 Troubleshooting
Model not loading?
Check if kmeans_clustering_model.joblib is in the correct path (model/ for local or update the Drive path).

Columns don't match?
The script standardizes column names and transformations. Ensure your CSV uses consistent names or let the script handle renaming.

Still having issues?
Reach out or raise an issue for support.

