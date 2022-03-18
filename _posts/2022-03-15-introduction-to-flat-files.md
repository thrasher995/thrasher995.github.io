---
layout: post
title: Introduction to Flat Files
subtitle: Using Iterators to Load Large Files into Memory
categories: Python Pandas
tags: [pandas, flat files, python, data engineering]
mermaid: false
---
# Introduction to Flat Files
- Files in which data is stored as plain text (without any formatting).
- Each line in a flat file containts one row.
- Values for different fields (columns) are seperated using delimiters.
- Most common flat file type: **C**omma **S**eperated **V**alues (CSV files), in which the delimiter is a comma.
- `sep` argument for pandas' `read_csv()` method specifies the delimiter in the flat file to be loaded.
- Delimiters Table

| Delimiter | sep= |
|---|---|
| Comma | ',' (Default) |
| Tab | '\t' |
| Colon | ':' |
| Semi-colon | ';' |
| Vertical-Bar | '\|'| |


# Modifying Flat File Imports
- It's inefficient to have the program use huge amount of the memory resources, especially if the computer that's being used has little memory (RAM). Therefore, there are some ways to reduce the amount of memory while using pandas.

## Limiting Columns (`usecols`)
- The `usecols` argument for pandas' `read_csv()` method accepts a list of column numbers, or a function to filter column names.

#### **Example 2.1:** `usecols` argument
- The 'tweets.csv' dataset from DataCamp is used in this example

<pre>
import pandas as pd

col_names = ['lang','text','timestamp_ms']
col_nums = [17,27,28]
tweets_names = pd.read_csv('tweets.csv',usecols=col_names)
tweets_nums = pd.read_csv('tweets.csv',usecols=col_nums)
print('tweet_names:\n',tweets_names)
print('\ntweet_nums:\n',tweets_nums)
</pre>

Output: (Notice that both print calls resulted in the same output)

<pre>
tweet_names:
    lang                                               text   timestamp_ms
0    en  RT @bpolitics: .@krollbondrating's Christopher...  1459294817758
1    en  RT @HeidiAlpine: @dmartosko Cruz video found.....  1459294817810
2    et  Njihuni me Zonjën Trump !!! | Ekskluzive https...  1459294817917
3    en  Your an idiot she shouldn't have tried to grab...  1459294817903
4    en  RT @AlanLohner: The anti-American D.C. elites ...  1459294817851
..  ...                                                ...            ...
95   en  RT @claytoncubitt: Stop asking Bernie supporte...  1459294819805
96   en  Kasich is gonna fuck this up for Ted Cruz  htt...  1459294819766
97   en  RT @akaMaude13: Seriously can't make this up. ...  1459294819802
98   en  Kasich is gonna fuck this up for Ted Cruz  htt...  1459294819766
99   en  @marklevinshow try reporting this truth. https...  1459294819769

[100 rows x 3 columns]

tweet_nums:
    lang                                               text   timestamp_ms
0    en  RT @bpolitics: .@krollbondrating's Christopher...  1459294817758
1    en  RT @HeidiAlpine: @dmartosko Cruz video found.....  1459294817810
2    et  Njihuni me Zonjën Trump !!! | Ekskluzive https...  1459294817917
3    en  Your an idiot she shouldn't have tried to grab...  1459294817903
4    en  RT @AlanLohner: The anti-American D.C. elites ...  1459294817851
..  ...                                                ...            ...
95   en  RT @claytoncubitt: Stop asking Bernie supporte...  1459294819805
96   en  Kasich is gonna fuck this up for Ted Cruz  htt...  1459294819766
97   en  RT @akaMaude13: Seriously can't make this up. ...  1459294819802
98   en  Kasich is gonna fuck this up for Ted Cruz  htt...  1459294819766
99   en  @marklevinshow try reporting this truth. https...  1459294819769

[100 rows x 3 columns]

Process finished with exit code 0

</pre>


## Limiting Rows (`nrows`)
- The `nrows` argument for pandas' `read_csv()` method takes an integer as an argument, indicating the maximum number of rows to be imported.
- `nrows` is used with the `skiprows` argument to process a file in chunks.
(Refer to previous posts for more on `nrows` & `skiprows`).


# Handling Errors & Missing Data

