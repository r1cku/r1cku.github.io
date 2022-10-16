---
title: Chapter 02 - Intermediate Python
date: 2022-10-15 16:00:00 -0100
categories: [Python]
tags: [notes, python, datacamp, data, analyst]     # TAG names should always be lowercase---
img_path: /commons/images
#image:
   #path: /chirpy.jpeg
   #width: 300   # in pixels
   #height: 300   # in pixels
---

# Intermediate Python
Level up your data science skills by creating visualizations using Matplotlib and manipulating DataFrames with pandas.

## Course Description
Learning Python is crucial for any aspiring data science practitioner. Learn to visualize real data with Matplotlib’s functions and get acquainted with data structures such as the dictionary and pandas DataFrame. This four-hour intermediate course will help you to build on your existing Python skills and explore new Python applications and functions that expand your repertoire and help you work more efficiently.

You'll discover how dictionaries offer an alternative to Python lists, and why the pandas dataframe is the most popular way of working with tabular data. In the second chapter of this course, you’ll find out how you can create and manipulate datasets, and how to access them using these structures. Hands-on practice throughout the course will build your confidence in each area.

As you progress, you’ll look at logic, control flow, filtering and loops. These functions work to control decision-making in Python programs and help you to perform more operations with your data, including repeated statements. You’ll finish the course by applying all of your new skills by using hacker statistics to calculate your chances of winning a bet.

Once you’ve completed all of the chapters, you’ll be ready to apply your new skills in your job, new career, or personal project, and be prepared to move onto more advanced Python learning.



```python
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd

# import data
world = pd.read_csv('/DataCamp/data/world.csv')
print(world.head())

# Specify c and alpha inside plt.scatter()
plt.scatter(x = world['gdp_cap'], y = world['life_exp'], s = world['pop'] * 2, c = np.array(world['col']), alpha = 0.8)

# Previous customizations
plt.xscale('log') 
plt.xlabel('GDP per Capita [in USD]')
plt.ylabel('Life Expectancy [in years]')
plt.title('World Development in 2007')
plt.xticks([1000,10000,100000], ['1k','10k','100k'])
# Show the plot
plt.show()


```

            gdp_cap  life_exp        pop     col
    0    974.580338    43.828  31.889923     red
    1   5937.029526    76.423   3.600523   green
    2   6223.367465    72.301  33.333216    blue
    3   4797.231267    42.731  12.420476    blue
    4  12779.379640    75.320  40.301927  yellow



### Interpretation

If you have a look at your colorful plot, it's clear that people live longer in countries with a higher GDP per capita. No high income countries have really short life expectancy, and no low income countries have very long life expectancy. Still, there is a huge difference in life expectancy between countries on the same income level. Most people live in middle income countries where difference in lifespan is huge between countries; depending on how income is distributed and how it is used.

What can you say about the plot?

## Dictorionaries

Dictionaires connectct corresponding elements in two or more lists without requiring indexing.

- To create the dictionary, you need curly brackets.
- inside the curly brackets, you have a bunch of what are called <span style="color:green">key:value pairs</span>.

Using the index method looks like:
```python
pop = [30.55, 2.77, 39.21]
countries = ["afghanistan", "albania", "algeria"]
ind_alb = countries.index("albania")
ind_alb
pop[ind_alb]
```

Dictionary Method looks like:
```python
pop = [30.55, 2.77, 39.21]
countries = ["afghanistan", "albania", "algeria"]

world = {"afghanistan":30.55, "albania":2.77, "algeria":39.21}
print(world["albania"])
```
Printing keys can be done so as for example
```python
print(world.keys())
```
To add or update a new key-value pair, you can use something like this:
```python
europe['iceland'] = 20
```
To check if something is a key in a dictionary use something like (T/F):
```python
print('iceland' in europe)
```
To remove something from a dictionary use:
```python
del(world['iceland'])
```
To fetch information from a dictionary that is more sophisticated use chained square brackets:
```python
europe['spain']['population']
```
To create a sub-dictionary and add it to a dictionary you can use:
```python
europe = { 'spain': { 'capital':'madrid', 'population':46.77 },
           'france': { 'capital':'paris', 'population':66.03 },
           'germany': { 'capital':'berlin', 'population':80.62 },
           'norway': { 'capital':'oslo', 'population':5.084 } }
data = {'capital':'rome',
        'population':59.83}
europe['italy'] = data
```

