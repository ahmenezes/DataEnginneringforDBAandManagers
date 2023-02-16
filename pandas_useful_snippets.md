# Pandas Survival kit 

This is a set of survival snippets to start with Python Pandas

First of all some useful links

    https://allthesnippets.com/search
    https://gist.github.com/bsweger/e5817488d161f37dcbd2

    If you're more related with SQL
        https://pandas.pydata.org/docs/getting_started/comparison/comparison_with_sql.html#compare-with-sql

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

# Use tabulate to show sample data 
    from tabulate import tabulate
    print(tabulate(df.head(), headers='keys'))

# Sample shows n rows chosen at random from the dataframe (1 by default)
    print(tabulate(df.sample(5)))

# Select one column from the dataframe and show the tail of the data
    selected_column_content = df['selected_column']
    print(selected_column_content.tail(),"\n")

