## ROTTEN TOMATOES MOVIE REVIEW DATASET

### TASK:
I’m the host of a movie reviews podcast and I’m currently making an episode about movie review aggregators.
I found this data set from Rotten Tomatoes. Could you dig into the data and share any interesting insights that you find? My audience loves fun facts about movies.

## 0. Read in the Data


```python
# rotten tomatoes movie data set
import pandas as pd

movies = pd.read_csv('movie_review_dataset.csv')
movies.head(3)
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
      <th>movie_title</th>
      <th>movie_info</th>
      <th>critics_consensus</th>
      <th>rating</th>
      <th>genre</th>
      <th>directors</th>
      <th>writers</th>
      <th>cast</th>
      <th>in_theaters_date</th>
      <th>on_streaming_date</th>
      <th>runtime_in_minutes</th>
      <th>studio_name</th>
      <th>tomatometer_status</th>
      <th>tomatometer_rating</th>
      <th>tomatometer_count</th>
      <th>audience_rating</th>
      <th>audience_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Percy Jackson &amp; the Olympians: The Lightning T...</td>
      <td>A teenager discovers he's the descendant of a ...</td>
      <td>Though it may seem like just another Harry Pot...</td>
      <td>PG</td>
      <td>Action &amp; Adventure, Comedy, Drama, Science Fic...</td>
      <td>Chris Columbus</td>
      <td>Craig Titley</td>
      <td>Logan Lerman, Brandon T. Jackson, Alexandra Da...</td>
      <td>2010-02-12</td>
      <td>2010-06-29</td>
      <td>83.0</td>
      <td>20th Century Fox</td>
      <td>Rotten</td>
      <td>49</td>
      <td>144</td>
      <td>53.0</td>
      <td>254287.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Please Give</td>
      <td>Kate has a lot on her mind. There's the ethics...</td>
      <td>Nicole Holofcener's newest might seem slight i...</td>
      <td>R</td>
      <td>Comedy</td>
      <td>Nicole Holofcener</td>
      <td>Nicole Holofcener</td>
      <td>Catherine Keener, Amanda Peet, Oliver Platt, R...</td>
      <td>2010-04-30</td>
      <td>2010-10-19</td>
      <td>90.0</td>
      <td>Sony Pictures Classics</td>
      <td>Certified Fresh</td>
      <td>86</td>
      <td>140</td>
      <td>64.0</td>
      <td>11567.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10</td>
      <td>Blake Edwards' 10 stars Dudley Moore as George...</td>
      <td>NaN</td>
      <td>R</td>
      <td>Comedy, Romance</td>
      <td>Blake Edwards</td>
      <td>Blake Edwards</td>
      <td>Dudley Moore, Bo Derek, Julie Andrews, Robert ...</td>
      <td>1979-10-05</td>
      <td>1997-08-27</td>
      <td>118.0</td>
      <td>Waner Bros.</td>
      <td>Fresh</td>
      <td>68</td>
      <td>22</td>
      <td>53.0</td>
      <td>14670.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# working with subset of the data set
movies = movies[['movie_title', 'rating', 'genre', 'in_theaters_date','runtime_in_minutes',
                 'tomatometer_rating', 'tomatometer_count', 'audience_rating', 'audience_count']]
movies.head()
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
      <th>movie_title</th>
      <th>rating</th>
      <th>genre</th>
      <th>in_theaters_date</th>
      <th>runtime_in_minutes</th>
      <th>tomatometer_rating</th>
      <th>tomatometer_count</th>
      <th>audience_rating</th>
      <th>audience_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Percy Jackson &amp; the Olympians: The Lightning T...</td>
      <td>PG</td>
      <td>Action &amp; Adventure, Comedy, Drama, Science Fic...</td>
      <td>2010-02-12</td>
      <td>83.0</td>
      <td>49</td>
      <td>144</td>
      <td>53.0</td>
      <td>254287.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Please Give</td>
      <td>R</td>
      <td>Comedy</td>
      <td>2010-04-30</td>
      <td>90.0</td>
      <td>86</td>
      <td>140</td>
      <td>64.0</td>
      <td>11567.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10</td>
      <td>R</td>
      <td>Comedy, Romance</td>
      <td>1979-10-05</td>
      <td>118.0</td>
      <td>68</td>
      <td>22</td>
      <td>53.0</td>
      <td>14670.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12 Angry Men (Twelve Angry Men)</td>
      <td>NR</td>
      <td>Classics, Drama</td>
      <td>1957-04-13</td>
      <td>95.0</td>
      <td>100</td>
      <td>51</td>
      <td>97.0</td>
      <td>105000.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20,000 Leagues Under The Sea</td>
      <td>G</td>
      <td>Action &amp; Adventure, Drama, Kids &amp; Family</td>
      <td>1954-01-01</td>
      <td>127.0</td>
      <td>89</td>
      <td>27</td>
      <td>74.0</td>
      <td>68860.0</td>
    </tr>
  </tbody>
</table>
</div>



## 1. Explore the Data

How many movies are in this data set


```python
# number of rows and columns
movies.shape
```




    (16638, 9)



Filter data - only includes movies that came out in 2010 or later.


```python
# data types check
movies.dtypes
```




    movie_title            object
    rating                 object
    genre                  object
    in_theaters_date       object
    runtime_in_minutes    float64
    tomatometer_rating      int64
    tomatometer_count       int64
    audience_rating       float64
    audience_count        float64
    dtype: object




```python
# in_theatres_date to datetime field
movies['in_theaters_date'] = pd.to_datetime(movies.in_theaters_date)
movies.head(3)
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
      <th>movie_title</th>
      <th>rating</th>
      <th>genre</th>
      <th>in_theaters_date</th>
      <th>runtime_in_minutes</th>
      <th>tomatometer_rating</th>
      <th>tomatometer_count</th>
      <th>audience_rating</th>
      <th>audience_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Percy Jackson &amp; the Olympians: The Lightning T...</td>
      <td>PG</td>
      <td>Action &amp; Adventure, Comedy, Drama, Science Fic...</td>
      <td>2010-02-12</td>
      <td>83.0</td>
      <td>49</td>
      <td>144</td>
      <td>53.0</td>
      <td>254287.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Please Give</td>
      <td>R</td>
      <td>Comedy</td>
      <td>2010-04-30</td>
      <td>90.0</td>
      <td>86</td>
      <td>140</td>
      <td>64.0</td>
      <td>11567.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10</td>
      <td>R</td>
      <td>Comedy, Romance</td>
      <td>1979-10-05</td>
      <td>118.0</td>
      <td>68</td>
      <td>22</td>
      <td>53.0</td>
      <td>14670.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# filter on only movies from the 2010's and newer
