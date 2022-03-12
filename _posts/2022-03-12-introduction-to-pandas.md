---
layout: post
title: Introduction to Pandas
subtitle: DataFrames, Series, and functions
categories: Python Pandas
tags: [pandas, python, data engineering, data science]
mermaid: false
---

## What is Pandas?
- Pandas is a fast, powerful, flexible, and easy to use, **open source** data analysis and manipulation tool, built on top of the Numpy package.
- It's a **high-level** tool.
- Tabular data is stored in DataFrame objects.

## Why use Pandas?
- Makes analyzing big data much easier and more effiecient.
- It can clean messy data from datasets, increasing readibility and relevancy.

## Introduction to DataFrame objects
- **keys** in DataFrames represent column labels.
- **values** in DataFrames represent data in columns (column by column).

### Creating a DataFrame object
1. Creating a DataFrame from an existent dictionary:
    - Syntax: (refer to pandas doc. for all arguments)
        <pre>
        <i> identifier_name = pandas.DataFrame(dict_name) </i></pre>

    #### **Example 1:** *Creating a DataFrame from a dictionary*

    ```
    import pandas as pd

    engines_dict = {'Engine Block': ['4A', 'SR20', '1JZ', '2JZ', '3S'],
                                'Displacement in L': [1.6, 2.0, 2.5, 3.0, 2.0]}
    engines_df = pd.DataFrame(engines_dict)
    print(type(engines_df))
    print(engines_df)
    ```
    
    Output:

    ```
    <class 'pandas.core.frame.DataFrame'>
     Engine Block  Displacement in L
    0           4A                1.6
    1         SR20                2.0
    2          1JZ                2.5
    3          2JZ                3.0
    4           3S                2.0
    ```
    - First column (0,1,2,3,4) is called **index column**

2. Creating a DataFrame from a CSV file:
    - Using `pandas.read_csv()` method.
    - Syntax: (refer to pandas doc. for all arguments)
        <pre>
        <i> identifier_name = pandas.read_csv('path/.../filename.csv') </i></pre>
    - *names* argument for `read_csv()` method is used for custom headers.
    - *skiprows* argument for `read_csv()` method is used to skip rows at the start of the CSV file.
    - *index_col* argument for `read_csv()` method is used to replace **index column** with a column of
         choosing from CSV file.
    #### **Example 2:** *Creating a DataFrame from a CSV file*
    The data in the dictionary from **Example 1** has been saved in 'engines.csv'.
    1. Using headers in CSV file:

        ```
        import pandas as pd

        engines_df = pd.read_csv('engines.csv')
        print(type(engines_df))
        print(engines_df)
        ```
        
        Output:

        ```
        <class 'pandas.core.frame.DataFrame'>
          Engine Block  Displacement in L
        0           4A                1.6
        1         SR20                2.0
        2          1JZ                2.5
        3          2JZ                3.0
        4           3S                2.0
        ```

    2. Using custom header & skipping first row:
        
        ```
        import pandas as pd

        engines_df = pd.read_csv('engines.csv', names=['Engine','L'],skiprows=1)
        print(type(engines_df))
        print(engines_df)
        ```

        Output:

        ```
        <class 'pandas.core.frame.DataFrame'>
          Engine    L
        0     4A  1.6
        1   SR20  2.0
        2    1JZ  2.5
        3    2JZ  3.0
        4     3S  2.0
        ```
    
### Indexing & Selecting data from a DataFrame
+ Examples here use the DataFrame from **Example 2.2**

