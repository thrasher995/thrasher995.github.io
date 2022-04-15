---
layout: post
title: Introduction to Databases
subtitle: Building Pipelines to Relational Databases
categories: Python Pandas Pipelines
tags: [pandas, databases, python, data engineering]
mermaid: false
---

# What are Relational Databases?
- A **Relational Database** is a collection of data items with pre-defined relationships between them.
- Data is organized in tables.
- Rows are called **Records**.
- Columns are called **Fields**.
- **Tables** can be linked to each other using **unique keys**.
- **SQL** is used to interact with **Relational Databases**.

## Common Relational Databses:
    1- Microsoft SQL Server.
    2- ORACLE.
    3- PostgreSQL.
    4- SQLite.
        - SQLite databases are computer files, improving data sharability.
    
# Connecting to Relational Databases

1- Creating way to connect to database.
2- Query database.

## **Creating Database** Engine using **SQLAlchemy**:
- `sqlalchemy().create_engine()` method creates an engine to handle database connections.
- This method takes URL String as argument, and connects to it.

### Some URL Formats:
- **SQLite**: `sqlite:///path/to/filename.db`

## **Querying Databases** using **SQLAlchemy**:
- `pandas.read_sql(query, engine)`
- Arguments:
    - `query`: String containing SQL Query to run or Table to load.
    - `engine`: Connection/Database engine object.

## `inspect` function in SQLAlchemy:
- Returns an Inspector object.
- Inspector object is needed to list tables in database.

```Python
inspector_name = inspect(engine)
```


## Example 2.1: Printing Tables from a Database
- In this example, the "NYC Weather..." Database file (.db) is used.

```Python
import pandas as pd
from sqlalchemy import create_engine,inspect

# Creating the engine object:
sql_engine = create_engine("sqlite:///D:/Databases/nyc_data.db")

# To list table_names in database, an inspector object is needed; as engine.table_names() is deprecated.
inspector = inspect(sql_engine)

# Listing tables in database:
print("Tables in Database:")
print(inspector.get_table_names())

# Querying from Database using table name as query arg.
print("\nQuerying an entire table:")
weather_data = pd.read_sql("weather", sql_engine)
print(weather_data)

# Querying from Database using SQL command as query arg.
print("\nQuerying average of a column in weather table:")
average_maxTemps = pd.read_sql("SELECT AVG(tmax) FROM \"weather\"", sql_engine)
print(average_maxTemps)

# Querying from Database using a query String
query_str = """SELECT date, tmin
                FROM weather
                WHERE tmin >= 40
                """
min_temps = pd.read_sql(query_str,sql_engine)
print("\nDays where minimum temperatures >= 40:")
print(min_temps)

```

- Output:

<pre>
Tables in Database:
['boro_census', 'hpd311calls', 'weather']

Querying an entire table:
         station                         name  latitude  ...  tavg  tmax tmin
0    USW00094728  NY CITY CENTRAL PARK, NY US  40.77898  ...          52   42
1    USW00094728  NY CITY CENTRAL PARK, NY US  40.77898  ...          48   39
2    USW00094728  NY CITY CENTRAL PARK, NY US  40.77898  ...          48   42
3    USW00094728  NY CITY CENTRAL PARK, NY US  40.77898  ...          51   40
4    USW00094728  NY CITY CENTRAL PARK, NY US  40.77898  ...          61   50
..           ...                          ...       ...  ...   ...   ...  ...
116  USW00094728  NY CITY CENTRAL PARK, NY US  40.77898  ...          47   34
117  USW00094728  NY CITY CENTRAL PARK, NY US  40.77898  ...          52   38
118  USW00094728  NY CITY CENTRAL PARK, NY US  40.77898  ...          53   49
119  USW00094728  NY CITY CENTRAL PARK, NY US  40.77898  ...          62   44
120  USW00094728  NY CITY CENTRAL PARK, NY US  40.77898  ...          58   39

[121 rows x 13 columns]

Querying average of a column in weather table:
   AVG(tmax)
0  43.504132

Days where minimum temperatures >= 40:
          date  tmin
0   12/01/2017    42
1   12/03/2017    42
2   12/04/2017    40
3   12/05/2017    50
4   12/06/2017    40
5   12/19/2017    45
6   01/11/2018    41
7   01/12/2018    44
8   01/21/2018    42
9   01/28/2018    46
10  02/11/2018    45
11  02/15/2018    46
12  02/20/2018    47
13  02/21/2018    55
14  02/24/2018    42
15  02/25/2018    40
16  02/26/2018    43
17  02/28/2018    42
18  03/01/2018    44
19  03/29/2018    49
20  03/30/2018    44

Process finished with exit code 0

</pre>

