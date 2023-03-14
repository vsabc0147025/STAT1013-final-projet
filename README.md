---
jupyter:
  colab:
  kernelspec:
    display_name: Python 3
    name: python3
  language_info:
    name: python
  nbformat: 4
  nbformat_minor: 0
---

<div class="cell markdown" id="joi1jGaMMp0W">

## Formula 1 dataset background

**Description**:

Ergast Formula 1, from 1950 up to date (API)

**Github**:
<https://github.com/awesomedata/apd-core/blob/master/core/Sports/Ergast-Formula-1-from-1950-up-to-date-API.yml>

**Sample size**: 9575

**Feature documentation**:

| Feature         | Shape | Dtype   |
|:----------------|:------|:--------|
| resultId        | 25840 | int64   |
| raceId          | 25840 | int64   |
| driverId        | 25840 | int64   |
| constructorId_x | 25840 | int64   |
| number_x        | 25840 | object  |
| position_x      | 25840 | object  |
| grid            | 25840 | int64   |
| positionText    | 25840 | object  |
| positionOrder   | 25840 | int64   |
| points          | 25840 | float64 |
| laps            | 25840 | int64   |
| time            | 25840 | object  |
| milliseconds    | 25840 | object  |
| fastestLap      | 25840 | object  |
| rank            | 25840 | object  |
| fastestLapTime  | 25840 | object  |
| fastestLapSpeed | 25840 | object  |
| statusId        | 25840 | int64   |
| qualifyId       | 9575  | float64 |
| constructorId_y | 9575  | float64 |
| number_y        | 9575  | float64 |
| position_y      | 9575  | float64 |
| q1              | 9575  | object  |
| q2              | 9575  | object  |
| q3              | 9575  | object  |

</div>

<div class="cell markdown" id="sj9ojvDlMkT4">

## Hypothesis

-   Tell us what your idea is and why you have chosen to pursue this
    idea.

    -   The fastest driver in qualifying gets to start the race at the
        front, having no drivers in front of them. We call this Pole
        position

    -   We are interested in "*Does The Driver Who Starts On Pole Always
        Win?*"

-   What two groups you are comparing:

    -   **G1**: position of driver who start at pole ; **G2**: position
        of driver who not start at pole

-   What you will be measuring (i.e., what your response variable will
    be)

    -   `position`

-   Is your response variable quantitative rather than categorical?

    -   `position` is quantitative variable '2>1' but position'2' is
        slower than position'1'

-   Make a prediction about what kind of difference you expect to see
    between your samples and WHY.

    -   We'd expect that **G2** \> **G1**, starting at pole position
        should have advantages throughout the race since [HOW IMPORTANT
        IS POLE POSITION IN
        F1?](https://onestopracing.com/how-important-is-pole-position-in-f1/).

-   Talk about how you will gather your data

    -   From API <http://ergast.com/mrd/db/> and I downloaded this and
        uploaded it to Github:
        <https://github.com/vsabc0147025/Stat1013/blob/main/all.csv>

-   If you had unlimited resources (time, money, staff, etc.) how would
    you collect your data?

    -   \(i\) Attempt to collect more data on Formula 1; (ii)
        investigate if the provided dataset is a good random sampling
        subset of the Formula 1.

</div>

<div class="cell code" execution_count="47"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:875}"
id="dtFz9Nqdj-oQ" outputId="980e7f5b-cc4f-4ad8-d776-16ea71f3376a">

``` python
import pandas as pd

df = pd.read_csv('/content/drive/MyDrive/STAT1013/all.csv')
df.info()
df.head(5)
```

<div class="output stream stdout">

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 25840 entries, 0 to 25839
    Data columns (total 26 columns):
     #   Column           Non-Null Count  Dtype  
    ---  ------           --------------  -----  
     0   Unnamed: 0       25840 non-null  int64  
     1   resultId         25840 non-null  int64  
     2   raceId           25840 non-null  int64  
     3   driverId         25840 non-null  int64  
     4   constructorId_x  25840 non-null  int64  
     5   number_x         25834 non-null  float64
     6   grid             25840 non-null  int64  
     7   position_x       14989 non-null  float64
     8   positionText     25840 non-null  object 
     9   positionOrder    25840 non-null  int64  
     10  points           25840 non-null  float64
     11  laps             25840 non-null  int64  
     12  time             7088 non-null   object 
     13  milliseconds     7087 non-null   float64
     14  fastestLap       7379 non-null   float64
     15  rank             7591 non-null   float64
     16  fastestLapTime   7379 non-null   object 
     17  fastestLapSpeed  7379 non-null   float64
     18  statusId         25840 non-null  int64  
     19  qualifyId        9575 non-null   float64
     20  constructorId_y  9575 non-null   float64
     21  number_y         9575 non-null   float64
     22  position_y       9575 non-null   float64
     23  q1               9428 non-null   object 
     24  q2               5164 non-null   object 
     25  q3               3181 non-null   object 
    dtypes: float64(11), int64(9), object(6)
    memory usage: 5.1+ MB

