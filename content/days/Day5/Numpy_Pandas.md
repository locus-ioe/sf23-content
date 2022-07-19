---
title: "Day 5: (Part 1) Data, Data and More Data!"
date: 2022-07-10
tags: ["numpy", "pandas"]
draft: false
weight: 6
---

# Numpy

## Why numpy?? 


```python
import numpy as np
from timeit import timeit

def NPFunc():
    np.sum(np.power(np.arange(1,2000000), 2))
    return None


def PyFunc():
    sum([x*x for x in range(1,2000000)])
    return None


print(timeit(NPFunc, number=1))
print(timeit(PyFunc, number=1))
```

    0.029838398999999072
    0.4973828640000022


Numpy operations are a lot faster than built in python operations.

## Numpy array declaration and initialization


```python
arr1 = np.array([]) # declares an empty array
print(arr1)

sample_list = [1, 2, 3, 4, 5]
arr2 = np.array(sample_list) # initializes a numpy array using python list
print(arr2)
```

    []
    [1 2 3 4 5]


## Creating 1D and 2D array and initialize with zero


```python
#creates 1D array containing zeros
np.zeros(shape=3)
```




    array([0., 0., 0.])




```python
#creates 2D array containing zeros
np.zeros(shape=(3,3))#tuple must be provided as an input,(3,3) makes 2D matrix of size 3*3
```




    array([[0., 0., 0.],
           [0., 0., 0.],
           [0., 0., 0.]])



## Creating 1D and 2D array and initialize with one


```python
#creates 1D array containing ones
np.ones(shape=3)
```




    array([1., 1., 1.])




```python
#creates 2D array containing ones
np.ones(shape=(3,2))
```




    array([[1., 1.],
           [1., 1.],
           [1., 1.]])



## Creating identity matrix


```python
np.eye(4) #4*4 identity matrix
```




    array([[1., 0., 0., 0.],
           [0., 1., 0., 0.],
           [0., 0., 1., 0.],
           [0., 0., 0., 1.]])



## Random values


```python
#1D array
np.random.rand(5)# Generate an array of random values of length 5 and values lies between 0 & 1
```




    array([0.94558025, 0.95947647, 0.19921073, 0.13523719, 0.55870915])




```python
#2D array
np.random.rand(2,3)# Generate an array of random values of shape 2*3
```




    array([[0.602467  , 0.44441528, 0.54233334],
           [0.926806  , 0.11022771, 0.82283922]])




```python
np.random.randint(1,100)# select a random integer between 1 to 100
```




    74



## Attributes of numpy array


```python
x = np.array([1, 2, 3])#1D
y = np.array([1.1, 2.8, 1, 3])#1D
z = np.random.rand(3,4)#2D
```


```python
x.dtype# returns the data type of numpy array
```




    dtype('int64')




```python
y.dtype
```




    dtype('float64')




```python
x.astype(dtype='float64')#changes the data type of the numpy array
```




    array([1., 2., 3.])




```python
y.astype(dtype='int64')
```




    array([1, 2, 1, 3])




```python
x.ndim #gives the number of dimension in the array
```




    1




```python
z.ndim
```




    2




```python
x.shape #gives the shape of an array
```




    (3,)




```python
z.shape
```




    (3, 4)




```python
x.size #gives total number of elements in the array
```




    3




```python
z.size
```




    12




```python
#reshape an array from 1D to 2D
print(f"y before reshape:\n{y}\n")
print(f"y after reshape: \n{y.reshape(2,2)}")#reshapes the array -->size of the array should be same while reshaping
```

    y before reshape:
    [1.1 2.8 1.  3. ]
    
    y after reshape: 
    [[1.1 2.8]
     [1.  3. ]]



```python
print(f"z before reshape:\n{z}\n")# 3 rows 4 cloumns
print(f"z after reshape:\n{z.reshape(4,3)}")#reshapes to 4 rows 3 cloumns
```

    z before reshape:
    [[0.12975586 0.40850878 0.22285784 0.62197612]
     [0.04590619 0.13044902 0.12605415 0.08418587]
     [0.01843059 0.57758455 0.98372901 0.53596404]]
    
    z after reshape:
    [[0.12975586 0.40850878 0.22285784]
     [0.62197612 0.04590619 0.13044902]
     [0.12605415 0.08418587 0.01843059]
     [0.57758455 0.98372901 0.53596404]]



