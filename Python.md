# Introspection

https://www.golinuxcloud.com/python-type-of-variable/

```python
type(foo)

print (Foo.__class__)
#
print(Foo.__bases__)
print(Foo.__dict__)
print(Foo.__doc__)
```

https://stackoverflow.com/questions/34439/finding-what-methods-a-python-object-has

```python
l = []
dir(l)
# we can see that insert is one of the methods
l.insert.__doc__
# returns the documentation string about the insert method
```

# Formatting

## Python 2
```
>>> "hello, %s #%d" % ("world", 1)
'hello, world #1'
```
## Python 3 (and also Python 2)
```
>>> "hello, {} #{}".format("world", 1)
'hello, world #1'
```
### F-strings (only Python 3):
```
>>> who = "world"
>>> number = 1
>>> f"hello, {who} #{number}"
'hello, world #1'
```


# Lambdas

```python
add2 = lambda x: x + 2
add2(5)
> 7
```

# PyTorch

```
a = torch.tensor([1, 2, 3])
a.shape # returns result of type Size 
```

# pandas

## DataFrame

```python
import pandas as pd

df = pd.DataFrame([[1, 2, 3], 
				   [4, 5, 6]])

type(df)
> pandas.core.frame.DataFrame
```

## Make a DataFrame from dictionary (defining columns):
From: https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html
```python
d = {'col1': [1, 2], 'col2': [3, 4]}
df = pd.DataFrame(data=d)
df
```
Output:
```
>    col1  col2
> 0     1     3
> 1     2     4
```

Equivalently:
```python
d = [[1, 3],
    [2, 4]]
d.columns = ['col1', 'col2']
```


```python
# returns a DataFrame of True/False values, isnull() is evaluated for every cell of the original DataFrame
df.isnull()

# returns values (flattened?) as a numpy array:
df.isnull().values

type(df.isnull().values)
> numpy.ndarray

# returns numpy.bool_ value whether there are any null (numpy.nan) values in the DataFrame
df.isnull().values.any()
```

```python
# copy DataFrame
df_copy = df.copy()
```

```python
# drop NaN values
df_copy = df.dropna()
```

```python
# get all values in one column (series)
type(df["label"])
> pandas.core.series.Series
```

Can apply `value_counts()` to a series to get another series (like a "group by")
```python
df["label"].value_counts()
```

```python
# Can apply a lambda function to every element of the series:
df["label"].apply(lambda value: value + 2)

# To replace the values in the original DataFrame, you have to assign it back:
df["label"] = df["label"].apply(lambda value: value + 2)
```

`iloc` is the integer indexing of a DataFrame
```python
# get the first row
df.iloc[0]

# get all the rows, and all but the last one columns:
df.iloc[:,:-1]
```
