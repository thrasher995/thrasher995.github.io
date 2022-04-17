---
layout: post
title: Querying using Python
subtitle: Connecting to AWS DB & Querying
categories: Python Pipelines SQL 
tags: [python, data science, data engineering, data pipelines, SQL,queries]
mermaid: false
---

Starting with `import` statements:


```python
import pandas as pd
import psycopg2 as psy
from sqlalchemy import create_engine, inspect
from sqlalchemy.orm import sessionmaker
from sqlalchemy_utils import database_exists, create_database
from config import param_dic as param_dic
```

`param_dic` is a dictionary holding config info to connect to AWS DB

Creating a `connection` object using `psycopg2`:


```python
conn = psy.connect(database=param_dic['db'], user=param_dic['user'],
                   host=param_dic['host'], password=param_dic['password'], port=param_dic['port'])
```

Creating a `cursor` **Factory**


```python
def query_executer(query):
    cursor_obj = conn.cursor()
    cursor_obj.execute(query)
    conn.commit()
```

Neccessary methods:

Creating a `session` *getter* method:


```python
def get_session():
    engine = get_engine(param_dic['user'], param_dic['password'], param_dic['host'], param_dic['port'], param_dic['db'])
    session = sessionmaker(bind=engine)()
    return session
```

Creating an `engine` *getter* method:


```python
def get_engine(user, password, host, port, db):
    engine_url = f"postgresql://{user}:{password}@{host}:{port}/{db}"
    if not database_exists(engine_url):
        create_database(engine_url)
    sql_engine = create_engine(engine_url, pool_size=50, echo=False)
    return sql_engine
```

Creating engine object:


```python
engine = get_engine(param_dic['user'], param_dic['password'], param_dic['host'], param_dic['port'], param_dic['db'])
engine.connect()
session = get_session()
```

To list tables in a database, an inspector object is needed; as engine.table_names() is deprecated


```python
inspector = inspect(engine)
print("Tables in Database:")
tables = inspector.get_table_names()
print(tables)
```

    Tables in Database:
    []
    

Creating Table **users** if it doesn't already exist:


```python
if 'users' not in tables:
    query_executer("CREATE TABLE users (id INT NOT NULL PRIMARY KEY,username VARCHAR(15) UNIQUE,fullname VARCHAR(50),email VARCHAR(100));")
    print("TABLE CREATED")
else:
    print("TABLE 'users' EXISTS !")
```

    TABLE CREATED
    

Storing **query** as pandas `DataFrame`:


```python
query = "SELECT * FROM users"
```

Create a query object using `pandas.read_sql()` method:


```python
query_obj = pd.read_sql(query, engine)
print(query_obj)
```

    Empty DataFrame
    Columns: [id, username, fullname, email]
    Index: []
    

Inserting some data into the table with a function:


```python
def insert_data(id, username, fullname, email):
    try:
        ins_query = f'INSERT INTO users VALUES({id}, \'{username}\', \'{fullname}\', \'{email}\')'
        query_executer(ins_query)
        
    except Exception as e:
        print('Exception: ' + str(e))
        conn.rollback()
```

Using the `insert_data` method to INSERT 3 records into TABLE 'users':


```python
insert_data(1,"thrasher502","Mohammed Darras","some-email@domain")
insert_data(2,"Eddie","Mohammed Darras 2","some-different-email@domain")
query = "SELECT * FROM users"
query_obj = pd.read_sql(query, engine)
print(query_obj)
```

       id     username           fullname                        email
    0   1  thrasher502    Mohammed Darras            some-email@domain
    1   2        Eddie  Mohammed Darras 2  some-different-email@domain
    

Dynamic `id` (last id+1):


```python
if query_obj.empty:
    last_id = 1
else:
    last_id = (query_obj.iloc[-1])['id']
insert_data(last_id + 1,"dynamicID","using iloc","whatever@domain")
```

Printing Table after data insertion:


```python
query = "SELECT * FROM users"
query_obj = pd.read_sql(query, engine)
print(query_obj)
```

       id     username           fullname                        email
    0   1  thrasher502    Mohammed Darras            some-email@domain
    1   2        Eddie  Mohammed Darras 2  some-different-email@domain
    2   3    dynamicID         using iloc              whatever@domain
    

Query with `WHERE`:


```python
query = "SELECT * FROM users WHERE username = 'thrasher502'"
query_obj = pd.read_sql(query, engine)
print(query_obj)
```

       id     username         fullname              email
    0   1  thrasher502  Mohammed Darras  some-email@domain
    
