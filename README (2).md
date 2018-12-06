
# Heroes Of Pymoli Data Analysis 2


### ObservedTrend1: More Men than women Play the games

### ObservedTrend2: Most players are from 20-24

### ObservedTrend3:Most Popular items are  Hatred


```python
# Dependencies
import pandas as pd
import numpy as np

```


```python

file="purchase_data_2.json"
```


```python
file_original=pd.read_json(file)
#file_original.to_csv(r"c:\users\nagalakshmi\testdata.csv", sep=',')
file_original =  file_original.drop_duplicates(subset=None, keep='first', inplace=False)
file_original.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <td>24</td>
      <td>Female</td>
      <td>69</td>
      <td>Frenzy, Defender of the Harvest</td>
      <td>4.82</td>
      <td>Lirtjaskan85</td>
    </tr>
    <tr>
      <th>1</th>
      <td>12</td>
      <td>Female</td>
      <td>75</td>
      <td>Brutality Ivory Warmace</td>
      <td>4.12</td>
      <td>Chanjask65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>21</td>
      <td>Female</td>
      <td>114</td>
      <td>Yearning Mageblade</td>
      <td>2.67</td>
      <td>Aerithllora36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>24</td>
      <td>Male</td>
      <td>130</td>
      <td>Alpha</td>
      <td>4.53</td>
      <td>Aeralria27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>28</td>
      <td>Male</td>
      <td>9</td>
      <td>Thorn, Conqueror of the Corrupted</td>
      <td>4.60</td>
      <td>Haisrisuir60</td>
    </tr>
  </tbody>
</table>
</div>



# Total Player Count


```python
#Number of Total Players Count
first_data_frame=pd.DataFrame({"TotalPlayers":[file_original["SN"].nunique()]})
first_data_frame
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>TotalPlayers</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>581</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis(Total)


