---
layout: post
title: Importing Data from Excel Files
subtitle: Building pipelines to data in spreadsheets
categories: Python Pandas
tags: [pandas, spreadsheets, python, data engineering]
mermaid: false
---
# Introduction to Spreadsheets
- AKA Excel Files
- Data is stored in tabular form in them - cells arranged in rows & columns.
- Can have formatting & formulas, unlike flat files.
- A workbook can have multiple spreadsheets.
- Loaded using `pandas.read_excel()` function.
- `read_excel()` functions returns a DataFrame object.

#### Example 1.1: Loading a Spreadsheet
- The 'fcc_survey.xlsx' Spreadsheet from FreeCodeCamp is used in this example

```Python
import pandas as pd
survey_data = pd.read_excel("fcc_survey.xlsx")
print(survey_data.head())
print(type(survey_data))
```

- Output:
```
    Age  AttendedBootcamp  ...              SchoolMajor  StudentDebtOwe
0  28.0               0.0  ...                      NaN           20000
1  22.0               0.0  ...                      NaN             NaN
2  19.0               0.0  ...                      NaN             NaN
3  26.0               0.0  ...  Cinematography And Film            7000
4  20.0               0.0  ...                      NaN             NaN

[5 rows x 98 columns]
<class 'pandas.core.frame.DataFrame'>

```


# More about `read_excel()` Function:

- `read_excel()` method shares a lot of arguments with `read_csv()`, with some operating differently.

### Some arguments:
- `nrows`: Limits number of rows to load (same as `read_csv()`).
- `skiprows`: Specifies number of rows or row numbers to skip (same as `read_csv()`).
- `usecols`: Chooses columns by name, pos. number, or letter
- `sheet_name`: Selects sheets to load
    
    - By **name** or **zero-indexed pos. integers**.
    - Returns **dictionary** object.
        - `Keys` are sheet names, `Values` are DataFrame objects.
    - Passing *None* to `sheet_name` loads all sheets in a Workbook.
    - A list is passed to load multiple sheets.
    - All arguments passed to `read_excel()` are applied on all sheets loaded.

#### Example 2.1: Getting Data from Ranges A2:A11 & W2:AB11
- Loading Data from ranged A2:A11 & W2:AB11.
- Loading Data from first sheet.

```Python
import pandas as pd
survey_data = pd.read_excel("fcc_survey.xlsx", usecols="A,W:AB", nrows=10, skiprows=2)
print(survey_data)
```

- Output:
```
   Age  CommuteTime  ...      EmploymentFieldOther          EmploymentStatus
0   28           35  ...                       NaN        Employed for wages
1   22           90  ...                       NaN        Employed for wages
2   19           45  ...                       NaN        Employed for wages
3   26           45  ...                       NaN        Employed for wages
4   20           10  ...                       NaN        Employed for wages
5   34           45  ...                       NaN  Self-employed freelancer
6   23           60  ...                       NaN        Employed for wages
7   35          120  ...                       NaN        Employed for wages
8   33            0  ...                       NaN        Employed for wages
9   33           30  ...  Industrial manufacturing        Employed for wages

[10 rows x 7 columns]
```


#### Example 2.2: Getting Data from multiple sheets
- Loading Data from ranged A2:A11 & W2:AB11.
- Loading Data from sheets *2016* & *2017*.

```Python
import pandas as pd
survey_data = pd.read_excel("fcc_survey.xlsx", usecols="A,W:AB", nrows=10,skiprows=2, sheet_name=['2016','2017'])
print(survey_data)
print(type(survey_data))

# Printing data from 2016 sheet
print("\nFrom sheet '2016':")
print(survey_data['2016'])

```