```python
#converting multidimensional array to 1D array
print(z.ravel())
```

    [0.12975586 0.40850878 0.22285784 0.62197612 0.04590619 0.13044902
     0.12605415 0.08418587 0.01843059 0.57758455 0.98372901 0.53596404]


## Summary Statistics in the array


```python
# For 1D array
mat1D=np.array([1,2,3,4,5,6,7])
print(f"mean: {np.mean(mat1D)}")
print(f"min: {np.min(mat1D)}")
print(f"max: {np.max(mat1D)}")
print(f"std: {np.std(mat1D)}")
print(f"median: {np.median(mat1D)}")
print((f"index of max element:{np.argmax(mat1D)}"))
```

    mean: 4.0
    min: 1
    max: 7
    std: 2.0
    median: 4.0
    index of max element:6



```python

```


```python
# For 2D array
axis = 0
mat2D=np.array([[1,7,3],[4,5,6]])
print(f"array: {mat2D}")
print(f"mean: {np.mean(mat2D,axis=axis)}")
print(f"min: {np.min(mat2D,axis=axis)}")
print(f"max: {np.max(mat2D,axis=axis)}")
print(f"std: {np.std(mat2D,axis=axis)}")
print(f"median: {np.median(mat2D,axis=axis)}")
print((f"index of max element:{np.argmax(mat2D,axis=axis)}"))
```

    array: [[1 7 3]
     [4 5 6]]
    mean: [2.5 6.  4.5]
    min: [1 5 3]
    max: [4 7 6]
    std: [1.5 1.  1.5]
    median: [2.5 6.  4.5]
    index of max element:[1 0 1]


parameter: axis defines the direction along which the operations are to be performed.

![image.png](/attachments/cbimage.png)
## Slicing of numpy array


```python
#1D array
array_slice1D=np.array([-1,2,3,5,6])
array_slice1D[1:]
```




    array([2, 3, 5, 6])




```python
#2D array
array_slice2D=np.array([[1, 7, 3, 5, 8],
                        [4, 5, 6,-1, 4],
                        [2, 0, 6,-8, 9]])
array_slice2D[1:,2:]
```




    array([[ 6, -1,  4],
           [ 6, -8,  9]])




```python
array_slice2D[:2,:-2]
```




    array([[1, 7, 3],
           [4, 5, 6]])



## Conditional Selection


```python
conditional_array=np.arange(15)
conditional_array
```




    array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14])




```python
conditional_array[conditional_array>12]
```




    array([13, 14])



np.where vs list comprehension


```python
np.array([i if i>12 else 1 for i in conditional_array])
```




    array([ 1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1, 13, 14])




```python
np.where(conditional_array>12,conditional_array,1)
```




    array([ 1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,  1, 13, 14])



# Pandas


```python
import pandas as pd
```

What is series and dataframe?
- Series is a one-dimensional labeled array capable of holding any data type (integers, strings, floating point numbers, Python objects, etc.). The axis labels are collectively referred to as the index.
- DataFrame is a 2-dimensional labeled data structure with columns of potentially different types.

## Creating Series from python dictionary


```python
employee_dict={
          'name':['Aayush','Bishal','Gaurav','Kriti','Manjeet'],
          'roll_number':[7,28,37,43,48]
          }

name = pd.Series(employee_dict)
name
```




    name           [Aayush, Bishal, Gaurav, Kriti, Manjeet]
    roll_number                         [7, 28, 37, 43, 48]
    dtype: object



## Creating Dataframe from list of python dictionary