## Common Flat File import issues:
1. Column data types are wrong.
2. Values are missing.
3. Records that cannot be read by `pandas`.

## Specifying data types:
- `pandas` automatically infers data types upon import.
- `datatypes` attribute (of type Series) of a DataFrame object contains the type for each column in the DataFrame object.  
- `dtype` argument for `read_csv()` takes a dictionary, with column(s) name(s) as key(s), and specified type for column(s) as value.

#### **Example 3.1**: Printing the tweets DataFrame & its `datatypes` attribute

<pre>
import pandas as pd
tweets = pd.read_csv('tweets.csv')

print('tweets DataFrame:\n',tweets)
print('\ndatatypes:\n',tweets.dtypes)

# Reading CSV again with type of columns 'id_str' & 'quoted_status_id_str' set to str:
tweets = pd.read_csv('tweets.csv',dtype={'id_str': str, 'quoted_status_id_str':str})

print('\ntweets DataFrame:\n',tweets)
print('\ndatatypes:\n',tweets.dtypes)

</pre>

Output:

<pre>
tweets DataFrame:
     contributors  ...                                               user
0            NaN  ...  {'utc_offset': 3600, 'profile_image_url_https'...
1            NaN  ...  {'utc_offset': None, 'profile_image_url_https'...
2            NaN  ...  {'utc_offset': 7200, 'profile_image_url_https'...
3            NaN  ...  {'utc_offset': None, 'profile_image_url_https'...
4            NaN  ...  {'utc_offset': -18000, 'profile_image_url_http...
..           ...  ...                                                ...
95           NaN  ...  {'utc_offset': None, 'profile_image_url_https'...
96           NaN  ...  {'utc_offset': -18000, 'profile_image_url_http...
97           NaN  ...  {'utc_offset': None, 'profile_image_url_https'...
98           NaN  ...  {'utc_offset': -18000, 'profile_image_url_http...
99           NaN  ...  {'utc_offset': -21600, 'profile_image_url_http...

[100 rows x 31 columns]

datatypes:
 contributors                 float64
coordinates                  float64
created_at                    object
entities                      object
extended_entities             object
favorite_count                 int64
favorited                       bool
filter_level                  object
geo                          float64
id                             int64
id_str                         int64
in_reply_to_screen_name       object
in_reply_to_status_id        float64
in_reply_to_status_id_str    float64
in_reply_to_user_id          float64
in_reply_to_user_id_str      float64
is_quote_status                 bool
lang                          object
place                         object
possibly_sensitive            object
quoted_status                 object
quoted_status_id             float64
quoted_status_id_str         float64
retweet_count                  int64
retweeted                       bool
retweeted_status              object
source                        object
text                          object
timestamp_ms                   int64
truncated                       bool
user                          object
dtype: object

tweets DataFrame:
     contributors  ...                                               user
0            NaN  ...  {'utc_offset': 3600, 'profile_image_url_https'...
1            NaN  ...  {'utc_offset': None, 'profile_image_url_https'...
2            NaN  ...  {'utc_offset': 7200, 'profile_image_url_https'...
3            NaN  ...  {'utc_offset': None, 'profile_image_url_https'...
4            NaN  ...  {'utc_offset': -18000, 'profile_image_url_http...
..           ...  ...                                                ...
95           NaN  ...  {'utc_offset': None, 'profile_image_url_https'...
96           NaN  ...  {'utc_offset': -18000, 'profile_image_url_http...
97           NaN  ...  {'utc_offset': None, 'profile_image_url_https'...
98           NaN  ...  {'utc_offset': -18000, 'profile_image_url_http...
99           NaN  ...  {'utc_offset': -21600, 'profile_image_url_http...

[100 rows x 31 columns]

datatypes modified:
 contributors                 float64
coordinates                  float64
created_at                    object
entities                      object
extended_entities             object
favorite_count                 int64
favorited                       bool
filter_level                  object
geo                          float64
id                             int64
id_str                        object
in_reply_to_screen_name       object
in_reply_to_status_id        float64
in_reply_to_status_id_str    float64
in_reply_to_user_id          float64
in_reply_to_user_id_str      float64
is_quote_status                 bool
lang                          object
place                         object
possibly_sensitive            object
quoted_status                 object
quoted_status_id             float64
quoted_status_id_str          object
retweet_count                  int64
retweeted                       bool
retweeted_status              object
source                        object
text                          object
timestamp_ms                   int64
truncated                       bool
user                          object
dtype: object

Process finished with exit code 0
</pre>


## Missing Data Values
- `pandas` interepts values like 'NA' or 'Null' as missing data.
- Missing data is represented by two values in `pandas`:
1. **None:** None is a Python singleton object that is often used for missing data in Python code.
2. **NaN:** Not a Number, is a special floating-point value recognized by all systems that use the standard IEEE floating-point representation.

### Custom Missing Values
- `na_values` argument for `read_csv()` is used to set custom missing values 
- A single value, list, or a dictionary of columns & values can be passed to `na_values`.

#### **Example 3.2**: Passing a dictionary to `na_values`
- The **Vermont tax return data by ZIP code** dataset from DataCamp is used in this example
- Some rows have 0 values in the zipcode and should be set as missing values using the `na_values` argument.

<pre>
import pandas as pd
tax_df = pd.read_csv('vt_tax_data_2016.csv',dtype={'zipcode':str})
print(tax_df)

# Replacing 0 zipcodes with NaN
tax_df = pd.read_csv('vt_tax_data_2016.csv',na_values={'zipcode':0},dtype={'zipcode':str})
print("\nzipcodes = 0 replaced with 'NaN:\n",tax_df)
</pre>

Output:

<pre>
      STATEFIPS STATE zipcode  agi_stub  ...  N11901  A11901  N11902  A11902
0            50    VT       0         1  ...   10820    9734   88260  138337
1            50    VT       0         2  ...   12820   20029   68760  151729
2            50    VT       0         3  ...   10810   24499   34600   90583
3            50    VT       0         4  ...    7320   21573   21300   67045
4            50    VT       0         5  ...   12500   67761   23320  103034
...         ...   ...     ...       ...  ...     ...     ...     ...     ...
1471         50    VT   99999         2  ...     250     291    1630    3506
1472         50    VT   99999         3  ...     230     489     750    1829
1473         50    VT   99999         4  ...     150     305     390    1055
1474         50    VT   99999         5  ...     230     824     390    1580
1475         50    VT   99999         6  ...      60     575      40     190

[1476 rows x 147 columns]

zipcodes = 0 replaced with 'NaN:
       STATEFIPS STATE zipcode  agi_stub  ...  N11901  A11901  N11902  A11902
0            50    VT     NaN         1  ...   10820    9734   88260  138337
1            50    VT     NaN         2  ...   12820   20029   68760  151729
2            50    VT     NaN         3  ...   10810   24499   34600   90583
3            50    VT     NaN         4  ...    7320   21573   21300   67045
4            50    VT     NaN         5  ...   12500   67761   23320  103034
...         ...   ...     ...       ...  ...     ...     ...     ...     ...
1471         50    VT   99999         2  ...     250     291    1630    3506
1472         50    VT   99999         3  ...     230     489     750    1829
1473         50    VT   99999         4  ...     150     305     390    1055
1474         50    VT   99999         5  ...     230     824     390    1580
1475         50    VT   99999         6  ...      60     575      40     190

[1476 rows x 147 columns]

Process finished with exit code 0
</pre>

### Lines with Errors
- Handling `pandas.errors.ParserError: Error tokenizing data.`
    - This error is thrown when a record contains more values than the number of columns (more commas than the number of commas in the first row).
    - When this error is raised, no data is imported from the CSV and the program crashes.

#### **Example 3.3-a :** Throwing the ParserError
- The dataset from example 3.2 was corrupted by adding an extra comma in line 3 before the value corresponding to the 'zipcode' column, and saved as 'kurupt_tax_data_2016.csv'.

<pre>
import pandas as pd
kurupt_tax_df = pd.read_csv('kurupt_tax_data_2016.csv')
print(kurupt_tax_df)
</pre>

Output:

<pre>
Traceback (most recent call last):
  File "C:/Users/Mohammed Darras/PycharmProjects/untitled3/venv/Scripts/trial.py", line 2, in <module>
    kurupt_tax_df = pd.read_csv('kurupt_tax_data_2016.csv')
  File "C:\Anaconda\envs\untitled3\lib\site-packages\pandas\util\_decorators.py", line 311, in wrapper
    return func(*args, **kwargs)
  File "C:\Anaconda\envs\untitled3\lib\site-packages\pandas\io\parsers\readers.py", line 586, in read_csv
    return _read(filepath_or_buffer, kwds)
  File "C:\Anaconda\envs\untitled3\lib\site-packages\pandas\io\parsers\readers.py", line 488, in _read
    return parser.read(nrows)
  File "C:\Anaconda\envs\untitled3\lib\site-packages\pandas\io\parsers\readers.py", line 1047, in read
    index, columns, col_dict = self._engine.read(nrows)
  File "C:\Anaconda\envs\untitled3\lib\site-packages\pandas\io\parsers\c_parser_wrapper.py", line 224, in read
    chunks = self._reader.read_low_memory(nrows)
  File "pandas\_libs\parsers.pyx", line 801, in pandas._libs.parsers.TextReader.read_low_memory
  File "pandas\_libs\parsers.pyx", line 857, in pandas._libs.parsers.TextReader._read_rows
  File "pandas\_libs\parsers.pyx", line 843, in pandas._libs.parsers.TextReader._tokenize_rows
  File "pandas\_libs\parsers.pyx", line 1925, in pandas._libs.parsers.raise_parser_error
pandas.errors.ParserError: Error tokenizing data. C error: Expected 147 fields in line 3, saw 148


Process finished with exit code 1
</pre>

- The `error_bad_lines` & `warn_bad_lines` arguments for `read_csv()` method are used to handle this issue.
    - Both of those arguments take Booleans, and `=True` by default.
    - Setting `error_bad_lines=False` makes pandas skip bad lines.
    - **These arguments have been deprecated and will be removed in a future version.**
    

#### **Example 3.3-b :** Skipping bad lines
- `warn_bad_lines`'s default value is used in this example (**=True**).

<pre>
import pandas as pd
kurupt_tax_df = pd.read_csv('kurupt_tax_data_2016.csv',error_bad_lines=False)
print(kurupt_tax_df)
</pre>

Output:

<pre>
b'Skipping line 3: expected 147 fields, saw 148\n'
      STATEFIPS STATE  zipcode  agi_stub  ...  N11901  A11901  N11902  A11902
0            50    VT        0         1  ...   10820    9734   88260  138337
1            50    VT        0         3  ...   10810   24499   34600   90583
2            50    VT        0         4  ...    7320   21573   21300   67045
3            50    VT        0         5  ...   12500   67761   23320  103034
4            50    VT        0         6  ...    3900   93123    2870   39425
...         ...   ...      ...       ...  ...     ...     ...     ...     ...
1470         50    VT    99999         2  ...     250     291    1630    3506
1471         50    VT    99999         3  ...     230     489     750    1829
1472         50    VT    99999         4  ...     150     305     390    1055
1473         50    VT    99999         5  ...     230     824     390    1580
1474         50    VT    99999         6  ...      60     575      40     190

[1475 rows x 147 columns]

Process finished with exit code 0

</pre>

#### **Example 3.3-c :** Skipping bad lines & turning warnings off
- Setting `warn_bad_lines=False` (Skipping silently).

<pre>
import pandas as pd
kurupt_tax_df = pd.read_csv('kurupt_tax_data_2016.csv',error_bad_lines=False,warn_bad_lines=False)
print(kurupt_tax_df)
</pre>

Output:

<pre>
      STATEFIPS STATE  zipcode  agi_stub  ...  N11901  A11901  N11902  A11902
0            50    VT        0         1  ...   10820    9734   88260  138337
1            50    VT        0         3  ...   10810   24499   34600   90583
2            50    VT        0         4  ...    7320   21573   21300   67045
3            50    VT        0         5  ...   12500   67761   23320  103034
4            50    VT        0         6  ...    3900   93123    2870   39425
...         ...   ...      ...       ...  ...     ...     ...     ...     ...
1470         50    VT    99999         2  ...     250     291    1630    3506
1471         50    VT    99999         3  ...     230     489     750    1829
1472         50    VT    99999         4  ...     150     305     390    1055
1473         50    VT    99999         5  ...     230     824     390    1580
1474         50    VT    99999         6  ...      60     575      40     190

[1475 rows x 147 columns]

Process finished with exit code 0
</pre>