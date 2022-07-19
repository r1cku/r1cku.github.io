---
title: 10 Exploratory Data Analysis in Python
author: RvDW
date: 2022-07-15 12:44:00 +0800
categories: [Data Analyst, Demo]
tags: [data]
math: true
mermaid: true
# image:
#  path: /commons/devices-mockup.png
#  width: 800
#  height: 500
#  alt: Responsive rendering of Chirpy theme on multiple devices.
---

How do we get from data to answers? Exploratory data analysis is a process for exploring datasets, answering questions, and visualizing results. This course presents the tools you need to clean and validate data, to visualize distributions and relationships between variables, and to use regression models to predict and explain. You'll explore data related to demographics and health, including the National Survey of Family Growth and the General Social Survey. But the methods you learn apply to all areas of science, engineering, and business. You'll use Pandas, a powerful library for working with data, and other core Python libraries including NumPy and SciPy, StatsModels for regression, and Matplotlib for visualization. With these tools and skills, you will be prepared to work with real data, make discoveries, and present compelling results.

# Read, clean, and validate
The first step of almost any data project is to read the data, check for errors and special cases, and prepare data for analysis. This is exactly what you'll do in this chapter, while working with a dataset obtained from the National Survey of Family Growth.
## DataFrames and Series
```python
# Display the number of rows and columns
df.shape

# Display the names of the columns
df.columns

# Select column col_1: series_1
series_1 = df['col_1']

# Print the first 5 elements of series_1
print(series_1.head())

```
## Validate a variable
```python
# Return a Series containing counts of unique values
df['col_1'].value_counts()

```
## Clean a variable
```python
# Replace the value 8 with NaN
df['col_1'].replace([8], np.nan, inplace=True)

# Print the values and their frequencies
print(df['col_1'].value_counts())

```
## Compute a variable
```python
# Select the columns and divide by 100
ageconception = df['ageconception'] / 100
agepregnant = df['agepregnant'] / 100

# Compute the difference
preg_length = agepregnant - ageconception

# Compute summary statistics
print(preg_length.describe())

```
## Make a histogram
```python
# Plot the histogram
plt.hist(series_1, bins=20, histtype='step')

# Label the axes
plt.xlabel('xlabel')
plt.ylabel('ylabel')

# Show the figure
plt.show()

```
## Compute birth weight
```python
# Create a Boolean Series for col_1
series_1 = df['col_1'] >= 37

# Select the series_2 of series_1
series_3 = series_2[series_1]

# Compute the mean of series_3
print(series_3.mean())

```
## Filter
```python
# Filter col_1
series_1 = df_1['col_1'] >= 37

# Filter single births
series_2 = df_1['col_2'] == 1

# Compute birth weight for single full-term babies
series_3 = df_2[series_1 & series_2]
print('series_3_mean:', series_3.mean())

# Compute birth weight for multiple full-term babies
series_4 = df_2[series_1 & ~series_2]
print('series_4_mean:', series_4.mean())
```
# Distributions
In the first chapter, having cleaned and validated your data, you began exploring it by using histograms to visualize distributions. In this chapter, you'll learn how to represent distributions using Probability Mass Functions (PMFs) and Cumulative Distribution Functions (CDFs). You'll learn when to use each of them, and why, while working with a new dataset obtained from the General Social Survey.
## Make a Probability mass function (PMF)
_PMF_, tells us the probability that a discrete random variable takes on a certain value.
```python
# Compute the PMF for year
pmf_year = Pmf(gss['year'], normalize=False)

# Print the result
print(pmf_year)

```
## Plot a PMF
Now let's plot a PMF for the age of the respondents in the GSS dataset. The variable `'age'` contains respondents' age in years.
```python
# Select the column_1
series_1 = df['column_1']

# Make a PMF of series_1
series_2 = Pmf(series_1)

# Plot the PMF
series_2.bar()

# Label the axes
plt.xlabel('x')
plt.ylabel('PMF')
plt.show()

```
![[Pmf_bar_plot.png|300]]
## Make a Cumulative distribution function (CDF)
In this exercise, you'll make a _CDF_ and use it to determine the fraction of respondents in the GSS dataset who are OLDER than 30.
The GSS dataset has been preloaded for you into a DataFrame called `gss`.
As with the `Pmf` class from the previous lesson, the `Cdf` class you just saw in the video has been created for you, and you can access it outside of DataCamp via the [`empiricaldist`](https://pypi.org/project/empiricaldist/) library.
```python
# Select the column_1
series_1 = df['column_1']

# Compute the CDF of series_1
series_2 = Cdf(series_1)

# Calculate the CDF of 30
print(series_2[30])
```
## Compute IQR

Recall from the video that the interquartile range (IQR) is the difference between the 75th and 25th percentiles. It is a measure of variability that is robust in the presence of errors or extreme values.

In this exercise, you'll compute the interquartile range of income in the GSS dataset. Income is stored in the `'realinc'` column, and the CDF of income has already been computed and stored in `cdf_income`.
```python
# Calculate the 75th percentile 
percentile_75th = cdf_series.inverse(0.75)

# Calculate the 25th percentile
percentile_25th = cdf_series.inverse(0.25)

# Calculate the interquartile range
iqr = percentile_75th - percentile_25th

# Print the interquartile range
print(iqr)
```
## Plot a CDF
The distribution of income in almost every country is long-tailed; that is, there are a small number of people with very high incomes.
In the GSS dataset, the variable `'realinc'` represents total household income, converted to 1986 dollars. We can get a sense of the shape of this distribution by plotting the CDF.
```python
# Select column_1
series_1 = df['column_1']

# Make the CDF
cdf_series_1 = Cdf(series_1)

# Plot it
cdf_series_1.plot()

# Label the axes
plt.xlabel('x')
plt.ylabel('CDF')
plt.show()

```
## Plot income CDFs

Let's now see what the distribution of income looks like for people with different education levels. You can do this by plotting the CDFs. Recall how Allen plotted the income CDFs of respondents interviewed before and after 1995:

``` python
Cdf(income[pre95]).plot(label='Before 1995')
Cdf(income[~pre95]).plot(label='After 1995')
```

You can assume that Boolean Series have been defined, as in the previous exercise, to identify respondents with different education levels: `high`, `assc`, and `bach`.
```python
income = gss['realinc']

# Plot the CDFs
Cdf(income[high]).plot(label='High school')
Cdf(income[assc]).plot(label='Associate')
Cdf(income[bach]).plot(label='Bachelor')

# Label the axes
plt.xlabel('Income (1986 USD)')
plt.ylabel('CDF')
plt.legend()
plt.show()

```
![[Cdf_plot_income_distribution.png|300]]
## Distribution of income

In many datasets, the distribution of income is approximately lognormal, which means that the logarithms of the incomes fit a normal distribution. We'll see whether that's true for the GSS data. As a first step, you'll compute the mean and standard deviation of the log of incomes using NumPy's `np.log10()` function.

Then, you'll use the computed mean and standard deviation to make a `norm` object using the [`scipy.stats.norm()`](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.norm.html) function.
```python
# Extract realinc and compute its log
income = gss['realinc']
log_income = np.log10(income)

# Compute mean and standard deviation
mean = log_income.mean()
std = log_income.std()
print(mean, std)

# Make a norm object
from scipy.stats import norm
dist = norm(mean,std)

```
## Comparing CDFs

To see whether the distribution of income is well modeled by a lognormal distribution, we'll compare the CDF of the logarithm of the data to a normal distribution with the same mean and standard deviation. These variables from the previous exercise are available for use!

`dist` is a `scipy.stats.norm` object with the same mean and standard deviation as the data. It provides `.cdf()`, which evaluates the normal cumulative distribution function.

Be careful with capitalization: `Cdf()`, with an uppercase `C`, creates `Cdf` objects. `dist.cdf()`, with a lowercase `c`, evaluates the normal cumulative distribution function.
```python
# Evaluate the model CDF
xs = np.linspace(2, 5.5)
ys = dist.cdf(xs)

# Plot the model CDF
plt.clf()
plt.plot(xs, ys, color='gray')

# Create and plot the Cdf of log_income
Cdf(log_income).plot()
    
# Label the axes
plt.xlabel('log10 of realinc')
plt.ylabel('CDF')
plt.show()
```
![[lognormal_plot.png|300]]

## Comparing PDFs

In the previous exercise, we used CDFs to see if the distribution of income is lognormal. We can make the same comparison using a PDF and KDE. That's what you'll do in this exercise!

As before, the `norm` object `dist` is available in your workspace:

    from scipy.stats import norm
    dist = norm(mean, std)
    

Just as all `norm` objects have a `.cdf()` method, they also have a `.pdf()` method.

To create a KDE plot, you can use Seaborn's [`kdeplot()`](https://seaborn.pydata.org/generated/seaborn.kdeplot.html) function. Here, Seaborn has been imported for you as `sns`.
```python
# Evaluate the normal PDF
xs = np.linspace(2, 5.5)
ys = dist.pdf(xs)

# Plot the model PDF
plt.clf()
plt.plot(xs, ys, color='gray')

# Plot the data KDE
sns.kdeplot(log_income)

# Label the axes
plt.xlabel('log10 of realinc')
plt.ylabel('PDF')
plt.show()

```
![[KDE_plot.png|300]]
# Relationships
Up until this point, you've only looked at one variable at a time. In this chapter, you'll explore relationships between variables two at a time, using scatter plots and other visualizations to extract insights from a new dataset obtained from the Behavioral Risk Factor Surveillance Survey (BRFSS). You'll also learn how to quantify those relationships using correlation and simple regression.

## PMF of age

Do people tend to gain weight as they get older? We can answer this question by visualizing the relationship between weight and age. But before we make a scatter plot, it is a good idea to visualize distributions one variable at a time. Here, you'll visualize age using a bar chart first. Recall that all PMF objects have a `.bar()` method to make a bar chart.

The BRFSS dataset includes a variable, `'AGE'` (note the capitalization!), which represents each respondent's age. To protect respondents' privacy, ages are rounded off into 5-year bins. `'AGE'` contains the midpoint of the bins.
```python
# Extract age
age = brfss['AGE']

# Plot the PMF
pmf_age = Pmf(age)
pmf_age.bar()

# Label the axes
plt.xlabel('Age in years')
plt.ylabel('PMF')
plt.show()
```
## Scatter plot
Now let's make a scatterplot of `weight` versus `age`. To make the code run faster, I've selected only the first 1000 rows from the `brfss` DataFrame.

`weight` and `age` have already been extracted for you. Your job is to use `plt.plot()` to make a scatter plot.

```python
# Select the first 1000 respondents
brfss = brfss[:1000]

# Extract age and weight
age = brfss['AGE']
weight = brfss['WTKG3']

# Make a scatter plot
plt.plot(age, weight, 'o', alpha=0.1)

plt.xlabel('Age in years')
plt.ylabel('Weight in kg')

plt.show()

```
![[scatterplt_alpha_age.png|300]]

So far so good. By adjusting alpha we can avoid saturating the plot. Next we'll jitter the data to break up the columns.
## Jittering
In the previous exercise, the ages fall in columns because they've been rounded into 5-year bins. If we jitter them, the scatter plot will show the relationship more clearly. Recall how Allen jittered `height` and `weight` in the video:

```
height_jitter = height + np.random.normal(0, 2, size=len(brfss))
weight_jitter = weight + np.random.normal(0, 2, size=len(brfss))
```

```python
# Select the first 1000 respondents
brfss = brfss[:1000]

# Add jittering to age
age = brfss['AGE'] + np.random.normal(0, 2.5, size=len(brfss))
# Extract weight
weight = brfss['WTKG3']

# Make a scatter plot
plt.plot(age, weight, 'o', alpha=0.2)

plt.xlabel('Age in years')
plt.ylabel('Weight in kg')
plt.show()

```
Excellent. By smoothing out the ages and avoiding saturation, we get the best view of the data. But in this case the nature of the relationship is still hard to see. In the next lesson, we'll see some other ways to visualize it.
## Height and weight
Previously we looked at a scatter plot of height and weight, and saw that taller people tend to be heavier. Now let's take a closer look using a box plot. The `brfss` DataFrame contains a variable `'_HTMG10'` that represents height in centimeters, binned into 10 cm groups.
Recall how Allen created the box plot of `'AGE'` and `'WTKG3'` in the video, with the y-axis on a logarithmic scale:

```
sns.boxplot(x='AGE', y='WTKG3', data=data, whis=10)
plt.yscale('log')
```
![[boxplot-seaborn.png|300]]



# Multivariate Thinking
Explore multivariate relationships using multiple regression to describe non-linear relationships and logistic regression to explain and predict binary variables.


