

```python
import pandas as pd
```


```python
# Reading input file to dataframe
df = pd.read_json("purchase_data.json")
df.head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Player Count
totalplayers = len(df["SN"].unique())

totalplayers= pd.DataFrame({"Players": [totalplayers]})
totalplayers
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
      <th>Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>573</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis (Total)
#Number of Unique Items
uniqueitems = len(df["Item Name"].unique())
uniqueitems

#Average Purchase Price
avgprice = df["Price"].mean()
avgprice

#Total Number of Purchases
totalpurchases = df["Item Name"].count()
totalpurchases

#TOtal Revenue
Revenue = df["Price"].sum()
Revenue
```




    2286.33




```python
#Gender Demographics

#per gender
genders = df.groupby("Gender").SN.nunique()

```


```python
#Set variables
female = genders.Female.sum()
male = genders.Male.sum()
percentmale = male/totalplayers*100
percentfemale = female/totalplayers*100
```


```python
#create dataframe
genderframe = pd.DataFrame({"Gender": ["Male", "Female", "Other / Non-Disclose"],
                           "Total": [male, female, "8"],
                           "Percentage": [percentmale, percentfemale, "1.40"]})
genderframe
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
      <th>Percentage</th>
      <th>Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Male</td>
      <td>Players
0  81.151832</td>
      <td>465</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Female</td>
      <td>Players
0  17.452007</td>
      <td>100</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclose</td>
      <td>1.40</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis (Gender)

#Count of purchases by Gender
gg = df.groupby("Gender")
gg["Item ID"].count()
```




    Gender
    Female                   136
    Male                     633
    Other / Non-Disclosed     11
    Name: Item ID, dtype: int64




```python
#Average Purchase Price
gg["Price"].mean()
```




    Gender
    Female                   2.815515
    Male                     2.950521
    Other / Non-Disclosed    3.249091
    Name: Price, dtype: float64




```python
#Total Purchase Value
gg["Price"].sum()
```




    Gender
    Female                    382.91
    Male                     1867.68
    Other / Non-Disclosed      35.74
    Name: Price, dtype: float64




```python
#Age Demographics

bins = [4,9,14,19,24,29,34,39,44,49]
df["Age Range"] = pd.cut(df["Age"],bins)
df.head()

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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>Age Range</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
      <td>(34, 39]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
      <td>(19, 24]</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
      <td>(29, 34]</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
      <td>(19, 24]</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
      <td>(19, 24]</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchase Count
age_grouped = df.groupby("Age Range")["Item ID"].count()
age_grouped
```




    Age Range
    (4, 9]       28
    (9, 14]      35
    (14, 19]    133
    (19, 24]    336
    (24, 29]    125
    (29, 34]     64
    (34, 39]     42
    (39, 44]     16
    (44, 49]      1
    Name: Item ID, dtype: int64




```python
#Average Purchase Price
avg_price = df.groupby("Age Range")["Price"].mean()
avg_price
```




    Age Range
    (4, 9]      2.980714
    (9, 14]     2.770000
    (14, 19]    2.905414
    (19, 24]    2.913006
    (24, 29]    2.962640
    (29, 34]    3.082031
    (34, 39]    2.842857
    (39, 44]    3.189375
    (44, 49]    2.720000
    Name: Price, dtype: float64




```python
#Total Purchase Value
purch_value = df.groupby("Age Range")["Price"].sum()
purch_value
```




    Age Range
    (4, 9]       83.46
    (9, 14]      96.95
    (14, 19]    386.42
    (19, 24]    978.77
    (24, 29]    370.33
    (29, 34]    197.25
    (34, 39]    119.40
    (39, 44]     51.03
    (44, 49]      2.72
    Name: Price, dtype: float64




```python
#Top Spenders#Purchase Count#Avg Purchase Price#Total Value
#Total purchases
spenders = df.groupby("SN").Price.sum()
#Count
count = df.groupby("SN").Price.count()
#Average Price
average = df.groupby("SN").Price.mean()

blah = pd.DataFrame({"Count": count,
                    "Average": average,
                    "Total Purchase": spenders})
blah.nlargest(5, "Total Purchase")
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
      <th>Average</th>
      <th>Count</th>
      <th>Total Purchase</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Undirrala66</th>
      <td>3.412000</td>
      <td>5</td>
      <td>17.06</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>3.390000</td>
      <td>4</td>
      <td>13.56</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>3.185000</td>
      <td>4</td>
      <td>12.74</td>
    </tr>
    <tr>
      <th>Haellysu29</th>
      <td>4.243333</td>
      <td>3</td>
      <td>12.73</td>
    </tr>
    <tr>
      <th>Eoda93</th>
      <td>3.860000</td>
      <td>3</td>
      <td>11.58</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Popular Items

CountItems = df.groupby("Item Name").Price.count()
ItemGroup = df.groupby("Item Name")["Item ID"].mean().astype('int')
AveragePrice = df.groupby("Item Name").Price.mean()
TotalPurchaseValue = df.groupby("Item Name").Price.sum()

Most_Popular = pd.DataFrame({'Item id':ItemGroup,
                       'Purchase Count' : CountItems,
                       'Item Price' : AveragePrice, 
                       'Total Purchase Value' : TotalPurchaseValue})
Most_Popular.nlargest(5,'Purchase Count')
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
      <th>Item Price</th>
      <th>Item id</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Final Critic</th>
      <td>2.757143</td>
      <td>95</td>
      <td>14</td>
      <td>38.60</td>
    </tr>
    <tr>
      <th>Arcane Gem</th>
      <td>2.230000</td>
      <td>84</td>
      <td>11</td>
      <td>24.53</td>
    </tr>
    <tr>
      <th>Betrayal, Whisper of Grieving Widows</th>
      <td>2.350000</td>
      <td>39</td>
      <td>11</td>
      <td>25.85</td>
    </tr>
    <tr>
      <th>Stormcaller</th>
      <td>3.465000</td>
      <td>105</td>
      <td>10</td>
      <td>34.65</td>
    </tr>
    <tr>
      <th>Retribution Axe</th>
      <td>4.140000</td>
      <td>34</td>
      <td>9</td>
      <td>37.26</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Observations
Most players are between the age of 19 and 25

People on the age outliers did not buy a lot of things. Possibly player engagement or understanding of the game.

Most of the players were male
```
