# Experiment 2: Exploratory Data Analysis (EDA)

## 🎯 Aim
To perform Exploratory Data Analysis (EDA) on the heart disease dataset to understand the data distribution, relationships, and key patterns useful for business insights and model building.

## 📊 Dataset
The dataset used for this experiment is `heartdisease.csv`. It contains medical and demographic information such as age, sex, cholesterol levels (`totChol`), `BMI`, blood pressure, and target values (`TenYearCHD`) indicating heart disease presence.

## ⚙️ Algorithm / Steps Followed
1. Import required Python libraries (`numpy`, `pandas`, `seaborn`, `matplotlib`).
2. Load the dataset into a Pandas DataFrame.
3. Display the dataset structure, shape, and descriptive statistics.
4. Check for missing values and duplicate rows.
5. Examine correlations among numeric features using a correlation matrix and heatmap.
6. Visualize univariate distributions using histograms, boxplots, and countplots.
7. Analyze bivariate and multivariate relationships using scatter plots and pairplots.

## 🛠️ Functions and Methods Used

| Category | Function / Method | Purpose / Description |
| :--- | :--- | :--- |
| **Basic Exploration** | `df.info()` | Inspect dataset structure and data types |
| | `df.describe()` | Generate descriptive statistics |
| | `df.isnull().sum()` | Detect missing values in each column |
| | `df.duplicated().sum()` | Identify duplicate rows |
| | `df.corr()` | Find correlations between numeric variables |
| **Univariate Analysis** | `sns.histplot()` | Plot histogram (distribution of single variable) |
| | `sns.boxplot()` | Identify outliers using boxplot |
| | `sns.countplot()` | Count occurrences of categorical variables |
| **Bivariate Analysis** | `sns.scatterplot()` | Display relationship between two variables |
| | `sns.heatmap()` | Show correlation matrix visually |
| **Multivariate Analysis** | `sns.pairplot()` | Show pairwise relationships across variables |
| **Visualization Controls** | `plt.figure()`, `plt.title()`, `plt.xlabel()`, `plt.ylabel()`, `plt.show()` | Configure and display plotted charts |

## 💻 Program / Code

```python
# Exploratory Data Analysis (EDA) on Heart Disease Dataset

# Step 1: Import Essential Libraries
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# Step 2: Load the Dataset
# Update the file path to point to your local heartdisease.csv location
df = pd.read_csv('heartdisease.csv')

# Step 3: Basic Exploration
print("----- Dataset Information -----")
print(df.info())

print("\n----- Descriptive Statistics -----")
print(df.describe())

print("\n----- Dataset Shape -----")
print("Rows:", df.shape[0], "Columns:", df.shape[1])

print("\n----- First 10 Rows -----")
print(df.head(10))

# Step 4: Check Data Quality
print("\n----- Missing Values in Each Column -----")
print(df.isnull().sum())

print("\n----- Number of Duplicate Rows -----")
print(df.duplicated().sum())

# Step 5: Correlation Analysis
print("\n----- Correlation Matrix -----")
print(df.corr(numeric_only=True))

plt.figure(figsize=(10, 6))
sns.heatmap(df.corr(numeric_only=True), annot=True, cmap='coolwarm')
plt.title("Correlation Heatmap of Heart Disease Dataset")
plt.show()

# Step 6: Univariate Analysis
# Histogram for Age distribution
plt.figure(figsize=(8, 5))
sns.histplot(df['age'], kde=True, bins=20, color='teal')
plt.title("Distribution of Age")
plt.xlabel("Age")
plt.ylabel("Count")
plt.show()

# Boxplot for Cholesterol (to detect outliers)
plt.figure(figsize=(6, 4))
sns.boxplot(x=df['totChol'])
plt.title("Boxplot of Cholesterol Levels")
plt.xlabel("Cholesterol")
plt.show()

# Countplot for Gender (if available)
if 'sex' in df.columns:
    plt.figure(figsize=(5, 4))
    sns.countplot(x='sex', data=df)
    plt.title("Count of Gender")
    plt.xlabel("Sex (0 = Female, 1 = Male)")
    plt.ylabel("Count")
    plt.show()

# Step 7: Bivariate Analysis
# Scatter plot: Age vs Cholesterol
plt.figure(figsize=(8, 5))
sns.scatterplot(x='age', y='totChol', data=df, hue='TenYearCHD', palette='coolwarm')
plt.title("Age vs Cholesterol (by Heart Disease Target)")
plt.xlabel("Age")
plt.ylabel("Cholesterol")
plt.show()

# Step 8: Multivariate Analysis
# Pairplot for multiple relationships
selected_columns = ['age', 'totChol', 'BMI', 'TenYearCHD']
sns.pairplot(df[selected_columns], diag_kind='kde')
plt.suptitle("Pairwise Relationship between Variables", y=1.02)
plt.show()
```

## 🚀 How to Run
1. Install the required libraries:
   ```bash
   pip install numpy pandas seaborn matplotlib
   ```
2. Place `heartdisease.csv` in the same directory as your Python script.
3. Run the script:
   ```bash
   python exp2_eda.py
   ```