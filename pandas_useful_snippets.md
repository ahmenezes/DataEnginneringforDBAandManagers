# Pandas Survival kit 

This is a set of survival snippets to start with Python Pandas

First of all, some useful links:

    Interesting snippets sources
        https://allthesnippets.com/search
        https://gist.github.com/bsweger/e5817488d161f37dcbd2

    If you're more related with SQL
        https://pandas.pydata.org/docs/getting_started/comparison/comparison_with_sql.html#compare-with-sql
        https://sql2pandas.pythonanywhere.com/
        https://sql2pandas.pythonanywhere.com/download-files/sql-to-pandas-cheat-sheet

## Create a dataset from a CSV file
    import pandas as pd
    df = pd.read_csv("/Intro-to-Python/Data/sample.csv") 

##  Show the number of rows and columns - using shape
    n_rows, n_cols = df.shape
    print(f"There are {n_rows} rows and {n_cols} columns in the dataframe\n")

## Get a concise summary of a DataFrame on index, data types, memory usage
    print(df.info())

## Show the number of rows only - using shape
    df.shape[0]

## Show the number of rows only - using inbuilt len() function (len meaning 'length')
    len(df)

## Show the number of columns only - using shape
    df.shape[1]

# The data types of the columns
    print(df.dtypes, '\n')

# Get a list of column names
    colnames = list(df.columns)
    print(colnames,"\n")

# Statistics - Describing Numerical Data
the built in function called `.describe()` which will provide some descriptive statistics for all the numerical columns in a dataframe.

    df.describe()

# Statistics - Describing Text (or Categorical) Data
We can still use `describe()` to look at text data, however we need to specify that we're looking at object (text) data types.

Really, the descriptive statistics below are for categorical data, they don't work very well if every value in a field is a different piece of text!

    df.describe(include=['O'])

# Statistics - Count 
count() can be defined for all datatypes, so all columns are computed. Note which columns have some missing data.
    
    df.count()

# Statistics - Minimum & Max value
    
    # min() and max() has a definition for numeric and text data.
    # The minimum value of a text field is the text which is first alphabetically.
    df.min()

    # The maximum value of a text field is the text which is last alphabetically.
    df.max() 

# Use tabulate to show sample data 
    from tabulate import tabulate
    print(tabulate(df.head(), headers='keys'))

# Sample shows n rows chosen at random from the dataframe (1 by default)
    print(tabulate(df.sample(5)))

# Select one column from the dataframe and show the tail of the data
    selected_column_content = df['selected_column']
    print(selected_column_content.tail(),"\n")

# Filtering rows from a dataframe 
works in a very similar way to selecting columns. Simple filtering can be achieved by passing a range to the DataFrame indexer, just like slicing a list.

    # first 5 rows
    df[:5] 

    # arbitrary slice
    df[102:109]

    # 1 row
    df[123:124]


### Export Data Using pandas

Pandas can export DataFrame or Series objects to a range of different data formats, they are all prefixed with `.to`.

    df.to_excel('../Save/output_file.xlsx')


## Conditional Filtering

Most filtering is a more involved operation where we first specify the condition(s) that must be met in order for rows to be included in or excluded from the output dataframe.

## The Filtering Process

The way that pandas filters rows can be though of as a two-step process.

1. Create a 'mask' that specifies inclusion and exclusion for each row in the dataframe.
2. Mask the dataframe to return the subset of rows that are included.

This sounds a bit abstract, so let's consider what this might look like in practice.

Imagine you have the following (very simple) dataframe, called 'catdog':

| index | Animal | Name            |
|-------|--------|-----------------|
| 0     | Cat    | Catalie Portman |
| 1     | Cat    | Pico de Gato    |
| 2     | Dog    | Chewbarka       |
| 3     | Cat    | JK Meowling     |

You want to filter so you just have 'Cat' rows. Therefore you design the following condition:

```python 
mask = catdog['Animal'] == 'Cat'
```

There are a lot of = (equals) in the above statement.
* The first = indicates assignment, we are assigning the outcome of the expression on the right to the variable on the left of the equals sign.
* The second double equals sign, ==, indicates a comparison, in this case it assesses whether each value in the 'Animal' column of catdog is equal to the text 'Cat'. If python finds that the column value and 'Cat' are the same it assigns a True value, and if not a False value.

This produces a 'mask' which is a Series of `True` and `False` values against the DataFrame index.