```python
employee_dict_df=pd.DataFrame(employee_dict)
employee_dict_df
```





  <div id="df-486fffcb-6577-4341-972d-89ff41d3e1b6">
    <div class="colab-df-container">
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
      <th>name</th>
      <th>roll_number</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aayush</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bishal</td>
      <td>28</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Gaurav</td>
      <td>37</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kriti</td>
      <td>43</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Manjeet</td>
      <td>48</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-486fffcb-6577-4341-972d-89ff41d3e1b6')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>
  </div>




Note: Difference between Series and DataFrame
- Series works in form of index and values
- DataFrame is more like tabular form

## Creating DataFrame from python list


```python
employee_list=[['Aayush',7],['Bishal',28],['Gaurav',37],['Kriti',43],['Manjeet',48]]
```


```python
employee_list_df=pd.DataFrame(employee_list)
employee_list_df
```





  <div id="df-942f8c17-9911-4a8e-a3b4-3656fe61afa7">
    <div class="colab-df-container">
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
      <th>0</th>
      <th>1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aayush</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bishal</td>
      <td>28</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Gaurav</td>
      <td>37</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kriti</td>
      <td>43</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Manjeet</td>
      <td>48</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-942f8c17-9911-4a8e-a3b4-3656fe61afa7')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>


  </div>





```python
employee_list_df.columns=['name','roll_number']
employee_list_df
```





  <div id="df-01e49818-f08b-4121-b4cd-39818b220711">
    <div class="colab-df-container">
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
      <th>name</th>
      <th>roll_number</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aayush</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bishal</td>
      <td>28</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Gaurav</td>
      <td>37</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kriti</td>
      <td>43</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Manjeet</td>
      <td>48</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-01e49818-f08b-4121-b4cd-39818b220711')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

  </div>




## Useful attributes and methods in panda

- `.values` : A 2d numpy array of values
- `.columns` : Index of columns, column names
- `.index` : An index of rows, either row numbers or row names
- `.shape` :return number of rows and columns of dataframe
- `.head()` :return first few row of dataframe
- `.tail()` :return last few row of dataframe
- `.info()` :shows information of each of the columns such as data type and number of missing values
- `.describe()` :calculate few summary statistics for each column


```python
book_dict={
    'book_count':[272,491,np.nan,487,1356,226,969,360,311,3455,np.nan,210,995,896,710,274,201,376,566,239],
    'rating' : ['A','C', 'A', 'B','A', np.nan,'B','A','C','A', 'B', 'A','C','A',np.nan, 'B','A','C','A','C'], 

    'author':['Suzanne Collins','J.K. Rowling','Stephenie Meyer', 'Harper Lee', 'J.D. Salinger', 'John Green', \
              'J.R.R. Tolkien', 'J.D. Salinger','Dan Brown', 'Jane Austen', 'Khaled Hosseini', 'Veronica Roth', 'John Green',\
              'George Orwell', 'Anne Frank', 'Stieg Larsson, Reg Keeland', \
              'Suzanne Collins','J.K. Rowling',np.nan, 'Suzanne Collins'],
           
    'title':['The Hunger Games',"Harry Potter and the Philosopher's Stone",'Twilight','To Kill a Mockingbird',\
             'The Great Gatsby','The Fault in Our Stars','The Hobbit or There and Back Again', \
             'The Catcher in the Rye','Angels & Demons ','Pride and Prejudice','The Kite Runner ',\
             'Divergent','Nineteen Eighty-Four','Animal Farm: A Fairy Story','Het Achterhuis',\
             'Män som hatar kvinnor',np.nan,'Harry Potter and the Prisoner of Azkaban',' The Fellowship of the Ring','Mockingjay']
}
```


```python
book_df=pd.DataFrame(book_dict)
book_df.head()
```





  <div id="df-e9cb9aea-7d2d-4851-9666-fd97602a1e44">
    <div class="colab-df-container">
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
      <th>book_count</th>
      <th>rating</th>
      <th>author</th>
      <th>title</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>272.0</td>
      <td>A</td>
      <td>Suzanne Collins</td>
      <td>The Hunger Games</td>
    </tr>
    <tr>
      <th>1</th>
      <td>491.0</td>
      <td>C</td>
      <td>J.K. Rowling</td>
      <td>Harry Potter and the Philosopher's Stone</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>A</td>
      <td>Stephenie Meyer</td>
      <td>Twilight</td>
    </tr>
    <tr>
      <th>3</th>
      <td>487.0</td>
      <td>B</td>
      <td>Harper Lee</td>
      <td>To Kill a Mockingbird</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1356.0</td>
      <td>A</td>
      <td>J.D. Salinger</td>
      <td>The Great Gatsby</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-e9cb9aea-7d2d-4851-9666-fd97602a1e44')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    
  </div>





