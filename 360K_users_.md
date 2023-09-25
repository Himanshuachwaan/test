```python
import numpy as np
import pandas as pd

#display results to 3 decimal points, not in scientific notations
pd.set_option('display.float_format', lambda x: '%.3f' % x)
```


```python
#load dataset 
user_data = pd.read_table('D:/usersha1-artmbid-artname-plays.tsv', header = None, nrows = 2e7, names =['users', 'musicbrainz-artist-id', 'artist-name', 'plays'], usecols = ['users', 'artist-name', 'plays'] )
user_profile = pd.read_table('D:/usersha1-profile.tsv', header = None, names = ['users', 'gender', 'age', 'country', 'signup'], usecols = ['users', 'country'])
```


```python
#display first few rows
user_data.head()
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
      <th>users</th>
      <th>artist-name</th>
      <th>plays</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>betty blowtorch</td>
      <td>2137</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>die Ärzte</td>
      <td>1099</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>melissa etheridge</td>
      <td>897</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>elvenking</td>
      <td>717</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>juliette &amp; the licks</td>
      <td>706</td>
    </tr>
  </tbody>
</table>
</div>




```python
user_profile.head()
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
      <th>users</th>
      <th>country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00001411dc427966b17297bf4d69e7e193135d89</td>
      <td>Canada</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00004d2ac9316e22dc007ab2243d6fcb239e707d</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>3</th>
      <td>000063d3fe1cf2ba248b9e3c3f0334845a27a6bf</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00007a47085b9aab8af55f52ec8846ac479ac4fe</td>
      <td>United States</td>
    </tr>
  </tbody>
</table>
</div>




```python
#to get only null values in artist-name but complete dataset
user_data[user_data['artist-name'].isnull()]
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
      <th>users</th>
      <th>artist-name</th>
      <th>plays</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>244853</th>
      <td>039e5d61d65bbf5e6d95b07b1b3b67f7fd287a62</td>
      <td>NaN</td>
      <td>18</td>
    </tr>
    <tr>
      <th>431015</th>
      <td>065a001be5a8a55971042077933e263d0d5cde46</td>
      <td>NaN</td>
      <td>186</td>
    </tr>
    <tr>
      <th>455721</th>
      <td>06b17c50402d06a497cb13a0375992fd1e90b392</td>
      <td>NaN</td>
      <td>3</td>
    </tr>
    <tr>
      <th>504026</th>
      <td>0757ac29973aab69bb31cd164c6df975bf4df9a1</td>
      <td>NaN</td>
      <td>38</td>
    </tr>
    <tr>
      <th>607282</th>
      <td>08e102b376abe856a3d4be5ea14ad6b37395fe82</td>
      <td>NaN</td>
      <td>208</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>17227026</th>
      <td>fb7aec57827b2bd6152b84ef2034bc5aa023fe89</td>
      <td>NaN</td>
      <td>13</td>
    </tr>
    <tr>
      <th>17306503</th>
      <td>fcaa2f605a2c6d2cd21942a20f80c7e1c14e1818</td>
      <td>NaN</td>
      <td>5</td>
    </tr>
    <tr>
      <th>17404362</th>
      <td>fe1503af166a337f6a572da66b99b4cd0da362b2</td>
      <td>NaN</td>
      <td>62</td>
    </tr>
    <tr>
      <th>17429832</th>
      <td>fe72cbf58e485fab12211834244ff8dbf314b590</td>
      <td>NaN</td>
      <td>63</td>
    </tr>
    <tr>
      <th>17480740</th>
      <td>ff2cb5365215e7bf4a64e7bee1f6c9b83a33609b</td>
      <td>NaN</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
<p>204 rows × 3 columns</p>
</div>




```python
""" to drop the rows which have null value in artist-name column, we check using isnull i.e. true or false
and .sum() converts true to 1 and false to 0 after it using dropna and putting the axis = 0, it drops every row where axis is 1
specifying column name in subset, in which we need to check null values"""
if user_data['artist-name'].isnull().sum() > 0:
    user_data = user_data.dropna(axis = 0, subset = ['artist-name'])
```


```python
user_data[user_data['artist-name'].isnull()]
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
      <th>users</th>
      <th>artist-name</th>
      <th>plays</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
"""use groupby to get sum of plays .sum and reset it after using reset_index(), 
rename to rename column, double brackets to get specified columns"""
artist_plays = (user_data.groupby(by=['artist-name'])['plays'].sum().reset_index().rename(columns = {'plays':'total_artist_plays'})[['artist-name', 'total_artist_plays']])
artist_plays.head()
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
      <th>artist-name</th>
      <th>total_artist_plays</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>04)]</td>
      <td>6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1606</td>
    </tr>
    <tr>
      <th>2</th>
      <td>58725ab=&gt;</td>
      <td>23</td>
    </tr>
    <tr>
      <th>3</th>
      <td>80lİ yillarin tÜrkÇe sÖzlÜ aŞk Şarkilari</td>
      <td>70</td>
    </tr>
    <tr>
      <th>4</th>
      <td>amy winehouse</td>
      <td>23</td>
    </tr>
  </tbody>
</table>
</div>




```python
#merge two tables
user_data_with_artist_plays = user_data.merge(artist_plays, on = 'artist-name', how = 'left')
user_data_with_artist_plays.head()

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
      <th>users</th>
      <th>artist-name</th>
      <th>plays</th>
      <th>total_artist_plays</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>betty blowtorch</td>
      <td>2137</td>
      <td>25651</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>die Ärzte</td>
      <td>1099</td>
      <td>3704875</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>melissa etheridge</td>
      <td>897</td>
      <td>180391</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>elvenking</td>
      <td>717</td>
      <td>410725</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>juliette &amp; the licks</td>
      <td>706</td>
      <td>90498</td>
    </tr>
  </tbody>
</table>
</div>




```python
#stats, only used in columns with numerical values
artist_plays['total_artist_plays'].describe()
```




    count     292363.000
    mean       12907.022
    std       185981.631
    min            1.000
    25%           53.000
    50%          208.000
    75%         1048.000
    max     30466827.000
    Name: total_artist_plays, dtype: float64




```python
artist_plays['total_artist_plays'].max()
```




    30466827




```python
artist_plays[artist_plays['total_artist_plays'] == artist_plays['total_artist_plays'].max()]
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
      <th>artist-name</th>
      <th>total_artist_plays</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>252494</th>
      <td>the beatles</td>
      <td>30466827</td>
    </tr>
  </tbody>
</table>
</div>




```python
# use quantile function to represent data distribution
artist_plays['total_artist_plays'].quantile(np.arange(.9, 1, .01))
```




    0.900     6137.800
    0.910     7409.420
    0.920     9102.040
    0.930    11474.660
    0.940    14898.000
    0.950    19964.500
    0.960    28420.120
    0.970    43541.420
    0.980    79403.560
    0.990   198483.660
    Name: total_artist_plays, dtype: float64




```python
# to count values
artist_plays['total_artist_plays'].value_counts()
```




    total_artist_plays
    1        2816
    2        2724
    3        2365
    4        2211
    5        2123
             ... 
    13635       1
    36958       1
    47740       1
    13197       1
    28195       1
    Name: count, Length: 28112, dtype: int64




```python
#Taking only top artists(where no of plays are more)
popularity_threshold = 40000
user_data_popular_artists = user_data_with_artist_plays.query('total_artist_plays >= @popularity_threshold')
user_data_popular_artists.head()
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
      <th>users</th>
      <th>artist-name</th>
      <th>plays</th>
      <th>total_artist_plays</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>die Ärzte</td>
      <td>1099</td>
      <td>3704875</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>melissa etheridge</td>
      <td>897</td>
      <td>180391</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>elvenking</td>
      <td>717</td>
      <td>410725</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>juliette &amp; the licks</td>
      <td>706</td>
      <td>90498</td>
    </tr>
    <tr>
      <th>5</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>red hot chili peppers</td>
      <td>691</td>
      <td>13547741</td>
    </tr>
  </tbody>
</table>
</div>




```python
user_data_with_artist_plays.head()
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
      <th>users</th>
      <th>artist-name</th>
      <th>plays</th>
      <th>total_artist_plays</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>betty blowtorch</td>
      <td>2137</td>
      <td>25651</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>die Ärzte</td>
      <td>1099</td>
      <td>3704875</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>melissa etheridge</td>
      <td>897</td>
      <td>180391</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>elvenking</td>
      <td>717</td>
      <td>410725</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>juliette &amp; the licks</td>
      <td>706</td>
      <td>90498</td>
    </tr>
  </tbody>