## Pandas, Part 1

### Build a DataFrame is from a dictionary

```python
# Pre-defined lists
names = ['United States', 'Australia', 'Japan', 'India', 'Russia', 'Morocco', 'Egypt']
dr =  [True, False, False, False, True, True, True]
cpc = [809, 731, 588, 18, 200, 70, 45]

# Import pandas as pd
import pandas as pd

# Create dictionary my_dict with three key:value pairs: my_dict
my_dict = {"country":names,"drives_right":dr,"cars_per_cap":cpc,}

# Build a DataFrame cars from my_dict: cars
cars = pd.DataFrame(my_dict)

# Print cars
print(cars)
```

### Specify the row labels
```python
cars.index = [row_labels]
```

### Import CSV data into Python as a Pandas DataFrame
``` python
cars = pd.read_csv('cars.csv')
```

### these steps can be combined so that:
``` python
cars = pd.read_csv('cars.csv'm index_col = 0)
```


### Square brackets

``` python
cars['cars_per_cap']
cars[['cars_per_cap']]
```

The single bracket version gives a Pandas **Series**, the double bracket version gives a Pandas **DataFrame**.
The following call selects the first five rows from the cars DataFrame:

``` python
cars[0:5]
```
N.B you're using the integer indexes of the rows here, not the row labels! i.e. first row = 0, label≠0

### loc and iloc

With <span style="color:green">loc</span> and <span style="color:green">iloc</span> you can do practically any data selection operation on DataFrames you can think of. loc is label-based, which means that you have to specify rows and columns based on their row and column labels. iloc is integer index based, so you have to specify rows and columns by their integer index like you did in the previous exercise.

```python
cars.loc['RU']
cars.iloc[4]

cars.loc[['RU']]
cars.iloc[[4]]

cars.loc[['RU', 'AUS']]
cars.iloc[[4, 1]]
```

<span style="color:green">loc</span> and <span style="color:green">iloc</span> also allow you to select both rows and columns from a DataFrame

```python
cars.loc['IN', 'cars_per_cap']
cars.iloc[3, 0]

cars.loc[['IN', 'RU'], 'cars_per_cap']
cars.iloc[[3, 4], 0]

cars.loc[['IN', 'RU'], ['cars_per_cap', 'country']]
cars.iloc[[3, 4], [0, 1]]
```

It's also possible to select only columns with loc and iloc. In both cases, you simply put a slice going from beginning to end in front of the comma:

```python
cars.loc[:, 'country'] #series
cars.iloc[:, 1]

cars.loc[:, ['country','drives_right']] # df
cars.iloc[:, [1, 2]]
```

## Comparison Operators

- equal → ==
- inequality → !=
- less than → <- 
- greater than → >
- g.eq → >=
- l.eq → <=b

## Boolean Operators
Before, the operational operators like < and >= worked with Numpy arrays out of the box. Unfortunately, this is not true for the boolean operators and, or, and not.

To use these operators with Numpy, you will need <span style="color:green">np.logical_and()</span>, <span style="color:green">np.logical_or()</span> and <span style="color:green">np.logical_not()</span>. Here's an example on the my_house and your_house arrays from before to give you an idea:
``` python
np.logical_and(my_house > 13, 
               your_house < 15)
```

To experiment with if and else a bit, have a look at this code sample:
``` python
area = 10.0
if(area < 9) :
    print("small")
elif(area < 12) :
    print("medium")
else :
    print("large")
```

## Filtering pandas DataFrames

Filter pandas DataFrames as follows:

- Step 1. select the column you are interested in:
``` python
brics["area"] # or brics.loc[:,"area"] or brics.iloc[:,2]
```
- Step 2. Compare 
``` python
is_huge = brics["area"] > 8
```
- Step 3. subset df
``` python
brics[is_huge]
```
- or all in one step:
``` python
brics[brics["area"] > 8]
```

Remember about np.logical_and(), np.logical_or() and np.logical_not()
You can also use them on Pandas Series to do more advanced filtering operations.
``` python
cpc = cars['cars_per_cap']
between = np.logical_and(cpc > 10, cpc < 80)
medium = cars[between]
```


## While Looping
Below you can find the example from the video where the error variable, initially equal to 50.0, is divided by 4 and printed out on every run:
``` python
# Initialize offset
offset = -6

# Code the while loop
while offset != 0 :
    print("correcting...")
    if offset > 0 :
      offset = offset - 1 
    else : 
      offset = offset + 1    
    print(offset)
```