movies = movies[movies.in_theaters_date.dt.year >= 2010]
movies.head(3)
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
      <th>movie_title</th>
      <th>rating</th>
      <th>genre</th>
      <th>in_theaters_date</th>
      <th>runtime_in_minutes</th>
      <th>tomatometer_rating</th>
      <th>tomatometer_count</th>
      <th>audience_rating</th>
      <th>audience_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Percy Jackson &amp; the Olympians: The Lightning T...</td>
      <td>PG</td>
      <td>Action &amp; Adventure, Comedy, Drama, Science Fic...</td>
      <td>2010-02-12</td>
      <td>83.0</td>
      <td>49</td>
      <td>144</td>
      <td>53.0</td>
      <td>254287.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Please Give</td>
      <td>R</td>
      <td>Comedy</td>
      <td>2010-04-30</td>
      <td>90.0</td>
      <td>86</td>
      <td>140</td>
      <td>64.0</td>
      <td>11567.0</td>
    </tr>
    <tr>
      <th>97</th>
      <td>Fireflies in the Garden</td>
      <td>R</td>
      <td>Drama</td>
      <td>2011-10-14</td>
      <td>98.0</td>
      <td>22</td>
      <td>54</td>
      <td>45.0</td>
      <td>45150.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# number of movies
movies.shape
```




    (6053, 9)



Find the highest rated movies according to both critics (*tomatometer_rating*) and the general audience (*audience_rating*).


```python
# highest rated movies by critics
movies.sort_values('tomatometer_rating', ascending=False).head()
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
      <th>movie_title</th>
      <th>rating</th>
      <th>genre</th>
      <th>in_theaters_date</th>
      <th>runtime_in_minutes</th>
      <th>tomatometer_rating</th>
      <th>tomatometer_count</th>
      <th>audience_rating</th>
      <th>audience_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3093</th>
      <td>Batman: The Dark Knight Returns, Part 1</td>
      <td>PG-13</td>
      <td>Action &amp; Adventure, Animation</td>
      <td>2012-01-01</td>
      <td>134.0</td>
      <td>100</td>
      <td>5</td>
      <td>93.0</td>
      <td>8482.0</td>
    </tr>
    <tr>
      <th>8500</th>
      <td>King Georges</td>
      <td>NR</td>
      <td>Documentary</td>
      <td>2016-02-26</td>
      <td>78.0</td>
      <td>100</td>
      <td>9</td>
      <td>54.0</td>
      <td>240.0</td>
    </tr>
    <tr>
      <th>8495</th>
      <td>King Charles III</td>
      <td>NR</td>
      <td>Drama</td>
      <td>2017-05-14</td>
      <td>88.0</td>
      <td>100</td>
      <td>9</td>
      <td>48.0</td>
      <td>65.0</td>
    </tr>
    <tr>
      <th>8477</th>
      <td>Killing for Love (Das Versprechen)</td>
      <td>NR</td>
      <td>Art House &amp; International, Documentary</td>
      <td>2017-12-15</td>
      <td>124.0</td>
      <td>100</td>
      <td>9</td>
      <td>82.0</td>
      <td>201.0</td>
    </tr>
    <tr>
      <th>8461</th>
      <td>Kill Zone 2 (Saat po long 2)</td>
      <td>NR</td>
      <td>Action &amp; Adventure, Art House &amp; International,...</td>
      <td>2016-05-13</td>
      <td>120.0</td>
      <td>100</td>
      <td>22</td>
      <td>63.0</td>
      <td>544.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# highest rated movies by the audience