```python
second_data_frame=pd.DataFrame({"Number of unique items":[file_original["Item ID"].nunique()],
                                "Average Price":[file_original["Price"].mean()],
                              "Number Of Purchases":[file_original["SN"].count()],
                                "Total Revenue":[file_original["Price"].sum()],
                               }
                              )
second_data_frame
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Price</th>
      <th>Number Of Purchases</th>
      <th>Number of unique items</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.029691</td>
      <td>777</td>
      <td>181</td>
      <td>2354.07</td>
    </tr>
  </tbody>
</table>
</div>




```python
second_data_frame.style.format({"Average Price": "${:.2f}","Total Revenue":"${:.2f}"})
#file_df.style.format({"avg_cost": "${:.2f}", "population":"{:,}", "other":"{:<2.2f}"})
```




<style  type="text/css" >
</style>  
<table id="T_f5694df8_8f5d_11e7_9eb5_8ff3606768aa" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Average Price</th> 
        <th class="col_heading level0 col1" >Number Of Purchases</th> 
        <th class="col_heading level0 col2" >Number of unique items</th> 
        <th class="col_heading level0 col3" >Total Revenue</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_f5694df8_8f5d_11e7_9eb5_8ff3606768aa" class="row_heading level0 row0" >0</th> 
        <td id="T_f5694df8_8f5d_11e7_9eb5_8ff3606768aarow0_col0" class="data row0 col0" >$3.03</td> 
        <td id="T_f5694df8_8f5d_11e7_9eb5_8ff3606768aarow0_col1" class="data row0 col1" >777</td> 
        <td id="T_f5694df8_8f5d_11e7_9eb5_8ff3606768aarow0_col2" class="data row0 col2" >181</td> 
        <td id="T_f5694df8_8f5d_11e7_9eb5_8ff3606768aarow0_col3" class="data row0 col3" >$2354.07</td> 
    </tr></tbody> 
</table> 



# Gender Demographics


```python
# group_SN_data=pd.DataFrame(file_original.groupby(["SN"])["Age"].unique().value_counts(),columns=["Age"])
# group_SN_data.head()
# group_SN_data = file_original.groupby(["SN"]).Gender.value_counts().head()
```


```python
uniqueData =  file_original.drop_duplicates(subset=["SN","Gender"], keep='first', inplace=False)
uniqueData = pd.DataFrame({"Total Count":uniqueData.Gender.value_counts()})
uniqueData['Pecentage']= (uniqueData["Total Count"]/uniqueData["Total Count"].sum())*100
uniqueData.style.format({"Pecentage": "{:.2f}%","Total Count":"{}"})
```




<style  type="text/css" >
</style>  
<table id="T_f56e12d8_8f5d_11e7_be29_8ff3606768aa" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Total Count</th> 
        <th class="col_heading level0 col1" >Pecentage</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_f56e12d8_8f5d_11e7_be29_8ff3606768aa" class="row_heading level0 row0" >Male</th> 
        <td id="T_f56e12d8_8f5d_11e7_be29_8ff3606768aarow0_col0" class="data row0 col0" >475</td> 
        <td id="T_f56e12d8_8f5d_11e7_be29_8ff3606768aarow0_col1" class="data row0 col1" >81.76%</td> 
    </tr>    <tr> 
        <th id="T_f56e12d8_8f5d_11e7_be29_8ff3606768aa" class="row_heading level0 row1" >Female</th> 
        <td id="T_f56e12d8_8f5d_11e7_be29_8ff3606768aarow1_col0" class="data row1 col0" >99</td> 
        <td id="T_f56e12d8_8f5d_11e7_be29_8ff3606768aarow1_col1" class="data row1 col1" >17.04%</td> 
    </tr>    <tr> 
        <th id="T_f56e12d8_8f5d_11e7_be29_8ff3606768aa" class="row_heading level0 row2" >Other / Non-Disclosed</th> 
        <td id="T_f56e12d8_8f5d_11e7_be29_8ff3606768aarow2_col0" class="data row2 col0" >7</td> 
        <td id="T_f56e12d8_8f5d_11e7_be29_8ff3606768aarow2_col1" class="data row2 col1" >1.20%</td> 
    </tr></tbody> 
</table> 




```python
group_data = pd.DataFrame({"Total Count":file_original.groupby(["Gender"]).SN.nunique()})
group_data['Pecentage']= (group_data["Total Count"]/group_data["Total Count"].sum())*100
group_data.style.format({"Pecentage": "{:.2f}%","Total Count":"{}"})
```




<style  type="text/css" >
</style>  
<table id="T_f57173de_8f5d_11e7_951e_8ff3606768aa" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Total Count</th> 
        <th class="col_heading level0 col1" >Pecentage</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Gender</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_f57173de_8f5d_11e7_951e_8ff3606768aa" class="row_heading level0 row0" >Female</th> 
        <td id="T_f57173de_8f5d_11e7_951e_8ff3606768aarow0_col0" class="data row0 col0" >99</td> 
        <td id="T_f57173de_8f5d_11e7_951e_8ff3606768aarow0_col1" class="data row0 col1" >17.04%</td> 
    </tr>    <tr> 
        <th id="T_f57173de_8f5d_11e7_951e_8ff3606768aa" class="row_heading level0 row1" >Male</th> 
        <td id="T_f57173de_8f5d_11e7_951e_8ff3606768aarow1_col0" class="data row1 col0" >475</td> 
        <td id="T_f57173de_8f5d_11e7_951e_8ff3606768aarow1_col1" class="data row1 col1" >81.76%</td> 
    </tr>    <tr> 
        <th id="T_f57173de_8f5d_11e7_951e_8ff3606768aa" class="row_heading level0 row2" >Other / Non-Disclosed</th> 
        <td id="T_f57173de_8f5d_11e7_951e_8ff3606768aarow2_col0" class="data row2 col0" >7</td> 
        <td id="T_f57173de_8f5d_11e7_951e_8ff3606768aarow2_col1" class="data row2 col1" >1.20%</td> 
    </tr></tbody> 
</table> 



# Purchasing Analysis(Gender)


```python
gender_data_frame=pd.DataFrame({"Total Count":file_original.groupby("Gender").SN.nunique(),
                                "Priceval":file_original.groupby("Gender").Price.nunique()
                               })
