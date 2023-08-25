# Pandas 

Module for practical, real-world data analysis in Python.

*DataFrame* is a data structure that organizes data into a 2-dimensional  
table of rows and columns, much like a spreadsheet.  

## Simple example 

Create a small dataframe and show the columns, values, index, shape and size properties.  

```python
#!/usr/bin/python

import pandas as pd

data = [['Alex', 10], ['Ronald', 18], ['Jane', 33]]
df = pd.DataFrame(data, columns=['Name', 'Age'])

print(df)

print(df.columns)
print(df.values)
print(df.index)

print('----------------')

print(df.shape)
print(df.size)
```

## Change index

By default, the index starts from zero.  

```python
#!/usr/bin/python

import pandas as pd

df = pd.read_csv("military_spending.csv") 
df.index = df.index + 1

print(df)
```

## Custom index

Create a custom index.  

```python
#!/usr/bin/python

import pandas as pd

data = {'country': ['Brazil', 'Russia', 'India', 'China', 'South Africa'],
        'capital': ['Brasilia', 'Moscow', 'New Dehli', 'Beijing', 'Pretoria'],
        'area': [8.516, 17.10, 3.286, 9.597, 1.221],
        'population': [200.4, 143.5, 1252, 1357, 52.98]}

df = pd.DataFrame(data)
print(df)

print('------------------------------')

df.index = ['BR', 'RU', 'IN', 'CH', 'SA']
print(df)
```

## No header/index 

How to turn off header and index.  

```python
#!/usr/bin/python

import pandas as pd 
  
df = pd.read_csv("military_spending.csv") 

# print(df)
print(df.to_string(header=False, index=False))
```

## The head/tail functions

The functions return the first/last n rows.  

```python
#!/usr/bin/python

import pandas as pd 
  
df = pd.read_csv("military_spending.csv") 

print(df.head(4))

print('*******************************************')

print(df.tail(4))
```

## Counting

```python
#!/usr/bin/python

import pandas as pd

df = pd.read_csv("employees.csv")

print(df.count())
print(f'Number of columns: {len(df.columns)}')

print(df.shape)
```

## The describe function

The  `describe` function generates descriptive statistics.  
Descriptive statistics include those that summarize the central tendency,  
dispersion and shape of a dataset's distribution, excluding NaN values. 


```python
#!/usr/bin/python

import pandas as pd

s1 = pd.Series([1, 2, 3, 4, 5, 6, 7, 8])
s2 = pd.Series([12, 23, 31, 14, 11, 61, 17, 18])

data = {'Vals 1': s1, 'Vals 2': s2}
df = pd.DataFrame(data)

print(df.describe())
```

## Basic stats 

```python
#!/usr/bin/python

import pandas as pd
import numpy as np

df = pd.DataFrame(np.arange(0, 1200, 2), columns=['A'])

print(f'mean: {df.values.mean()}')
print(f'std: {df.values.std()}')
print(f'min: {df.values.min()}')
print(f'max: {df.values.max()}')
print(f'sum: {df.values.sum()}')
```

---

```python
#!/usr/bin/python

import pandas as pd
import numpy as np

rng = np.random.default_rng()
sample = rng.integers(low=0, high=12000, size=100) 

df = pd.DataFrame(sample, columns=['A'])

print(f"sum: {sum(df['A'])}")
print(f"min: {min(df['A'])}")
print(f"max: {max(df['A'])}")
print(f"len: {len(df['A'])}")
```

## Selections 

### The loc function 

Selecting rows with slicing syntax  

```python
#!/usr/bin/python

import pandas as pd
import numpy as np

df = pd.read_csv('military_spending.csv')

print(df[2:12:1].to_string(index=False))
```


Selecting columns with labels  

```python
#!/usr/bin/python

import pandas as pd

df = pd.read_csv("military_spending.csv") 

print(df.columns)
print(df.loc[:, [' Country']].to_string(index=False))
```

Selecting with conditions  

```python
#!/usr/bin/python

import pandas as pd

df = pd.read_csv("employees.csv")

data = df.loc[(df['Salary'] > 10000) & (df['Salary'] < 50000)]
print(data.head(15).to_string(index=False))
```

### The take function 

With `take` function we can select columns by index.  

```python
#!/usr/bin/python

import pandas as pd
import numpy as np

df = pd.read_csv('military_spending.csv')
df_c = df.take([1, 2, 3], axis=1)

print(df_c.to_string(index=False))
```


### The iloc function

Selecting columns with indexes  

```python
#!/usr/bin/python

import pandas as pd

df = pd.read_csv("military_spending.csv") 

print(df.iloc[:, [1, 2, 3]].to_string(index=False))
```

