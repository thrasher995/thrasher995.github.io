---
layout: post
title: Loading Data in Chunks
subtitle: Using Iterators to Load Large Files into Memory
categories: Python
tags: [iterators, large data, python, data engineering]
mermaid: false
---


## Loading Data in Chunks
- When the data is too large to be held in memory.
- Load data in chunks, perform operation on each chunk, store the result, discard the chunk, then load the next chunk.
    - Iterators are quite useful here.
- pandas `read_csv()` method:
    - Specify the chunk using `chunksize` argument for `read_csv()` method.

### Example: Some car data in 'cars.csv' (15777 rows with duplicate values)

| manufacturer | model_name | model_year | ODO |
|---|---|---|---|
|toyota|corolla|2001|200000|
|toyota|corolla|2001|200000|
|honda|civic|2010|132532|
|...|...|...|...|
|mitsubishi|lancer|2008|175849|

```
import pandas as pd
cars_dict = {}

for chunk in pd.read_csv('cars.csv',chunksize=1000):
    for car_model in chunk['model_name']:
        if car_model in cars_dict.keys():
            cars_dict[car_model]+=1
        else:
            cars_dict[car_model] = 1
print(cars_dict)
```

Output:
```
{'corolla': 4640, 'camry': 2784, 'civic': 3712, 'lancer': 2784, 'accord': 1856}
```


