Imported pandas library so as to read the csv file. 
```python 
import pandas as pd
df = pd.read_csv('craigslist_vehicles.csv')
df
```

Used sum() to figure out the value of data missing from each column and went ahead and dropped columns which had 80% of its data missing and also irrelevant columns.

```python 
df.isnull().sum()
df = df.drop(columns = ['url', 'image_url', 'region_url', 'image_url', 'lat', 'long', 'county', 'size'])
df
```

Used info() method to determine the data types of each column then filled in missing values using mode and median depending on the data type. The posting_date and removal_date columns were then converted to datetime.

```python 
df.info()

df['year'].fillna(df['year'].median(), inplace = True)
df['odometer'].fillna(df['odometer'].median(), inplace = True)
df

df['manufacturer'].fillna(df['manufacturer'].mode()[0], inplace = True)
df['model'].fillna(df['model'].mode()[0], inplace = True)
df['condition'].fillna(df['condition'].mode()[0], inplace = True)
df['cylinders'].fillna(df['cylinders'].mode()[0], inplace = True)
df['fuel'].fillna(df['fuel'].mode()[0], inplace = True)
df['title_status'].fillna(df['title_status'].mode()[0], inplace = True)
df['transmission'].fillna(df['transmission'].mode()[0], inplace = True)
df['VIN'].fillna(df['VIN'].mode()[0], inplace = True)
df['drive'].fillna(df['drive'].mode()[0], inplace = True)
df['type'].fillna(df['type'].mode()[0], inplace = True)
df['paint_color'].fillna(df['paint_color'].mode()[0], inplace = True)
df['description'].fillna(df['description'].mode()[0], inplace = True)
df['state'].fillna(df['state'].mode()[0], inplace = True)
df['posting_date'].fillna(df['posting_date'].mode()[0], inplace = True)
df['removal_date'].fillna(df['removal_date'].mode()[0], inplace = True)
df

df['posting_date'] = pd.to_datetime(df['posting_date'])
df['removal_date'] = pd.to_datetime(df['removal_date'])
```

Posting_date column was then set as the index column using set_index() method.

```python
df.set_index('posting_date', inplace = True)
df
```

Vusialization libraries were then imported to help visualize graphs. 

```python
import matplotlib.pyplot as plt
%matplotlib inline
from matplotlib.pyplot import rcParams
rcParams['figure.figsize'] = 10, 6
import plotly as py
import plotly.express as px 
```

A new dataframe was creating that focused on one region. This new dataframe was used to plot a grapgh of time against price to check trend.

```python
df1 = df[df['region'] == 'abilene']
df1

plt.xlabel('Price')
plt.ylabel('Date')
plt.plot(df1.index)
```