</div>

<div class="output execute_result" execution_count="47">

       Unnamed: 0  resultId  raceId  driverId  constructorId_x  number_x  grid  \
    0           0         1      18         1                1      22.0     1   
    1           1         2      18         2                2       3.0     5   
    2           2         3      18         3                3       7.0     7   
    3           3         4      18         4                4       5.0    11   
    4           4         5      18         5                1      23.0     3   

       position_x positionText  positionOrder  ...  fastestLapTime  \
    0         1.0            1              1  ...         01:27.5   
    1         2.0            2              2  ...         01:27.7   
    2         3.0            3              3  ...         01:28.1   
    3         4.0            4              4  ...         01:28.6   
    4         5.0            5              5  ...         01:27.4   

       fastestLapSpeed statusId  qualifyId  constructorId_y  number_y position_y  \
    0          218.300        1        1.0              1.0      22.0        1.0   
    1          217.586        1        5.0              2.0       3.0        5.0   
    2          216.719        1        7.0              3.0       7.0        7.0   
    3          215.464        1       12.0              4.0       5.0       12.0   
    4          218.385        1        3.0              1.0      23.0        3.0   

            q1       q2       q3  
    0  01:26.6  01:25.2  01:26.7  
    1  01:26.0  01:25.5  01:27.2  
    2  01:26.3  01:26.1  01:28.7  
    3  01:26.9  01:26.2      NaN  
    4  01:25.7  01:25.5  01:27.1  

    [5 rows x 26 columns]

</div>

</div>

<div class="cell code" execution_count="49" id="WTkFYZAKd7Yw">

``` python
df=df.dropna()
df=df.dropna(axis=0)
```

</div>

<div class="cell code" execution_count="56"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="j2Gc0SzPfsTG" outputId="8f8e5b22-48c4-41ca-b249-c5751145136b">

``` python
df.info()
```

<div class="output stream stdout">

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 2285 entries, 0 to 25829
    Data columns (total 26 columns):
     #   Column           Non-Null Count  Dtype  
    ---  ------           --------------  -----  
     0   Unnamed: 0       2285 non-null   int64  
     1   resultId         2285 non-null   int64  
     2   raceId           2285 non-null   int64  
     3   driverId         2285 non-null   int64  
     4   constructorId_x  2285 non-null   int64  
     5   number_x         2285 non-null   float64
     6   grid             2285 non-null   int64  
     7   position_x       2285 non-null   float64
     8   positionText     2285 non-null   object 
     9   positionOrder    2285 non-null   int64  
     10  points           2285 non-null   float64
     11  laps             2285 non-null   int64  
     12  time             2285 non-null   object 
     13  milliseconds     2285 non-null   float64
     14  fastestLap       2285 non-null   float64
     15  rank             2285 non-null   float64
     16  fastestLapTime   2285 non-null   object 
     17  fastestLapSpeed  2285 non-null   float64
     18  statusId         2285 non-null   int64  
     19  qualifyId        2285 non-null   float64
     20  constructorId_y  2285 non-null   float64
     21  number_y         2285 non-null   float64
     22  position_y       2285 non-null   float64
     23  q1               2285 non-null   object 
     24  q2               2285 non-null   object 
     25  q3               2285 non-null   object 
    dtypes: float64(11), int64(9), object(6)
    memory usage: 482.0+ KB

</div>

</div>

<div class="cell markdown" id="8d8YrgfCYj5h">

-   Tell us what groups you want to compare in the dataset
    -   **G1** (position_x \| position_y == 1) vs. **G2** (position_x \|
        position_y != 1)

</div>

<div class="cell code" execution_count="50"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="6qw767esWsuj" outputId="26f64ad0-0f63-4af3-d730-d434a7282427">

