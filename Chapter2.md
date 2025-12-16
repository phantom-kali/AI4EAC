# Chapter 2: Preparing Your Dataset for Modeling

## Introduction

Congratulations on completing Chapter 1! Now that you can generate and load datasets, let's prepare that data for AI modeling. This is like cleaning and organizing ingredients before cooking—essential for good results.

**Objective**: Learn to clean data, split it for training, select features, preprocess, and visualize patterns. We'll use simple terms and build on your `student_data.csv` from Chapter 1. This should take 1-2 hours.

In the AI4EAC Innovation Challenge, clean and ethical data preparation ensures your models are fair and relevant to East African contexts, like predicting student outcomes across diverse regions.

Continue in Google Colab—it's perfect for data prep.


## Data Quality: Cleaning Your Dataset

Real data is often messy—missing values, duplicates, or errors. Cleaning fixes this to avoid bad model results.

**Key Steps**:

- **Missing Values**: Data points that are blank. Fill them (e.g., with averages) or drop rows.
- **Duplicates**: Remove repeated rows to keep data unique.
- **Outliers**: Extreme values; we'll spot them later via visuals.

Run this code in Colab (upload `student_data.csv` if needed via the left sidebar):

```python
import pandas as pd

# Load data
df = pd.read_csv('student_data.csv')

# Check for missing values
print(df.isnull().sum())  # Shows count per column

# Fill missing (if any; our generated data has none, but practice!)
df['grade'].fillna(df['grade'].mean(), inplace=True)

# Remove duplicates
df.drop_duplicates(inplace=True)

# View cleaned data
print(df.head())
```

If your data has no issues, that's fine—real datasets often do!

![Data Cleaning Cycle](https://av-eks-blogoptimized.s3.amazonaws.com/19855data%20cleaning%20cycle.png)


## Splitting Data: Train and Test Sets

To test if your model works on new data (not just memorized), split into:

- **Train Set**: ~80% for learning.
- **Test Set**: ~20% for evaluation.

Why? Prevents "overfitting" (like a student who memorizes answers but can't apply knowledge).

Use scikit-learn (pre-installed in Colab):

```python
from sklearn.model_selection import train_test_split

# Features (inputs) and target (output)
X = df[['hours_studied', 'attendance']]  # Inputs
y = df['grade']  # Output to predict

# Split: 80% train, 20% test
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

print("Train shape:", X_train.shape)  # e.g., (80, 2)
print("Test shape:", X_test.shape)    # e.g., (20, 2)
```

`random_state=42` ensures reproducibility (same split every time).

![Train Test Split](https://builtin.com/sites/www.builtin.com/files/styles/ckeditor_optimize/public/inline-images/20_train-test-split.jpg)


## Feature Selection and Basic Preprocessing

- **Features**: Input columns (e.g., `hours_studied`, `attendance`).
- **Target**: What to predict (e.g., `grade`).

Preprocessing: Scale features so they're on the same range (helps models learn better). Use MinMaxScaler (0-1 range).

```python
from sklearn.preprocessing import MinMaxScaler

# Scale features
scaler = MinMaxScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

print("Scaled train sample:", X_train_scaled[:2])
```

No categories in our data, so skip encoding for now.

## Visualizing Data: Spot Patterns

Plots help see relationships, like if more study hours mean higher grades.

Use matplotlib (pre-installed):

```python
import matplotlib.pyplot as plt

# Scatter plot: hours vs. grade
plt.scatter(df['hours_studied'], df['grade'])
plt.xlabel('Hours Studied')
plt.ylabel('Grade')
plt.title('Study Hours vs. Grade')
plt.show()
```

Look for trends—a positive slope means correlation.

![Correlation](https://bookdown.org/yshang/book/images/scatterplot.1.png)


## Hands-On Exercise

1. Generate a new CSV in Chapter 1 code, but add missing values: Set 5 random grades to `None` (e.g., `df.loc[5:10, 'grade'] = None` before saving).
2. Load it here, clean (fill missing with mean), split, scale, and plot. How does the plot change?