```python
book_df.values
```




    array([[272.0, 'A', 'Suzanne Collins', 'The Hunger Games'],
           [491.0, 'C', 'J.K. Rowling',
            "Harry Potter and the Philosopher's Stone"],
           [nan, 'A', 'Stephenie Meyer', 'Twilight'],
           [487.0, 'B', 'Harper Lee', 'To Kill a Mockingbird'],
           [1356.0, 'A', 'J.D. Salinger', 'The Great Gatsby'],
           [226.0, nan, 'John Green', 'The Fault in Our Stars'],
           [969.0, 'B', 'J.R.R. Tolkien',
            'The Hobbit or There and Back Again'],
           [360.0, 'A', 'J.D. Salinger', 'The Catcher in the Rye'],
           [311.0, 'C', 'Dan Brown', 'Angels & Demons '],
           [3455.0, 'A', 'Jane Austen', 'Pride and Prejudice'],
           [nan, 'B', 'Khaled Hosseini', 'The Kite Runner '],
           [210.0, 'A', 'Veronica Roth', 'Divergent'],
           [995.0, 'C', 'John Green', 'Nineteen Eighty-Four'],
           [896.0, 'A', 'George Orwell', 'Animal Farm: A Fairy Story'],
           [710.0, nan, 'Anne Frank', 'Het Achterhuis'],
           [274.0, 'B', 'Stieg Larsson, Reg Keeland',
            'Män som hatar kvinnor'],
           [201.0, 'A', 'Suzanne Collins', nan],
           [376.0, 'C', 'J.K. Rowling',
            'Harry Potter and the Prisoner of Azkaban'],
           [566.0, 'A', nan, ' The Fellowship of the Ring'],
           [239.0, 'C', 'Suzanne Collins', 'Mockingjay']], dtype=object)




```python
book_df.columns
```




    Index(['book_count', 'rating', 'author', 'title'], dtype='object')




```python
book_df.index
```




    RangeIndex(start=0, stop=20, step=1)




```python
book_df.shape
```




    (20, 4)