+ Using square brackets: 
    - Indexing columns:
        1. Using square brackets `[]`:
            - Returns the entire column as a Series object, which is a 1D-Array.
                <pre><i> dataframe_name['column_header'] </i></pre>
        2. Using nested square brackets `[[]]`:
            - Returns the entire column as a DataFrame object.
                <pre><i> dataframe_name[['column_header']] </i></pre>

    - Indexing rows:
    
        * Rows in a range `[:]`:
            - Returns the entire column as a DataFrame object.
                <pre><i> dataframe_name[start_row_ind:end_row_ind] </i></pre>
            - To return a single a row:
                <pre><i> dataframe_name[row_ind:row_ind + 1] </i></pre>

    #### **Example 3.1**: *Square brackets Example*
    
    ```
    import pandas as pd

    engines_df = pd.read_csv('engines.csv', names=['Engine', 'L'], skiprows=1)
    print(engines_df)

    # Data from rows in a single column as a Series:
    print('\nData from rows in a single column as a Series:')
    print(engines_df['Engine'])
    print(type(engines_df['Engine']))

    # Data from rows in a single column as a DataFrame:
    print('\nData from rows in a single column as a DataFrame:')
    print(engines_df[['Engine']])
    print(type(engines_df[['Engine']]))

    # Data from a single Row:
    print('\nData from a single Row:')
    print(engines_df[0:1])
    print(type(engines_df[0:1]))

    # Data from rows in a range:
    print('\nData from rows in a range:')
    print(engines_df[1:4])
    print(type(engines_df[1:4]))

    ```

    Output:
    
    ```
      Engine    L
    0     4A  1.6
    1   SR20  2.0
    2    1JZ  2.5
    3    2JZ  3.0
    4     3S  2.0

    Data from in rows a single column as a Series:
    0      4A
    1    SR20
    2     1JZ
    3     2JZ
    4      3S
    Name: Engine, dtype: object
    <class 'pandas.core.series.Series'>

    Data from rows in a single column as a DataFrame:
      Engine
    0     4A
    1   SR20
    2    1JZ
    3    2JZ
    4     3S
    <class 'pandas.core.frame.DataFrame'>

    Data from a single Row:
      Engine    L
    0     4A  1.6
    <class 'pandas.core.frame.DataFrame'>

    Data from rows in a range:
      Engine    L
    1   SR20  2.0
    2    1JZ  2.5
    3    2JZ  3.0
    <class 'pandas.core.frame.DataFrame'>
    ```