</table>
</div>






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
      <th>users</th>
      <th>artist-name</th>
      <th>plays</th>
      <th>total_artist_plays</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>betty blowtorch</td>
      <td>2137</td>
      <td>25651</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>die Ärzte</td>
      <td>1099</td>
      <td>3704875</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>melissa etheridge</td>
      <td>897</td>
      <td>180391</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>elvenking</td>
      <td>717</td>
      <td>410725</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>juliette &amp; the licks</td>
      <td>706</td>
      <td>90498</td>
    </tr>
  </tbody>
</table>
</div>




```python
user_data_popular_artists.head(100)
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
      <th>users</th>
      <th>artist-name</th>
      <th>plays</th>
      <th>total_artist_plays</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>die Ärzte</td>
      <td>1099</td>
      <td>3704875</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>melissa etheridge</td>
      <td>897</td>
      <td>180391</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>elvenking</td>
      <td>717</td>
      <td>410725</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>juliette &amp; the licks</td>
      <td>706</td>
      <td>90498</td>
    </tr>
    <tr>
      <th>5</th>
      <td>00000c289a1829a808ac09c00daf10bc3c4e223b</td>
      <td>red hot chili peppers</td>
      <td>691</td>
      <td>13547741</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>110</th>
      <td>00004d2ac9316e22dc007ab2243d6fcb239e707d</td>
      <td>nick cave &amp; the bad seeds</td>
      <td>135</td>
      <td>592844</td>
    </tr>
    <tr>
      <th>115</th>
      <td>00004d2ac9316e22dc007ab2243d6fcb239e707d</td>
      <td>antony and the johnsons</td>
      <td>107</td>
      <td>1516288</td>
    </tr>
    <tr>
      <th>116</th>
      <td>00004d2ac9316e22dc007ab2243d6fcb239e707d</td>
      <td>marissa nadler</td>
      <td>107</td>
      <td>185751</td>
    </tr>
    <tr>
      <th>117</th>
      <td>00004d2ac9316e22dc007ab2243d6fcb239e707d</td>
      <td>a silver mt. zion</td>
      <td>106</td>
      <td>504328</td>
    </tr>
    <tr>
      <th>118</th>
      <td>00004d2ac9316e22dc007ab2243d6fcb239e707d</td>
      <td>einstürzende neubauten</td>
      <td>105</td>
      <td>1026492</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 4 columns</p>
</div>




```python
user_data_with_artist_plays.query('plays>40000')
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
      <th>users</th>
      <th>artist-name</th>
      <th>plays</th>
      <th>total_artist_plays</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>27358</th>
      <td>006261139d787c1e43b4c69d304f2772367c1005</td>
      <td>garbage</td>
      <td>62054</td>
      <td>2461628</td>
    </tr>
    <tr>
      <th>43276</th>
      <td>00a20b9791abd8b29903a8a43e343ae93a98d9fd</td>
      <td>lil wayne</td>
      <td>107758</td>
      <td>2432188</td>
    </tr>
    <tr>
      <th>166489</th>
      <td>0268c4ff8eba994c93fc0e49644bac7b49caa068</td>
      <td>mindless self indulgence</td>
      <td>43251</td>
      <td>3172270</td>
    </tr>
    <tr>
      <th>175680</th>
      <td>028b91859a012251da23c3dbfd2215154a789f9f</td>
      <td>afi</td>
      <td>59169</td>
      <td>3918876</td>
    </tr>
    <tr>
      <th>191656</th>
      <td>02ccf45baa7fe62f0935b8a6a64ff8869a7b0387</td>
      <td>christina aguilera</td>
      <td>135392</td>
      <td>2680164</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>17217137</th>
      <td>fb587892425d6ce7a939ddbd84ab337aeee172d9</td>
      <td>the used</td>
      <td>53008</td>
      <td>2861379</td>
    </tr>
    <tr>
      <th>17239960</th>
      <td>fbab9ccd006ea82729b527cdd9b1549a7314e5a6</td>
      <td>布袋寅泰</td>
      <td>47053</td>
      <td>79023</td>
    </tr>
    <tr>
      <th>17305007</th>
      <td>fca2614e3834feb94726f6334b4948d776a767a1</td>
      <td>oasis</td>
      <td>60618</td>
      <td>6348953</td>
    </tr>
    <tr>
      <th>17346197</th>
      <td>fd3baa3d1fc07a4e078f33773dbb1b27ae88c756</td>
      <td>chamillionaire</td>
      <td>57310</td>
      <td>813382</td>
    </tr>
    <tr>
      <th>17488566</th>
      <td>ff4b19c43528846b3c2cbdf5434fa8a3ea5875df</td>
      <td>kylie minogue</td>
      <td>96568</td>
      <td>3359413</td>
    </tr>
  </tbody>
</table>
<p>313 rows × 4 columns</p>
</div>




