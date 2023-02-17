# Python Survival kit

This is a set of survival snippets and notes to start with Python adapted to data engineering.

First of all, some useful links:
    
    Python 3 Cheat Sheet
        https://perso.limsi.fr/pointal/python:memento#python_3_cheat_sheet
    
# Determine the type of an object
use the built-in type() function. In Python, everything is an object. As a result, when you use the type() function to print the type of a variable's value to the console, it returns the class type of the object.
```python
        type(my_object)
```
# Replace in a string
```python
        string.replace(oldvalue, newvalue, count)
        
        my_string.replace(' ', '_').replace('Id','ID')
```
# declare an empty list
```python

        my_list = []
  
        print("Type of a:", my_list(a))
        print("Size of a:", my_list(a)) 
```

# Using `for` with lists
```python
for column_name in lego_cleaned_data.columns:
     new_column_name = column_name.title().replace(' ', '_').replace('Id', 'ID').replace('date', 'Date').replace('name', 'Name').replace('_', '')
     new_columns_list.append(new_column_name)
```


# Using inline `for` with lists 
```python
    new_columns_list = [column_name.title().replace(' ', '_').replace('Id', 'ID').replace('date', 'Date').replace('name', 'Name').replace('_', '') for column_name in lego_cleaned_data.columns]
```

# Replace / update values from a list
```python
df_cleaned['Country'].replace({'Austria':'AU',
                               'Dn':'DN',
                               'CH ':'CH'},
                              inplace = True)
```