``` python
## First 5 records of G1 (Pole)
(df[df['position_y'] == 1]['position_x']).head(5)
```

<div class="output execute_result" execution_count="50">

    0      1.0
    46     3.0
    66     1.0
    88     1.0
    110    3.0
    Name: position_x, dtype: float64

</div>

</div>

<div class="cell code" execution_count="51"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="_OvVFk3KaDBY" outputId="05a671c4-353b-4881-8510-f2318630cc88">

``` python
## First 5 records of G2 (Not Pole)
(df[df['position_y'] != 1]['position_x']).head(5)
```

<div class="output execute_result" execution_count="51">

    1     2.0
    2     3.0
    4     5.0
    22    1.0
    23    2.0
    Name: position_x, dtype: float64

</div>

</div>

<div class="cell code" execution_count="57"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="yjWhx8ztf2WV" outputId="4dc4599b-2945-44f0-8773-1f7fe82d7a4b">

``` python
## Types of columns
df.info()
```

<div class="output stream stdout">

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 2285 entries, 0 to 25829
    Data columns (total 26 columns):
     #   Column           Non-Null Count  Dtype  
    ---  ------           --------------  -----  
     0   Unnamed: 0       2285 non-null   int64  
     1   resultId         2285 non-null   int64  
     2   raceId           2285 non-null   int64  
     3   driverId         2285 non-null   int64  
     4   constructorId_x  2285 non-null   int64  
     5   number_x         2285 non-null   float64
     6   grid             2285 non-null   int64  
     7   position_x       2285 non-null   float64
     8   positionText     2285 non-null   object 
     9   positionOrder    2285 non-null   int64  
     10  points           2285 non-null   float64
     11  laps             2285 non-null   int64  
     12  time             2285 non-null   object 
     13  milliseconds     2285 non-null   float64
     14  fastestLap       2285 non-null   float64
     15  rank             2285 non-null   float64
     16  fastestLapTime   2285 non-null   object 
     17  fastestLapSpeed  2285 non-null   float64
     18  statusId         2285 non-null   int64  
     19  qualifyId        2285 non-null   float64
     20  constructorId_y  2285 non-null   float64
     21  number_y         2285 non-null   float64
     22  position_y       2285 non-null   float64
     23  q1               2285 non-null   object 
     24  q2               2285 non-null   object 
     25  q3               2285 non-null   object 
    dtypes: float64(11), int64(9), object(6)
    memory usage: 482.0+ KB

</div>

</div>

<div class="cell code" execution_count="58"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:855}"
id="Ed3mKQZ_f4Kg" outputId="2a565333-a7a2-44f8-ac87-349f257e096d">

``` python
## check the basic statistics for all columns
df.describe(include='all').T
```