| index | &#xfeff; |
|-------|----------|
| 0     | True     |
| 1     | True     |
| 2     | False    |
| 3     | True     |

Now, you just have to pass the mask to the original dataframe to complete the filtering process.

```python
catdog2 = catdog[mask]
catdog2
```
This subsets the catdog dataframe based on the True (include) and False (exclude) values. Producing:

| index | Animal | Name            |
|-------|--------|-----------------|
| 0     | Cat    | Catalie Portman |
| 1     | Cat    | Pico de Gato    |
| 3     | Cat    | JK Meowling     |

The row that had a 'Dog' value for 'Animal', has been removed. Note though that the index has remained the same as the original. Sometimes it is important to reset the index after filtering to restore the index to sequential integers starting at 0.

If you want to reset the index - you can do so by using this code - 

```python
catdog2 = catdog2.reset_index(drop = True)
catdog2
```
| index | Animal | Name            |
|-------|--------|-----------------|
| 0     | Cat    | Catalie Portman |
| 1     | Cat    | Pico de Gato    |
| 2     | Cat    | JK Meowling     |


See above that the index has been reset to be sequential.

## Filtering Data

Just like with simple conditional statements, we filter by using logical comparison statements

* == 'is equal to' notice the double == and watch out! A single one would be assigning to a variable!
* != 'does not equal' - the opposite of ==
* $\gt$  greater than
* $\lt$ less than
* $\gt$= greater than or equal too
* $\lt$= less than or equal too.

In addition, pandas includes some functions to make particular comparisons easier:

* .isin(list) which we can use for multiple conditions 
* .between() which we can use to specify upper and lower bounds

Finally, the ~ (tilde) allows us to flip or invert an expression. Basically, if an expression returns `[True, True, False]`, the same expression with a ~ in front of it will return `[False, False, True]`.

However, we'll concentrate on the simple operators in the top list for now.

**_PAUSE!_**


This was being very interesting, but my brain was only thinking about SQL.

I kept thinking:
_"How can I make the bridge from SQL to Pandas?"_

That is when I found this interesting link to compare with SQL  help me to translate Pandas to SQL 
https://pandas.pydata.org/docs/getting_started/comparison/comparison_with_sql.html#compare-with-sql

and then I wondered _"maybe someone already created a converter?"_.. and the answer is **YES**
The converter can be found here: https://sql2pandas.pythonanywhere.com/
and the cheat sheet: https://sql2pandas.pythonanywhere.com/download-files/sql-to-pandas-cheat-sheet
here is some examples using the tips dataset
```sql
SELECT * FROM tips WHERE time = 'Dinner' order by tip limit 10
```

The Pandas equivalent version is 
```python
tips[tips['time'] == 'Dinner'].sort_values('tip', ascending = True).head(10)
```

suddenly it started to get a bit easier

```sql
select sex, smoker, count(1) cenas from tips 
where smoker in ('No','Yes')
group by sex, smoker
```

The Pandas equivalent version is 
```python
tips[tips['smoker'].isin(['No','Yes'])].groupby(['sex', 'smoker']).size()
```


# Working with null values
```python
tips[tips['smoker'].isnull()]
```

# Number of non-null count and datatype of each column
```python
df.info()
```

# Duplicated values
```python
# One way we could check for other name duplicates is by taking the mode.
# As mode can be non-unique it returns a series
tips['name'].mode()
```

# Unique / distinct values
```python
unique_countries = list(df['Country'].unique())
```


# Create a new binary variable 
```python
# called 'child', it should have the value 1 when age is under 18 and 0 otherwise.

df['child'] = (df['age'] < 18).astype(int)
print(df['child'].head(),'\n')
```

```python
# Create a new variable called 'embarked_city', map 'S' to 'Southampton', 'C' to 'Cherbourg', and 'Q' to 'Queenstown'.

df['embarked_city'] = df['embarked'].map({'S':'Southampton','C':'Cherbourg','Q':'Queenstown'})
print(df['embarked_city'].sample(5),'\n')
```

# Change Columns order 
```python
columns_reordered = ['ProdID', 'SetName', 'ProdDesc', 'ProdLongDesc', 'ThemeName',
                     'Country', 'Ages', 'ReviewDifficulty', 'NumReviews', 'ListPrice',
                     'WeightGrs', 'PieceCount', 'ValStarRating', 'LaunchDate']

lego_cleaned_data = lego_cleaned_data[columns_reordered]
```