```python
# use query to filter and merge a pd function
combined = user_data_popular_artists.merge(user_profile, on = 'users', how = 'left')
usa_data = combined.query('country == "United States"')
usa_data.head()
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
      <th>users</th>
      <th>artist-name</th>
      <th>plays</th>
      <th>total_artist_plays</th>
      <th>country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>156</th>
      <td>00007a47085b9aab8af55f52ec8846ac479ac4fe</td>
      <td>devendra banhart</td>
      <td>456</td>
      <td>2366807</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>157</th>
      <td>00007a47085b9aab8af55f52ec8846ac479ac4fe</td>
      <td>boards of canada</td>
      <td>407</td>
      <td>6115545</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>158</th>
      <td>00007a47085b9aab8af55f52ec8846ac479ac4fe</td>
      <td>cocorosie</td>
      <td>386</td>
      <td>2194862</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>159</th>
      <td>00007a47085b9aab8af55f52ec8846ac479ac4fe</td>
      <td>aphex twin</td>
      <td>213</td>
      <td>4248296</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>160</th>
      <td>00007a47085b9aab8af55f52ec8846ac479ac4fe</td>
      <td>animal collective</td>
      <td>203</td>
      <td>3495537</td>
      <td>United States</td>
    </tr>
  </tbody>
</table>
</div>




```python
combined.query('plays>100000')
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
      <th>users</th>
      <th>artist-name</th>
      <th>plays</th>
      <th>total_artist_plays</th>
      <th>country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34568</th>
      <td>00a20b9791abd8b29903a8a43e343ae93a98d9fd</td>
      <td>lil wayne</td>
      <td>107758</td>
      <td>2432188</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>155324</th>
      <td>02ccf45baa7fe62f0935b8a6a64ff8869a7b0387</td>
      <td>christina aguilera</td>
      <td>135392</td>
      <td>2680164</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <th>542544</th>
      <td>09d12dfa05a0852053a9017121034a837fa4019e</td>
      <td>alice cooper</td>
      <td>134993</td>
      <td>1542185</td>
      <td>United Kingdom</td>
    </tr>
    <tr>
      <th>617078</th>
      <td>0b2956b319a3ac466b0cf1a8c49fa73498d0898c</td>
      <td>in flames</td>
      <td>112989</td>
      <td>11288367</td>
      <td>Russian Federation</td>
    </tr>
    <tr>
      <th>1159053</th>
      <td>14ea4c6f3c2e86b4937f1158bd13d3173d780bd7</td>
      <td>dean martin</td>
      <td>288375</td>
      <td>655025</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>1298741</th>
      <td>177653480857c3bb69b9a71b4f7166b7cd62129c</td>
      <td>rush</td>
      <td>100846</td>
      <td>2518951</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>1353498</th>
      <td>1872585e74857e4888dfa63bd1186d210aae7681</td>
      <td>tokio hotel</td>
      <td>141661</td>
      <td>952834</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>1821162</th>
      <td>20d54d757ff07da456dfaa26e9077f5fa12fe71a</td>
      <td>marilyn manson</td>
      <td>111455</td>
      <td>6417868</td>
      <td>Poland</td>
    </tr>
    <tr>
      <th>1914297</th>
      <td>228eb001a7ad5408dce7d40859e5935081518ff1</td>
      <td>the rasmus</td>
      <td>100080</td>
      <td>1156417</td>
      <td>Russian Federation</td>
    </tr>
    <tr>
      <th>2170271</th>
      <td>274f8ab91b73503c3a18cb5c230affa56e0a677d</td>
      <td>u2</td>
      <td>116025</td>
      <td>8111215</td>
      <td>France</td>
    </tr>
    <tr>
      <th>2264157</th>
      <td>28f4de1761a599cf2b689bc6610d3d40a62caadd</td>
      <td>lil wayne</td>
      <td>113961</td>
      <td>2432188</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>2324291</th>
      <td>2a088c171293674c39d0e02f495c6f91362357b0</td>
      <td>enrique iglesias</td>
      <td>232650</td>
      <td>1069095</td>
      <td>New Zealand</td>
    </tr>
    <tr>
      <th>2507156</th>
      <td>2d5669ab469c8399e07e8ae34918e6309d574aad</td>
      <td>동방신기</td>
      <td>114386</td>
      <td>1170927</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>2852693</th>
      <td>33b19ba7b795dd6abd8cb4e0ec9d27456f4a4044</td>
      <td>t.a.t.u.</td>
      <td>186028</td>
      <td>1818384</td>
      <td>Finland</td>
    </tr>
    <tr>
      <th>3001148</th>
      <td>366c0b8cf44374df47d874b16f8a81e12c157c1f</td>
      <td>britney spears</td>
      <td>157737</td>
      <td>7465258</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <th>3498971</th>
      <td>3f40dad7b10658c66c1de6d560c92ae2a7ccacbb</td>
      <td>madonna</td>
      <td>109232</td>
      <td>7633843</td>
      <td>Bulgaria</td>
    </tr>
    <tr>
      <th>4166200</th>
      <td>4b79df05a80b733e6422e52e5d1f25b50cd3aadb</td>
      <td>dir en grey</td>
      <td>270122</td>
      <td>2814331</td>
      <td>Japan</td>
    </tr>
    <tr>
      <th>4330180</th>
      <td>4e773f3f8e3f74fa23836ede43d8364dd8b4062d</td>
      <td>mary j. blige</td>
      <td>192749</td>
      <td>950017</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>4638643</th>
      <td>54027330bb09fe82d2b7e85749d4041eab3d5e4e</td>
      <td>the pillows</td>
      <td>129630</td>
      <td>1533376</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>5337679</th>
      <td>609d4e3aa03afeefa282d873d3abe7c484e21225</td>
      <td>shakira</td>
      <td>113204</td>
      <td>1641903</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>5443486</th>
      <td>6279d62ad11b724950845a026b0d4a70aec5b5e0</td>
      <td>30 seconds to mars</td>
      <td>104493</td>
      <td>3317407</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <th>5677810</th>
      <td>66b94d3bff0458037b7c85650331a10727833a58</td>
      <td>hans zimmer</td>
      <td>173163</td>
      <td>2450338</td>
      <td>Slovakia</td>
    </tr>
    <tr>
      <th>6151014</th>
      <td>6f460e97cc8512f300004ec6c697c2216ec6c28f</td>
      <td>hide</td>
      <td>102235</td>
      <td>468424</td>
      <td>Japan</td>
    </tr>
    <tr>
      <th>6938460</th>
      <td>7d8b040d3226b187b8a1a95ac1527f395373b51f</td>
      <td>clutch</td>
      <td>180785</td>
      <td>1124251</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>7357696</th>
      <td>8519545b80b95da502233743fa9bd1ff941ab13f</td>
      <td>frank sinatra</td>
      <td>155482</td>
      <td>2873146</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>7729721</th>
      <td>8bc02e7e4842b0a3c33a17149ea1ea5b37be6273</td>
      <td>kylie minogue</td>
      <td>102921</td>
      <td>3359413</td>
      <td>Saudi Arabia</td>
    </tr>
    <tr>
      <th>7798019</th>
      <td>8d0384537845e7f2b1b8b3e8a9f67eb8d9439794</td>
      <td>nofx</td>
      <td>419157</td>
      <td>5025614</td>
      <td>Austria</td>
    </tr>
    <tr>
      <th>8111123</th>
      <td>92aa9c188586c2e57dfa76326ee8b8bdd62dd426</td>
      <td>bruce springsteen &amp; the e street band</td>
      <td>139187</td>
      <td>308535</td>
      <td>United Kingdom</td>
    </tr>
    <tr>
      <th>8783645</th>
      <td>9ed77196358c5a9aeff4543e43e11d6bf6d02d34</td>
      <td>2pac</td>
      <td>140801</td>
      <td>3113303</td>
      <td>Poland</td>
    </tr>
    <tr>
      <th>9590714</th>
      <td>ada8a9ac4f6ea943e6ed858e8f194947181e03d7</td>
      <td>mary j. blige</td>
      <td>147770</td>
      <td>950017</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>10197619</th>
      <td>b88d16f3ebdad0bf701ecd46cf4725ea31911849</td>
      <td>the smiths</td>
      <td>272359</td>
      <td>6408722</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <th>10197620</th>
      <td>b88d16f3ebdad0bf701ecd46cf4725ea31911849</td>
      <td>morrissey</td>
      <td>101509</td>
      <td>3338687</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <th>10326013</th>
      <td>baee6143fb184f2014f05c737c28cd57d6d0486f</td>
      <td>madonna</td>
      <td>242328</td>
      <td>7633843</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <th>10809771</th>
      <td>c3a03caf33ae7818d8e7783c4575bc63a594181b</td>
      <td>the smashing pumpkins</td>
      <td>112415</td>
      <td>7172332</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <th>10856851</th>
      <td>c46c9683e1ac940b53b8ea52ac27ce160fade9a2</td>
      <td>regina spektor</td>
      <td>144827</td>
      <td>4327113</td>
      <td>Canada</td>
    </tr>
    <tr>
      <th>10974450</th>
      <td>c6888d7be46acf6deab52f7bc2bd5900a1b216ba</td>
      <td>radiohead</td>
      <td>106639</td>
      <td>27426234</td>
      <td>Russian Federation</td>
    </tr>
    <tr>
      <th>11535253</th>
      <td>d09386fb62a50ae6d4daad5a17fecbf07faad701</td>
      <td>coldplay</td>
      <td>101459</td>
      <td>16686772</td>
      <td>France</td>
    </tr>
    <tr>
      <th>11554368</th>
      <td>d0e63bd9ecdde014b0a389fe8ffeecc305428ad2</td>
      <td>coldplay</td>
      <td>118857</td>
      <td>16686772</td>
      <td>Italy</td>
    </tr>
    <tr>
      <th>11614507</th>
      <td>d1f816fb11d62d24dd9a3babe4bb2e49b5444bbc</td>
      <td>nirvana</td>
      <td>136695</td>
      <td>9276637</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <th>11825607</th>
      <td>d5c1fe51720f69baae1281e09efbc9080d7c304f</td>
      <td>nightwish</td>
      <td>179843</td>
      <td>9754161</td>
      <td>Russian Federation</td>
    </tr>
    <tr>
      <th>12214252</th>
      <td>dcce20638cf6b541dfebd820df1146abe4bf1e86</td>
      <td>live</td>
      <td>107209</td>
      <td>908119</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>13391354</th>
      <td>f21bd3764c6ee7968a8a5102f2076dc029b4525f</td>
      <td>fey</td>
      <td>194868</td>
      <td>306296</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <th>13413034</th>
      <td>f27c8d76cf15dd6e79fec7affb684804475292de</td>
      <td>a*teens</td>
      <td>219355</td>
      <td>397773</td>
      <td>Chile</td>
    </tr>
    <tr>
      <th>13573418</th>
      <td>f55928c81b10964f51f4cf12ffdd8c6f5b27f356</td>
      <td>enigma</td>
      <td>124501</td>
      <td>2581103</td>
      <td>Poland</td>
    </tr>
    <tr>
      <th>13671953</th>
      <td>f714eaff944bdf422df2a42354d31c40a0e73240</td>
      <td>belle and sebastian</td>
      <td>170096</td>
      <td>6129314</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>13894169</th>
      <td>fb30d581e1ddf82812e7bdfae7a7d965a6cf54bc</td>
      <td>marilyn manson</td>
      <td>110098</td>
      <td>6417868</td>
      <td>United States</td>
    </tr>
  </tbody>
</table>
</div>




```python
#.shape to get rows and columns count
initial_rows = usa_data.shape[0]
print('Initial Dataframe Shape {0}'.format(usa_data.shape))
#use drop_duplicates to drop down rows having duplicate values
usa_data = usa_data.drop_duplicates(['users', 'artist-name'])
current_rows = usa_data.shape[0]
print('New Dataframe Shape {0}'.format(usa_data.shape))
print('Removed {0} Rows'.format(initial_rows - current_rows))
```

    Initial Dataframe Shape (2788019, 5)
    New Dataframe Shape (2788013, 5)
    Removed 6 Rows
    