<div class="output execute_result" execution_count="58">

                      count unique      top freq            mean             std  \
    Unnamed: 0       2285.0    NaN      NaN  NaN    18695.397812     8759.033358   
    resultId         2285.0    NaN      NaN  NaN    18699.208315     8760.640806   
    raceId           2285.0    NaN      NaN  NaN      727.505033      398.985077   
    driverId         2285.0    NaN      NaN  NaN       305.77593      390.466345   
    constructorId_x  2285.0    NaN      NaN  NaN       41.515974       65.068853   
    number_x         2285.0    NaN      NaN  NaN       17.958425       20.174882   
    grid             2285.0    NaN      NaN  NaN        4.985558        3.102491   
    position_x       2285.0    NaN      NaN  NaN        4.715536        2.992921   
    positionText       2285     16        1  324             NaN             NaN   
    positionOrder    2285.0    NaN      NaN  NaN        4.715536        2.992921   
    points           2285.0    NaN      NaN  NaN       10.700875        7.396492   
    laps             2285.0    NaN      NaN  NaN       59.820131        8.853969   
    time               2285   2261      8.8    3             NaN             NaN   
    milliseconds     2285.0    NaN      NaN  NaN  5884034.307221  1059491.536945   
    fastestLap       2285.0    NaN      NaN  NaN       46.856455       14.221123   
    rank             2285.0    NaN      NaN  NaN        5.828446        3.923455   
    fastestLapTime     2285    471  01:16.2   15             NaN             NaN   
    fastestLapSpeed  2285.0    NaN      NaN  NaN       205.91138       20.785249   
    statusId         2285.0    NaN      NaN  NaN        1.056893         2.71957   
    qualifyId        2285.0    NaN      NaN  NaN     5639.321225     2826.070804   
    constructorId_y  2285.0    NaN      NaN  NaN       41.515974       65.068853   
    number_y         2285.0    NaN      NaN  NaN       17.958425       20.174882   
    position_y       2285.0    NaN      NaN  NaN        4.852079        2.739093   
    q1                 2285    486  01:20.4   15             NaN             NaN   
    q2                 2285    472  01:26.1   15             NaN             NaN   
    q3                 2285    507  01:36.2   14             NaN             NaN   

                           min        25%        50%        75%         max  
    Unnamed: 0             0.0    20542.0    22417.0    24161.0     25829.0  
    resultId               1.0    20545.0    22421.0    24167.0     25835.0  
    raceId                 1.0      346.0      913.0     1008.0      1096.0  
    driverId               1.0        5.0       20.0      817.0       855.0  
    constructorId_x        1.0        4.0        7.0       23.0       214.0  
    number_x               1.0        5.0       10.0       23.0        99.0  
    grid                   0.0        2.0        5.0        7.0        24.0  
    position_x             1.0        2.0        4.0        7.0        17.0  
    positionText           NaN        NaN        NaN        NaN         NaN  
    positionOrder          1.0        2.0        4.0        7.0        17.0  
    points                 0.0        5.0       10.0       15.0        50.0  
    laps                  28.0       53.0       57.0       67.0        87.0  
    time                   NaN        NaN        NaN        NaN         NaN  
    milliseconds     4252092.0  5352532.0  5668044.0  6018017.0  14729991.0  
    fastestLap             2.0       39.0       49.0       56.0        85.0  
    rank                   1.0        3.0        5.0        8.0        19.0  
    fastestLapTime         NaN        NaN        NaN        NaN         NaN  
    fastestLapSpeed    150.511    195.502    206.221    218.847     255.014  
    statusId               1.0        1.0        1.0        1.0       131.0  
    qualifyId              1.0     3546.0     6175.0     7924.0      9622.0  
    constructorId_y        1.0        4.0        7.0       23.0       214.0  
    number_y               1.0        5.0       10.0       23.0        99.0  
    position_y             1.0        2.0        5.0        7.0        14.0  
    q1                     NaN        NaN        NaN        NaN         NaN  
    q2                     NaN        NaN        NaN        NaN         NaN  
    q3                     NaN        NaN        NaN        NaN         NaN  

</div>

</div>

<div class="cell code" execution_count="52" id="KLeJIHiFcJ3h">

``` python
import matplotlib.pyplot as plt
import seaborn as sns
plt.rcParams['figure.figsize'] = [10, 5]

sns.set()
```

</div>

<div class="cell code" execution_count="54"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:661}"
id="3oJ8KIPse4XC" outputId="75885312-78a3-4b9a-a1d7-13eed7da25bf">

``` python
sns.histplot(df, x='position_x')
plt.show()
## position_x is the position of the race. Some driver did not finish the race so the count will drop with ranking.


sns.histplot(df, x='position_y')
plt.show()
## position_y is the position in qualifying. There is data of position larger than 10.
```

<div class="output display_data">

![](08e932717132d138c96d15ee0e5a600fbd213cf9.png)

</div>

<div class="output display_data">

![](8f28839fe81e572877f3b06b5aa0090e9022fe13.png)

</div>

</div>

<div class="cell code" execution_count="60"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:339}"
id="oqaXwIyZfIcb" outputId="508f2374-af78-4cc5-9eb5-d51643f150f9">

``` python
sns.violinplot(x=df['position_x'])
plt.show()
## Position =1 is the most frequent data as there is a champion in every race until all the driver did not finish.
```

<div class="output display_data">

![](a3088aea8db3e91265f870827d74dd82d7c83343.png)

</div>

</div>

<div class="cell code" execution_count="62"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:339}"
id="7NgjmU3Diiv5" outputId="1c9ca62e-0658-4803-ec7b-4389b0d38d6a">

``` python
sns.histplot(df, x='position_x', hue='position_y')
plt.show()
## We can see that if the driver start at Pole postion, he will likely become the champhion.
```

<div class="output display_data">

![](a7618c05e36e9d9eea59d09fdc9d6f0e0195b28c.png)

</div>

</div>

<div class="cell code" id="jjPlIlM2jHYT">

``` python
```

</div>