movies.sort_values('audience_rating', ascending=False).head()
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
      <th>movie_title</th>
      <th>rating</th>
      <th>genre</th>
      <th>in_theaters_date</th>
      <th>runtime_in_minutes</th>
      <th>tomatometer_rating</th>
      <th>tomatometer_count</th>
      <th>audience_rating</th>
      <th>audience_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>14566</th>
      <td>The Miners' Hymns</td>
      <td>NR</td>
      <td>Documentary, Drama, Special Interest</td>
      <td>2012-02-08</td>
      <td>52.0</td>
      <td>100</td>
      <td>10</td>
      <td>100.0</td>
      <td>148.0</td>
    </tr>
    <tr>
      <th>9051</th>
      <td>Little Monsters</td>
      <td>R</td>
      <td>Comedy, Horror</td>
      <td>2019-10-08</td>
      <td>94.0</td>
      <td>83</td>
      <td>94</td>
      <td>100.0</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>7137</th>
      <td>Haunt</td>
      <td>R</td>
      <td>Horror, Mystery &amp; Suspense</td>
      <td>2019-09-13</td>
      <td>92.0</td>
      <td>68</td>
      <td>38</td>
      <td>100.0</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>16438</th>
      <td>Wonders of the Sea</td>
      <td>NR</td>
      <td>Documentary</td>
      <td>2019-01-17</td>
      <td>82.0</td>
      <td>76</td>
      <td>17</td>
      <td>100.0</td>
      <td>13.0</td>
    </tr>
    <tr>
      <th>14580</th>
      <td>The Most Dangerous Year</td>
      <td>NR</td>
      <td>Documentary</td>
      <td>2019-04-12</td>
      <td>90.0</td>
      <td>91</td>
      <td>11</td>
      <td>100.0</td>
      <td>40.0</td>
    </tr>
  </tbody>
</table>
</div>



These top movies seem to have very few critics and audience members writing the reviews. We want to look at only the most popular movies. Filter - movies data set to only include movies that have 100k+ audience ratings.


```python
# about 300 movies to work with
movies_popular = movies[movies.audience_count > 100000]
movies_popular.shape
```




    (316, 9)



Find the highest rated **popular** movies according to both critics (*tomatometer_rating*) and the general audience (*audience_rating*).