```python
pip install scipy
```

    Collecting scipy
      Obtaining dependency information for scipy from https://files.pythonhosted.org/packages/06/15/e73734f9170b66c6a84a0bd7e03586e87e77404e2eb8e34749fc49fa43f7/scipy-1.11.2-cp311-cp311-win_amd64.whl.metadata
      Downloading scipy-1.11.2-cp311-cp311-win_amd64.whl.metadata (59 kB)
         ---------------------------------------- 0.0/59.1 kB ? eta -:--:--
         ------ --------------------------------- 10.2/59.1 kB ? eta -:--:--
         ------ --------------------------------- 10.2/59.1 kB ? eta -:--:--
         ------------- ------------------------ 20.5/59.1 kB 108.9 kB/s eta 0:00:01
         -------------------------- ----------- 41.0/59.1 kB 163.4 kB/s eta 0:00:01
         -------------------------------- ----- 51.2/59.1 kB 201.8 kB/s eta 0:00:01
         -------------------------------------- 59.1/59.1 kB 183.7 kB/s eta 0:00:00
    Requirement already satisfied: numpy<1.28.0,>=1.21.6 in c:\users\himan\anaconda3\envs\pyspark-env\lib\site-packages (from scipy) (1.25.2)
    Downloading scipy-1.11.2-cp311-cp311-win_amd64.whl (44.0 MB)
       ---------------------------------------- 0.0/44.0 MB ? eta -:--:--
       ---------------------------------------- 0.1/44.0 MB 3.4 MB/s eta 0:00:13
       ---------------------------------------- 0.2/44.0 MB 3.0 MB/s eta 0:00:15
       ---------------------------------------- 0.2/44.0 MB 2.0 MB/s eta 0:00:23
       ---------------------------------------- 0.3/44.0 MB 2.1 MB/s eta 0:00:21
       ---------------------------------------- 0.5/44.0 MB 2.6 MB/s eta 0:00:17
        --------------------------------------- 0.8/44.0 MB 3.3 MB/s eta 0:00:13
        --------------------------------------- 1.0/44.0 MB 3.5 MB/s eta 0:00:13
       - -------------------------------------- 1.3/44.0 MB 4.0 MB/s eta 0:00:11
       - -------------------------------------- 1.6/44.0 MB 4.4 MB/s eta 0:00:10
       - -------------------------------------- 1.8/44.0 MB 4.4 MB/s eta 0:00:10
       - -------------------------------------- 2.1/44.0 MB 4.5 MB/s eta 0:00:10
       -- ------------------------------------- 2.8/44.0 MB 5.5 MB/s eta 0:00:08
       -- ------------------------------------- 3.1/44.0 MB 5.7 MB/s eta 0:00:08
       --- ------------------------------------ 3.3/44.0 MB 5.7 MB/s eta 0:00:08
       --- ------------------------------------ 3.6/44.0 MB 5.9 MB/s eta 0:00:07
       --- ------------------------------------ 3.8/44.0 MB 6.0 MB/s eta 0:00:07
       --- ------------------------------------ 4.1/44.0 MB 5.8 MB/s eta 0:00:07
       --- ------------------------------------ 4.3/44.0 MB 5.8 MB/s eta 0:00:07
       ---- ----------------------------------- 4.6/44.0 MB 5.9 MB/s eta 0:00:07
       ---- ----------------------------------- 5.0/44.0 MB 6.1 MB/s eta 0:00:07
       ---- ----------------------------------- 5.4/44.0 MB 6.1 MB/s eta 0:00:07
       ----- ---------------------------------- 5.7/44.0 MB 6.3 MB/s eta 0:00:07
       ----- ---------------------------------- 6.0/44.0 MB 6.2 MB/s eta 0:00:07
       ----- ---------------------------------- 6.4/44.0 MB 6.2 MB/s eta 0:00:07
       ------ --------------------------------- 6.7/44.0 MB 6.3 MB/s eta 0:00:06
       ------ --------------------------------- 6.9/44.0 MB 6.3 MB/s eta 0:00:06
       ------ --------------------------------- 6.9/44.0 MB 6.2 MB/s eta 0:00:06
       ------ --------------------------------- 7.2/44.0 MB 6.0 MB/s eta 0:00:07
       ------ --------------------------------- 7.5/44.0 MB 6.0 MB/s eta 0:00:07
       ------- -------------------------------- 7.9/44.0 MB 6.2 MB/s eta 0:00:06
       ------- -------------------------------- 8.2/44.0 MB 6.3 MB/s eta 0:00:06
       ------- -------------------------------- 8.5/44.0 MB 6.3 MB/s eta 0:00:06
       ------- -------------------------------- 8.7/44.0 MB 6.2 MB/s eta 0:00:06
       -------- ------------------------------- 9.0/44.0 MB 6.2 MB/s eta 0:00:06
       -------- ------------------------------- 9.3/44.0 MB 6.3 MB/s eta 0:00:06
       -------- ------------------------------- 9.6/44.0 MB 6.4 MB/s eta 0:00:06
       --------- ------------------------------ 10.0/44.0 MB 6.4 MB/s eta 0:00:06
       --------- ------------------------------ 10.4/44.0 MB 6.6 MB/s eta 0:00:06
       --------- ------------------------------ 10.7/44.0 MB 7.0 MB/s eta 0:00:05
       --------- ------------------------------ 11.0/44.0 MB 7.0 MB/s eta 0:00:05
       ---------- ----------------------------- 11.2/44.0 MB 7.1 MB/s eta 0:00:05
       ---------- ----------------------------- 11.3/44.0 MB 7.0 MB/s eta 0:00:05
       ---------- ----------------------------- 11.6/44.0 MB 7.0 MB/s eta 0:00:05
       ---------- ----------------------------- 11.9/44.0 MB 6.9 MB/s eta 0:00:05
       ----------- ---------------------------- 12.3/44.0 MB 7.0 MB/s eta 0:00:05
       ----------- ---------------------------- 12.6/44.0 MB 6.9 MB/s eta 0:00:05
       ----------- ---------------------------- 12.8/44.0 MB 6.7 MB/s eta 0:00:05
       ------------ --------------------------- 13.2/44.0 MB 6.7 MB/s eta 0:00:05
       ------------ --------------------------- 13.4/44.0 MB 6.6 MB/s eta 0:00:05
       ------------ --------------------------- 13.6/44.0 MB 6.5 MB/s eta 0:00:05
       ------------ --------------------------- 13.6/44.0 MB 6.3 MB/s eta 0:00:05
       ------------ --------------------------- 13.9/44.0 MB 6.4 MB/s eta 0:00:05
       ------------ --------------------------- 14.1/44.0 MB 6.5 MB/s eta 0:00:05
       ------------ --------------------------- 14.3/44.0 MB 6.3 MB/s eta 0:00:05
       ------------- -------------------------- 14.8/44.0 MB 6.4 MB/s eta 0:00:05
       ------------- -------------------------- 15.2/44.0 MB 6.4 MB/s eta 0:00:05
       -------------- ------------------------- 15.6/44.0 MB 6.4 MB/s eta 0:00:05
       -------------- ------------------------- 15.8/44.0 MB 6.4 MB/s eta 0:00:05
       -------------- ------------------------- 16.3/44.0 MB 6.5 MB/s eta 0:00:05
       --------------- ------------------------ 16.6/44.0 MB 6.4 MB/s eta 0:00:05
       --------------- ------------------------ 16.9/44.0 MB 6.4 MB/s eta 0:00:05
       --------------- ------------------------ 17.1/44.0 MB 6.4 MB/s eta 0:00:05
       --------------- ------------------------ 17.2/44.0 MB 6.4 MB/s eta 0:00:05
       --------------- ------------------------ 17.4/44.0 MB 6.2 MB/s eta 0:00:05
       ---------------- ----------------------- 17.6/44.0 MB 6.2 MB/s eta 0:00:05
       ---------------- ----------------------- 17.8/44.0 MB 6.2 MB/s eta 0:00:05
       ---------------- ----------------------- 18.0/44.0 MB 6.1 MB/s eta 0:00:05
       ---------------- ----------------------- 18.2/44.0 MB 6.0 MB/s eta 0:00:05
       ---------------- ----------------------- 18.2/44.0 MB 6.0 MB/s eta 0:00:05
       ---------------- ----------------------- 18.2/44.0 MB 6.0 MB/s eta 0:00:05
       ---------------- ----------------------- 18.4/44.0 MB 5.5 MB/s eta 0:00:05
       ---------------- ----------------------- 18.4/44.0 MB 5.4 MB/s eta 0:00:05
       ----------------- ---------------------- 18.7/44.0 MB 5.4 MB/s eta 0:00:05
       ----------------- ---------------------- 18.9/44.0 MB 5.4 MB/s eta 0:00:05
       ----------------- ---------------------- 19.1/44.0 MB 5.4 MB/s eta 0:00:05
       ----------------- ---------------------- 19.3/44.0 MB 5.3 MB/s eta 0:00:05
       ----------------- ---------------------- 19.4/44.0 MB 5.2 MB/s eta 0:00:05
       ----------------- ---------------------- 19.6/44.0 MB 5.2 MB/s eta 0:00:05
       ----------------- ---------------------- 19.7/44.0 MB 5.2 MB/s eta 0:00:05
       ------------------ --------------------- 19.9/44.0 MB 5.1 MB/s eta 0:00:05
       ------------------ --------------------- 20.1/44.0 MB 5.0 MB/s eta 0:00:05
       ------------------ --------------------- 20.4/44.0 MB 5.0 MB/s eta 0:00:05
       ------------------ --------------------- 20.6/44.0 MB 5.0 MB/s eta 0:00:05
       ------------------ --------------------- 20.6/44.0 MB 4.9 MB/s eta 0:00:05
       ------------------ --------------------- 20.8/44.0 MB 4.8 MB/s eta 0:00:05
       ------------------- -------------------- 21.1/44.0 MB 4.9 MB/s eta 0:00:05
       ------------------- -------------------- 21.4/44.0 MB 4.9 MB/s eta 0:00:05
       ------------------- -------------------- 21.6/44.0 MB 4.8 MB/s eta 0:00:05
       ------------------- -------------------- 21.8/44.0 MB 4.8 MB/s eta 0:00:05
       ------------------- -------------------- 21.9/44.0 MB 4.8 MB/s eta 0:00:05
       ------------------- -------------------- 22.0/44.0 MB 4.7 MB/s eta 0:00:05
       -------------------- ------------------- 22.1/44.0 MB 4.6 MB/s eta 0:00:05
       -------------------- ------------------- 22.3/44.0 MB 4.6 MB/s eta 0:00:05
       -------------------- ------------------- 22.3/44.0 MB 4.6 MB/s eta 0:00:05
       -------------------- ------------------- 22.3/44.0 MB 4.6 MB/s eta 0:00:05
       -------------------- ------------------- 22.5/44.0 MB 4.4 MB/s eta 0:00:05
       -------------------- ------------------- 22.6/44.0 MB 4.4 MB/s eta 0:00:05
       -------------------- ------------------- 22.9/44.0 MB 4.4 MB/s eta 0:00:05
       --------------------- ------------------ 23.3/44.0 MB 4.4 MB/s eta 0:00:05
       --------------------- ------------------ 23.6/44.0 MB 4.4 MB/s eta 0:00:05
       --------------------- ------------------ 23.8/44.0 MB 4.4 MB/s eta 0:00:05
       --------------------- ------------------ 23.9/44.0 MB 4.5 MB/s eta 0:00:05
       --------------------- ------------------ 24.0/44.0 MB 4.5 MB/s eta 0:00:05
       --------------------- ------------------ 24.0/44.0 MB 4.5 MB/s eta 0:00:05
       --------------------- ------------------ 24.1/44.0 MB 4.3 MB/s eta 0:00:05
       --------------------- ------------------ 24.1/44.0 MB 4.2 MB/s eta 0:00:05
       ---------------------- ----------------- 24.2/44.0 MB 4.2 MB/s eta 0:00:05
       ---------------------- ----------------- 24.4/44.0 MB 4.2 MB/s eta 0:00:05
       ---------------------- ----------------- 24.6/44.0 MB 4.2 MB/s eta 0:00:05
       ---------------------- ----------------- 24.9/44.0 MB 4.2 MB/s eta 0:00:05
       ---------------------- ----------------- 25.2/44.0 MB 4.1 MB/s eta 0:00:05
       ----------------------- ---------------- 25.4/44.0 MB 4.0 MB/s eta 0:00:05
       ----------------------- ---------------- 25.7/44.0 MB 4.1 MB/s eta 0:00:05
       ----------------------- ---------------- 25.8/44.0 MB 4.0 MB/s eta 0:00:05
       ----------------------- ---------------- 26.0/44.0 MB 4.0 MB/s eta 0:00:05
       ----------------------- ---------------- 26.2/44.0 MB 4.0 MB/s eta 0:00:05
       ------------------------ --------------- 26.5/44.0 MB 3.9 MB/s eta 0:00:05
       ------------------------ --------------- 26.7/44.0 MB 3.9 MB/s eta 0:00:05
       ------------------------ --------------- 26.8/44.0 MB 3.9 MB/s eta 0:00:05
       ------------------------ --------------- 27.0/44.0 MB 3.9 MB/s eta 0:00:05
       ------------------------ --------------- 27.2/44.0 MB 3.9 MB/s eta 0:00:05
       ------------------------ --------------- 27.4/44.0 MB 4.0 MB/s eta 0:00:05
       ------------------------- -------------- 27.8/44.0 MB 4.0 MB/s eta 0:00:05
       ------------------------- -------------- 28.1/44.0 MB 4.0 MB/s eta 0:00:04
       ------------------------- -------------- 28.3/44.0 MB 4.0 MB/s eta 0:00:04
       ------------------------- -------------- 28.5/44.0 MB 4.2 MB/s eta 0:00:04
       -------------------------- ------------- 28.8/44.0 MB 4.3 MB/s eta 0:00:04
       -------------------------- ------------- 29.0/44.0 MB 4.3 MB/s eta 0:00:04
       -------------------------- ------------- 29.2/44.0 MB 4.3 MB/s eta 0:00:04
       -------------------------- ------------- 29.4/44.0 MB 4.3 MB/s eta 0:00:04
       -------------------------- ------------- 29.6/44.0 MB 4.3 MB/s eta 0:00:04
       --------------------------- ------------ 29.7/44.0 MB 4.3 MB/s eta 0:00:04
       --------------------------- ------------ 30.3/44.0 MB 4.4 MB/s eta 0:00:04
       --------------------------- ------------ 30.4/44.0 MB 4.4 MB/s eta 0:00:04
       --------------------------- ------------ 30.5/44.0 MB 4.4 MB/s eta 0:00:04
       ---------------------------- ----------- 30.9/44.0 MB 4.5 MB/s eta 0:00:03
       ---------------------------- ----------- 31.3/44.0 MB 4.5 MB/s eta 0:00:03
       ---------------------------- ----------- 31.4/44.0 MB 4.5 MB/s eta 0:00:03
       ---------------------------- ----------- 31.7/44.0 MB 4.5 MB/s eta 0:00:03
       ----------------------------- ---------- 31.9/44.0 MB 4.5 MB/s eta 0:00:03
       ----------------------------- ---------- 32.3/44.0 MB 4.6 MB/s eta 0:00:03
       ----------------------------- ---------- 32.7/44.0 MB 5.0 MB/s eta 0:00:03
       ------------------------------ --------- 33.0/44.0 MB 5.0 MB/s eta 0:00:03
       ------------------------------ --------- 33.8/44.0 MB 5.2 MB/s eta 0:00:02
       ------------------------------ --------- 34.0/44.0 MB 5.2 MB/s eta 0:00:02
       ------------------------------- -------- 34.4/44.0 MB 5.8 MB/s eta 0:00:02
       ------------------------------- -------- 34.7/44.0 MB 5.8 MB/s eta 0:00:02
       ------------------------------- -------- 35.0/44.0 MB 6.0 MB/s eta 0:00:02
       -------------------------------- ------- 35.3/44.0 MB 6.0 MB/s eta 0:00:02
       -------------------------------- ------- 35.7/44.0 MB 6.1 MB/s eta 0:00:02
       -------------------------------- ------- 36.0/44.0 MB 6.1 MB/s eta 0:00:02
       --------------------------------- ------ 36.6/44.0 MB 6.4 MB/s eta 0:00:02
       --------------------------------- ------ 36.9/44.0 MB 6.4 MB/s eta 0:00:02
       ---------------------------------- ----- 37.5/44.0 MB 6.9 MB/s eta 0:00:01
       ---------------------------------- ----- 37.9/44.0 MB 7.0 MB/s eta 0:00:01
       ---------------------------------- ----- 38.1/44.0 MB 6.9 MB/s eta 0:00:01
       ----------------------------------- ---- 38.5/44.0 MB 7.0 MB/s eta 0:00:01
       ----------------------------------- ---- 39.0/44.0 MB 7.4 MB/s eta 0:00:01
       ----------------------------------- ---- 39.3/44.0 MB 7.4 MB/s eta 0:00:01
       ------------------------------------ --- 39.9/44.0 MB 8.0 MB/s eta 0:00:01
       ------------------------------------ --- 40.3/44.0 MB 7.9 MB/s eta 0:00:01
       ------------------------------------- -- 40.7/44.0 MB 8.2 MB/s eta 0:00:01
       ------------------------------------- -- 41.5/44.0 MB 8.5 MB/s eta 0:00:01
       -------------------------------------- - 42.0/44.0 MB 8.8 MB/s eta 0:00:01
       -------------------------------------- - 42.6/44.0 MB 9.1 MB/s eta 0:00:01
       ---------------------------------------  42.9/44.0 MB 9.2 MB/s eta 0:00:01
       ---------------------------------------  43.3/44.0 MB 9.2 MB/s eta 0:00:01
       ---------------------------------------  43.4/44.0 MB 9.1 MB/s eta 0:00:01
       ---------------------------------------  43.6/44.0 MB 8.7 MB/s eta 0:00:01
       ---------------------------------------  43.9/44.0 MB 8.6 MB/s eta 0:00:01
       ---------------------------------------  44.0/44.0 MB 8.5 MB/s eta 0:00:01
       ---------------------------------------  44.0/44.0 MB 8.5 MB/s eta 0:00:01
       ---------------------------------------  44.0/44.0 MB 8.5 MB/s eta 0:00:01
       ---------------------------------------  44.0/44.0 MB 8.5 MB/s eta 0:00:01
       ---------------------------------------  44.0/44.0 MB 8.5 MB/s eta 0:00:01
       ---------------------------------------  44.0/44.0 MB 8.5 MB/s eta 0:00:01
       ---------------------------------------  44.0/44.0 MB 8.5 MB/s eta 0:00:01
       ---------------------------------------  44.0/44.0 MB 8.5 MB/s eta 0:00:01
       ---------------------------------------  44.0/44.0 MB 8.5 MB/s eta 0:00:01
       ---------------------------------------  44.0/44.0 MB 8.5 MB/s eta 0:00:01
       ---------------------------------------  44.0/44.0 MB 8.5 MB/s eta 0:00:01
       ---------------------------------------  44.0/44.0 MB 8.5 MB/s eta 0:00:01
       ---------------------------------------- 44.0/44.0 MB 5.7 MB/s eta 0:00:00
    Installing collected packages: scipy
    Successfully installed scipy-1.11.2
    Note: you may need to restart the kernel to use updated packages.
    


