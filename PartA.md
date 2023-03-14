---
jupyter:
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
  language_info:
    codemirror_mode:
      name: ipython
      version: 3
    file_extension: .py
    mimetype: text/x-python
    name: python
    nbconvert_exporter: python
    pygments_lexer: ipython3
    version: 3.9.13
  nbformat: 4
  nbformat_minor: 5
---

<div class="cell code" execution_count="3">

``` python
df = pd.read_csv('https://raw.githubusercontent.com/datasciencedojo/datasets/master/titanic.csv')
df.head(5)
```

<div class="output execute_result" execution_count="3">

       PassengerId  Survived  Pclass  \
    0            1         0       3   
    1            2         1       1   
    2            3         1       3   
    3            4         1       1   
    4            5         0       3   

                                                    Name     Sex   Age  SibSp  \
    0                            Braund, Mr. Owen Harris    male  22.0      1   
    1  Cumings, Mrs. John Bradley (Florence Briggs Th...  female  38.0      1   
    2                             Heikkinen, Miss. Laina  female  26.0      0   
    3       Futrelle, Mrs. Jacques Heath (Lily May Peel)  female  35.0      1   
    4                           Allen, Mr. William Henry    male  35.0      0   

       Parch            Ticket     Fare Cabin Embarked  
    0      0         A/5 21171   7.2500   NaN        S  
    1      0          PC 17599  71.2833   C85        C  
    2      0  STON/O2. 3101282   7.9250   NaN        S  
    3      0            113803  53.1000  C123        S  
    4      0            373450   8.0500   NaN        S  

</div>

</div>

<div class="cell code" execution_count="4">

``` python
print(len(df['Survived']>2))
```

<div class="output stream stdout">

    891

</div>

</div>

<div class="cell code" execution_count="21">

``` python
df.groupby("Pclass")['Survived'].mean()
```

<div class="output execute_result" execution_count="21">

    Pclass
    1    0.629630
    2    0.472826
    3    0.242363
    Name: Survived, dtype: float64

</div>

</div>

<div class="cell code" execution_count="12">

``` python
print(len((df['Pclass']==1) & (df['Survived']==1))/len((df['Pclass']==1)))
```

<div class="output stream stdout">

    1.0

</div>

</div>

<div class="cell code" execution_count="23">

``` python
len(df[(df['Pclass'] == 1) & (df['Survived'] == 1)]) / len((df['Pclass']==1))
```

<div class="output execute_result" execution_count="23">

    0.1526374859708193

</div>

</div>

<div class="cell code" execution_count="24">

``` python
len(df[(df['Pclass'] == 2) & (df['Survived'] == 1)]) / len((df['Pclass']==2))
```

<div class="output execute_result" execution_count="24">

    0.09764309764309764

</div>

</div>

<div class="cell code" execution_count="25">

``` python
len(df[(df['Pclass'] == 3) & (df['Survived'] == 1)]) / len((df['Pclass']==3))
```

<div class="output execute_result" execution_count="25">

    0.1335578002244669

</div>

</div>

<div class="cell code" execution_count="9">

``` python
print(df.groupby('Pclass')['Fare'].median())
```

<div class="output stream stdout">

    Pclass
    1    60.2875
    2    14.2500
    3     8.0500
    Name: Fare, dtype: float64

</div>

</div>

<div class="cell code" execution_count="10">

``` python
print(df.groupby('Embarked')['Fare'].std())
```

<div class="output stream stdout">

    Embarked
    C    83.912994
    Q    14.188047
    S    35.887993
    Name: Fare, dtype: float64

</div>

</div>

<div class="cell code" execution_count="2">

``` python
import pandas as pd
```

</div>

<div class="cell code" execution_count="16">

``` python
df = pd.read_csv(r'/Users/raytse/Downloads/f1db_csv/qualifying.csv')
df
```

<div class="output execute_result" execution_count="16">

          qualifyId  raceId  driverId  constructorId  number  position        q1  \
    0             1      18         1              1      22         1  1:26.572   
    1             2      18         9              2       4         2  1:26.103   
    2             3      18         5              1      23         3  1:25.664   
    3             4      18        13              6       2         4  1:25.994   
    4             5      18         2              2       3         5  1:25.960   
    ...         ...     ...       ...            ...     ...       ...       ...   
    9570       9628    1096       825            210      20        16  1:25.834   
    9571       9629    1096       842            213      10        17  1:25.859   
    9572       9630    1096       822             51      77        18  1:25.892   
    9573       9631    1096       848              3      23        19  1:26.028   
    9574       9632    1096       849              3       6        20  1:26.054   

                q2        q3  
    0     1:25.187  1:26.714  
    1     1:25.315  1:26.869  
    2     1:25.452  1:27.079  
    3     1:25.691  1:27.178  
    4     1:25.518  1:27.236  
    ...        ...       ...  
    9570        \N        \N  
    9571        \N        \N  
    9572        \N        \N  
    9573        \N        \N  
    9574        \N        \N  

    [9575 rows x 9 columns]

</div>

</div>

<div class="cell code" execution_count="15">

``` python
df2 = pd.read_csv(r'/Users/raytse/Downloads/f1db_csv/results.csv')
df2
```

<div class="output execute_result" execution_count="15">

           resultId  raceId  driverId  constructorId number  grid position  \
    0             1      18         1              1     22     1        1   
    1             2      18         2              2      3     5        2   
    2             3      18         3              3      7     7        3   
    3             4      18         4              4      5    11        4   
    4             5      18         5              1     23     3        5   
    ...         ...     ...       ...            ...    ...   ...      ...   
    25835     25841    1096       854            210     47    12       16   
    25836     25842    1096       825            210     20    16       17   
    25837     25843    1096         1            131     44     5       18   
    25838     25844    1096       849              3      6    20       19   
    25839     25845    1096         4            214     14    10       \N   

          positionText  positionOrder  points  laps         time milliseconds  \
    0                1              1    10.0    58  1:34:50.616      5690616   
    1                2              2     8.0    58       +5.478      5696094   
    2                3              3     6.0    58       +8.163      5698779   
    3                4              4     5.0    58      +17.181      5707797   
    4                5              5     4.0    58      +18.014      5708630   
    ...            ...            ...     ...   ...          ...          ...   
    25835           16             16     0.0    57           \N           \N   
    25836           17             17     0.0    57           \N           \N   
    25837           18             18     0.0    55           \N           \N   
    25838           19             19     0.0    55           \N           \N   
    25839            R             20     0.0    27           \N           \N   

          fastestLap rank fastestLapTime fastestLapSpeed  statusId  
    0             39    2       1:27.452         218.300         1  
    1             41    3       1:27.739         217.586         1  
    2             41    5       1:28.090         216.719         1  
    3             58    7       1:28.603         215.464         1  
    4             43    1       1:27.418         218.385         1  
    ...          ...  ...            ...             ...       ...  
    25835         39   12       1:29.833         211.632        11  
    25836         40   20       1:31.158         208.556        11  
    25837         42   11       1:29.788         211.738         9  
    25838         45   14       1:30.309         210.517       130  
    25839         24   17       1:30.579         209.889        47  

    [25840 rows x 18 columns]

</div>

</div>

<div class="cell code" execution_count="10">

``` python
df3= pd.read_csv(r'/Users/raytse/Downloads/f1db_csv/drivers.csv')
```

</div>

<div class="cell code">

``` python
df3= pd.read_csv(r'/Users/raytse/Downloads/f1db_csv/drivers.csv')
```

</div>

<div class="cell code" execution_count="13">

``` python
merged = df2.merge(df,how='left',on=['raceId','driverId'])
```

</div>

<div class="cell code" execution_count="17">

``` python
merged.to_csv(r'/Users/raytse/Downloads/f1db_csv/all.csv')
```

</div>

<div class="cell code" execution_count="19">

``` python
merged
```

<div class="output execute_result" execution_count="19">

           resultId  raceId  driverId  constructorId_x number_x  grid position_x  \
    0             1      18         1                1       22     1          1   
    1             2      18         2                2        3     5          2   
    2             3      18         3                3        7     7          3   
    3             4      18         4                4        5    11          4   
    4             5      18         5                1       23     3          5   
    ...         ...     ...       ...              ...      ...   ...        ...   
    25835     25841    1096       854              210       47    12         16   
    25836     25842    1096       825              210       20    16         17   
    25837     25843    1096         1              131       44     5         18   
    25838     25844    1096       849                3        6    20         19   
    25839     25845    1096         4              214       14    10         \N   

          positionText  positionOrder  points  ...  fastestLapTime  \
    0                1              1    10.0  ...        1:27.452   
    1                2              2     8.0  ...        1:27.739   
    2                3              3     6.0  ...        1:28.090   
    3                4              4     5.0  ...        1:28.603   
    4                5              5     4.0  ...        1:27.418   
    ...            ...            ...     ...  ...             ...   
    25835           16             16     0.0  ...        1:29.833   
    25836           17             17     0.0  ...        1:31.158   
    25837           18             18     0.0  ...        1:29.788   
    25838           19             19     0.0  ...        1:30.309   
    25839            R             20     0.0  ...        1:30.579   

          fastestLapSpeed statusId qualifyId constructorId_y number_y position_y  \
    0             218.300        1       1.0             1.0     22.0        1.0   
    1             217.586        1       5.0             2.0      3.0        5.0   
    2             216.719        1       7.0             3.0      7.0        7.0   
    3             215.464        1      12.0             4.0      5.0       12.0   
    4             218.385        1       3.0             1.0     23.0        3.0   
    ...               ...      ...       ...             ...      ...        ...   
    25835         211.632       11    9625.0           210.0     47.0       13.0   
    25836         208.556       11    9628.0           210.0     20.0       16.0   
    25837         211.738        9    9617.0           131.0     44.0        5.0   
    25838         210.517      130    9632.0             3.0      6.0       20.0   
    25839         209.889       47    9623.0           214.0     14.0       11.0   

                 q1        q2        q3  
    0      1:26.572  1:25.187  1:26.714  
    1      1:25.960  1:25.518  1:27.236  
    2      1:26.295  1:26.059  1:28.687  
    3      1:26.907  1:26.188        \N  
    4      1:25.664  1:25.452  1:27.079  
    ...         ...       ...       ...  
    25835  1:25.711  1:25.225        \N  
    25836  1:25.834        \N        \N  
    25837  1:25.594  1:24.774  1:24.508  
    25838  1:26.054        \N        \N  
    25839  1:25.782  1:25.096        \N  

    [25840 rows x 25 columns]

</div>

</div>

<div class="cell code" execution_count="18">

``` python
merged.info()
```

<div class="output stream stdout">

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 25840 entries, 0 to 25839
    Data columns (total 25 columns):
     #   Column           Non-Null Count  Dtype  
    ---  ------           --------------  -----  
     0   resultId         25840 non-null  int64  
     1   raceId           25840 non-null  int64  
     2   driverId         25840 non-null  int64  
     3   constructorId_x  25840 non-null  int64  
     4   number_x         25840 non-null  object 
     5   grid             25840 non-null  int64  
     6   position_x       25840 non-null  object 
     7   positionText     25840 non-null  object 
     8   positionOrder    25840 non-null  int64  
     9   points           25840 non-null  float64
     10  laps             25840 non-null  int64  
     11  time             25840 non-null  object 
     12  milliseconds     25840 non-null  object 
     13  fastestLap       25840 non-null  object 
     14  rank             25840 non-null  object 
     15  fastestLapTime   25840 non-null  object 
     16  fastestLapSpeed  25840 non-null  object 
     17  statusId         25840 non-null  int64  
     18  qualifyId        9575 non-null   float64
     19  constructorId_y  9575 non-null   float64
     20  number_y         9575 non-null   float64
     21  position_y       9575 non-null   float64
     22  q1               9567 non-null   object 
     23  q2               9424 non-null   object 
     24  q3               9276 non-null   object 
    dtypes: float64(5), int64(8), object(12)
    memory usage: 5.1+ MB

</div>

</div>