+ Using `loc` & `iloc`:
    - `loc`: based on labels
        1. Accessing an single row `[]`:
            - Returns a single row as a **Series** object, which is a 1D-Array.
                <pre><i> dataframe_name.col[row_label] </i></pre>
            
        2. Accessing multiple rows `[:]` or `[[,]]`:
            - Returns multiple rows as a **DataFrame** object.
            - Not indicating start & end rows returns all rows.
            - Returning rows in a range `[:]`:
                <pre><i> dataframe_name.col[start_row_label:end_row_label] </i></pre>
            - Returning rows not in a range `[[,]]`:
                <pre><i> dataframe_name.col[row1_label,row2_label,...] </i></pre>

        3. Accessing a value in a specific row & specific col. `[][]`:
            - Returns the value in RxCy of its type.
                <pre><i> dataframe_name[row_label][column_header] </i></pre>

        4. Accessing multiple rows & a single specific col. `[:][]`:
            - Returns a **Series** object.
                <pre><i> dataframe_name[start_row_label:end_row_label][column_label] </i></pre> 

        5. Accessing single/multiple rows & specific columns `[:,[]]` or `[[,],]`:
            - Returns a **DataFrame** object.
            - To access a single row, remove colon.
            - Returning rows in a range `[:,[]]`:
                <pre><i> dataframe_name[start_row_label:end_row_label,[column1_label,column2_label,...]] </i></pre>
            - Returning rows not in a range `[[,],]`:
                <pre><i> dataframe_name[[row1_label,row2_label,...],[column1_label,column2_label,...]] </i></pre>
    
    - `iloc`: based on integer positions
        * Same as iloc, but integer positions are used instead.
        * In specified ranges`[a:b]`, the ending range (b) is not included in output.

    #### **Example 3.2**: *`loc` & `iloc` Example*
    ```
    import pandas as pd

    engines_df = pd.read_csv('engines.csv', names=['Engine', 'L'], skiprows=1)
    print(engines_df)
    loc_list = []
    iloc_list = []

    # Data from a single row `[]`:
    print('\nData from a single row as a Series:')
    temp_loc = engines_df.loc[2]
    temp_iloc = engines_df.iloc[2]
    temp_loc_tuple = (temp_loc,type(temp_loc))
    temp_iloc_tuple = (temp_iloc,type(temp_iloc))
    loc_list.append(temp_loc_tuple)
    iloc_list.append(temp_iloc_tuple)

    print(temp_loc)
    print(type(temp_loc))

    # Data from multiple rows `[:]` or `[,]`:
    print('\nData from multiple rows in a range as a DataFrame:')
    temp_loc = engines_df.loc[0:3]
    temp_iloc = engines_df.iloc[0:4]
    temp_loc_tuple = (temp_loc,type(temp_loc))
    temp_iloc_tuple = (temp_iloc,type(temp_iloc))
    loc_list.append(temp_loc_tuple)
    iloc_list.append(temp_iloc_tuple)

    print(temp_loc)
    print(type(temp_loc))

    print('\nData from multiple rows not in a range as a DataFrame:')
    temp_loc = engines_df.loc[[1,2]]
    temp_iloc = engines_df.iloc[[1,2]]
    temp_loc_tuple = (temp_loc,type(temp_loc))
    temp_iloc_tuple = (temp_iloc,type(temp_iloc))
    loc_list.append(temp_loc_tuple)
    iloc_list.append(temp_iloc_tuple)

    print(temp_loc)
    print(type(temp_loc))

    # A value from a specific row & specific col. `[][]`:
    print('\nData from a specific row & specific col. as a DataFrame:')
    temp_loc = engines_df.loc[1]['Engine']
    temp_iloc = engines_df.iloc[1][0]
    temp_loc_tuple = (temp_loc,type(temp_loc))
    temp_iloc_tuple = (temp_iloc,type(temp_iloc))
    loc_list.append(temp_loc_tuple)
    iloc_list.append(temp_iloc_tuple)

    print(temp_loc)
    print(type(temp_loc))

    # Data from multiple rows & a single specific col. `[:][]`:
    print('\nData from multiple rows & specific col. as a DataFrame:')
    temp_loc = engines_df.loc[0:3,'Engine']
    temp_iloc = engines_df.iloc[0:4,0]
    temp_loc_tuple = (temp_loc,type(temp_loc))
    temp_iloc_tuple = (temp_iloc,type(temp_iloc))
    loc_list.append(temp_loc_tuple)
    iloc_list.append(temp_iloc_tuple)

    print(temp_loc)
    print(temp_iloc)
    print(type(temp_loc))

    # Data from single/multiple rows & specific columns `[:,[]]` or `[[,],]`:
    print('\nData from a single row & specific columns as a Series:')
    temp_loc = engines_df.loc[2,['Engine','L']]
    temp_iloc = engines_df.iloc[2,[0,1]]
    temp_loc_tuple = (temp_loc,type(temp_loc))
    temp_iloc_tuple = (temp_iloc,type(temp_iloc))
    loc_list.append(temp_loc_tuple)
    iloc_list.append(temp_iloc_tuple)

    print(temp_loc)
    print(type(temp_loc))

    print('\nData from a multiple rows & specific columns as a DataFrame:')
    temp_loc = engines_df.loc[[1,4],['Engine','L']]
    temp_iloc = engines_df.iloc[[1,4],[0,1]]
    temp_loc_tuple = (temp_loc,type(temp_loc))
    temp_iloc_tuple = (temp_iloc,type(temp_iloc))
    loc_list.append(temp_loc_tuple)
    iloc_list.append(temp_iloc_tuple)

    print(temp_loc)
    print(type(temp_loc))



    flag = True

    # Comparing the 2 lists:
    for i in range(len(iloc_list)):
        if (type(iloc_list[i][0])==pd.Series) or (type(iloc_list[i][0])==pd.DataFrame):
            # print(type(iloc_list[i][0]))
            if not (loc_list[i][0].equals(iloc_list[i][0])):
                print(not (loc_list[i][0].equals(iloc_list[i][0])))
                print(iloc_list[i][0])
                print(loc_list[i][0])
                flag = False
                print(str(i),type(iloc_list[i][0]))
        else:
            if not (loc_list[i][0]==(iloc_list[i][0])):
                print(1)
                print(not (loc_list[i][0].equals(iloc_list[i][0])))
                print(iloc_list[i][0])
                print(loc_list[i][0])
                flag = False
                print(str(i),type(iloc_list[i][0]))

    print('Lists are equal (T/F):',flag)
    ```

    Output:

    ```
      Engine    L
    0     4A  1.6
    1   SR20  2.0
    2    1JZ  2.5
    3    2JZ  3.0
    4     3S  2.0

    Data from a single row as a Series:
      Engine    1JZ
    L         2.5
    Name: 2, dtype: object
    <class 'pandas.core.series.Series'>

    Data from multiple rows in a range as a DataFrame:
      Engine    L
    0     4A  1.6
    1   SR20  2.0
    2    1JZ  2.5
    3    2JZ  3.0
    <class 'pandas.core.frame.DataFrame'>

    Data from multiple rows not in a range as a DataFrame:
      Engine    L
    1   SR20  2.0
    2    1JZ  2.5
    <class 'pandas.core.frame.DataFrame'>

    Data from a specific row & specific col. as a DataFrame:
    SR20
    <class 'str'>

    Data from multiple rows & specific col. as a DataFrame:
    0      4A
    1    SR20
    2     1JZ
    3     2JZ
    Name: Engine, dtype: object
    0      4A
    1    SR20
    2     1JZ
    3     2JZ
    Name: Engine, dtype: object
    <class 'pandas.core.series.Series'>

    Data from a single row & specific columns as a Series:
    Engine    1JZ
    L         2.5
    Name: 2, dtype: object
    <class 'pandas.core.series.Series'>

    Data from a multiple rows & specific columns as a DataFrame:
      Engine    L
    1   SR20  2.0
    4     3S  2.0
    <class 'pandas.core.frame.DataFrame'>
    Lists are equal (T/F): True

    Process finished with exit code 0

    ```