## For Looping
``` python
fam = [1.73, 1.68, 1.71, 1.89]
for height in fam : 
    print(height)
````

 If you also want to access the index information, so where the list element you're iterating over is located, you can use enumerate().

``` python
# areas list
areas = [11.25, 18.0, 20.0, 10.75, 9.50]

# Change for loop to use enumerate() and update print()
for room_number, area in enumerate(areas) :
    print("room " +str(room_number+1) +":"+str(area))
```

## Loop over list of lists


```python
# house list of lists
house = [["hallway", 11.25], 
         ["kitchen", 18.0], 
         ["living room", 20.0], 
         ["bedroom", 10.75], 
         ["bathroom", 9.50]]
         
# Build a for loop from scratch

for x in house :
    print("the " + x[0] + " is " + str(x[1])+" sqm")
```

    the hallway is 11.25 sqm
    the kitchen is 18.0 sqm
    the living room is 20.0 sqm
    the bedroom is 10.75 sqm
    the bathroom is 9.5 sqm


## Loop over dictionary


```python
# Definition of dictionary
europe = {'spain':'madrid', 'france':'paris', 'germany':'berlin',
          'norway':'oslo', 'italy':'rome', 'poland':'warsaw', 'austria':'vienna' }
          
# Iterate over europe
for key, value in europe.items() :
    print("the capital of " + str(key) + " is " + str(value))
```

    the capital of spain is madrid
    the capital of france is paris
    the capital of germany is berlin
    the capital of norway is oslo
    the capital of italy is rome
    the capital of poland is warsaw
    the capital of austria is vienna


## Loop over Numpy array
If you're dealing with a 1D Numpy array, looping over all elements can be as simple as:
``` python
for x in my_array :
    print(str(x) + " cm")
```
If you're dealing with a 2D Numpy array, it's more complicated. A 2D array is built up of multiple 1D arrays. To explicitly iterate over all separate elements of a multi-dimensional array, you'll need this syntax:
``` python
for x in np.nditer(my_array) :
    print(str(x) + " cm")
```

## Loop over DataFrame

Iterating over a Pandas DataFrame is typically done with the <span style="color:green">iterrows()</span> method. Used in a for loop, every observation is iterated over and on every iteration the row label and actual row contents are available:

``` python
for lab, row in brics.iterrows() :
    ...
```
e.g 

``` python
# Import cars data
import pandas as pd
cars = pd.read_csv('cars.csv', index_col = 0)

# Adapt for loop
for lab, row in cars.iterrows() :
    print(str(lab)+": "+str(row['cars_per_cap']))
```
### add column
``` python
# Import cars data
import pandas as pd
cars = pd.read_csv('cars.csv', index_col = 0)

# Code for loop that adds COUNTRY column
for lab, row in cars.iterrows():
    cars.loc[lab,"COUNTRY"]= (row['country']).upper()


# Print cars
print(cars)
```

If you want to add a column to a DataFrame by calling a function on another column, the iterrows() method in combination with a for loop is not the preferred way to go. Instead, you'll want to use apply().

Compare the iterrows() version with the apply() version to get the same result in the brics DataFrame:
```python
# Import cars data
import pandas as pd
cars = pd.read_csv('cars.csv', index_col = 0)

# Use .apply(str.upper)
cars["COUNTRY"] = cars["country"].apply(str.upper)
print(cars)
```


## Random float

<span style="color:green">random</span> is a sub-package of <span style="color:green">numpy</span>

From the random sub-package there are two functions that will be used: <span style="color:green">seed()</span> and <span style="color:green">rand()</span>

``` python
# Import numpy as np
import numpy as np

# Set the seed
np.random.seed(123)

# Generate and print random float
print(np.random.rand())
```

### Roll the dice
<span style="color:green">randint()</span> generates intergers randomly

Here is an example that returns intergers found on a dice
``` python
import numpy as np
print(np.random.randint(1, 7))
```

Here is an example using randint that could be implemented in a game
``` python
import numpy as np
np.rand.seed(123)
# Starting step
step = 50

# Roll the dice
dice = np.random.randint(1,7)

# Finish the control construct
if dice <= 2 :
    step = step - 1
elif dice <= 5 :
    step = step + 1
