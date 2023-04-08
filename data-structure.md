# Data structure

Understanding pandas data structure is essential. It helps you better select your dataset, do operations on it and so on.

pandas is built on top of NumPy. A dataframe has two components: a numpy array and labels (row labels and column labels)

*pandas = label + a numpy array*

*todo: show an illustration of data structure here*

Label in pandas is used to access your data, rows and / or columns. Any operation on a numpy array can be applied on pandas.

Let me illustrate the internal data structure to you step by step.

## Build pandas from scratch

To create a dataframe with DataFrame constructor `pandas.DataFrame(data=None, index=None, columns=None, dtype=None, copy=None)`

*todo: move to the DataFrame constructor webpage to show it*

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

Now I want to select the first two columns, how to do it? Actually there are several ways. First, let's use the most common one, which is with the square brackets `[]`.

```py
print(df2[['col1', 'col2', 'col3']])
```

output.

```
      col1  col2  col3
row1   1.0   1.0   1.0
row2   1.0   1.0   1.0
row3   1.0   1.0   1.0
row4   1.0   1.0   1.0
row5   1.0   1.0   1.0
```

Second, use the `loc` operator, which is more generic. You can just specify the beginning label and end label instead of making a list of the column names as we see in the above way.

```py
print(df2.loc[:, 'col1':'col3'])
```

Inside the `[]`, on left is your row label, while on right is your column label.

output.

```
      col1  col2  col3
row1   1.0   1.0   1.0
row2   1.0   1.0   1.0
row3   1.0   1.0   1.0
row4   1.0   1.0   1.0
row5   1.0   1.0   1.0
```

Third, use the `iloc` operator. Actually this is numpy thing, not pandas thing.

```py
print(df2.iloc[:, :3])
```

Inside the `[]`, on left is your row index, on right is your column index.

output.

```
      col1  col2  col3
row1   1.0   1.0   1.0
row2   1.0   1.0   1.0
row3   1.0   1.0   1.0
row4   1.0   1.0   1.0
row5   1.0   1.0   1.0
```

## Mapping between pandas label and index of numpy array

The reason why I show you how to select your dataset with label and with index is that I guess there must be a mapping between the label and the index which is the index of the numpy array. When you select a subset of your data by label, under the hood it is achieved by index of your numpy array.

*todo: show the mapping relationship in Excel so that your audience can have a visualized understanding*

Similarly, the selecting principles on column label can be applied on row label. In fact, row label and column label are  the same in essence, the only difference is that they are on different direction.

I will make a complete video on selecting your dataset. The focus on today's video is on pandas data structure.

## Do any operation on your pandas data with numpy operation

After understanding pandas data structure, you will understand why numpy's operations can be applied on pandas as well.

Let me show you an brief example.

```py
print(data * 15)
```

output.

```
[[15. 15. 15. 15. 15.]
 [15. 15. 15. 15. 15.]
 [15. 15. 15. 15. 15.]
 [15. 15. 15. 15. 15.]
 [15. 15. 15. 15. 15.]]
```

The `data` numpy array is multiplied by 10 now.

Let's do the same operation on our pandas dataset.

```py
print(df2 * 10)
```

output.

```
      col1  col2  col3  col4  col5
row1  10.0  10.0  10.0  10.0  10.0
row2  10.0  10.0  10.0  10.0  10.0
row3  10.0  10.0  10.0  10.0  10.0
row4  10.0  10.0  10.0  10.0  10.0
row5  10.0  10.0  10.0  10.0  10.0
```

Wonderful! The whole dataset is multiplied by 10.

## Conclusion