---

```python
#!/usr/bin/python

import pandas as pd

df = pd.read_csv("employees.csv")

# integer-location based indexing for selection by position.
# Multiple row and column selections using iloc and DataFrame

print(df.iloc[0:6])  # first six rows of dataframe
print('--------------------------------------')

print(df.iloc[:, 0:2])  # first two columns of data frame with all rows
print('--------------------------------------')

# 1st, 4th, 7th, 25th row + 1st 6th 8th column
print(df.iloc[[0, 3, 6, 24], [0, 5, 7]])
print('--------------------------------------')

# first 5 rows and 5th, 6th, 7th columns of data frame (county -> phone1).
print(df.iloc[:5, 5:8])
print('--------------------------------------')
```

---

Computing the mean for all columns/rows and for a specific column/row

```python
#!/usr/bin/python

import pandas as pd
import numpy as np

df = pd.DataFrame(np.arange(12).reshape(3, 4), columns=['A', 'B', 'C', 'D'])
df.index = df.index + 1
print(df)

print('----------------------------------------')

print(df.mean(axis=1))

print('----------------------------------------')

print(df.mean(axis=0))

print('----------------------------------------')

print(df['A'].mean())

print('----------------------------------------')

print(df.iloc[2].mean())

print('----------------------------------------')
```

## The isin function

Check if the a column is equal to one of the given options.  

```python
#!/usr/bin/python

import pandas as pd

df = pd.read_csv("employees.csv")

res = df.loc[df['Team'].isin(['Marketing', 'Finance'])]
print(res.to_string(index=False))
```

---

The OR selection is similar to the `isin` function.  

```python
#!/usr/bin/env python

import pandas as pd

df = pd.read_csv('employees.csv')

res = df.loc[df['Team'] == 'Finance']
print(res.head(10))

print('---------------------------------')

res = df[(df['Team'] == 'Finance') | (df['Team'] == 'Legal')]
print(res.tail(10))
```



## The drop function 

The `drop` function removes the given columns or rows.  

```python
#!/usr/bin/python

import pandas as pd
import numpy as np

df = pd.DataFrame(np.arange(16).reshape(4, 4), columns=['A', 'B', 'C', 'D'])
df.index = df.index + 1
print(df)

print('----------------------------------------')

df2 = df.drop(['A', 'B'], axis=1)
print(df2)

print('----------------------------------------')

df3 = df.drop([2, 3], axis=0)
print(df3)
```

## Random sample

Return a set of random rows or columns.  

```python
#!/usr/bin/python

import pandas as pd

df = pd.read_csv("military_spending.csv")

print(df.sample(3, axis=0))
```

## Sorting 

Sorting by multiple columns.  

```python
#!/usr/bin/python

import pandas as pd

df = pd.read_csv('products.csv')
print(df.sort_values(['category', 'unit_price', 'units_in_stock'], ascending=[True, False, True]).to_string())
```

## Grouping 

We use the `groupby` function to perform grouping.  
Calculate the number of groups and number of rows in each group  
with `nunique`, `ngroups`, and `size`.   

```python
#!/usr/bin/python

import pandas as pd 
  
df = pd.read_csv('products.csv') 
print(df['category'].nunique())

g = df.groupby('category')
print(g.ngroups)

print('----------------------')

print(g.size())
```

Take the first, last, nth row from each group. 

```python
#!/usr/bin/python

import pandas as pd 

df = pd.read_csv('products.csv') 
g = df.groupby('category')

print(g.first())
print('----------------------')

print(g.last())
print('----------------------')

print(g.nth(6))
print('----------------------')
```


## The to_csv function

The `to_csv` function writes the dataframe to CSV.  

```python
#!/usr/bin/python

import pandas as pd

df = pd.read_csv('products.csv')

res = df[df.index % 2 == 0]
res.to_csv('products2.csv', index=False)
```

## Transform to dictionary

```python
#!/usr/bin/python

import pandas as pd 

data = [['Alex', 10], ['Ronald', 18], ['Jane', 33]]
df = pd.DataFrame(data, columns=['Name', 'Age'])

# df = pd.read_csv("military_spending.csv") 

print('list')
print(df.to_dict(orient='list'))

print('************************************')

print('series')
print(df.to_dict(orient='series'))

print('************************************')

print('dict')
print(df.to_dict(orient='dict'))

print('************************************')

print('split')
print(df.to_dict(orient='split'))

print('************************************')

print('records')
print(df.to_dict(orient='records'))

print('************************************')

print('index')
print(df.to_dict(orient='index'))

print('************************************')

print('tight')
print(df.to_dict(orient='tight'))
```