```python
book_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 20 entries, 0 to 19
    Data columns (total 4 columns):
     #   Column      Non-Null Count  Dtype  
    ---  ------      --------------  -----  
     0   book_count  18 non-null     float64
     1   rating      18 non-null     object 
     2   author      19 non-null     object 
     3   title       19 non-null     object 
    dtypes: float64(1), object(3)
    memory usage: 768.0+ bytes



```python
book_df.describe()
```





  <div id="df-54c90c40-56ca-4751-bb1c-d08199e8338a">
    <div class="colab-df-container">
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
      <th>book_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>18.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>688.555556</td>
    </tr>
    <tr>
      <th>std</th>
      <td>766.418963</td>
    </tr>
    <tr>
      <th>min</th>
      <td>201.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>272.500000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>431.500000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>849.500000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>3455.000000</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-54c90c40-56ca-4751-bb1c-d08199e8338a')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

  </div>





```python
book_df.describe(include="O")
```





  <div id="df-3ebe8bca-647a-4f67-b60c-ac5aca34cc9d">
    <div class="colab-df-container">
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
      <th>rating</th>
      <th>author</th>
      <th>title</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>18</td>
      <td>19</td>
      <td>19</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>3</td>
      <td>15</td>
      <td>19</td>
    </tr>
    <tr>
      <th>top</th>
      <td>A</td>
      <td>Suzanne Collins</td>
      <td>The Hunger Games</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>9</td>
      <td>3</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-3ebe8bca-647a-4f67-b60c-ac5aca34cc9d')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

  </div>




## Summary Statistics

- `.median()`
- `.mean()`
- `.mode()`
- `.max()`
- `.min()`
- `.var()`
- `.std()`
- `.sum()`
- .`value_counts()`


```python
book_df['book_count'].mean()
```




    688.5555555555555




```python
book_df['author'].value_counts()
```




    Suzanne Collins               3
    J.K. Rowling                  2
    J.D. Salinger                 2
    John Green                    2
    Stephenie Meyer               1
    Harper Lee                    1
    J.R.R. Tolkien                1
    Dan Brown                     1
    Jane Austen                   1
    Khaled Hosseini               1
    Veronica Roth                 1
    George Orwell                 1
    Anne Frank                    1
    Stieg Larsson, Reg Keeland    1
    Name: author, dtype: int64



### Handling missing values


```python
book_df.isna().sum()
```




    book_count    2
    rating        2
    author        1
    title         1
    dtype: int64




```python
mean_book_count = book_df["book_count"].mean()
book_df["book_count"].fillna(mean_book_count, inplace=True)
```


```python
mode_of_ratings = book_df["rating"].mode()[0]
book_df["rating"].fillna(mode_of_ratings, inplace=True)
```


```python
book_df.dropna(axis=0, how='any', thresh=None, subset=["author"], inplace=True)
# axis: defines which direction the values are to be deleted
# how: Determine if row or column is removed from DataFrame, when we have at least one NA or all
# thresh: Require that many non-NA values
# subset: Labels along other axis to consider
```

### iloc vs loc for slicing
- loc: gets rows (and/or columns) with particular labels.

- iloc: gets rows (and/or columns) at integer locations.



```python
book_df.iloc[:5]
```





  <div id="df-718f270a-2b00-423c-ba42-c80906dc076c">
    <div class="colab-df-container">
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
      <th>book_count</th>
      <th>rating</th>
      <th>author</th>
      <th>title</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>272.0</td>
      <td>A</td>
      <td>Suzanne Collins</td>
      <td>The Hunger Games</td>
    </tr>
    <tr>
      <th>1</th>
      <td>491.0</td>
      <td>C</td>
      <td>J.K. Rowling</td>
      <td>Harry Potter and the Philosopher's Stone</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>A</td>
      <td>Stephenie Meyer</td>
      <td>Twilight</td>
    </tr>
    <tr>
      <th>3</th>
      <td>487.0</td>
      <td>B</td>
      <td>Harper Lee</td>
      <td>To Kill a Mockingbird</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1356.0</td>
      <td>A</td>
      <td>J.D. Salinger</td>
      <td>The Great Gatsby</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-718f270a-2b00-423c-ba42-c80906dc076c')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

  </div>





```python
book_df.loc[:2,"book_count":"author"]#different than python slicing