gender_data_frame#["priceval"]=file_original.Price.nunique()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Priceval</th>
      <th>Total Count</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>85</td>
      <td>99</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>143</td>
      <td>475</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>8</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>




```python
group_data_frame=file_original.groupby("Gender")
group_data_frame=pd.DataFrame({"Purchase Count" : file_original.groupby("Gender").Price.nunique(),
                               "AveragePrice" : file_original.groupby("Gender").Price.mean(),
                              "Total Purchase Value":file_original.groupby("Gender").Price.sum(),
                              "Normalized Counts ": (file_original.groupby("Gender").Price.nunique().sum() / group_data_frame.Price.nunique())})
                              
group_data_frame.style.format({"AveragePrice":"${:.2f}","Normalized Counts ": "${:.2f}","Total Purchase Value":"${:.2f}"})        
```




<style  type="text/css" >
</style>  
<table id="T_f57afda2_8f5d_11e7_a54c_8ff3606768aa" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >AveragePrice</th> 
        <th class="col_heading level0 col1" >Normalized Counts </th> 
        <th class="col_heading level0 col2" >Purchase Count</th> 
        <th class="col_heading level0 col3" >Total Purchase Value</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Gender</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_f57afda2_8f5d_11e7_a54c_8ff3606768aa" class="row_heading level0 row0" >Female</th> 
        <td id="T_f57afda2_8f5d_11e7_a54c_8ff3606768aarow0_col0" class="data row0 col0" >$3.03</td> 
        <td id="T_f57afda2_8f5d_11e7_a54c_8ff3606768aarow0_col1" class="data row0 col1" >$2.78</td> 
        <td id="T_f57afda2_8f5d_11e7_a54c_8ff3606768aarow0_col2" class="data row0 col2" >85</td> 
        <td id="T_f57afda2_8f5d_11e7_a54c_8ff3606768aarow0_col3" class="data row0 col3" >$390.87</td> 
    </tr>    <tr> 
        <th id="T_f57afda2_8f5d_11e7_a54c_8ff3606768aa" class="row_heading level0 row1" >Male</th> 
        <td id="T_f57afda2_8f5d_11e7_a54c_8ff3606768aarow1_col0" class="data row1 col0" >$3.03</td> 
        <td id="T_f57afda2_8f5d_11e7_a54c_8ff3606768aarow1_col1" class="data row1 col1" >$1.65</td> 
        <td id="T_f57afda2_8f5d_11e7_a54c_8ff3606768aarow1_col2" class="data row1 col2" >143</td> 
        <td id="T_f57afda2_8f5d_11e7_a54c_8ff3606768aarow1_col3" class="data row1 col3" >$1939.34</td> 
    </tr>    <tr> 
        <th id="T_f57afda2_8f5d_11e7_a54c_8ff3606768aa" class="row_heading level0 row2" >Other / Non-Disclosed</th> 
        <td id="T_f57afda2_8f5d_11e7_a54c_8ff3606768aarow2_col0" class="data row2 col0" >$2.98</td> 
        <td id="T_f57afda2_8f5d_11e7_a54c_8ff3606768aarow2_col1" class="data row2 col1" >$29.50</td> 
        <td id="T_f57afda2_8f5d_11e7_a54c_8ff3606768aarow2_col2" class="data row2 col2" >8</td> 
        <td id="T_f57afda2_8f5d_11e7_a54c_8ff3606768aarow2_col3" class="data row2 col3" >$23.86</td> 
    </tr></tbody> 
</table> 



# Age Demographics


