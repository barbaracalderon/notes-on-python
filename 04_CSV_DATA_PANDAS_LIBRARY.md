# CSV Files and Data

```python
import csv
```

CSV = *Comma Separated Values*

It's a great way to represent tabula data, which is data that fits into a table. Python works well with this and even got specific libraries to deal with it - like the Pandas library for Data Analysis.

Let's check out these two libraries: CSV (built-in library) and Pandas Library. 

## CSV (Built-in Library)
There is no need to install packages. CSV is a built-in library.

### ```csv.reader()``` method

```python
impost csv      # No need to install packages, it's built-in
with open("weather_data.csv", mode="r") as data_file:
    data = csv.reader(data_file)
    for row in data:
        print(row)

# It prints:
# ['day', 'temp', 'condition']
# ['Monday', '12', 'Sunny']
# ['Tuesday', '14', 'Rain']
# ['Wednesday', '15', 'Rain']
```

## Pandas - (Install Packages)

You gotta install the packages for access to this library.

*PS: Find the documentation at [Pandas Pydata Org](https://pandas.pydata.org/docs/).*

### ```pandas.read_csv()``` method

Your data is in a beautiful format.

```python
import pandas   # Click to install package
data = pandas.read_csv("weather_data.csv")
print(data)

# It prints:

#         day  temp condition
# 0     Monday    12     Sunny
# 1    Tuesday    14      Rain
# 2  Wednesday    15      Rain
# 3   Thursday    14    Cloudy
# 4     Friday    21     Sunny
# 5   Saturday    22     Sunny
# 6     Sunday    24     Sunny
```

You can check out only the temp column, for example.

```python
import pandas   # Click to install package
data = pandas.read_csv("weather_data.csv")
print(data["temp"])         # Selects only the "temp" column

# It prints:
# 0    12
# 1    14
# 2    15
# 3    14
# 4    21
# 5    22
# 6    24

```
### Overview

Check out the documentation for an accurate explanation.

These are only notes to remind.

Pandas work with two types of objects: dataframe and series. The dataframe corresponds to your data table. The series corresponds to an object list - each column, for example. Like the ```data["temp"]``` from the previous code box.

To know more about what you can do with Pandas, check out their API documentation.

**SERIES**: Documentation [methods for Series](https://pandas.pydata.org/docs/reference/series.html).

**DATAFRAME**: Documentation [methods for Data Frames](https://pandas.pydata.org/docs/reference/frame.html).


*Some methods are specific for dataframes and other methods are specific for series.*

PS: One final thing to add is... behind the curtains, Pandas take the data table label (first row) and turn each label into an attribute. So you can also call ```data["temp"].max()``` as if temp was an attribute, like this: ```data.temp.max()```.

### Method: ```dataframe.to_dict()```

Your data morphs into a Python dictionary.

```python
import pandas   # Click to install package
data = pandas.read_csv("weather_data.csv")
data_dict = data.to_dict()
print(data_dict)

# It prints:
# {'day': {0: 'Monday', 1: 'Tuesday', 2: 'Wednesday', 3: 'Thursday', 4: 'Friday', 5: 'Saturday', 6: 'Sunday'}, 'temp': {0: 12, 1: 14, 2: 15, 3: 14, 4: 21, 5: 22, 6: 24}, 'condition': {0: 'Sunny', 1: 'Rain', 2: 'Rain', 3: 'Cloudy', 4: 'Sunny', 5: 'Sunny', 6: 'Sunny'}}
```
### Method: ```series.to_list()```

Your data morphs into a Python list.

```python
import pandas   # Click to install package
data = pandas.read_csv("weather_data.csv")
temp_list = data["temp"].to_list()
print(temp_list)

# It prints:
# [12, 14, 15, 14, 21, 22, 24]
```
### Method ```series.mean()```

Return the average values for the corresponded axis.

### Method ```series["axis"].max()```

Return the maximum value for the corresponded axis. Remember Pandas morphs the data table label (first row) into attributes. You can also call it ```series.axis.max()```

### Get Data in Row

```python
import pandas   # Click to install package
data = pandas.read_csv("weather_data.csv")
print(data[data.day == "Monday"])       # Get the entire row

# It prints the row:
#       day  temp condition
# 0  Monday    12     Sunny

# Print the row with the maximum temperature:
print(data[data.temp == data.temp.max()])

# It prints:
#       day  temp condition
# 6  Sunday    24     Sunny
```

### Create a Dataframe from Scratch and Save it as a CSV File

You can also create a dataframe with Pandas.

Here's an example.

```python
import pandas   # Click to install package

data_dictionary = {
    "students": ["Amy", "James", "Angela"],
    "scores": [76, 56, 65]
}

data = pandas.DataFrame(data_dictionary)
print(data)

# It prints your dataframe recently created:
#   students  scores
# 0      Amy      76
# 1    James      56
# 2   Angela      65

# Save it as a CSV File:

data.to_csv("new_data.csv")
```

A file will be created in the same folder you're working in.

## Information Table

LIBRARY | SERIES OR DATAFRAME| METHODS | WHAT IT DOES | WHAT IT RETURNS
:------- | :------------------ | :------- | :------------ | :----------------
csv *(built-in)* | - | ```reader()``` | It reads the file and output the data | It returns the content as a csv.reader object, which can be looped through: now, each line is a list and each word is an item inside the line list
pandas *(install package)* | dataframe | ```.to_dict()``` | It morphs the data into a Python dictionary | Nothing
pandas *(install package)* | series | ```.to_list()``` | It morphs the data axis into a Python list | Nothing
pandas *(install package)* | series | ```.mean()``` | It calculates the average number of an axis | Returns the average
pandas *(install package)* | series | ```.max()``` | It locates the maximum value of an axis | Returns the maximum value
pandas *(install package)* | dictionary -> dataframe | ```.DataFrame()``` | It morphs your dictionary to a dataframe | Nothing
pandas *(install package)* | dataframe | ```.to_csv(data)``` | It creates a CSV file for your dataframe | Nothing