```python
from scipy.sparse import csr_matrix
```


```python
# sampling data 
sample_usa_data = usa_data.sample(frac=0.001)
```


```python
# Reshape data into sparse matrix
wide_artist_data = sample_usa_data.pivot(index = 'artist-name', columns = 'users', values = 'plays').fillna(0)
wide_artist_data_sparse = csr_matrix(wide_artist_data.values) 
```


```python
wide_artist_data.head()
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
      <th>users</th>
      <th>002b63c6eb63945fcbde6e842a399ce107f1bd35</th>
      <th>002d3f566c5ed4e36bf3332285a7b2ec0d433586</th>
      <th>0050d2483a5573b7256f84fa085c6a4682bfe8b4</th>
      <th>0056f9124c776ff1dd158c2d12440cee874ff3cb</th>
      <th>005d8987be11acc60b0742b48e83eaa4528b5af0</th>
      <th>00b6d6c87345a38718aaa028647a3ad08e78cf91</th>
      <th>00ccb469c03056eaf2bbdcbe2463690d2f793511</th>
      <th>00ceb431517fe93dbb701752ddc51ae9d6a7123f</th>
      <th>0155a3a7398aa65d8d924c38a74bb444b7cb80d4</th>
      <th>01a0ed8062e1c833b3d16aa237d502347a5a93ff</th>
      <th>...</th>
      <th>ff3aed279ceb9a00c15b7b958cc00b1bb3bc073a</th>
      <th>ff480c4cf197e6fd9c525cb627b287444d4d706c</th>
      <th>ff49add8ffbf6cfcca11ccf807938e03a7af1f76</th>
      <th>ff679c0a24b75ba27a9debf76bd536a4334fb3e6</th>
      <th>ff70e7e0a99441c910cb53fedf055ff787aa5da8</th>
      <th>ff8842150157e07f848801544911efb348b53808</th>
      <th>ff9269f5debd942b86ef2a35f2c5a00fa17fc793</th>
      <th>ff9d855523b290088795f2ff22155353b9dc092f</th>
      <th>ffa8f4dd3ec2dba999f693c0bcfd7f4dca1bd1a7</th>
      <th>ffd41e64d50ea0e7ef1c480faef0f2ba4bd87a0b</th>
    </tr>
    <tr>
      <th>artist-name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>!!!</th>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>...</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>*nsync</th>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>...</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>...and you will know us by the trail of dead</th>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>...</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>10 years</th>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>...</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>112</th>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>...</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 2733 columns</p>
</div>




```python
wide_artist_data.shape
```




    (1556, 2733)




```python
# use data to retrieve non-zero element and 1 for row 1
wide_artist_data_sparse[1].data
```




    array([213.,  17.])




```python
wide_artist_data_sparse
```




    <1556x2733 sparse matrix of type '<class 'numpy.float64'>'
    	with 2788 stored elements in Compressed Sparse Row format>




```python
wide_artist_data_sparse.data
```




    array([128., 213.,  17., ..., 262., 138., 391.])




```python
pip install scikit-learn
```

    Collecting scikit-learnNote: you may need to restart the kernel to use updated packages.
    
      Obtaining dependency information for scikit-learn from https://files.pythonhosted.org/packages/77/85/bff3a1e818ec6aa3dd466ff4f4b0a727db9fdb41f2e849747ad902ddbe95/scikit_learn-1.3.0-cp311-cp311-win_amd64.whl.metadata
      Downloading scikit_learn-1.3.0-cp311-cp311-win_amd64.whl.metadata (11 kB)
    Requirement already satisfied: numpy>=1.17.3 in c:\users\himan\anaconda3\envs\pyspark-env\lib\site-packages (from scikit-learn) (1.25.2)
    Requirement already satisfied: scipy>=1.5.0 in c:\users\himan\anaconda3\envs\pyspark-env\lib\site-packages (from scikit-learn) (1.11.2)
    Collecting joblib>=1.1.1 (from scikit-learn)
      Obtaining dependency information for joblib>=1.1.1 from https://files.pythonhosted.org/packages/10/40/d551139c85db202f1f384ba8bcf96aca2f329440a844f924c8a0040b6d02/joblib-1.3.2-py3-none-any.whl.metadata
      Downloading joblib-1.3.2-py3-none-any.whl.metadata (5.4 kB)
    Collecting threadpoolctl>=2.0.0 (from scikit-learn)
      Obtaining dependency information for threadpoolctl>=2.0.0 from https://files.pythonhosted.org/packages/81/12/fd4dea011af9d69e1cad05c75f3f7202cdcbeac9b712eea58ca779a72865/threadpoolctl-3.2.0-py3-none-any.whl.metadata
      Downloading threadpoolctl-3.2.0-py3-none-any.whl.metadata (10.0 kB)
    Downloading scikit_learn-1.3.0-cp311-cp311-win_amd64.whl (9.2 MB)
       ---------------------------------------- 0.0/9.2 MB ? eta -:--:--
       ---------------------------------------- 0.0/9.2 MB ? eta -:--:--
       ---------------------------------------- 0.1/9.2 MB 1.1 MB/s eta 0:00:09
       - -------------------------------------- 0.5/9.2 MB 4.7 MB/s eta 0:00:02
       --- ------------------------------------ 0.9/9.2 MB 6.3 MB/s eta 0:00:02
       ----- ---------------------------------- 1.2/9.2 MB 7.0 MB/s eta 0:00:02
       ------- -------------------------------- 1.7/9.2 MB 7.6 MB/s eta 0:00:01
       -------- ------------------------------- 2.0/9.2 MB 8.1 MB/s eta 0:00:01
       ------------ --------------------------- 2.9/9.2 MB 9.3 MB/s eta 0:00:01
       -------------- ------------------------- 3.4/9.2 MB 9.4 MB/s eta 0:00:01
       ---------------- ----------------------- 3.8/9.2 MB 8.9 MB/s eta 0:00:01
       ----------------- ---------------------- 4.0/9.2 MB 9.2 MB/s eta 0:00:01
       ------------------ --------------------- 4.2/9.2 MB 8.3 MB/s eta 0:00:01
       -------------------- ------------------- 4.7/9.2 MB 8.9 MB/s eta 0:00:01
       -------------------- ------------------- 4.7/9.2 MB 8.4 MB/s eta 0:00:01
       ---------------------- ----------------- 5.1/9.2 MB 7.9 MB/s eta 0:00:01
       ------------------------ --------------- 5.6/9.2 MB 8.3 MB/s eta 0:00:01
       -------------------------- ------------- 6.0/9.2 MB 8.3 MB/s eta 0:00:01
       --------------------------- ------------ 6.3/9.2 MB 8.3 MB/s eta 0:00:01
       ----------------------------- ---------- 6.7/9.2 MB 8.4 MB/s eta 0:00:01
       ------------------------------ --------- 7.1/9.2 MB 8.4 MB/s eta 0:00:01
       -------------------------------- ------- 7.4/9.2 MB 8.3 MB/s eta 0:00:01
       --------------------------------- ------ 7.8/9.2 MB 8.4 MB/s eta 0:00:01
       ------------------------------------ --- 8.3/9.2 MB 8.6 MB/s eta 0:00:01
       -------------------------------------- - 8.8/9.2 MB 8.7 MB/s eta 0:00:01
       ---------------------------------------  9.2/9.2 MB 8.9 MB/s eta 0:00:01
       ---------------------------------------  9.2/9.2 MB 8.9 MB/s eta 0:00:01
       ---------------------------------------- 9.2/9.2 MB 8.3 MB/s eta 0:00:00
    Downloading joblib-1.3.2-py3-none-any.whl (302 kB)
       ---------------------------------------- 0.0/302.2 kB ? eta -:--:--
       ---------------------------------------- 302.2/302.2 kB 9.4 MB/s eta 0:00:00
    Downloading threadpoolctl-3.2.0-py3-none-any.whl (15 kB)
    Installing collected packages: threadpoolctl, joblib, scikit-learn
    Successfully installed joblib-1.3.2 scikit-learn-1.3.0 threadpoolctl-3.2.0
    


```python
#Apply KNN model
from sklearn.neighbors  import NearestNeighbors