else :
    step = step + np.random.randint(1,7)

# Print out dice and step
print(dice)
print(step)
```

### Randomwalk


```python
# Numpy is imported, seed is set
import numpy as np
np.random.seed(123)
# Initialize random_walk
random_walk = [0]

# Complete the ___
for x in range(100) :
    # Set step: last element in random_walk
    step = random_walk[-1]

    # Roll the dice
    dice = np.random.randint(1,7)

    # Determine next step
    if dice <= 2:
         # Replace below: use max to make sure step can't go below 0
        step = max(0, step - 1)
    elif dice <= 5:
        step = step + 1
    else:
        step = step + np.random.randint(1,7)

    # append next_step to random_walk
    random_walk.append(step)

# Print random_walk
print(random_walk)

# Import matplotlib.pyplot as plt
import matplotlib.pyplot as plt

# Plot random_walk
plt.plot(random_walk)

# Show the plot
plt.show()
```

    [0, 3, 4, 5, 4, 5, 6, 7, 6, 5, 4, 3, 2, 1, 0, 0, 1, 6, 5, 4, 5, 4, 5, 6, 7, 8, 9, 8, 9, 8, 9, 10, 11, 12, 11, 15, 16, 15, 16, 15, 16, 17, 18, 19, 20, 21, 22, 25, 26, 27, 28, 33, 34, 38, 39, 38, 39, 40, 39, 40, 41, 43, 44, 45, 44, 43, 44, 45, 44, 43, 44, 45, 47, 46, 45, 46, 45, 46, 47, 48, 50, 49, 50, 51, 52, 53, 54, 53, 52, 53, 52, 53, 54, 53, 56, 57, 58, 59, 58, 59, 60]



### Simulate multiple walks


```python
# numpy and matplotlib imported, seed set.
import numpy as np
np.random.seed(123)
import matplotlib.pyplot as plt

# initialize and populate all_walks
all_walks = []
for i in range(10) :
    random_walk = [0]
    for x in range(100) :
        step = random_walk[-1]
        dice = np.random.randint(1,7)
        if dice <= 2:
            step = max(0, step - 1)
        elif dice <= 5:
            step = step + 1
        else:
            step = step + np.random.randint(1,7)
        random_walk.append(step)
    all_walks.append(random_walk)

# Convert all_walks to Numpy array: np_aw
np_aw = np.array(all_walks)

# Plot np_aw and show
plt.plot(np_aw)
plt.show()
# Clear the figure
plt.clf()

# Transpose np_aw: np_aw_t
np_aw_t = np.transpose(np_aw)

# Plot np_aw_t and show
plt.plot(np_aw_t)
plt.show()
```



```python
### Implement Clumsiness
```


```python
# numpy and matplotlib imported, seed set
import numpy as np
np.random.seed(123)
import matplotlib.pyplot as plt

# Simulate random walk 250 times
all_walks = []
for i in range(250) :
    random_walk = [0]
    for x in range(100) :
        step = random_walk[-1]
        dice = np.random.randint(1,7)
        if dice <= 2:
            step = max(0, step - 1)
        elif dice <= 5:
            step = step + 1
        else:
            step = step + np.random.randint(1,7)

        # Implement clumsiness
        if np.random.rand() <= 0.001 :
            step = 0

        random_walk.append(step)
    all_walks.append(random_walk)

# Create and plot np_aw_t
np_aw_t = np.transpose(np.array(all_walks))
plt.plot(np_aw_t)
plt.show()
```


Notice how some random walks drop to zero

### Plot the Distribution



```python
# numpy and matplotlib imported, seed set
import numpy as np
np.random.seed(123)
import matplotlib.pyplot as plt
# Simulate random walk 500 times
all_walks = []
for i in range(500) :
    random_walk = [0]
    for x in range(100) :
        step = random_walk[-1]
        dice = np.random.randint(1,7)
        if dice <= 2:
            step = max(0, step - 1)
        elif dice <= 5:
            step = step + 1
        else:
            step = step + np.random.randint(1,7)
        if np.random.rand() <= 0.001 :
            step = 0
        random_walk.append(step)
    all_walks.append(random_walk)

# Create and plot np_aw_t
np_aw_t = np.transpose(np.array(all_walks))

# Select last row from np_aw_t: ends
ends = np_aw_t[-1,]
# Plot histogram of ends, display plot
plt.hist(ends)
plt.show()
```