```python
uniqueData =  file_original.drop_duplicates(subset=["SN","Age"], keep='first', inplace=False)
intervals =[0,10,15,20,25,30,35,40,uniqueData.Age.max()+1]
names = [" <10","10-14","15-19","20-24","25-29","30-34","35-39","40+"]
d =pd.cut(uniqueData.Age, bins =intervals,labels =names,include_lowest =True,right=False).value_counts().sort_index(ascending=True)
age_range_data_frame=pd.DataFrame({"Total Count":d,
              "Percentage of Players":np.round((d/d.sum())*100,2)})
```


```python
age_range_data_frame
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>4.48</td>
      <td>26</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>3.61</td>
      <td>21</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>17.73</td>
      <td>103</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>39.59</td>
      <td>230</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>18.07</td>
      <td>105</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>8.09</td>
      <td>47</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>7.06</td>
      <td>41</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>1.38</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis(Age)


```python
uniqueData =  file_original.drop_duplicates(subset=["SN","Age"], keep='first', inplace=False)
uniqueData.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <td>24</td>
      <td>Female</td>
      <td>69</td>
      <td>Frenzy, Defender of the Harvest</td>
      <td>4.82</td>
      <td>Lirtjaskan85</td>
    </tr>
    <tr>
      <th>1</th>
      <td>12</td>
      <td>Female</td>
      <td>75</td>
      <td>Brutality Ivory Warmace</td>
      <td>4.12</td>
      <td>Chanjask65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>21</td>
      <td>Female</td>
      <td>114</td>
      <td>Yearning Mageblade</td>
      <td>2.67</td>
      <td>Aerithllora36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>24</td>
      <td>Male</td>
      <td>130</td>
      <td>Alpha</td>
      <td>4.53</td>
      <td>Aeralria27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>28</td>
      <td>Male</td>
      <td>9</td>
      <td>Thorn, Conqueror of the Corrupted</td>
      <td>4.60</td>
      <td>Haisrisuir60</td>
    </tr>
  </tbody>
</table>
</div>




```python
bins=[[0,10,15,20,25,30,35,40,uniqueData.Age.max()+1]]
```


```python
names = [" <10","10-14","15-19","20-24","25-29","30-34","35-39","40+"]

```


```python
uniqueData =  file_original.drop_duplicates(subset=["SN","Age"], keep='first', inplace=False)
intervals =[0,10,15,20,25,30,35,40,uniqueData.Age.max()]
#priceintervals=[0.0,1.0,2.0,3.0,4.0,5.0,6.0,7.0,uniqueData.Price.max()]

names = [" <10","10-14","15-19","20-24","25-29","30-34","35-39","40+"]
d =pd.cut(uniqueData.Age, bins =intervals,labels =names,right=False)
#p=pd.cut(uniqueData.Price,bins=priceintervals,labels=names).value_counts()
purchase_df=uniqueData.groupby(d)['Price'].count()
purchase_df=pd.DataFrame({"purchaseCount":uniqueData.groupby(d)['Price'].count(),
                         "AveragePurchasePrice":(uniqueData.groupby(d)['Price'].sum())/ (uniqueData.groupby(d)['Price'].count()),
                         "TotalPurchasedValues":uniqueData.groupby(d)['Price'].sum(),
                        "NormalizedTotals" :(uniqueData.groupby(d)['Price'].sum()) / (uniqueData.groupby(d)['Price'].nunique())})
purchase_df.style.format({"AveragePurchasePrice":"${:.2f}","NormalizedTotals": "${:.2f}","TotalPurchasedValues":"${:.2f}"}) 
```