model_knn = NearestNeighbors(metric = 'cosine', algorithm = 'brute')
```


```python
model_knn
```




<style>#sk-container-id-1 {color: black;}#sk-container-id-1 pre{padding: 0;}#sk-container-id-1 div.sk-toggleable {background-color: white;}#sk-container-id-1 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-1 label.sk-toggleable__label-arrow:before {content: "▸";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-1 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-1 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-1 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-1 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-1 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-1 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: "▾";}#sk-container-id-1 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-1 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-1 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-1 div.sk-parallel-item::after {content: "";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-1 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-serial::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-1 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-1 div.sk-item {position: relative;z-index: 1;}#sk-container-id-1 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-1 div.sk-item::before, #sk-container-id-1 div.sk-parallel-item::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-1 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-1 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-1 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-1 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-1 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-1 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-1 div.sk-label-container {text-align: center;}#sk-container-id-1 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-1 div.sk-text-repr-fallback {display: none;}</style><div id="sk-container-id-1" class="sk-top-container"><div class="sk-text-repr-fallback"><pre>NearestNeighbors(algorithm=&#x27;brute&#x27;, metric=&#x27;cosine&#x27;)</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br />On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class="sk-container" hidden><div class="sk-item"><div class="sk-estimator sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-1" type="checkbox" checked><label for="sk-estimator-id-1" class="sk-toggleable__label sk-toggleable__label-arrow">NearestNeighbors</label><div class="sk-toggleable__content"><pre>NearestNeighbors(algorithm=&#x27;brute&#x27;, metric=&#x27;cosine&#x27;)</pre></div></div></div></div></div>




```python
model_knn.fit(wide_artist_data_sparse)
```




<style>#sk-container-id-2 {color: black;}#sk-container-id-2 pre{padding: 0;}#sk-container-id-2 div.sk-toggleable {background-color: white;}#sk-container-id-2 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-2 label.sk-toggleable__label-arrow:before {content: "▸";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-2 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-2 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-2 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-2 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-2 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-2 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: "▾";}#sk-container-id-2 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-2 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-2 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-2 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-2 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-2 div.sk-parallel-item::after {content: "";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-2 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-2 div.sk-serial::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-2 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-2 div.sk-item {position: relative;z-index: 1;}#sk-container-id-2 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-2 div.sk-item::before, #sk-container-id-2 div.sk-parallel-item::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-2 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-2 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-2 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-2 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-2 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-2 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-2 div.sk-label-container {text-align: center;}#sk-container-id-2 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-2 div.sk-text-repr-fallback {display: none;}</style><div id="sk-container-id-2" class="sk-top-container"><div class="sk-text-repr-fallback"><pre>NearestNeighbors(algorithm=&#x27;brute&#x27;, metric=&#x27;cosine&#x27;)</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br />On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class="sk-container" hidden><div class="sk-item"><div class="sk-estimator sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-2" type="checkbox" checked><label for="sk-estimator-id-2" class="sk-toggleable__label sk-toggleable__label-arrow">NearestNeighbors</label><div class="sk-toggleable__content"><pre>NearestNeighbors(algorithm=&#x27;brute&#x27;, metric=&#x27;cosine&#x27;)</pre></div></div></div></div></div>




```python
model_knn
```




<style>#sk-container-id-3 {color: black;}#sk-container-id-3 pre{padding: 0;}#sk-container-id-3 div.sk-toggleable {background-color: white;}#sk-container-id-3 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-3 label.sk-toggleable__label-arrow:before {content: "▸";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-3 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-3 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-3 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-3 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-3 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-3 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: "▾";}#sk-container-id-3 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-3 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-3 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-3 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-3 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-3 div.sk-parallel-item::after {content: "";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-3 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-3 div.sk-serial::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-3 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-3 div.sk-item {position: relative;z-index: 1;}#sk-container-id-3 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-3 div.sk-item::before, #sk-container-id-3 div.sk-parallel-item::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-3 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-3 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-3 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-3 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-3 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-3 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-3 div.sk-label-container {text-align: center;}#sk-container-id-3 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-3 div.sk-text-repr-fallback {display: none;}</style><div id="sk-container-id-3" class="sk-top-container"><div class="sk-text-repr-fallback"><pre>NearestNeighbors(algorithm=&#x27;brute&#x27;, metric=&#x27;cosine&#x27;)</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br />On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class="sk-container" hidden><div class="sk-item"><div class="sk-estimator sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-3" type="checkbox" checked><label for="sk-estimator-id-3" class="sk-toggleable__label sk-toggleable__label-arrow">NearestNeighbors</label><div class="sk-toggleable__content"><pre>NearestNeighbors(algorithm=&#x27;brute&#x27;, metric=&#x27;cosine&#x27;)</pre></div></div></div></div></div>




```python
query_index = np.random.choice(wide_artist_data.shape[0])
```


```python
query_index
```




    1177




```python
# label based indexing in dataframe
wide_artist_data.loc['the beatles']
```




    users
    002b63c6eb63945fcbde6e842a399ce107f1bd35   0.000
    002d3f566c5ed4e36bf3332285a7b2ec0d433586   0.000
    0050d2483a5573b7256f84fa085c6a4682bfe8b4   0.000
    0056f9124c776ff1dd158c2d12440cee874ff3cb   0.000
    005d8987be11acc60b0742b48e83eaa4528b5af0   0.000
                                                ... 
    ff8842150157e07f848801544911efb348b53808   0.000
    ff9269f5debd942b86ef2a35f2c5a00fa17fc793   0.000
    ff9d855523b290088795f2ff22155353b9dc092f   0.000
    ffa8f4dd3ec2dba999f693c0bcfd7f4dca1bd1a7   0.000
    ffd41e64d50ea0e7ef1c480faef0f2ba4bd87a0b   0.000
    Name: the beatles, Length: 2733, dtype: float64




```python
#accessing 1000th row and .values to convert into numpy array from pandas series and reshape to get all columns values
wide_artist_data.iloc[1000, :].values.reshape(1,-1)
```




    array([[0., 0., 0., ..., 0., 0., 0.]])




```python
query_index = 1100
# .flatten to convert 2d array to 1d
# n_neighbors to get top 6 
# .index to get artist-name stored at index
distances, indices = model_knn.kneighbors(wide_artist_data.iloc[query_index, :].values.reshape(1,-1), n_neighbors = 6)
for i in range(0, len(distances.flatten())):
    if i == 0:
        print('recomendations {0}'.format(wide_artist_data.index[query_index]))
    else:
        print('{0}: {1}, with distance of {2}'.format(i, wide_artist_data.index[indices.flatten()[i]], distances.flatten()[i]))
