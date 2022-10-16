---
title: Chapter 01 - Introduction to Python for Finance
date: 2022-10-15 16:00:00 -0100
categories: [Python]
tags: [notes, python, datacamp, data, analyst]     # TAG names should always be lowercase---
img_path: /commons/images
#image:
   #path: /chirpy.jpeg
   #width: 300   # in pixels
   #height: 300   # in pixels
---

# Introduction to Python for Finance
Dive into data science using Python and learn how to effectively analyze and visualize your data. No coding experience or skills needed.

## Course Description
Begin your journey into Data Science! Even if you've never written a line of code in your life, you'll be able to follow this course and witness the power of Python to perform Data Science. You'll use data to solve the mystery of Bayes, the kidnapped Golden Retriever, and along the way you'll become familiar with basic Python syntax and popular Data Science modules like Matplotlib (for charts and graphs) and pandas (for tabular data).


## Welcome to Python
Variables can be used to store information and can be used to complete functions

```python
revenue_1 = 229.23
revenue_2 = 177.86
revenue_3 = 89.95
total = revenue_1+revenue_2+revenue_3
print(total)
```

Find the average revenue of the three revenues above!

```python
average = total/3
print(average)
```

## Variable Data Types

There are four data type in Python: 
- *Strings* (str)- 'hello world'
- Integers (int)- 40
- Floats (float)- 3.1417
- Booleens (bool)- True or False


## Boolean Data Types

Vairables in Python may consist of three data types.

 **Strings** require '_ _ _' to enclose the variable


```python
company_1 = 'Apple'
print(company_1)
```

**Intergers** do not require anything additional


```python
year_1 = 2017
print(year_1)
```

**Floats** also do not require any additional information


```python
revenue_1 = 229.23
print(revenue_1)
```

### Determining Types

Python has a built-in command type() that can determine the type of a variable or literal value. 


```python
print(type(company_1))
print(type(year_1))
print(type(revenue_1))
```

### Booleans in Python

Booleans are values that are either True or False. Boolean comparisons include:

operators descriptions:

\ > greater than
    
\ >= greater than or equal
    
< less than
    
<= less than or equal
    
== equal
    
!= does not equal
    


```python
# Test equality
test_company = 'apple'
print(company_1 == test_company)
```


```python
# Compare revenue_1 and revenue_2
print(revenue_1 > revenue_2)
```

### Combining data types

**Strings** and **Floats** cannot be mathematically combined.
To convert a variable x to an integer, you can use the command int(x)
To convert a variable y to a string, you can use the command str(y)


```python
# Update data types
year_1_str = str(year_1)
revenue_1_str = str(revenue_1)

# Create a complete sentence combining only the string data types
sentence = 'The revenue of ' + company_1 + ' in ' + year_1_str + ' was $' + revenue_1_str + ' billion.'

# Print sentence
print(sentence)
```

## Lists


```python
months=['Jan','Feb','Mar','Apr','May','June']
```


```python
months[0]
```


```python
months[3]
```


```python
months[-1]
```


```python
months[-2]
```

### Slicing
Slicing takes a specified series of contents out of a list.
Remember, this syntax indicates subsetting all elements from the start and up to but not including the end element.


```python
months[2:5]
```


```python
months[-4:-1]
```

#### Extended slicing with lists


```python
months[3:]
```


```python
months[:3]
```

#### Slicing with steps
myslist[startAt : endBefore : step]
default step size is 1


```python
months[0:6:2]
```


```python
months[0:6:3]
```

### Exercise


```python
# Create and print list names
names = ["Apple Inc","Coca-Cola","Walmart"]
print(names)

# Create and print list prices
prices = [159.54,37.13,71.17]
print(prices)
```


```python
# Print the first item in names
print(names[0])

# Print the second item in names
print(names[1])

# Print the last element in prices
print(prices[-1])
```


```python
# names
names = ['Apple Inc', 'Coca-Cola', 'Walmart']

# Use slicing on list names
names_subset = names[-2:]
print(names_subset)
```


```python
# prices
prices = [159.54, 37.13, 71.17]

# Use extended slicing on the list prices
prices_subset = prices[:2]
print(prices_subset)
```

#### List Inside of a List


```python
# Create and print the nested list stocks
stocks = [names,prices]
print(stocks)

# Use list indexing to obtain the list of prices
print(stocks[1])
```

#### Subset a nested list


```python
stocks = [['Apple Inc', 'Coca-Cola', 'Walmart'], [159.54, 37.13, 71.17]]

# Use indexing to obtain company name Coca-Cola
print(stocks[0][1])

# Use indexing to obtain 71.17
print(stocks[1][2])
```

### Methods and Functions
Methods are a subset of functions. ie all methods are functions but not all functions are methods.

Functions take objects as inputs are are "passed" an object. e.g type(prices), min(prices), max(prices)

