---
title: "Day 5: (Part 2) Data, Data and More Data!"
date: 2022-07-10
tags: ["EDA"]
draft: false
---

## Collab link for numpy and pandas [**link**](https://colab.research.google.com/drive/1f4DdhBsaVZ0BafAgMeZ5U_QWq-VK8ijL?usp=sharing)

## Collab link for Data analytics [**link**](https://colab.research.google.com/drive/1Zp7JOOOAj2Hq_g9_NJm_5jye4SkIKI3F?usp=sharing)

# Welcome to Data Analytics

- Data analytics is the science of analyzing raw data to make conclusions about that information.

## Five Step of Data Analytics

![da.jpg](https://raw.githubusercontent.com/locus-ioe/sf23-content/master/static/Day5/da.jpg)

# Importing the required libraries

```python
import pandas as pd
import json
import plotly.express as px
from urllib.request import urlopen
```

# Download the dataset from [sf23-content Day_05 - Data Analytics](https://raw.githubusercontent.com/locus-ioe/sf23-content/master/static/Day5/admission.csv)

```python
!wget https://raw.githubusercontent.com/locus-ioe/sf23-content/master/static/Day5/admission.csv
```

# Read the admission dataset downloaded before as pandas dataframe

```python
admission_df = pd.read_csv("admission.csv")
admission_df.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Rank</th>
      <th>College</th>
      <th>Program</th>
      <th>EntranceScore</th>
      <th>District</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Suman Tamang</td>
      <td>1</td>
      <td>Pulchowk Campus</td>
      <td>BCE</td>
      <td>131.2</td>
      <td>DADELDHURA</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Prasun Sitaula</td>
      <td>2</td>
      <td>Pulchowk Campus</td>
      <td>BCT</td>
      <td>131.2</td>
      <td>RUKUM</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Saroj Basnet</td>
      <td>3</td>
      <td>Pulchowk Campus</td>
      <td>BME</td>
      <td>131.2</td>
      <td>TANAHU</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Utsav Manandhar</td>
      <td>4</td>
      <td>Pulchowk Campus</td>
      <td>BCT</td>
      <td>129.0</td>
      <td>JHAPA</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Kalpesh Manandhar</td>
      <td>5</td>
      <td>Pulchowk Campus</td>
      <td>BCT</td>
      <td>129.0</td>
      <td>JHAPA</td>
      <td>Male</td>
    </tr>
  </tbody>
</table>
</div>

```python
admission_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 3543 entries, 0 to 3542
    Data columns (total 7 columns):
     #   Column         Non-Null Count  Dtype
    ---  ------         --------------  -----
     0   Name           3543 non-null   object
     1   Rank           3543 non-null   int64
     2   College        3543 non-null   object
     3   Program        3543 non-null   object
     4   EntranceScore  3543 non-null   float64
     5   District       3543 non-null   object
     6   Gender         3543 non-null   object
    dtypes: float64(1), int64(1), object(5)
    memory usage: 193.9+ KB

The dataset has already been preprocessed and has no null values.

# Exploratory Data Analysis

## Task 1

- Male and Female Population distribution in engineering field

```python
sample = admission_df["Gender"].value_counts()
sample
```

    Male      2815
    Female     728
    Name: Gender, dtype: int64

```python
sample = sample.reset_index()
sample
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Male</td>
      <td>2815</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Female</td>
      <td>728</td>
    </tr>
  </tbody>
</table>
</div>

```python
sample.rename(columns={"index":"Gender", "Gender":"Count"}, inplace=True)
sample
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Male</td>
      <td>2815</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Female</td>
      <td>728</td>
    </tr>
  </tbody>
</table>
</div>

### Pie chart showing the population distribution of male and female gender in engineering field

```python
fig = px.pie(sample, values='Count', names='Gender', title='Gender distribution in engineering field')
fig.show()
```

![piechart.png](/attachments/piechart.png)

## Task 2

- Top 5 most common first name of students

In the dataset, we only have full name of the student. To obtain the first name, we have to split the full name by " " and get the first element i.e index 0. For uniformity, convert the names to uppercase.

```python
admission_df["FirstName"] = admission_df["Name"].str.split(" ").str[0].str.upper()
admission_df["FirstName"].head()
```

    0      SUMAN
    1     PRASUN
    2      SAROJ
    3      UTSAV
    4    KALPESH
    Name: FirstName, dtype: object

```python
sample = admission_df["FirstName"].value_counts()[:5].reset_index() \
            .rename(columns={"index":"FirstName", "FirstName":"Count"})

fig = px.bar(sample, x='FirstName', y='Count', title='Top 5 most common first names')
fig.show()
```

![barchart.png](/attachments/barchart.png)

## Assignment 1

- Find the top 5 unique names and visualize it

```python
### Your Code Goes Here

### End Code
```

## Task 3

- Visualization of population distribution of students based on districts

### Obtain the number of students based on districts

```python
sample = admission_df.groupby("District").count()["Program"]
sample
```

    District
    ACHHAM          74
    ARGHAKHANCHI    12
    BAGLUNG         49
    BAITADI          5
    BAJHANG         77
                    ..
    SURKHET         51
    SYANGJA         12
    TANAHU          11
    TEHRATHUM       43
    UDAYAPUR        21
    Name: Program, Length: 71, dtype: int64

```python
sample = pd.DataFrame({"District":sample.index.values, "count":sample.values})
max, min = sample["count"].agg(["max", "min"])
```

### Loading the geojson file of Nepal for visualizing map in plotly

```python
with urlopen('https://raw.githubusercontent.com/mesaugat/geoJSON-Nepal/master/nepal-districts.geojson') as response:
    districts = json.load(response)
```

A Choropleth Map is a map composed of colored polygons. It is used to represent spatial variations of a quantity.

```python
fig = px.choropleth(sample, geojson=districts, locations='District', color='count',
                           color_continuous_scale="Viridis",
                           range_color=(0, max),
                           scope="asia",
                           hover_name="District",
                           featureidkey="properties.DISTRICT",
                           labels={'count':'Total no of students'}
                          )
fig.update_layout(margin={"r":0,"t":0,"l":0,"b":0})
fig.show()
```

![map.png](/attachments/map.png)

## Task 4

- Rank distribution in each constituent colleges

```python
fig = px.box(admission_df, x="College" ,y="Rank")
fig.show()
```

![boxplot.png](/attachments/boxplot.png)

## Task 5

- Rank distribution and comparison based on Gender in 'Pulchowk Campus', 'Thapathali Campus', 'Paschimanchal Campus'

```python
colleges = ['Pulchowk Campus', 'Thapathali Campus', 'Paschimanchal Campus']

sample = admission_df[admission_df["College"].isin(colleges)]

fig = px.box(sample, x="College" ,y="Rank", color="Gender")
fig.show()
```

![stackbox.png](/attachments/stackbox.png)

## Task 6

- Program wise gender distribution visualization

```python
sample = admission_df.groupby(["Program", "Gender"]).count()["Name"].reset_index().rename(columns={"Name":"Count"})
sample.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Program</th>
      <th>Gender</th>
      <th>Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BAG</td>
      <td>Female</td>
      <td>16</td>
    </tr>
    <tr>
      <th>1</th>
      <td>BAG</td>
      <td>Male</td>
      <td>32</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BAM</td>
      <td>Female</td>
      <td>10</td>
    </tr>
    <tr>
      <th>3</th>
      <td>BAM</td>
      <td>Male</td>
      <td>84</td>
    </tr>
    <tr>
      <th>4</th>
      <td>BAR</td>
      <td>Female</td>
      <td>164</td>
    </tr>
  </tbody>
</table>
</div>

```python
total = sample.groupby("Program").sum().rename(columns={"Count":"Total"})
total.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total</th>
    </tr>
    <tr>
      <th>Program</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BAG</th>
      <td>48</td>
    </tr>
    <tr>
      <th>BAM</th>
      <td>94</td>
    </tr>
    <tr>
      <th>BAR</th>
      <td>262</td>
    </tr>
    <tr>
      <th>BAS</th>
      <td>47</td>
    </tr>
    <tr>
      <th>BCE</th>
      <td>1332</td>
    </tr>
  </tbody>
</table>
</div>

```python
sample = sample.merge(total, on="Program", how="left")
sample.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Program</th>
      <th>Gender</th>
      <th>Count</th>
      <th>Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BAG</td>
      <td>Female</td>
      <td>16</td>
      <td>48</td>
    </tr>
    <tr>
      <th>1</th>
      <td>BAG</td>
      <td>Male</td>
      <td>32</td>
      <td>48</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BAM</td>
      <td>Female</td>
      <td>10</td>
      <td>94</td>
    </tr>
    <tr>
      <th>3</th>
      <td>BAM</td>
      <td>Male</td>
      <td>84</td>
      <td>94</td>
    </tr>
    <tr>
      <th>4</th>
      <td>BAR</td>
      <td>Female</td>
      <td>164</td>
      <td>262</td>
    </tr>
  </tbody>
</table>
</div>

```python
sample["Percentage"] = sample["Count"]*100/sample["Total"]
```

```python
sample.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Program</th>
      <th>Gender</th>
      <th>Count</th>
      <th>Total</th>
      <th>Percentage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BAG</td>
      <td>Female</td>
      <td>16</td>
      <td>48</td>
      <td>33.333333</td>
    </tr>
    <tr>
      <th>1</th>
      <td>BAG</td>
      <td>Male</td>
      <td>32</td>
      <td>48</td>
      <td>66.666667</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BAM</td>
      <td>Female</td>
      <td>10</td>
      <td>94</td>
      <td>10.638298</td>
    </tr>
    <tr>
      <th>3</th>
      <td>BAM</td>
      <td>Male</td>
      <td>84</td>
      <td>94</td>
      <td>89.361702</td>
    </tr>
    <tr>
      <th>4</th>
      <td>BAR</td>
      <td>Female</td>
      <td>164</td>
      <td>262</td>
      <td>62.595420</td>
    </tr>
  </tbody>
</table>
</div>

```python
fig = px.bar(sample, x="Program", y="Percentage", color="Gender", title="Program wise Gender distribution")
fig.show()
```

![stackbar.png](/attachments/stackbar.png)

## Assignment 2

- Visualize the male/female population based on geographical location

```python
### Your Code Goes Here

### End Code
```

# End of content
