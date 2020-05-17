---
title: "New York Property Tax Fraud Analysis"
date: 2020-04-15
tags: [machine learning, data science, neural network, visualization]
header:
  image: "/images/laptop.jpg"
excerpt: "Machine Learning, Fraud Analysis, Data Science"
mathjax: "true"
---


[Link to my project detals!](https://github.com/siyulai100/Fraud-Analysis-)
## Project Description

* Build an algorithmic system that can look through ~1 million property records to find potential tax fraud.

* Find people underpaying tax or otherwise misrepresenting their property characteristics.

### Import the packages

```python
  import pandas as pd
  import numpy as np
  import matplotlib.pyplot as plt
  import seaborn as sns
  %matplotlib inline
  start_time = pd.datetime.now()
  mydata = pd.read_csv('NY property data.csv')
```

### fill the missing/zero value in zip with the previous non-missing value

```python
  data['zip5'] = data.zip5.replace('nan','10314')
  data['zip3'] = data['zip5'].str[:3]
```

### fill the missing/zero value in Stories with the mean of each group zip5 and BLOCK.

```python
  data['STORIES'] = data['STORIES'].replace(0, np.nan)
  data['STORIES'] = data.groupby(['zip5','BLOCK'])['STORIES'].transform(lambda x:  x.fillna(x.mean()))
  data['STORIES']=data['STORIES'].replace(np.nan,2)
  data.loc[data['STORIES'].isna()]
```



$$ z = x+y $$