Methods act on objects. e.g list.sort(), list.append(), list.extend(), list.index()

### Exercises


```python
# Print the sorted list prices
prices = [159.54, 37.13, 71.17]
prices.sort()
print(prices)
```


```python
# Find the maximum price in the list price
price_max = max(prices)
print(price_max)
```

.append() increases the lenght of a list by one

.extend() increase the length of the list by the number of elelemtbst that are provided to the methods


```python
# Append a name to the list names
names.append('Amazon.com')
print(names)

# Extend list names
more_elements = ['DowDuPont', 'Alphabet Inc']
names.extend(more_elements)
print(names)
```

.index() return the index of the element specified 


```python
prices = [159.54, 37.13, 71.17, 1705.54, 66.43, 1132.34]

# Do not modify this
max_price = max(prices)
print(prices)
print(max_price)

# Identify index of max price
max_index = prices.index(max_price)
print(max_index)

# Identify the name of the company with max price
max_stock_name = names[max_index]
print(max_stock_name)

# Fill in the blanks 
print('The largest stock price is associated with ' + max_stock_name + ' and is $' + str(max_price) + '.')
```

## Arrays
pip3 install package_name_here

import package_name_here

### Create an array
You can use the NumPy package to create arrays. NumPy arrays are optimized for numerical analyses and contain only a single data type. To convert a list to an array, you can use the array() function from NumPy.


```python
# Import numpy as np
import numpy as np

# Lists
prices = [170.12, 93.29, 55.28, 145.30, 171.81, 59.50, 100.50]
earnings = [9.2, 5.31, 2.41, 5.91, 15.42, 2.51, 6.79]

# NumPy arrays
prices_array = np.array(prices)
earnings_array = np.array(earnings)

# Print the arrays
print(prices_array)
print(earnings_array)
```

### Elementwise operations on arrays
Arrays allow for efficient numerical manipulation of its elements. Let's explore element-wise mathematical operations by calculating price to earnings ratio using two arrays, __prices_array and earnings_array__ from the previous exercise.

This price to earnings ratio, or PE ratio, is a financial indicator of the dollar amount an investor can expect to invest in a company in order to receive one dollar of that company’s earnings.


```python
# Import numpy as np
import numpy as np

# Create PE ratio array
pe_array = prices_array/earnings_array

# Print pe_array
print(pe_array)
```


```python
# Subset the first three elements
prices_subset_1 = prices_array[0:3]
print(prices_subset_1)
```


```python
# Subset last three elements 
prices_subset_2 = prices_array[4:]
print(prices_subset_2)
```


```python
# Subset every third element
prices_subset_3 = prices_array[0:7:3]
print(prices_subset_3)
```

### 2D arrays and functions

Arrays in numpy can also be 2 dimensional.

array=np.array([months,prices])

.shape gives you the dimensions of an array

    e.g print(cpi_array.shape)
    
(2,3) → 2 rows and 3 colums

.size gives you total number of elements in the array

    e.g print(cpi_array.size)
    
6

np.mean calculates the mean of an input

    print(np.mean(prices_array))
    
    
np.std() calculates the standard deviation of an input

    print(np.std(prices_array))
    
    
numpy.arange() creates an array with start, end, step (default step size = 1)

    months = np.arange(1,13)
    
    print(months)
    
[1 2 3 4 5 6 7 8 9 10 11 12]


numpy.transpose() switches rows and columns of a numpy array (2,3) → (3,2)


### Array indexing for 2D arrays

row index 1, column index 2
array[1,2]

all row slice, thrid column
print(array[:,2])


```python
# Create a 2D array of prices and earnings
stock_array = np.array([prices,earnings])
print(stock_array)

# Print the shape of stock_array
print(stock_array.shape)

# Print the size of stock_array
print(stock_array.size)
```


```python
# Transpose stock_array n.b numpy is set as np
stock_array_transposed = np.transpose(stock_array)
print(stock_array_transposed)

# Print the shape of stock_array
print(stock_array_transposed.shape)

# Print the size of stock_array
print(stock_array_transposed.size)
```

### Subsetting 2D arrays
Subsetting 2D arrays is similar to subsetting nested lists. In a 2D array, the indexing or slicing must be specific to the dimension of the array:

array[row_index, column_index]


```python
# Extract the first column from stock_array_transposed and assign it to prices.
# Subset prices from stock_array_transposed
prices = stock_array_transposed[:, 0]
print(prices)
```


```python
# Extract the second column from stock_array_transposed and assign it to earnings.
# Subset earnings from stock_array_transposed
earnings = stock_array_transposed[:,1]
print(earnings)
```


```python
# Subset the price and earning of the first company (row 0) from stock_array_transposed and assign it to company_1.
# Subset the price and earning for first company
company_1 = stock_array_transposed[0,:]
print(company_1)
```