```

    recomendations roy harper
    1: propagandhi, with distance of 1.0
    2: pretty girls make graves, with distance of 1.0
    3: primus, with distance of 1.0
    4: prince, with distance of 1.0
    5: prefab sprout, with distance of 1.0
    


```python
distances
```




    array([[0., 1., 1., 1., 1., 1.]])




```python
indices
```




    array([[1100, 1040, 1037, 1038, 1039, 1035]], dtype=int64)




```python
query_index
```




    1100




```python
def print_recomendations(query_index):
    distances, indices = model_knn.kneighbors(wide_artist_data.iloc[query_index, :].values.reshape(1,-1), n_neighbors = 6)
    for i in range(0, len(distances.flatten())):
        if i == 0:
            print('recomendations {0}'.format(wide_artist_data.index[query_index]))
        else:
            print('{0}: {1}, with distance of {2}'.format(i, wide_artist_data.index[indices.flatten()[i]], distances.flatten()[i]))
    
```


```python
inlist = wide_artist_data.index
artist_name = 'michael jackson'

query_index = [x for x in range(len(inlist)) if inlist[x]==artist_name  ]
query_index
```




    [867]




```python
print_recomendations(query_index)
```

    recomendations Index(['michael jackson'], dtype='object', name='artist-name')
    1: prince, with distance of 1.0
    2: propellerheads, with distance of 1.0
    3: pretty girls make graves, with distance of 1.0
    4: primus, with distance of 1.0
    5: prefab sprout, with distance of 1.0
    


```python
inlist
```




    Index(['!!!', '*nsync', '...and you will know us by the trail of dead',
           '10 years', '112', '2pac', '3', '3 doors down', '30 seconds to mars',
           '311',
           ...
           'Аквариум', 'すぎやまこういち', 'モーニング娘。', '下村陽子', '久石譲', '倖田來未', '大島ミチル',
           '菅野よう子', '菊田裕樹', '동방신기'],
          dtype='object', name='artist-name', length=1556)




```python
# Make all plays count binary
wide_artist_data_zero_one = wide_artist_data.apply(np.sign)
wide_artist_data_zero_one_sparse = csr_matrix(wide_artist_data_zero_one.values)
```


```python
wide_artist_data_zero_one.head()
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
      <th>users</th>
      <th>002b63c6eb63945fcbde6e842a399ce107f1bd35</th>
      <th>002d3f566c5ed4e36bf3332285a7b2ec0d433586</th>
      <th>0050d2483a5573b7256f84fa085c6a4682bfe8b4</th>
      <th>0056f9124c776ff1dd158c2d12440cee874ff3cb</th>
      <th>005d8987be11acc60b0742b48e83eaa4528b5af0</th>
      <th>00b6d6c87345a38718aaa028647a3ad08e78cf91</th>
      <th>00ccb469c03056eaf2bbdcbe2463690d2f793511</th>
      <th>00ceb431517fe93dbb701752ddc51ae9d6a7123f</th>
      <th>0155a3a7398aa65d8d924c38a74bb444b7cb80d4</th>
      <th>01a0ed8062e1c833b3d16aa237d502347a5a93ff</th>
      <th>...</th>
      <th>ff3aed279ceb9a00c15b7b958cc00b1bb3bc073a</th>
      <th>ff480c4cf197e6fd9c525cb627b287444d4d706c</th>
      <th>ff49add8ffbf6cfcca11ccf807938e03a7af1f76</th>
      <th>ff679c0a24b75ba27a9debf76bd536a4334fb3e6</th>
      <th>ff70e7e0a99441c910cb53fedf055ff787aa5da8</th>
      <th>ff8842150157e07f848801544911efb348b53808</th>
      <th>ff9269f5debd942b86ef2a35f2c5a00fa17fc793</th>
      <th>ff9d855523b290088795f2ff22155353b9dc092f</th>
      <th>ffa8f4dd3ec2dba999f693c0bcfd7f4dca1bd1a7</th>
      <th>ffd41e64d50ea0e7ef1c480faef0f2ba4bd87a0b</th>
    </tr>
    <tr>
      <th>artist-name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>!!!</th>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>...</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>*nsync</th>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>...</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>...and you will know us by the trail of dead</th>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>...</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>10 years</th>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>...</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>112</th>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>...</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>0.000</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 2733 columns</p>