# book_df.iloc[:2,"book_count":"author"] # throws error
```





  <div id="df-40dd7565-8c78-4a52-9c6e-61efe3160ff5">
    <div class="colab-df-container">
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
      <th>book_count</th>
      <th>rating</th>
      <th>author</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>272.0</td>
      <td>A</td>
      <td>Suzanne Collins</td>
    </tr>
    <tr>
      <th>1</th>
      <td>491.0</td>
      <td>C</td>
      <td>J.K. Rowling</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>A</td>
      <td>Stephenie Meyer</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-40dd7565-8c78-4a52-9c6e-61efe3160ff5')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-40dd7565-8c78-4a52-9c6e-61efe3160ff5 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-40dd7565-8c78-4a52-9c6e-61efe3160ff5');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




## Selection and assigning


```python
book_df[book_df["book_count"]>300]
```





  <div id="df-fa14089f-0091-4dff-9819-a4dc42f588d3">
    <div class="colab-df-container">
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
      <th>book_count</th>
      <th>rating</th>
      <th>author</th>
      <th>title</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>491.000000</td>
      <td>C</td>
      <td>J.K. Rowling</td>
      <td>Harry Potter and the Philosopher's Stone</td>
    </tr>
    <tr>
      <th>2</th>
      <td>688.555556</td>
      <td>A</td>
      <td>Stephenie Meyer</td>
      <td>Twilight</td>
    </tr>
    <tr>
      <th>3</th>
      <td>487.000000</td>
      <td>B</td>
      <td>Harper Lee</td>
      <td>To Kill a Mockingbird</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1356.000000</td>
      <td>A</td>
      <td>J.D. Salinger</td>
      <td>The Great Gatsby</td>
    </tr>
    <tr>
      <th>6</th>
      <td>969.000000</td>
      <td>B</td>
      <td>J.R.R. Tolkien</td>
      <td>The Hobbit or There and Back Again</td>
    </tr>
    <tr>
      <th>7</th>
      <td>360.000000</td>
      <td>A</td>
      <td>J.D. Salinger</td>
      <td>The Catcher in the Rye</td>
    </tr>
    <tr>
      <th>8</th>
      <td>311.000000</td>
      <td>C</td>
      <td>Dan Brown</td>
      <td>Angels &amp; Demons</td>
    </tr>
    <tr>
      <th>9</th>
      <td>3455.000000</td>
      <td>A</td>
      <td>Jane Austen</td>
      <td>Pride and Prejudice</td>
    </tr>
    <tr>
      <th>10</th>
      <td>688.555556</td>
      <td>B</td>
      <td>Khaled Hosseini</td>
      <td>The Kite Runner</td>
    </tr>
    <tr>
      <th>12</th>
      <td>995.000000</td>
      <td>C</td>
      <td>John Green</td>
      <td>Nineteen Eighty-Four</td>
    </tr>
    <tr>
      <th>13</th>
      <td>896.000000</td>
      <td>A</td>
      <td>George Orwell</td>
      <td>Animal Farm: A Fairy Story</td>
    </tr>
    <tr>
      <th>14</th>
      <td>710.000000</td>
      <td>A</td>
      <td>Anne Frank</td>
      <td>Het Achterhuis</td>
    </tr>
    <tr>
      <th>17</th>
      <td>376.000000</td>
      <td>C</td>
      <td>J.K. Rowling</td>
      <td>Harry Potter and the Prisoner of Azkaban</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-fa14089f-0091-4dff-9819-a4dc42f588d3')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

  </div>





```python
# Adding new columns
book_df["isAvailable"] = True # performs broadcasting to all rows
# book_df.isAvailable = True # can not create new columns using dot operator