<style  type="text/css" >
</style>  
<table id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aa" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >AveragePurchasePrice</th> 
        <th class="col_heading level0 col1" >NormalizedTotals</th> 
        <th class="col_heading level0 col2" >TotalPurchasedValues</th> 
        <th class="col_heading level0 col3" >purchaseCount</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Age</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aa" class="row_heading level0 row0" > <10</th> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow0_col0" class="data row0 col0" >$2.91</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow0_col1" class="data row0 col1" >$3.03</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow0_col2" class="data row0 col2" >$75.65</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow0_col3" class="data row0 col3" >26</td> 
    </tr>    <tr> 
        <th id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aa" class="row_heading level0 row1" >10-14</th> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow1_col0" class="data row1 col0" >$3.02</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow1_col1" class="data row1 col1" >$3.17</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow1_col2" class="data row1 col2" >$63.35</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow1_col3" class="data row1 col3" >21</td> 
    </tr>    <tr> 
        <th id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aa" class="row_heading level0 row2" >15-19</th> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow2_col0" class="data row2 col0" >$3.06</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow2_col1" class="data row2 col1" >$4.38</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow2_col2" class="data row2 col2" >$315.06</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow2_col3" class="data row2 col3" >103</td> 
    </tr>    <tr> 
        <th id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aa" class="row_heading level0 row3" >20-24</th> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow3_col0" class="data row3 col0" >$2.98</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow3_col1" class="data row3 col1" >$6.22</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow3_col2" class="data row3 col2" >$684.52</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow3_col3" class="data row3 col3" >230</td> 
    </tr>    <tr> 
        <th id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aa" class="row_heading level0 row4" >25-29</th> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow4_col0" class="data row4 col0" >$3.08</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow4_col1" class="data row4 col1" >$4.61</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow4_col2" class="data row4 col2" >$322.95</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow4_col3" class="data row4 col3" >105</td> 
    </tr>    <tr> 
        <th id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aa" class="row_heading level0 row5" >30-34</th> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow5_col0" class="data row5 col0" >$3.08</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow5_col1" class="data row5 col1" >$3.61</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow5_col2" class="data row5 col2" >$144.53</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow5_col3" class="data row5 col3" >47</td> 
    </tr>    <tr> 
        <th id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aa" class="row_heading level0 row6" >35-39</th> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow6_col0" class="data row6 col0" >$3.05</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow6_col1" class="data row6 col1" >$3.58</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow6_col2" class="data row6 col2" >$125.18</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow6_col3" class="data row6 col3" >41</td> 
    </tr>    <tr> 
        <th id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aa" class="row_heading level0 row7" >40+</th> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow7_col0" class="data row7 col0" >$3.70</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow7_col1" class="data row7 col1" >$4.32</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow7_col2" class="data row7 col2" >$25.90</td> 
        <td id="T_f59bed6e_8f5d_11e7_b373_8ff3606768aarow7_col3" class="data row7 col3" >7</td> 
    </tr></tbody> 
</table> 



# Top Spenders


```python
group_SN = file_original.groupby("SN")
group_SN.head()
data = pd.DataFrame({"Purchase Count":group_SN["Item ID"].count(),
"AveragePurchasePrice":np.round((group_SN["Item ID"].count())/((group_SN["Item ID"].count())*(group_SN["Price"].sum()))*100,2),
                    "TotalPurchaseValue":(group_SN["Item ID"].count())*(group_SN["Price"].sum())}).sort_values("TotalPurchaseValue", ascending=False).head(5)

    
#data.sort_values("TotalPurchaseValue", ascending=False).head(5)
#data.style.format({"AveragePurchasePrice":"$"})
data.style.format({"AveragePurchasePrice":"${:.2f}","TotalPurchaseValue":"${:.2f}"})

```




