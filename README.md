# Repository: BI-Project

## 1. README.md (Project Overview)
'''
# BI-Project

This repository contains scripts and documentation for a Business Intelligence (BI) project using Power BI and Python.

## Project Structure
```
📂 BI-Project
│── 📂 Data
│   ├── raw_data/        # Store raw datasets (CSV, Excel, SQL scripts)
│   ├── processed_data/  # Store cleaned and transformed data (optional)
│── 📂 Scripts
│   ├── data_cleaning.py # Python script for data preprocessing
│   ├── etl_pipeline.py  # ETL process for automation
│   ├── powerbi_api.py   # Automate Power BI report updates
│── 📂 Reports
│   ├── dashboard.pbix   # Power BI project file
│   ├── dashboard.pdf    # Exported report for reference
│── 📂 Documentation
│   ├── README.md        # Project overview
│   ├── Data_Dictionary.md # Explain dataset fields
│── 📂 Notebooks
│   ├── exploratory_analysis.ipynb # Jupyter Notebook for EDA
│── .gitignore
│── requirements.txt
│── LICENSE
```

## Setup Instructions
1. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
2. Run data cleaning:
   ```bash
   python scripts/data_cleaning.py
   ```
3. Run ETL pipeline:
   ```bash
   python scripts/etl_pipeline.py
   ```
4. Refresh Power BI dataset:
   ```bash
   python scripts/powerbi_api.py
   ```
'''

## 2. data_cleaning.py (Preprocessing Script)
import pandas as pd

def clean_data(input_file, output_file):
    """Load, clean, and save processed data."""
    df = pd.read_csv(input_file)
    df.drop_duplicates(inplace=True)
    df.fillna(method='ffill', inplace=True)
    df.to_csv(output_file, index=False)
    print(f"Cleaned data saved to {output_file}")

if __name__ == "__main__":
    clean_data("data/raw_data/dataset.csv", "data/processed_data/cleaned_dataset.csv")

## 3. etl_pipeline.py (ETL Process)
import os
import pandas as pd

def extract():
    """Extract raw data from CSV files."""
    return pd.read_csv("data/raw_data/dataset.csv")

def transform(df):
    """Transform the dataset (e.g., create new features)."""
    df['new_col'] = df['existing_col'] * 2
    return df

def load(df):
    """Load transformed data into a new CSV file."""
    df.to_csv("data/processed_data/transformed_dataset.csv", index=False)

if __name__ == "__main__":
    data = extract()
    transformed_data = transform(data)
    load(transformed_data)
    print("ETL process completed.")

## 4. powerbi_api.py (Power BI Dataset Refresh)
import requests

POWER_BI_WORKSPACE_ID = "your_workspace_id"
POWER_BI_DATASET_ID = "your_dataset_id"
POWER_BI_ACCESS_TOKEN = "your_access_token"

def refresh_dataset():
    url = f"https://api.powerbi.com/v1.0/myorg/groups/{POWER_BI_WORKSPACE_ID}/datasets/{POWER_BI_DATASET_ID}/refreshes"
    headers = {"Authorization": f"Bearer {POWER_BI_ACCESS_TOKEN}"}
    response = requests.post(url, headers=headers)
    if response.status_code == 202:
        print("Dataset refresh initiated successfully.")
    else:
        print("Failed to refresh dataset.", response.text)

if __name__ == "__main__":
    refresh_dataset()

## 5. exploratory_analysis.ipynb (Exploratory Data Analysis - Jupyter Notebook)
'''
# Exploratory Data Analysis

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("data/processed_data/cleaned_dataset.csv")
print(df.describe())

df.hist(figsize=(10, 6))
plt.show()
```
'''