# Accessing columns
book_df["isAvailable"]
book_df.isAvailable
```




    0     True
    1     True
    2     True
    3     True
    4     True
    5     True
    6     True
    7     True
    8     True
    9     True
    10    True
    11    True
    12    True
    13    True
    14    True
    15    True
    16    True
    17    True
    18    True
    19    True
    Name: isAvailable, dtype: bool



## Grouping and sorting


```python
book_df.groupby(["author"]).sum()
```





  <div id="df-fc04e890-8495-4a7e-abc9-b9fdf32e45b6">
    <div class="colab-df-container">
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
      <th>book_count</th>
      <th>isAvailable</th>
    </tr>
    <tr>
      <th>author</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Anne Frank</th>
      <td>710.000000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Dan Brown</th>
      <td>311.000000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>George Orwell</th>
      <td>896.000000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Harper Lee</th>
      <td>487.000000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>J.D. Salinger</th>
      <td>1716.000000</td>
      <td>2</td>
    </tr>
    <tr>
      <th>J.K. Rowling</th>
      <td>867.000000</td>
      <td>2</td>
    </tr>
    <tr>
      <th>J.R.R. Tolkien</th>
      <td>969.000000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Jane Austen</th>
      <td>3455.000000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>John Green</th>
      <td>1221.000000</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Khaled Hosseini</th>
      <td>688.555556</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Stephenie Meyer</th>
      <td>688.555556</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Stieg Larsson, Reg Keeland</th>
      <td>274.000000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Suzanne Collins</th>
      <td>712.000000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Veronica Roth</th>
      <td>210.000000</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-fc04e890-8495-4a7e-abc9-b9fdf32e45b6')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

  </div>





```python
book_df.sort_values(["author", "book_count"])#try ascending=False
```





  <div id="df-6efb4a2b-c3b3-47f4-a5b8-6d4f94153f0f">
    <div class="colab-df-container">
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
      <th>book_count</th>
      <th>rating</th>
      <th>author</th>
      <th>title</th>
      <th>isAvailable</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>14</th>
      <td>710.000000</td>
      <td>A</td>
      <td>Anne Frank</td>
      <td>Het Achterhuis</td>
      <td>True</td>
    </tr>
    <tr>
      <th>8</th>
      <td>311.000000</td>
      <td>C</td>
      <td>Dan Brown</td>
      <td>Angels &amp; Demons</td>
      <td>True</td>
    </tr>
    <tr>
      <th>13</th>
      <td>896.000000</td>
      <td>A</td>
      <td>George Orwell</td>
      <td>Animal Farm: A Fairy Story</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>487.000000</td>
      <td>B</td>
      <td>Harper Lee</td>
      <td>To Kill a Mockingbird</td>
      <td>True</td>
    </tr>
    <tr>
      <th>7</th>
      <td>360.000000</td>
      <td>A</td>
      <td>J.D. Salinger</td>
      <td>The Catcher in the Rye</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1356.000000</td>
      <td>A</td>
      <td>J.D. Salinger</td>
      <td>The Great Gatsby</td>
      <td>True</td>
    </tr>
    <tr>
      <th>17</th>
      <td>376.000000</td>
      <td>C</td>
      <td>J.K. Rowling</td>
      <td>Harry Potter and the Prisoner of Azkaban</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>491.000000</td>
      <td>C</td>
      <td>J.K. Rowling</td>
      <td>Harry Potter and the Philosopher's Stone</td>
      <td>True</td>
    </tr>
    <tr>
      <th>6</th>
      <td>969.000000</td>
      <td>B</td>
      <td>J.R.R. Tolkien</td>
      <td>The Hobbit or There and Back Again</td>
      <td>True</td>
    </tr>
    <tr>
      <th>9</th>
      <td>3455.000000</td>
      <td>A</td>
      <td>Jane Austen</td>
      <td>Pride and Prejudice</td>
      <td>True</td>
    </tr>
    <tr>
      <th>5</th>
      <td>226.000000</td>
      <td>A</td>
      <td>John Green</td>
      <td>The Fault in Our Stars</td>
      <td>True</td>
    </tr>
    <tr>
      <th>12</th>
      <td>995.000000</td>
      <td>C</td>
      <td>John Green</td>
      <td>Nineteen Eighty-Four</td>
      <td>True</td>
    </tr>
    <tr>
      <th>10</th>
      <td>688.555556</td>
      <td>B</td>
      <td>Khaled Hosseini</td>
      <td>The Kite Runner</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>688.555556</td>
      <td>A</td>
      <td>Stephenie Meyer</td>
      <td>Twilight</td>
      <td>True</td>
    </tr>
    <tr>
      <th>15</th>
      <td>274.000000</td>
      <td>B</td>
      <td>Stieg Larsson, Reg Keeland</td>
      <td>Män som hatar kvinnor</td>
      <td>True</td>
    </tr>
    <tr>
      <th>16</th>
      <td>201.000000</td>
      <td>A</td>
      <td>Suzanne Collins</td>
      <td>NaN</td>
      <td>True</td>
    </tr>
    <tr>
      <th>19</th>
      <td>239.000000</td>
      <td>C</td>
      <td>Suzanne Collins</td>
      <td>Mockingjay</td>
      <td>True</td>
    </tr>
    <tr>
      <th>0</th>
      <td>272.000000</td>
      <td>A</td>
      <td>Suzanne Collins</td>
      <td>The Hunger Games</td>
      <td>True</td>
    </tr>
    <tr>
      <th>11</th>
      <td>210.000000</td>
      <td>A</td>
      <td>Veronica Roth</td>
      <td>Divergent</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-6efb4a2b-c3b3-47f4-a5b8-6d4f94153f0f')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

  </div>





```python
book_df.rename(columns={'author': 'Author', 'book_count': 'Book_counts'})
```





  <div id="df-e85e1841-6305-49b4-82a1-7bc7725b47a4">
    <div class="colab-df-container">
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
      <th>Book_counts</th>
      <th>rating</th>
      <th>Author</th>
      <th>title</th>
      <th>isAvailable</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>272.000000</td>
      <td>A</td>
      <td>Suzanne Collins</td>
      <td>The Hunger Games</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>491.000000</td>
      <td>C</td>
      <td>J.K. Rowling</td>
      <td>Harry Potter and the Philosopher's Stone</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>688.555556</td>
      <td>A</td>
      <td>Stephenie Meyer</td>
      <td>Twilight</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>487.000000</td>
      <td>B</td>
      <td>Harper Lee</td>
      <td>To Kill a Mockingbird</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1356.000000</td>
      <td>A</td>
      <td>J.D. Salinger</td>
      <td>The Great Gatsby</td>
      <td>True</td>
    </tr>
    <tr>
      <th>5</th>
      <td>226.000000</td>
      <td>A</td>
      <td>John Green</td>
      <td>The Fault in Our Stars</td>
      <td>True</td>
    </tr>
    <tr>
      <th>6</th>
      <td>969.000000</td>
      <td>B</td>
      <td>J.R.R. Tolkien</td>
      <td>The Hobbit or There and Back Again</td>
      <td>True</td>
    </tr>
    <tr>
      <th>7</th>
      <td>360.000000</td>
      <td>A</td>
      <td>J.D. Salinger</td>
      <td>The Catcher in the Rye</td>
      <td>True</td>
    </tr>
    <tr>
      <th>8</th>
      <td>311.000000</td>
      <td>C</td>
      <td>Dan Brown</td>
      <td>Angels &amp; Demons</td>
      <td>True</td>
    </tr>
    <tr>
      <th>9</th>
      <td>3455.000000</td>
      <td>A</td>
      <td>Jane Austen</td>
      <td>Pride and Prejudice</td>
      <td>True</td>
    </tr>
    <tr>
      <th>10</th>
      <td>688.555556</td>
      <td>B</td>
      <td>Khaled Hosseini</td>
      <td>The Kite Runner</td>
      <td>True</td>
    </tr>
    <tr>
      <th>11</th>
      <td>210.000000</td>
      <td>A</td>
      <td>Veronica Roth</td>
      <td>Divergent</td>
      <td>True</td>
    </tr>
    <tr>
      <th>12</th>
      <td>995.000000</td>
      <td>C</td>
      <td>John Green</td>
      <td>Nineteen Eighty-Four</td>
      <td>True</td>
    </tr>
    <tr>
      <th>13</th>
      <td>896.000000</td>
      <td>A</td>
      <td>George Orwell</td>
      <td>Animal Farm: A Fairy Story</td>
      <td>True</td>
    </tr>
    <tr>
      <th>14</th>
      <td>710.000000</td>
      <td>A</td>
      <td>Anne Frank</td>
      <td>Het Achterhuis</td>
      <td>True</td>
    </tr>
    <tr>
      <th>15</th>
      <td>274.000000</td>
      <td>B</td>
      <td>Stieg Larsson, Reg Keeland</td>
      <td>Män som hatar kvinnor</td>
      <td>True</td>
    </tr>
    <tr>
      <th>16</th>
      <td>201.000000</td>
      <td>A</td>
      <td>Suzanne Collins</td>
      <td>NaN</td>
      <td>True</td>
    </tr>
    <tr>
      <th>17</th>
      <td>376.000000</td>
      <td>C</td>
      <td>J.K. Rowling</td>
      <td>Harry Potter and the Prisoner of Azkaban</td>
      <td>True</td>
    </tr>
    <tr>
      <th>19</th>
      <td>239.000000</td>
      <td>C</td>
      <td>Suzanne Collins</td>
      <td>Mockingjay</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-e85e1841-6305-49b4-82a1-7bc7725b47a4')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

  </div>