- Output:
```
{'2016':    Age  CommuteTime  ...      EmploymentFieldOther          EmploymentStatus
0   28           35  ...                       NaN        Employed for wages
1   22           90  ...                       NaN        Employed for wages
2   19           45  ...                       NaN        Employed for wages
3   26           45  ...                       NaN        Employed for wages
4   20           10  ...                       NaN        Employed for wages
5   34           45  ...                       NaN  Self-employed freelancer
6   23           60  ...                       NaN        Employed for wages
7   35          120  ...                       NaN        Employed for wages
8   33            0  ...                       NaN        Employed for wages
9   33           30  ...  Industrial manufacturing        Employed for wages

[10 rows x 7 columns], '2017':    Age  ...                    EmploymentStatus
0   27  ...                  Employed for wages
1   34  ...    Not working but looking for work
2   21  ...                  Employed for wages
3   26  ...                  Employed for wages
4   20  ...    Not working but looking for work
5   28  ...                      Unable to work
6   29  ...                  Employed for wages
7   29  ...  A stay-at-home parent or homemaker
8   23  ...                  Employed for wages
9   24  ...    Not working but looking for work

[10 rows x 7 columns]}
<class 'dict'>

From sheet '2016':
   Age  CommuteTime  ...      EmploymentFieldOther          EmploymentStatus
0   28           35  ...                       NaN        Employed for wages
1   22           90  ...                       NaN        Employed for wages
2   19           45  ...                       NaN        Employed for wages
3   26           45  ...                       NaN        Employed for wages
4   20           10  ...                       NaN        Employed for wages
5   34           45  ...                       NaN  Self-employed freelancer
6   23           60  ...                       NaN        Employed for wages
7   35          120  ...                       NaN        Employed for wages
8   33            0  ...                       NaN        Employed for wages
9   33           30  ...  Industrial manufacturing        Employed for wages

[10 rows x 7 columns]

```

# Parsing Dates

- Python stores dates as `Datetime` objects.
- Datetime columns are loaded as `String` objects by default.
- Specifying date columns is done using by passing (`not dtype !`) to `parse_dates` argument.
    - `parse_dates` can accept:
        - a list of column names/numbers to be parsed.
        - a list containing lists of columns to combine & parse.
        - a dictionary `keys` are new column names and `values` are lists of columns to parse together.
        - **DOES NOT** work with non-standard datetime formats:
            - `pandas.to_datetime(arg, format= date_format_str)` is used after loading data when `parse_dates` doesn't work. (refer to docs for more info)
#### Example 3.1 Parsing Dates
- Dataset has been modified "fcc_survey_datesMod.xlsx".
- Part2StartTime has non-standard date format and that's handled in this example.

```Python
import pandas as pd

date_cols = ["Part1StartTime", "Part1EndTime","Part2EndTime","Part2StartTime"]
survey_df = pd.DataFrame()
survey_df = pd.read_excel("fcc_survey_datesMod.xlsx", parse_dates = date_cols)
print(survey_df.dtypes)
print(survey_df.loc[0:5,'Part1StartTime':])

format_str = "%d%m%Y %H:%M:%S"
survey_df['Part2StartTime'] = pd.to_datetime(survey_df['Part2StartTime'],format=format_str)

print("\nAfter fix:")
print(survey_df.dtypes)
print(survey_df.loc[0:5,'Part1StartTime':])
```

- Output:

<pre>
ID.x                      object
Part1EndTime      datetime64[ns]
Part1StartTime    datetime64[ns]
Part2EndTime      datetime64[ns]
Part2StartTime            object
dtype: object
       Part1StartTime        Part2EndTime     Part2StartTime
0 2016-03-29 21:23:13 2016-03-29 21:27:25  29032016 21:24:57
1 2016-03-29 21:24:59 2016-03-29 21:29:10  29032016 21:27:14
2 2016-03-29 21:25:37 2016-03-29 21:28:21  29032016 21:27:13
3 2016-03-29 21:21:37 2016-03-29 21:30:51  29032016 21:28:51
4 2016-03-29 21:26:22 2016-03-29 21:31:54  29032016 21:29:32
5 2016-03-29 21:29:33 2016-03-29 21:32:19  29032016 21:30:44

After fix:
ID.x                      object
Part1EndTime      datetime64[ns]
Part1StartTime    datetime64[ns]
Part2EndTime      datetime64[ns]
Part2StartTime    datetime64[ns]
dtype: object
       Part1StartTime        Part2EndTime      Part2StartTime
0 2016-03-29 21:23:13 2016-03-29 21:27:25 2016-03-29 21:24:57
1 2016-03-29 21:24:59 2016-03-29 21:29:10 2016-03-29 21:27:14
2 2016-03-29 21:25:37 2016-03-29 21:28:21 2016-03-29 21:27:13
3 2016-03-29 21:21:37 2016-03-29 21:30:51 2016-03-29 21:28:51
4 2016-03-29 21:26:22 2016-03-29 21:31:54 2016-03-29 21:29:32
5 2016-03-29 21:29:33 2016-03-29 21:32:19 2016-03-29 21:30:44

Process finished with exit code 0

</pre>
