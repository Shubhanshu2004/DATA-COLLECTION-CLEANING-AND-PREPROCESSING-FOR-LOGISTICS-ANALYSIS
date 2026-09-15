🚚 Week 2 — Logistics Data Collection, Cleaning & Preprocessing

📌 Project Overview

This project focuses on the data collection, cleaning, and preprocessing stage of a logistics data science project.

The objective is to prepare a high-quality logistics dataset that can be used for further analysis, machine learning, KPI evaluation, demand forecasting, and logistics optimization.

The project demonstrates how raw logistics data can be transformed into a clean and structured dataset using Python, Pandas, NumPy, and Scikit-learn.

⸻

🎯 Objectives

The main objectives of this project are:

* Collect and understand a publicly available logistics dataset
* Inspect the structure and quality of the dataset
* Identify missing values
* Remove duplicate records
* Detect and handle outliers
* Correct incorrect data types
* Standardize inconsistent categorical values
* Perform feature engineering
* Encode categorical variables
* Normalize numerical features
* Generate a clean dataset for future analysis

⸻

📊 Dataset

The project uses a publicly available logistics/supply-chain dataset containing information related to logistics operations.

The dataset may include variables such as:

* Order ID
* Customer ID
* Product ID
* Warehouse
* Order Date
* Shipping Date
* Delivery Date
* Product Category
* Quantity
* Distance
* Shipping Mode
* Transportation Cost
* Inventory Level
* Delivery Status

The dataset is used to simulate a real-world logistics data collection and preprocessing workflow.

⸻

🧹 Data Cleaning

The following data-quality issues are identified and addressed:

Missing Values

Missing values are identified using Pandas:

df.isnull().sum()

Depending on the variable, missing values are handled using:

* Median imputation for numerical variables
* Mode imputation for categorical variables
* Business-based handling for date/status fields

Duplicate Records

Duplicate records are identified and removed:

df.duplicated().sum()
df = df.drop_duplicates()

Incorrect Data Types

Date columns are converted into proper datetime format:

df["order_date"] = pd.to_datetime(
    df["order_date"],
    errors="coerce"
)

Inconsistent Categories

Categorical values are standardized:

df["shipping_mode"] = (
    df["shipping_mode"]
    .str.strip()
    .str.lower()
)

⸻

📈 Outlier Detection

Outliers can represent unusual delivery times, transportation costs, distances, or order quantities.

The Interquartile Range (IQR) method is used to identify potential outliers.

Q1 = df["delivery_time"].quantile(0.25)
Q3 = df["delivery_time"].quantile(0.75)
IQR = Q3 - Q1
lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR
outliers = df[
    (df["delivery_time"] < lower) |
    (df["delivery_time"] > upper)
]

Outliers are investigated before deciding whether they should be removed, capped, or retained.

⸻

⚙️ Feature Engineering

New features are created to support future logistics analysis.

Delivery Time

df["delivery_time"] = (
    df["delivery_date"] -
    df["order_date"]
).dt.days

Processing Time

df["processing_time"] = (
    df["shipping_date"] -
    df["order_date"]
).dt.days

Delivery Delay

df["delivery_delay"] = (
    df["delivery_date"] >
    df["expected_delivery"]
).astype(int)

These features can later be used for delivery performance analysis and machine learning.

⸻

🔢 Data Normalization

Numerical features can have different scales. Standardization is therefore applied where appropriate.

from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
columns = [
    "distance",
    "transport_cost",
    "quantity"
]
df[columns] = scaler.fit_transform(
    df[columns]
)

This converts numerical variables to a comparable scale and can be particularly useful for algorithms such as clustering.

⸻

🔠 Categorical Encoding

Categorical variables are converted into numerical representations using one-hot encoding.

df = pd.get_dummies(
    df,
    columns=["shipping_mode"],
    drop_first=True
)

This makes categorical information suitable for machine learning algorithms.

⸻

🔄 Preprocessing Workflow

Raw Logistics Dataset
        ↓
Data Collection
        ↓
Data Inspection
        ↓
Missing Value Analysis
        ↓
Duplicate Removal
        ↓
Data Type Correction
        ↓
Categorical Standardization
        ↓
Outlier Detection
        ↓
Data Validation
        ↓
Feature Engineering
        ↓
Categorical Encoding
        ↓
Normalization / Scaling
        ↓
Final Quality Check
        ↓
Clean Logistics Dataset

⸻

💻 Technologies Used

Technology	Purpose
Python	Data processing and analysis
Pandas	Data cleaning and manipulation
NumPy	Numerical operations
Matplotlib	Data visualization
Seaborn	Statistical visualization
Scikit-learn	Scaling and preprocessing
Google Colab	Python development environment
GitHub	Version control and project documentation

⸻

📁 Project Structure

logistics-data-collection-preprocessing/
│
├── data/
│   ├── logistics_data.csv
│   └── cleaned_logistics_data.csv
│
├── notebooks/
│   └── logistics_data_preprocessing.ipynb
│
├── reports/
│   └── week2_data_preprocessing_report.docx
│
├── src/
│   └── preprocessing.py
│
├── requirements.txt
│
└── README.md

⸻

📓 Google Colab

The complete preprocessing implementation is available in the Jupyter Notebook.

The notebook covers:

* Dataset loading
* Data inspection
* Missing-value analysis
* Duplicate detection
* Data cleaning
* Outlier detection
* Feature engineering
* Encoding
* Normalization
* Final dataset validation

▶️ Open in Google Colab

Replace the link above with the GitHub URL of your .ipynb file to open this specific notebook directly in Google Colab.

⸻

📄 Project Report

The detailed Week 2 report explains the complete methodology, data-quality issues, preprocessing techniques, Python implementation, and impact of data quality on logistics analytics.

Report:
reports/week2_data_preprocessing_report.docx

⸻

🎯 Expected Outcomes

After preprocessing, the project aims to produce a dataset that is:

* Clean
* Consistent
* Structured
* Validated
* Suitable for analysis
* Suitable for machine learning
* Ready for future logistics modeling

The cleaned dataset will serve as the foundation for future tasks involving EDA, KPI analysis, predictive modeling, clustering, demand forecasting, and route optimization.

⸻

💡 Key Learning

This project demonstrates that data preprocessing is a critical step in logistics analytics.

Poor-quality data can result in incorrect KPIs, unreliable predictions, inefficient inventory decisions, and poor resource allocation.

By systematically identifying and correcting data-quality issues, the reliability of subsequent analysis and machine learning models can be significantly improved.

⸻

👨‍💻 Author

Shubhanshu Kumar

B.Tech — Computer Science & Engineering
IILM University, Greater Noida

Skills Demonstrated

Python Pandas NumPy Scikit-learn Data Cleaning Data Preprocessing Feature Engineering Data Analysis Machine Learning Google Colab GitHub

⸻

📌 Project Status

Week 2 — Completed

Focus: Data Collection, Cleaning & Preprocessing for Logistics Analysis