```python
# highest rated popular movies by critics
movies_popular.sort_values('tomatometer_rating', ascending=False).head()
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
      <th>movie_title</th>
      <th>rating</th>
      <th>genre</th>
      <th>in_theaters_date</th>
      <th>runtime_in_minutes</th>
      <th>tomatometer_rating</th>
      <th>tomatometer_count</th>
      <th>audience_rating</th>
      <th>audience_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>7558</th>
      <td>How to Train Your Dragon</td>
      <td>PG</td>
      <td>Animation, Kids &amp; Family, Science Fiction &amp; Fa...</td>
      <td>2010-03-26</td>
      <td>98.0</td>
      <td>99</td>
      <td>208</td>
      <td>91.0</td>
      <td>312342.0</td>
    </tr>
    <tr>
      <th>15416</th>
      <td>Toy Story 3</td>
      <td>G</td>
      <td>Animation, Comedy, Kids &amp; Family</td>
      <td>2010-06-18</td>
      <td>103.0</td>
      <td>98</td>
      <td>305</td>
      <td>89.0</td>
      <td>606931.0</td>
    </tr>
    <tr>
      <th>7925</th>
      <td>Inside Out</td>
      <td>PG</td>
      <td>Animation, Kids &amp; Family</td>
      <td>2015-06-19</td>
      <td>94.0</td>
      <td>98</td>
      <td>357</td>
      <td>89.0</td>
      <td>136125.0</td>
    </tr>
    <tr>
      <th>16634</th>
      <td>Zootopia</td>
      <td>PG</td>
      <td>Action &amp; Adventure, Animation, Comedy</td>
      <td>2016-03-04</td>
      <td>108.0</td>
      <td>97</td>
      <td>279</td>
      <td>92.0</td>
      <td>100946.0</td>
    </tr>
    <tr>
      <th>9355</th>
      <td>Mad Max: Fury Road</td>
      <td>R</td>
      <td>Action &amp; Adventure, Science Fiction &amp; Fantasy</td>
      <td>2015-05-15</td>
      <td>120.0</td>
      <td>97</td>
      <td>410</td>
      <td>85.0</td>
      <td>127428.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# highest rated popular movies by the audience
movies_popular.sort_values('audience_rating', ascending=False).head()
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
      <th>movie_title</th>
      <th>rating</th>
      <th>genre</th>
      <th>in_theaters_date</th>
      <th>runtime_in_minutes</th>
      <th>tomatometer_rating</th>
      <th>tomatometer_count</th>
      <th>audience_rating</th>
      <th>audience_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>16634</th>
      <td>Zootopia</td>
      <td>PG</td>
      <td>Action &amp; Adventure, Animation, Comedy</td>
      <td>2016-03-04</td>
      <td>108.0</td>
      <td>97</td>
      <td>279</td>
      <td>92.0</td>
      <td>100946.0</td>
    </tr>
    <tr>
      <th>6950</th>
      <td>Guardians of the Galaxy</td>
      <td>PG-13</td>
      <td>Action &amp; Adventure, Science Fiction &amp; Fantasy</td>
      <td>2014-08-01</td>
      <td>121.0</td>
      <td>91</td>
      <td>316</td>
      <td>92.0</td>
      <td>254717.0</td>
    </tr>
    <tr>
      <th>4077</th>
      <td>Captain America: The Winter Soldier</td>
      <td>PG-13</td>
      <td>Action &amp; Adventure, Science Fiction &amp; Fantasy</td>
      <td>2014-04-04</td>
      <td>136.0</td>
      <td>90</td>
      <td>292</td>
      <td>92.0</td>
      <td>281524.0</td>
    </tr>
    <tr>
      <th>14397</th>
      <td>The King's Speech</td>
      <td>PG-13</td>
      <td>Drama</td>
      <td>2010-11-26</td>
      <td>118.0</td>
      <td>95</td>
      <td>292</td>
      <td>92.0</td>
      <td>144306.0</td>
    </tr>
    <tr>
      <th>14549</th>
      <td>The Martian</td>
      <td>PG-13</td>
      <td>Science Fiction &amp; Fantasy</td>
      <td>2015-10-02</td>
      <td>164.0</td>
      <td>91</td>
      <td>361</td>
      <td>91.0</td>
      <td>131093.0</td>
    </tr>
  </tbody>
</table>
</div>



A lot of these popular movies seem to have a PG or PG-13 rating.

*Use this popular movies data from now on*


```python
# number of movies that fall under each type of rating
movies_popular.rating.value_counts()
```




    rating
    PG-13    160
    R        100
    PG        51
    G          5
    Name: count, dtype: int64



What is the average audience rating for each movie rating type? Which rating type is most highly rated?


```python
# PG-13 movies - most highly rated
movies_popular.groupby('rating')['audience_rating'].mean()
```




    rating
    G        66.200000
    PG       66.823529
    PG-13    67.293750
    R        63.010000
    Name: audience_rating, dtype: float64



## 2. Create New Columns

Create a column in the DataFrame called 'Animation' and return a 1 if a movie is an 'Animation' movie and 0 otherwise. Do the same for *Action & Adventure* and *Comedy*.

*Hint: use np.where and str.contains*


```python
movies_popular.head()
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
      <th>movie_title</th>
      <th>rating</th>
      <th>genre</th>
      <th>in_theaters_date</th>
      <th>runtime_in_minutes</th>
      <th>tomatometer_rating</th>
      <th>tomatometer_count</th>
      <th>audience_rating</th>
      <th>audience_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Percy Jackson &amp; the Olympians: The Lightning T...</td>
      <td>PG</td>
      <td>Action &amp; Adventure, Comedy, Drama, Science Fic...</td>
      <td>2010-02-12</td>
      <td>83.0</td>
      <td>49</td>
      <td>144</td>
      <td>53.0</td>
      <td>254287.0</td>
    </tr>
    <tr>
      <th>248</th>
      <td>Tron Legacy</td>
      <td>PG</td>
      <td>Action &amp; Adventure, Science Fiction &amp; Fantasy</td>
      <td>2010-12-17</td>
      <td>125.0</td>
      <td>51</td>
      <td>239</td>
      <td>63.0</td>
      <td>171385.0</td>
    </tr>
    <tr>
      <th>265</th>
      <td>The Last Song</td>
      <td>PG</td>
      <td>Drama, Kids &amp; Family, Romance</td>
      <td>2010-03-31</td>
      <td>107.0</td>
      <td>20</td>
      <td>118</td>
      <td>66.0</td>
      <td>160777.0</td>
    </tr>
    <tr>
      <th>274</th>
      <td>Repo Men</td>
      <td>R</td>
      <td>Action &amp; Adventure, Science Fiction &amp; Fantasy</td>
      <td>2010-03-19</td>
      <td>119.0</td>
      <td>22</td>
      <td>151</td>
      <td>41.0</td>
      <td>100453.0</td>
    </tr>
    <tr>
      <th>284</th>
      <td>Predators</td>
      <td>R</td>
      <td>Action &amp; Adventure, Horror, Science Fiction &amp; ...</td>
      <td>2010-07-09</td>
      <td>107.0</td>
      <td>65</td>
      <td>198</td>
      <td>52.0</td>
      <td>159760.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
