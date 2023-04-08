# Data structure

Understanding pandas data structure is essential. It helps you better select your data, do operations on it and so on.

Pandas is built on top of NumPy. A dataframe has two components: a numpy array and labels (row labels and column labels)

*pandas = label + a numpy array*

*todo: put an illustration here*

Any operation on a numpy array can be applied on pandas. Label in pandas is used to access your data, rows and / or columns.

Let me illustrate the internal data structure to you step by step.

## Build pandas from scratch

To create a dataframe with DataFrame constructor `pandas.DataFrame(data=None, index=None, columns=None, dtype=None, copy=None)`

The simplest way to create a dataframe is just to pass your data, or a numpy array to the constructor. For example

```py
import pandas as pd
import numpy as np

data = np.ones((5, 5))

df1 = pd.DataFrame(data)

print(df1)
```

output.

```
     0    1    2    3    4
0  1.0  1.0  1.0  1.0  1.0
1  1.0  1.0  1.0  1.0  1.0
2  1.0  1.0  1.0  1.0  1.0
3  1.0  1.0  1.0  1.0  1.0
4  1.0  1.0  1.0  1.0  1.0
```

If you do not specify your row label or column label, pandas will use the integer label by default.

The first row `     0    1    2    3    4` you see on the screen is the column labels, while the first column ranging from 0 to 4 is the row labels.

Let's validate it now.

```py
print('row labels: ', df1.index)
print('column labels', df1.columns)
```

You can get a dataframe's internal data with `DataFrame.values` method.

```py
print(df1.values)
```

output.

```
[[1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1.]]
```

which is a 2D numpy array. let's confirm it with the `type` function.

```py
print(type(df1.values))
```

output.

```
<class 'numpy.ndarray'>
```

Usually we use text as our label instead of integers, now let's create a dataframe with our labels.

```py
data = np.ones((5, 5))

df2 = pd.DataFrame(
     data,
     columns=['col1', 'col2', 'col3', 'col4', 'col5'],
     index=['row1', 'row2', 'row3', 'row4', 'row5']
)

print(df2)
```

output.

```
      col1  col2  col3  col4  col5
row1   1.0   1.0   1.0   1.0   1.0
row2   1.0   1.0   1.0   1.0   1.0
row3   1.0   1.0   1.0   1.0   1.0
row4   1.0   1.0   1.0   1.0   1.0
row5   1.0   1.0   1.0   1.0   1.0
```

Let me illustrate pandas data structure again.

First the label.

```py
print('column labels: ', df2.columns)
print('row labels: ', df2.index)
```

output.

```
column labels:  Index(['col1', 'col2', 'col3', 'col4', 'col5'], dtype='object')
row labels:  Index(['row1', 'row2', 'row3', 'row4', 'row5'], dtype='object')
```

Second, the data or a numpy array.

```py
print(df2.values)
```

output

```
[[1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1.]]
```

Let's output our dataset to Excel to have a nicer view for better understanding.

```py
df2.to_excel('~/Desktop/dataset-with-labels.xlsx')
```

Now we've uncovered the pandas internal data sturcture, it has two components, label and a numpy array.

## Access you pandas dataset by label

With labels, you can easily access your data.

For example, select the first column.

```py
print(df2['col1'])
```

output.

```
row1    1.0
row2    1.0
row3    1.0
row4    1.0
row5    1.0
Name: col1, dtype: float64
```

Select the first two columns.

```py
print(df2[['col1', 'col2']])
```

output.

```
      col1  col2
row1   1.0   1.0
row2   1.0   1.0
row3   1.0   1.0
row4   1.0   1.0
row5   1.0   1.0
```

## Do any operation on your pandas data with numpy operation

