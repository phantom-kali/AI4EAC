# Chapter 1: Getting Started with Python and Data Basics

## Introduction
Welcome to the first chapter of our beginner's guide to training AI models using self-generated datasets in Python! This guide is designed for club members who are new to AI and model training, especially in preparation for the AI4EAC Innovation Challenge. We'll start from the absolute basics to build confidence step by step.

**Objective**: By the end of this chapter, you'll be comfortable setting up a Python environment, understanding basic Python concepts, and creating/loading simple datasets. This should take about 1 hour.

**Why Python for AI?**  
Python is the go-to language for AI because it's simple to learn, completely free, and has a massive community that provides tons of resources and libraries. Tools like pandas make handling data easy, and it's perfect for beginners participating in challenges like AI4EAC, where you'll build models for regional problems in East Africa.

## Setting Up Google Colab
No need to install anything on your computer! We'll use Google Colab, a free online platform from Google that lets you write and run Python code in your web browser.

1. Go to [colab.research.google.com](https://colab.research.google.com).
2. Sign in with a Google account (create one if you don't have it—it's free).
3. Click "New Notebook" to start a fresh file.

Colab looks like this:
![Google Colab interface](https://images.ctfassets.net/lzny33ho1g45/5fve83iqCwV7IzFxJkKWfJ/28d89db81c4efc95f2a28eb3d953f170/what-is-google-colab-image9.png)




It has cells where you can type code and run it by clicking the play button or pressing Shift+Enter. Output appears right below the cell.

## Basic Python Concepts
Let's cover the essentials: variables, lists, and functions. These are building blocks for everything we'll do.

### Variables
Variables store data. Think of them as labeled boxes.

```python
# Example: Storing a number
age = 20
print(age)  # Output: 20

# Storing text
name = "Alex"
print("Hello, " + name)  # Output: Hello, Alex
```

### Lists
Lists hold multiple items, like a shopping list.

```python
# Creating a list
fruits = ["apple", "banana", "cherry"]
print(fruits)  # Output: ['apple', 'banana', 'cherry']

# Accessing items (index starts at 0)
print(fruits[0])  # Output: apple

# Adding to the list
fruits.append("date")
print(fruits)  # Output: ['apple', 'banana', 'cherry', 'date']
```

### Functions
Functions are reusable code blocks. Python has built-in ones, or you can make your own.

```python
# Built-in function: len() for length
print(len(fruits))  # Output: 4 (assuming after append)

# Custom function
def greet(person):
    return "Hi, " + person

print(greet("Sam"))  # Output: Hi, Sam
```

Here's a visual example of simple Python code:
![Iteration Example](https://dq-blog-files.s3.amazonaws.com/list-tutorial/py1m2_cb25.svg)



Practice these in your Colab notebook. Experiment—change values and see what happens!

## Introduction to Datasets
In AI, a dataset is just organized data, like a table of information. We'll use CSV (Comma-Separated Values) files because they're simple text files that store data in rows and columns, like a spreadsheet.

**What is CSV?** It's a file format where each line is a row, and values are separated by commas. Example:  
`Name,Age,City`  
`Alex,20,Nairobi`  
`Sam,22,Kampala`

**Why self-generate datasets?** For beginners, it's easier to control the data, avoid privacy issues, and learn without downloading files. Plus, no internet needed beyond Colab. In AI4EAC, you might generate data simulating East African scenarios, like student performance in regional schools.

Here's what a CSV structure looks like:
![CSV Structure](https://cdn-wordpress-info.futurelearn.com/info/wp-content/uploads/fl-pdata-w2-step04-csv-image-1.png)



## Generating a Simple CSV
We'll use the `pandas` library (pre-installed in Colab) to create a dataset. Imagine data for "student performance prediction"—relevant to education in East Africa.

Copy this code into a Colab cell and run it:

```python
import pandas as pd  # Import pandas
import numpy as np   # For random numbers

# Generate random data (100 students)
data = {
    'hours_studied': np.random.randint(1, 10, 100),  # 1-9 hours
    'attendance': np.random.randint(70, 100, 100),   # 70-99%
    'grade': np.random.randint(50, 100, 100)         # 50-99 score
}

# Create a DataFrame (table)
df = pd.DataFrame(data)

# Save to CSV
df.to_csv('student_data.csv', index=False)

print("CSV file generated! Download it from Colab's files panel.")
```

This creates `student_data.csv` with 100 rows. Download it from the left sidebar in Colab (refresh if needed).

## Loading and Exploring Data
Now, load the CSV back and explore it.

Run this in a new cell:

```python
# Load the CSV
df = pd.read_csv('student_data.csv')

# View first 5 rows
print(df.head())

# Basic stats
print(df.describe())  # Means, mins, maxes, etc.

# Example output for head():
#    hours_studied  attendance  grade
# 0              5          85     72
# 1              3          92     88
# ...
```

`df.head()` shows a preview, and `df.describe()` gives summaries like average grade.

## Hands-On Exercise
1. Run the generation code, but modify it to add a new column: `'sleep_hours': np.random.randint(5, 9, 100)`.
2. Save the new CSV, load it, and print the description. What’s the average sleep hours?

Share your modified code with club members!