import numpy as np

movies_popular['Animation'] = np.where(movies_popular.genre.str.contains('Animation'), 1, 0)
```

    C:\Users\ALKAPODDAR\AppData\Local\Temp\ipykernel_23820\1899839453.py:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      movies_popular['Animation'] = np.where(movies_popular.genre.str.contains('Animation'), 1, 0)
    


```python
# note: copied the movie to avoid warning
movies_popular = movies[movies.audience_count > 100000].copy()
```


```python
movies_popular['Animation'] = np.where(movies_popular.genre.str.contains('Animation'), 1, 0)
```


```python
movies_popular['Action & Adventure'] = np.where(movies_popular.genre.str.contains('Action & Adventure'), 1, 0)
```


```python
movies_popular['Comedy'] = np.where(movies_popular.genre.str.contains('Comedy'), 1, 0)
```

Create table - each row is a rating, each column is a genre and each value is the number of movies of that particular rating and genre for insights.


```python
movies_popular.groupby('rating')[['Animation', 'Action & Adventure', 'Comedy']].sum()
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
      <th>Animation</th>
      <th>Action &amp; Adventure</th>
      <th>Comedy</th>
    </tr>
    <tr>
      <th>rating</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>G</th>
      <td>5</td>
      <td>3</td>
      <td>5</td>
    </tr>
    <tr>
      <th>PG</th>
      <td>26</td>
      <td>27</td>
      <td>29</td>
    </tr>
    <tr>
      <th>PG-13</th>
      <td>0</td>
      <td>102</td>
      <td>35</td>
    </tr>
    <tr>
      <th>R</th>
      <td>0</td>
      <td>41</td>
      <td>35</td>
    </tr>
  </tbody>
