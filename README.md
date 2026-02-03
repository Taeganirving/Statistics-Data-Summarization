# Construction Cost and Operations Analysis

## Overview
Analyzes trends and seasonal patterns in construction costs, employees, contracts, and lumber prices using descriptive statistics and visualizations.

## Data
- Source: Course-provided construction dataset
- Time period: 1990–2003
- Key variables: Costs, Employees, Contracts, Lumber price

## Tools
Python (pandas, matplotlib), Quarto

## Analysis Steps
1. Loaded and cleaned the dataset
2. Grouped data by month and year
3. Calculated descriptive statistics (mean, median, variability)
4. Visualized trends and seasonality
5. Interpreted results using economic reasoning

## Key Results
- Costs show clear seasonality, lowest in winter and highest in late summer
- Long-run costs increase steadily over time
- Input price volatility contributes to higher cost variability

## Code Examples

# Treat Month as a category for clean grouping
df["Month"] = df["Month"].astype("category")

# Define numeric variables used throughout the analysis
numeric_vars = ["Costs", "Employees", "Contracts", "Lumber price"]

# Apply consistent styling to all plots
plt.rcParams["figure.figsize"] = (9, 4.5)
plt.rcParams["figure.dpi"] = 120
plt.rcParams["axes.grid"] = True
# Prepares the dataset for analysis by setting correct data types, defining the variables of interest, and enforcing consistent chart formatting across all visualizations.


# Calculate mean and median by month
central_month = df.groupby("Month")[numeric_vars].agg(["mean", "median"])
central_month
# Groups the data by month and calculates average and typical values for each variable. This highlights seasonal patterns in costs, staffing, contracts, and lumber prices.

# Calculate mean and median by year
central_year = df.groupby("Year")[numeric_vars].agg(["mean", "median"])
central_year
# Groups the data by year to summarize long-run trends. This shows how costs and operational measures change over time as the business grows.

# Measure variability by Month
variability_month = df.groupby("Month")[numeric_vars].agg(
    ["std", "var", lambda x: x.max() - x.min()]
)

# Rename the lambda column to "range"
variability_month.columns = [
    f"{col}_{stat if stat != '<lambda>' else 'range'}"
    for col, stat in variability_month.columns
)

variability_month
# Measures how volatile each variable is within each month using standard deviation, variance, and range. This identifies months with more unpredictable costs or activity.

# Measure variability by Year
variability_year = df.groupby("Year")[numeric_vars].agg(
    ["std", "var", lambda x: x.max() - x.min()]
)

# Rename the lambda column to "range"
variability_year.columns = [
    f"{col}_{stat if stat != '<lambda>' else 'range'}"
    for col, stat in variability_year.columns
]

variability_year
# Measures how variability changes over time. Increasing spread in later years indicates growing uncertainty as the company expands and input prices fluctuate.

# Together, these steps use descriptive statistics to identify seasonality, long-run growth, and rising volatility in operational and cost data, which were then visualized through graphs and incorporated into a PowerPoint presentation to clearly communicate insights and conclusions.

