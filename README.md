# ECE-2112-PA-4
**Submitted by: Niamh Reese B. Pamilar | 2ECE-C**

**Date Submitted: September 17, 2026**


This repository contains Programming Assignment 4 for the course **ECE 2112: Advanced Computer Programming and Algorithms**. The assignment, titled **Experiment 4: Data Wrangling and Data Visualization**, consists of three Python problems that apply Pandas DataFrames, conditional filtering, column selection, DataFrame subsetting, group-by aggregation, mean calculation, and Matplotlib bar-chart visualization.



**Objectives:**

By the end of this activity, students should be able to:
1. load a CSV dataset into a Pandas DataFrame;
2. select rows and columns using positional and label-based indexing;
3. filter records using conditions on a DataFrame column; and
4. extract a well-defined subset of data without changing the source data.



## A. Visayas Communication DataFrame Problem

Create a DataFrame named `VisComm` containing students whose `Hometown` is Visayas and whose `Track` is Communication. Retain only the columns Name, Gender, Math, Electronics, and Average, in that order. The resulting DataFrame and its number of rows must be displayed.

The following operators, functions, and methods were used in this problem:
- `import pandas as pd` - imports the Pandas library and gives it the shorter name `pd`.
- `df.loc[]` - performs label-based selection and can be combined with Boolean conditions to filter rows and select columns.
- `==` - compares a column value with a specified category.
- `&` - the AND operator combines multiple Boolean conditions. Both conditions must be `True` for a row to be selected.
- `['Name', 'Gender', 'Math', 'Electronics', 'Average']` - specifies the columns to retain and their order.
- `len()` - returns the number of rows in the resulting DataFrame.


The overall mean was calculated by using:

```python
overall_mean = df[['Math', 'Electronics', 'GEAS', 'Communication', 'Average']].mean()

overall_mean
```

The filtering and column selection were performed using:

```python
VisComm = df.loc[
    (df['Hometown'] == 'Visayas') & (df['Track'] == 'Communication'),
    ['Name', 'Gender', 'Math', 'Electronics', 'Average']
]

VisComm
```

The two conditions are explicitly written in the filtering expression. The first condition:

```python
df['Hometown'] == 'Visayas'
```

selects students whose Hometown is Visayas.

The second condition:

```python
df['Track'] == 'Communication'
```

selects students whose Track is Communication.

The `&` operator means AND, so only students satisfying both conditions are included.

The number of rows was obtained using:

```python
len(VisComm)
```



## B. Visayas Female DataFrame Problem

Create a DataFrame named `VisFemale` containing students whose `Hometown` is Visayas and whose `Gender` is Female. Retain only the columns Name, Track, GEAS, Electronics, and Average. Display `VisFemale`, then display only the rows whose Average is at least 60 without overwriting `VisFemale`.

The following functions, methods, and operators were used:
- `df.loc[]` - selects rows and columns using labels and Boolean conditions.
- `==` - checks whether a column value matches the required category.
- `&` - combines the Hometown and Gender conditions using AND.
- `['Name', 'Track', 'GEAS', 'Electronics', 'Average']` - selects the required columns in the specified order.
- `>=` - checks whether a numerical value is greater than or equal to a specified threshold.


The overall mean was calculated by using:

```python
overall_mean = df[['Math', 'Electronics', 'GEAS', 'Communication', 'Average']].mean()

overall_mean
```

The required DataFrame was created using:

```python
VisFemale = df.loc[
    (df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female'),
    ['Name', 'Track', 'GEAS', 'Electronics', 'Average']
]

VisFemale
```

The condition:

```python
(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female')
```

means that both requirements must be satisfied. A student is included only when the student's Hometown is Visayas AND the student's Gender is Female.

The second filtering operation was performed using:

```python
VisFemale.loc[VisFemale['Average'] >= 60]
```

The condition:

```python
VisFemale['Average'] >= 60
```

selects only rows whose Average is at least 60.

`VisFemale` is not overwritten. The filtered result is displayed separately, which preserves the original `VisFemale` DataFrame as required.


## C. Category-Average Visualization Problem

Exaine how the recorded `Average` differs across the three categorical features `Track`, `Gender`, and `Hometown`.

The problem requires:
1. computing the mean of Average for every category using Pandas;
2. displaying the three summary tables;
3. creating one figure containing three bar charts; and
4. writing three concise statements identifying the category with the highest sample mean for each feature.

The following functions, methods, and operations were used:
- `.groupby()` - groups rows according to the values of a categorical column.
- `['Average']` - selects the numerical variable whose mean is being calculated.
- `.mean()` - calculates the arithmetic mean for each category.
- `plt.figure()` - creates the figure used for the visualizations.
- `plt.subplot()` - divides the figure into three plotting areas.
- `plt.bar()` - creates bar charts from category labels and their corresponding mean values.
- `plt.title()` - label the horizontal and vertical axes.
- `plt.tight_layout()` - automatically adjusts the spacing between the three charts.
- `fig.text` - adds the text at specific positions within a figure outside the plot area.
- `plt.show()` - displays the completed figure.

### Mean Average by Track

The mean Average for each Track category was calculated using:

```python
track_mean = df.groupby('Track')['Average'].mean()
track_mean
```

`.groupby('Track')` places students into groups according to their Track. Selecting `['Average']` identifies the numerical column to summarize, while `.mean()` calculates the sample mean for each Track category.

### Mean Average by Gender

The mean Average for each Gender category was calculated using:

```python
gender_mean = df.groupby('Gender')['Average'].mean()
gender_mean
```

This groups the dataset by Gender and computes the mean Average for every Gender category.

### Mean Average by Hometown

The mean Average for each Hometown category was calculated using:

```python
hometown_mean = df.groupby('Hometown')['Average'].mean()
hometown_mean
```

This groups the dataset by Hometown and computes the mean Average for every Hometown category.

### Three Bar Charts

The three summary results were visualized in one figure using:

```python
fig = plt.figure(figsize=(15, 4))

plt.subplot(1, 3, 1)
plt.bar(track_mean.index, track_mean.values, color = '#bdbbec')
plt.title('Mean Average by Track')

plt.subplot(1, 3, 2)
plt.bar(gender_mean.index, gender_mean.values, color = '#E3C4D8')
plt.title('Mean Average by Gender')

plt.subplot(1, 3, 3)
plt.bar(hometown_mean.index, hometown_mean.values, color = '#c1e6df')
plt.title('Mean Average by Hometown')

plt.tight_layout()
fig.text(0,-0.2, 'Interpretation\n\n1. Communication has the highest sample mean Average (67.97) in the Track category.\n2. Male has the highest sample mean Average (67.18) in the Gender category.\n3. Luzon has the highest sample mean Average (68.08) in the Hometown category.')
plt.show()
```

`track_mean.index`, `gender_mean.index`, and `hometown_mean.index` provide the category labels directly from the calculated Pandas results. The corresponding `.values` provide the mean Average values used as the heights of the bars. Therefore, the plotted values are derived from the dataset rather than manually entered.


The figure contains three separate bar charts:
- Mean Average by Track
- Mean Average by Gender
- Mean Average by Hometown


## Jupyter Notebook

To view the complete Python program for Programming Assignment 4, open [ECE2112 - PA4.ipynb](https://github.com/niamhreesepamilar/ECE-2112-PA-4/blob/main/ECE2112%20-%20PA4.ipynb) in Jupyter Notebook and select **Run All** to execute every cell.

Thank you for reading!