### Calculating Array Stats
Not only can you perform elementwise calculations on NumPy arrays, you can also calculate summary stats such as mean and standard deviation of arrays using functions from NumPy.


```python
prices = [170.12, 93.29, 55.28, 145.30, 171.81, 59.50, 100.50]

# Calculate the mean 
prices_mean = np.mean(prices)
print(prices_mean)
```


```python
# Calculate the standard deviation 
prices_std = np.std(prices)
print(prices_std)
```

### Generating a sequence of numbers
You may want to create an array of a range of numbers (e.g., 1 to 10) without having to type in every single number. The NumPy function arange() is an efficient way to create numeric arrays of a range of numbers. The arguments for arange() include the start, stop, and step interval as shown below:

np.arange(start, stop, step)

(numpy is imported as np)


```python
# Create an array company_ids containing the numbers 1 through 7 (inclusive).
# Create and print company IDs
company_ids = np.arange(1, 8, 1)
print(company_ids)

# Create an array company_ids_odd containing only the odd numbers from 1 through 7 (inclusive).
# Use array slicing to select specific company IDs
company_ids_odd = np.arange(1, 8, 2)
print(company_ids_odd)
```

### Using arrays for analysis
Numpy arrays can also be indexed with other arrays. 


```python
months_array = np.array(['Jan','Feb','Mar','Apr','May', 'Jun'])
indexing_array = np.array([1,3,5])

months_subset = months_array[indexing_array]
print(months_subset)
```


```python
negative_index = np.array([-1,-2])
print(months_array[negative_index])
```


```python
boolean_array = np.array([True,True,True,False,False,False])
print((months_array[boolean_array]))
```

### More on Boolean arrays


```python
prices_array = np.array([238.11,237.81,238.91])
# Create a Boolean Array
boolean_array = (prices_array > 238)
print(boolean_array)
print(prices_array[boolean_array])
```


```python
print(prices_array)

# Find the mean
price_mean = np.mean(prices_array)
print(price_mean)

# Create boolean array
boolean_array = (prices_array > price_mean)
print(boolean_array)

# Select prices that are greater than average
above_avg = (prices_array[boolean_array])
print(above_avg)
```


```python
import numpy as np

names = ['Apple Inc','Abbvie Inc','Abbott Laboratories','Accenture Technologies','Allergan Plc']
sector = ['Information Technology','Health Care','Health Care','Information Technologies','Health Care']

names_array = np.array(names)
sector_array = np.array(sector)

# Find elements in sectors that are equivalent to 'Health Care' and assign the result to boolean_array.
# Create boolean array
boolean_array = (sector_array == 'Health Care')
print(boolean_array)

# Subset names using boolean_array and assign the result to health_care.
# Print only health care companies
health_care = (names_array[boolean_array])
print(health_care)
```

    [False  True  True False  True]
    ['Abbvie Inc' 'Abbott Laboratories' 'Allergan Plc']


## Visualisations in Python

plt.plot() takes arguements that describe the data to be plotted

plt.show() displays plot to screen

plt.xlabel()

plt.ylabel()

plt.title()

plt.scatter()

### Importing matplotlib and pyplot
Pyplot is a collection of functions in the popular visualization package Matplotlib. Its functions manipulate elements of a figure, such as creating a figure, creating a plotting area, plotting lines, adding plot labels, etc.


```python
import matplotlib.pyplot as plt
```


```python
days = [1, 2, 3, ... , 2337, 2338]
prices = [78.72, 78.31, 75.98, ... , 1103.68, 1094.22]

# Import matplotlib.pyplot with the alias plt
import matplotlib.pyplot as plt

# Plot the price of stock over time
plt.plot(days, prices, color="red", linestyle="--")

# Display the plot
plt.show()

```

### Adding axis labels and titles


```python
# Plot the price of stock over time
plt.plot(days, prices, color="red", linestyle="--")

# Add x and y labels
plt.xlabel('Days')
plt.ylabel('Prices, $')

# Add plot title
plt.title('Company Stock Prices Over Time')

# Display the plot
plt.show()
```



```python
days = [1, 2, 3, ... , 1259, 1260]
prices1 = [78.72, 78.31, ... 298.94, 303.4]
prices2 = [62.957142000000005, 62.185715, 62.971428, ..., 192.449997, 193.059998]

# Plot the second line of green colour
plt.plot(days, prices1, color='red')
plt.plot(days, prices2, color='green')

# Add labels
plt.xlabel('Days')
plt.ylabel('Prices, $')
plt.title('Stock Prices Over Time')
plt.show()
```

### Scatterplots
The pyplot module can also be used to make other types of plots, like scatterplots.


```python
days = [1, 2, 3, ..., 2337, 2338]
prices = [78.72, 78.31, 75.98, ..., 1103.68, 1094.22]

# Plot price as a function of time
plt.scatter(days, prices, color='green', s=0.1)

# Show plot
plt.show()
```