<style  type="text/css" >
</style>  
<table id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aa" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >AveragePurchasePrice</th> 
        <th class="col_heading level0 col1" >Purchase Count</th> 
        <th class="col_heading level0 col2" >TotalPurchaseValue</th> 
    </tr>    <tr> 
        <th class="index_name level0" >SN</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aa" class="row_heading level0 row0" >Chamalo71</th> 
        <td id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aarow0_col0" class="data row0 col0" >$7.43</td> 
        <td id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aarow0_col1" class="data row0 col1" >4</td> 
        <td id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aarow0_col2" class="data row0 col2" >$53.80</td> 
    </tr>    <tr> 
        <th id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aa" class="row_heading level0 row1" >Strithenu87</th> 
        <td id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aarow1_col0" class="data row1 col0" >$7.79</td> 
        <td id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aarow1_col1" class="data row1 col1" >4</td> 
        <td id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aarow1_col2" class="data row1 col2" >$51.32</td> 
    </tr>    <tr> 
        <th id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aa" class="row_heading level0 row2" >Chamistast30</th> 
        <td id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aarow2_col0" class="data row2 col0" >$9.73</td> 
        <td id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aarow2_col1" class="data row2 col1" >4</td> 
        <td id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aarow2_col2" class="data row2 col2" >$41.12</td> 
    </tr>    <tr> 
        <th id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aa" class="row_heading level0 row3" >Lirtilsa71</th> 
        <td id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aarow3_col0" class="data row3 col0" >$10.13</td> 
        <td id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aarow3_col1" class="data row3 col1" >4</td> 
        <td id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aarow3_col2" class="data row3 col2" >$39.48</td> 
    </tr>    <tr> 
        <th id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aa" class="row_heading level0 row4" >Aeralria27</th> 
        <td id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aarow4_col0" class="data row4 col0" >$8.79</td> 
        <td id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aarow4_col1" class="data row4 col1" >3</td> 
        <td id="T_f5a1b15c_8f5d_11e7_a6a2_8ff3606768aarow4_col2" class="data row4 col2" >$34.14</td> 
    </tr></tbody> 
</table> 



# Most Popular Items


```python
group_item=file_original.groupby(["Item ID","Item Name"])
group_item.head()
purcahse_count=pd.DataFrame({"PurchaseCount":group_item["Item ID"].count(),
                            "Item Price":group_item["Price"].max(),
                            "TotalPurchaseValue":(group_item["Item ID"].count()) *(group_item["Price"].max() )}).sort_values("PurchaseCount", ascending=False).head(5)
purcahse_count.style.format({"Item Price":"${:.2f}","TotalPurchaseValue":"${:.2f}"})
```




<style  type="text/css" >
</style>  
<table id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aa" > 
<thead>    <tr> 
        <th class="blank" ></th> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Item Price</th> 
        <th class="col_heading level0 col1" >PurchaseCount</th> 
        <th class="col_heading level0 col2" >TotalPurchaseValue</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Item ID</th> 
        <th class="index_name level1" >Item Name</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aa" class="row_heading level0 row0" >52</th> 
        <th id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aa" class="row_heading level1 row0" >Hatred</th> 
        <td id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aarow0_col0" class="data row0 col0" >$4.59</td> 
        <td id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aarow0_col1" class="data row0 col1" >11</td> 
        <td id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aarow0_col2" class="data row0 col2" >$50.49</td> 
    </tr>    <tr> 
        <th id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aa" class="row_heading level0 row1" >174</th> 
        <th id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aa" class="row_heading level1 row1" >Primitive Blade</th> 
        <td id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aarow1_col0" class="data row1 col0" >$1.39</td> 
        <td id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aarow1_col1" class="data row1 col1" >9</td> 
        <td id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aarow1_col2" class="data row1 col2" >$12.51</td> 
    </tr>    <tr> 
        <th id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aa" class="row_heading level0 row2" >111</th> 
        <th id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aa" class="row_heading level1 row2" >Misery's End</th> 
        <td id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aarow2_col0" class="data row2 col0" >$4.90</td> 
        <td id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aarow2_col1" class="data row2 col1" >9</td> 
        <td id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aarow2_col2" class="data row2 col2" >$44.10</td> 
    </tr>    <tr> 
        <th id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aa" class="row_heading level0 row3" >91</th> 
        <th id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aa" class="row_heading level1 row3" >Celeste</th> 
        <td id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aarow3_col0" class="data row3 col0" >$2.07</td> 
        <td id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aarow3_col1" class="data row3 col1" >8</td> 
        <td id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aarow3_col2" class="data row3 col2" >$16.56</td> 
    </tr>    <tr> 
        <th id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aa" class="row_heading level0 row4" >143</th> 
        <th id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aa" class="row_heading level1 row4" >Frenzied Scimitar</th> 
        <td id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aarow4_col0" class="data row4 col0" >$3.35</td> 
        <td id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aarow4_col1" class="data row4 col1" >8</td> 
        <td id="T_f5a6761c_8f5d_11e7_8302_8ff3606768aarow4_col2" class="data row4 col2" >$26.80</td> 
    </tr></tbody> 