</div>




```python
wide_artist_data_zero_one_sparse.data
```




    array([1., 1., 1., ..., 1., 1., 1.])




```python
wide_artist_data_zero_one_sparse[7].data
```




    array([1.])




```python
# New KNN-Model on 0-1 values
from sklearn.neighbors import NearestNeighbors
model_mn_binary = NearestNeighbors(metric = 'cosine' , algorithm = 'brute' )
model_mn_binary.fit(wide_artist_data_zero_one_sparse)
```




<style>#sk-container-id-6 {color: black;}#sk-container-id-6 pre{padding: 0;}#sk-container-id-6 div.sk-toggleable {background-color: white;}#sk-container-id-6 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-6 label.sk-toggleable__label-arrow:before {content: "▸";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-6 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-6 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-6 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-6 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-6 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-6 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: "▾";}#sk-container-id-6 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-6 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-6 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-6 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-6 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-6 div.sk-parallel-item::after {content: "";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-6 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-6 div.sk-serial::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-6 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-6 div.sk-item {position: relative;z-index: 1;}#sk-container-id-6 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-6 div.sk-item::before, #sk-container-id-6 div.sk-parallel-item::before {content: "";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-6 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-6 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-6 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-6 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-6 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-6 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-6 div.sk-label-container {text-align: center;}#sk-container-id-6 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-6 div.sk-text-repr-fallback {display: none;}</style><div id="sk-container-id-6" class="sk-top-container"><div class="sk-text-repr-fallback"><pre>NearestNeighbors(algorithm=&#x27;brute&#x27;, metric=&#x27;cosine&#x27;)</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br />On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class="sk-container" hidden><div class="sk-item"><div class="sk-estimator sk-toggleable"><input class="sk-toggleable__control sk-hidden--visually" id="sk-estimator-id-6" type="checkbox" checked><label for="sk-estimator-id-6" class="sk-toggleable__label sk-toggleable__label-arrow">NearestNeighbors</label><div class="sk-toggleable__content"><pre>NearestNeighbors(algorithm=&#x27;brute&#x27;, metric=&#x27;cosine&#x27;)</pre></div></div></div></div></div>




```python
query_index = 900
distances, indices = model_mn_binary.kneighbors(wide_artist_data_zero_one.iloc[query_index, :].values.reshape(1,-1), n_neighbors = 6)

for i in range(0,len(distances.flatten())):
    if i == 0:
        print('Recommendations with binary play data {0}\n'.format(wide_artist_data_zero_one.index[query_index]))
    else:
        print('{0}: {1}, with distance of {2}'.format(i, wide_artist_data_zero_one.index[indices.flatten()[i]], distances.flatten()[i]))
```

    Recommendations with binary play data mstrkrft
    
    1: mirah, with distance of 0.42264973081037416
    2: primus, with distance of 1.0
    3: prince, with distance of 1.0
    4: propagandhi, with distance of 1.0
    5: protest the hero, with distance of 1.0
    


```python
def print_recomendations(query_index):
    distances, indices = model_mn_binary.kneighbors(wide_artist_data_zero_one.iloc[query_index, :].values.reshape(1,-1), n_neighbors = 6)
    
    for i in range(0,len(distances.flatten())):
        if i==0:
            print('Recommendations with binary play data {0}\n'.format(wide_artist_data_zero_one.index[query_index]))
        else:
            print('{0}: {1}, with distance of {2}'.format(i, wide_artist_data_zero_one.index[indices.flatten()[i]], distances.flatten()[i]))
```


```python
in_list = wide_artist_data.index
artist_name = '2pac'

query_index=[x for x in range(len(in_list)) if in_list[x]==artist_name] 
query_index
```




    [5]




```python
print_recomendations(query_index)
```

    Recommendations with binary play data Index(['2pac'], dtype='object', name='artist-name')
    
    1: propagandhi, with distance of 1.0
    2: pretty girls make graves, with distance of 1.0
    3: primus, with distance of 1.0
    4: prince, with distance of 1.0
    5: prefab sprout, with distance of 1.0
    


```python

```


```python

```