</table>
</div>



Find the average critic and audience rating for an Animation movie vs a non-Animation movie. Do the same for Action & Adventure and Comedy. What insights do you gather?


```python
# both critics and the general audience love animated movies
movies_popular.groupby('Animation')[['tomatometer_rating', 'audience_rating']].mean()
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
      <th>tomatometer_rating</th>
      <th>audience_rating</th>
    </tr>
    <tr>
      <th>Animation</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>58.340351</td>
      <td>64.831579</td>
    </tr>
    <tr>
      <th>1</th>
      <td>75.258065</td>
      <td>75.161290</td>
    </tr>
  </tbody>
</table>
</div>




```python
# the general audience likes action movies more than critics
movies_popular.groupby('Action & Adventure')[['tomatometer_rating', 'audience_rating']].mean()
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
      <th>tomatometer_rating</th>
      <th>audience_rating</th>
    </tr>
    <tr>
      <th>Action &amp; Adventure</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>59.111888</td>
      <td>65.391608</td>
    </tr>
    <tr>
      <th>1</th>
      <td>60.734104</td>
      <td>66.219653</td>
    </tr>
  </tbody>
</table>
</div>




```python
# comedies have lower ratings than other genres
movies_popular.groupby('Comedy')[['tomatometer_rating', 'audience_rating']].mean()
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
      <th>tomatometer_rating</th>
      <th>audience_rating</th>
    </tr>
    <tr>
      <th>Comedy</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>62.169811</td>
      <td>67.353774</td>
    </tr>
    <tr>
      <th>1</th>
      <td>55.576923</td>
      <td>62.769231</td>
    </tr>
  </tbody>
</table>
</div>



## 3. Visualize the Data

Create a pair plot from the popular movies DataFrame.


```python
import seaborn as sns
```


```python
sns.pairplot(movies_popular);
```


    
![png](output_42_0.png)
    



```python
# excluding - newly created columns
sns.pairplot(movies_popular.iloc[:, :-3]);
```


    
![png](output_43_0.png)
    


What insights can you gather from the pair plot?
* How do the critic ratings (tomatometer_rating) compare with the audience ratings (compare the histograms)?
* What are some surprising findings about the run times of movies compared with other fields (look at the scatter plots)?
* What is the most popular movie by far in terms of the number of audience ratings?


```python
# Insights:
# critics give harsher reviews - there are quite a few low ratings in the tomatometer histogram
# the run time of movies seems to be correlated with the no. of critic ratings
# the most popular movie is 'Shutter Island' with lots of audience ratings and not as many critic ratings
# (this is so extreme that it could potentially be an outlier or error)
```


```python
movies_popular[movies_popular.audience_count > 1000000]
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
      <th>movie_title</th>
      <th>rating</th>
      <th>genre</th>
      <th>in_theaters_date</th>
      <th>runtime_in_minutes</th>
      <th>tomatometer_rating</th>
      <th>tomatometer_count</th>
      <th>audience_rating</th>
      <th>audience_count</th>
      <th>Animation</th>
      <th>Action &amp; Adventure</th>
      <th>Comedy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1646</th>
      <td>Shutter Island</td>
      <td>R</td>
      <td>Action &amp; Adventure, Drama, Mystery &amp; Suspense</td>
      <td>2010-02-19</td>
      <td>138.0</td>
      <td>68</td>
      <td>253</td>
      <td>76.0</td>
      <td>2373625.0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>9581</th>
      <td>Marvel's The Avengers</td>
      <td>PG-13</td>
      <td>Action &amp; Adventure, Science Fiction &amp; Fantasy</td>
      <td>2012-05-04</td>
      <td>142.0</td>
      <td>92</td>
      <td>348</td>
      <td>91.0</td>
      <td>1134955.0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>13936</th>
      <td>The Dark Knight Rises</td>
      <td>PG-13</td>
      <td>Action &amp; Adventure, Drama, Mystery &amp; Suspense</td>
      <td>2012-07-20</td>
      <td>165.0</td>
      <td>87</td>
      <td>360</td>
      <td>90.0</td>
      <td>1210957.0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