</table> 



#  Most Profitable Items



```python
group_item=file_original.groupby(["Item ID","Item Name"])
group_item.head()
purcahse_count=pd.DataFrame({"PurchaseCount":group_item["Item ID"].count(),
                            "Item Price":group_item["Price"].max(),
                            "TotalPurchaseValue":(group_item["Item ID"].count()) *(group_item["Price"].max() )}).sort_values("TotalPurchaseValue", ascending=False).head(5)

purcahse_count.style.format({"Item Price":"${:.2f}","TotalPurchaseValue":"${:.2f}"})
```




<style  type="text/css" >
</style>  
<table id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aa" > 
<thead>    <tr> 
        <th class="blank" ></th> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Item Price</th> 
        <th class="col_heading level0 col1" >PurchaseCount</th> 
        <th class="col_heading level0 col2" >TotalPurchaseValue</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Item ID</th> 
        <th class="index_name level1" >Item Name</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aa" class="row_heading level0 row0" >52</th> 
        <th id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aa" class="row_heading level1 row0" >Hatred</th> 
        <td id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aarow0_col0" class="data row0 col0" >$4.59</td> 
        <td id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aarow0_col1" class="data row0 col1" >11</td> 
        <td id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aarow0_col2" class="data row0 col2" >$50.49</td> 
    </tr>    <tr> 
        <th id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aa" class="row_heading level0 row1" >111</th> 
        <th id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aa" class="row_heading level1 row1" >Misery's End</th> 
        <td id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aarow1_col0" class="data row1 col0" >$4.90</td> 
        <td id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aarow1_col1" class="data row1 col1" >9</td> 
        <td id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aarow1_col2" class="data row1 col2" >$44.10</td> 
    </tr>    <tr> 
        <th id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aa" class="row_heading level0 row2" >93</th> 
        <th id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aa" class="row_heading level1 row2" >Apocalyptic Battlescythe</th> 
        <td id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aarow2_col0" class="data row2 col0" >$4.85</td> 
        <td id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aarow2_col1" class="data row2 col1" >8</td> 
        <td id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aarow2_col2" class="data row2 col2" >$38.80</td> 
    </tr>    <tr> 
        <th id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aa" class="row_heading level0 row3" >49</th> 
        <th id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aa" class="row_heading level1 row3" >The Oculus, Token of Lost Worlds</th> 
        <td id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aarow3_col0" class="data row3 col0" >$4.61</td> 
        <td id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aarow3_col1" class="data row3 col1" >8</td> 
        <td id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aarow3_col2" class="data row3 col2" >$36.88</td> 
    </tr>    <tr> 
        <th id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aa" class="row_heading level0 row4" >19</th> 
        <th id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aa" class="row_heading level1 row4" >Pursuit, Cudgel of Necromancy</th> 
        <td id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aarow4_col0" class="data row4 col0" >$4.41</td> 
        <td id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aarow4_col1" class="data row4 col1" >8</td> 
        <td id="T_f5a8d898_8f5d_11e7_91cc_8ff3606768aarow4_col2" class="data row4 col2" >$35.28</td> 
    </tr></tbody> 
</table> 




```python

```


```python

```
