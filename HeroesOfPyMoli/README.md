
# Heroes Of Pymoli Data Analysis


### ObservedTrend1:More Men than Women Play the games

### ObservedTrend2: Most players are from 20-24 age group

### ObservedTrend3: Most popular item players buy is 'GAE  Betrayal, Whisper of Grieving Windows'


```python
# Dependencies
import pandas as pd
import numpy as np

```


```python

file="purchase_data.json"
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
      <td>573</td>
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
                               })
  
                              

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
      <td>2.933488</td>
      <td>777</td>
      <td>183</td>
      <td>2279.32</td>
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
<table id="T_5acfef38_8ffb_11e7_a4bb_8ff3606768aa" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Average Price</th> 
        <th class="col_heading level0 col1" >Number Of Purchases</th> 
        <th class="col_heading level0 col2" >Number of unique items</th> 
        <th class="col_heading level0 col3" >Total Revenue</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_5acfef38_8ffb_11e7_a4bb_8ff3606768aa" class="row_heading level0 row0" >0</th> 
        <td id="T_5acfef38_8ffb_11e7_a4bb_8ff3606768aarow0_col0" class="data row0 col0" >$2.93</td> 
        <td id="T_5acfef38_8ffb_11e7_a4bb_8ff3606768aarow0_col1" class="data row0 col1" >777</td> 
        <td id="T_5acfef38_8ffb_11e7_a4bb_8ff3606768aarow0_col2" class="data row0 col2" >183</td> 
        <td id="T_5acfef38_8ffb_11e7_a4bb_8ff3606768aarow0_col3" class="data row0 col3" >$2279.32</td> 
    </tr></tbody> 
</table> 



# Gender Demographics


```python
uniqueData =  file_original.drop_duplicates(subset=["SN","Gender"], keep='first', inplace=False)
uniqueData = pd.DataFrame({"Total Count":uniqueData.Gender.value_counts()})
uniqueData['Pecentage']= (uniqueData["Total Count"]/uniqueData["Total Count"].sum())*100
uniqueData.style.format({"Pecentage": "{:.2f}%","Total Count":"{}"})
```




<style  type="text/css" >
</style>  
<table id="T_5ad6835e_8ffb_11e7_8258_8ff3606768aa" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Total Count</th> 
        <th class="col_heading level0 col1" >Pecentage</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_5ad6835e_8ffb_11e7_8258_8ff3606768aa" class="row_heading level0 row0" >Male</th> 
        <td id="T_5ad6835e_8ffb_11e7_8258_8ff3606768aarow0_col0" class="data row0 col0" >465</td> 
        <td id="T_5ad6835e_8ffb_11e7_8258_8ff3606768aarow0_col1" class="data row0 col1" >81.15%</td> 
    </tr>    <tr> 
        <th id="T_5ad6835e_8ffb_11e7_8258_8ff3606768aa" class="row_heading level0 row1" >Female</th> 
        <td id="T_5ad6835e_8ffb_11e7_8258_8ff3606768aarow1_col0" class="data row1 col0" >100</td> 
        <td id="T_5ad6835e_8ffb_11e7_8258_8ff3606768aarow1_col1" class="data row1 col1" >17.45%</td> 
    </tr>    <tr> 
        <th id="T_5ad6835e_8ffb_11e7_8258_8ff3606768aa" class="row_heading level0 row2" >Other / Non-Disclosed</th> 
        <td id="T_5ad6835e_8ffb_11e7_8258_8ff3606768aarow2_col0" class="data row2 col0" >8</td> 
        <td id="T_5ad6835e_8ffb_11e7_8258_8ff3606768aarow2_col1" class="data row2 col1" >1.40%</td> 
    </tr></tbody> 
</table> 




```python
group_data = pd.DataFrame({"Total Count":file_original.groupby(["Gender"]).SN.nunique()})
group_data['Pecentage']= (group_data["Total Count"]/group_data["Total Count"].sum())*100
group_data.style.format({"Pecentage": "{:.2f}%","Total Count":"{}"})
```




<style  type="text/css" >
</style>  
<table id="T_5adb2df8_8ffb_11e7_b3d2_8ff3606768aa" > 
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
        <th id="T_5adb2df8_8ffb_11e7_b3d2_8ff3606768aa" class="row_heading level0 row0" >Female</th> 
        <td id="T_5adb2df8_8ffb_11e7_b3d2_8ff3606768aarow0_col0" class="data row0 col0" >100</td> 
        <td id="T_5adb2df8_8ffb_11e7_b3d2_8ff3606768aarow0_col1" class="data row0 col1" >17.45%</td> 
    </tr>    <tr> 
        <th id="T_5adb2df8_8ffb_11e7_b3d2_8ff3606768aa" class="row_heading level0 row1" >Male</th> 
        <td id="T_5adb2df8_8ffb_11e7_b3d2_8ff3606768aarow1_col0" class="data row1 col0" >465</td> 
        <td id="T_5adb2df8_8ffb_11e7_b3d2_8ff3606768aarow1_col1" class="data row1 col1" >81.15%</td> 
    </tr>    <tr> 
        <th id="T_5adb2df8_8ffb_11e7_b3d2_8ff3606768aa" class="row_heading level0 row2" >Other / Non-Disclosed</th> 
        <td id="T_5adb2df8_8ffb_11e7_b3d2_8ff3606768aarow2_col0" class="data row2 col0" >8</td> 
        <td id="T_5adb2df8_8ffb_11e7_b3d2_8ff3606768aarow2_col1" class="data row2 col1" >1.40%</td> 
    </tr></tbody> 
</table> 



# Purchasing Analysis(Gender)


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
<table id="T_5ae55a94_8ffb_11e7_a179_8ff3606768aa" > 
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
        <th id="T_5ae55a94_8ffb_11e7_a179_8ff3606768aa" class="row_heading level0 row0" >Female</th> 
        <td id="T_5ae55a94_8ffb_11e7_a179_8ff3606768aarow0_col0" class="data row0 col0" >$2.83</td> 
        <td id="T_5ae55a94_8ffb_11e7_a179_8ff3606768aarow0_col1" class="data row0 col1" >$2.80</td> 
        <td id="T_5ae55a94_8ffb_11e7_a179_8ff3606768aarow0_col2" class="data row0 col2" >89</td> 
        <td id="T_5ae55a94_8ffb_11e7_a179_8ff3606768aarow0_col3" class="data row0 col3" >$381.55</td> 
    </tr>    <tr> 
        <th id="T_5ae55a94_8ffb_11e7_a179_8ff3606768aa" class="row_heading level0 row1" >Male</th> 
        <td id="T_5ae55a94_8ffb_11e7_a179_8ff3606768aarow1_col0" class="data row1 col0" >$2.95</td> 
        <td id="T_5ae55a94_8ffb_11e7_a179_8ff3606768aarow1_col1" class="data row1 col1" >$1.67</td> 
        <td id="T_5ae55a94_8ffb_11e7_a179_8ff3606768aarow1_col2" class="data row1 col2" >149</td> 
        <td id="T_5ae55a94_8ffb_11e7_a179_8ff3606768aarow1_col3" class="data row1 col3" >$1862.03</td> 
    </tr>    <tr> 
        <th id="T_5ae55a94_8ffb_11e7_a179_8ff3606768aa" class="row_heading level0 row2" >Other / Non-Disclosed</th> 
        <td id="T_5ae55a94_8ffb_11e7_a179_8ff3606768aarow2_col0" class="data row2 col0" >$3.25</td> 
        <td id="T_5ae55a94_8ffb_11e7_a179_8ff3606768aarow2_col1" class="data row2 col1" >$22.64</td> 
        <td id="T_5ae55a94_8ffb_11e7_a179_8ff3606768aarow2_col2" class="data row2 col2" >11</td> 
        <td id="T_5ae55a94_8ffb_11e7_a179_8ff3606768aarow2_col3" class="data row2 col3" >$35.74</td> 
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
      <td>3.32</td>
      <td>19</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>4.01</td>
      <td>23</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>17.45</td>
      <td>100</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>45.20</td>
      <td>259</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>15.18</td>
      <td>87</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>8.20</td>
      <td>47</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>4.71</td>
      <td>27</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>1.92</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis(Age)


```python
#uniqueData =  file_original.drop_duplicates(subset=["SN","Age"], keep='first', inplace=False)
#uniqueData.head()
```


```python
#bins=[[0,10,15,20,25,30,35,40,uniqueData.Age.max()+1]]
```


```python
#names = [" <10","10-14","15-19","20-24","25-29","30-34","35-39","40+"]

```


```python
uniqueData =  file_original.drop_duplicates(subset=["SN","Age"], keep='first', inplace=False)
intervals =[0,10,15,20,25,30,35,40,uniqueData.Age.max()]


names = [" <10","10-14","15-19","20-24","25-29","30-34","35-39","40+"]
d =pd.cut(uniqueData.Age, bins =intervals,labels =names,right=False)

purchase_df=uniqueData.groupby(d)['Price'].count()
purchase_df=pd.DataFrame({"purchaseCount":uniqueData.groupby(d)['Price'].count(),
                         "AveragePurchasePrice":(uniqueData.groupby(d)['Price'].sum())/ (uniqueData.groupby(d)['Price'].count()),
                         "TotalPurchasedValues":uniqueData.groupby(d)['Price'].sum(),
                        "NormalizedTotals" :(uniqueData.groupby(d)['Price'].sum()) / (uniqueData.groupby(d)['Price'].nunique())})
purchase_df.style.format({"AveragePurchasePrice":"${:.2f}","NormalizedTotals": "${:.2f}","TotalPurchasedValues":"${:.2f}"}) 
```




<style  type="text/css" >
</style>  
<table id="T_5b073df8_8ffb_11e7_998c_8ff3606768aa" > 
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
        <th id="T_5b073df8_8ffb_11e7_998c_8ff3606768aa" class="row_heading level0 row0" > <10</th> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow0_col0" class="data row0 col0" >$3.13</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow0_col1" class="data row0 col1" >$3.13</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow0_col2" class="data row0 col2" >$59.45</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow0_col3" class="data row0 col3" >19</td> 
    </tr>    <tr> 
        <th id="T_5b073df8_8ffb_11e7_998c_8ff3606768aa" class="row_heading level0 row1" >10-14</th> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow1_col0" class="data row1 col0" >$2.70</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow1_col1" class="data row1 col1" >$2.95</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow1_col2" class="data row1 col2" >$62.04</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow1_col3" class="data row1 col3" >23</td> 
    </tr>    <tr> 
        <th id="T_5b073df8_8ffb_11e7_998c_8ff3606768aa" class="row_heading level0 row2" >15-19</th> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow2_col0" class="data row2 col0" >$2.90</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow2_col1" class="data row2 col1" >$4.08</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow2_col2" class="data row2 col2" >$289.88</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow2_col3" class="data row2 col3" >100</td> 
    </tr>    <tr> 
        <th id="T_5b073df8_8ffb_11e7_998c_8ff3606768aa" class="row_heading level0 row3" >20-24</th> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow3_col0" class="data row3 col0" >$2.96</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow3_col1" class="data row3 col1" >$5.89</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow3_col2" class="data row3 col2" >$765.69</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow3_col3" class="data row3 col3" >259</td> 
    </tr>    <tr> 
        <th id="T_5b073df8_8ffb_11e7_998c_8ff3606768aa" class="row_heading level0 row4" >25-29</th> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow4_col0" class="data row4 col0" >$3.03</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow4_col1" class="data row4 col1" >$4.12</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow4_col2" class="data row4 col2" >$263.53</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow4_col3" class="data row4 col3" >87</td> 
    </tr>    <tr> 
        <th id="T_5b073df8_8ffb_11e7_998c_8ff3606768aa" class="row_heading level0 row5" >30-34</th> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow5_col0" class="data row5 col0" >$3.25</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow5_col1" class="data row5 col1" >$3.55</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow5_col2" class="data row5 col2" >$152.60</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow5_col3" class="data row5 col3" >47</td> 
    </tr>    <tr> 
        <th id="T_5b073df8_8ffb_11e7_998c_8ff3606768aa" class="row_heading level0 row6" >35-39</th> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow6_col0" class="data row6 col0" >$2.91</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow6_col1" class="data row6 col1" >$3.28</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow6_col2" class="data row6 col2" >$78.65</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow6_col3" class="data row6 col3" >27</td> 
    </tr>    <tr> 
        <th id="T_5b073df8_8ffb_11e7_998c_8ff3606768aa" class="row_heading level0 row7" >40+</th> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow7_col0" class="data row7 col0" >$3.15</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow7_col1" class="data row7 col1" >$3.15</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow7_col2" class="data row7 col2" >$31.53</td> 
        <td id="T_5b073df8_8ffb_11e7_998c_8ff3606768aarow7_col3" class="data row7 col3" >10</td> 
    </tr></tbody> 
</table> 



# Top Spenders


```python
group_SN = file_original.groupby("SN")
group_SN.head()
data = pd.DataFrame({"Purchase Count":group_SN["Item ID"].count(),
"AveragePurchasePrice":np.round((group_SN["Item ID"].count())/((group_SN["Item ID"].count())*(group_SN["Price"].sum()))*100,2),
                    "TotalPurchaseValue":(group_SN["Item ID"].count())*(group_SN["Price"].sum())}).sort_values("TotalPurchaseValue", ascending=False).head(5)

    

data.style.format({"AveragePurchasePrice":"${:.2f}","TotalPurchaseValue":"${:.2f}"})

```




<style  type="text/css" >
</style>  
<table id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aa" > 
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
        <th id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aa" class="row_heading level0 row0" >Undirrala66</th> 
        <td id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aarow0_col0" class="data row0 col0" >$5.86</td> 
        <td id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aarow0_col1" class="data row0 col1" >5</td> 
        <td id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aarow0_col2" class="data row0 col2" >$85.30</td> 
    </tr>    <tr> 
        <th id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aa" class="row_heading level0 row1" >Saedue76</th> 
        <td id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aarow1_col0" class="data row1 col0" >$7.37</td> 
        <td id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aarow1_col1" class="data row1 col1" >4</td> 
        <td id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aarow1_col2" class="data row1 col2" >$54.24</td> 
    </tr>    <tr> 
        <th id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aa" class="row_heading level0 row2" >Mindimnya67</th> 
        <td id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aarow2_col0" class="data row2 col0" >$7.85</td> 
        <td id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aarow2_col1" class="data row2 col1" >4</td> 
        <td id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aarow2_col2" class="data row2 col2" >$50.96</td> 
    </tr>    <tr> 
        <th id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aa" class="row_heading level0 row3" >Sondastan54</th> 
        <td id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aarow3_col0" class="data row3 col0" >$9.77</td> 
        <td id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aarow3_col1" class="data row3 col1" >4</td> 
        <td id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aarow3_col2" class="data row3 col2" >$40.96</td> 
    </tr>    <tr> 
        <th id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aa" class="row_heading level0 row4" >Qarwen67</th> 
        <td id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aarow4_col0" class="data row4 col0" >$10.03</td> 
        <td id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aarow4_col1" class="data row4 col1" >4</td> 
        <td id="T_5b0e6ecc_8ffb_11e7_bc1c_8ff3606768aarow4_col2" class="data row4 col2" >$39.88</td> 
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
<table id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aa" > 
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
        <th id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aa" class="row_heading level0 row0" >39</th> 
        <th id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aa" class="row_heading level1 row0" >Betrayal, Whisper of Grieving Widows</th> 
        <td id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aarow0_col0" class="data row0 col0" >$2.35</td> 
        <td id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aarow0_col1" class="data row0 col1" >11</td> 
        <td id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aarow0_col2" class="data row0 col2" >$25.85</td> 
    </tr>    <tr> 
        <th id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aa" class="row_heading level0 row1" >84</th> 
        <th id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aa" class="row_heading level1 row1" >Arcane Gem</th> 
        <td id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aarow1_col0" class="data row1 col0" >$2.23</td> 
        <td id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aarow1_col1" class="data row1 col1" >10</td> 
        <td id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aarow1_col2" class="data row1 col2" >$22.30</td> 
    </tr>    <tr> 
        <th id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aa" class="row_heading level0 row2" >31</th> 
        <th id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aa" class="row_heading level1 row2" >Trickster</th> 
        <td id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aarow2_col0" class="data row2 col0" >$2.07</td> 
        <td id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aarow2_col1" class="data row2 col1" >9</td> 
        <td id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aarow2_col2" class="data row2 col2" >$18.63</td> 
    </tr>    <tr> 
        <th id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aa" class="row_heading level0 row3" >175</th> 
        <th id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aa" class="row_heading level1 row3" >Woeful Adamantite Claymore</th> 
        <td id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aarow3_col0" class="data row3 col0" >$1.24</td> 
        <td id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aarow3_col1" class="data row3 col1" >9</td> 
        <td id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aarow3_col2" class="data row3 col2" >$11.16</td> 
    </tr>    <tr> 
        <th id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aa" class="row_heading level0 row4" >13</th> 
        <th id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aa" class="row_heading level1 row4" >Serenity</th> 
        <td id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aarow4_col0" class="data row4 col0" >$1.49</td> 
        <td id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aarow4_col1" class="data row4 col1" >9</td> 
        <td id="T_5b12a3f0_8ffb_11e7_9291_8ff3606768aarow4_col2" class="data row4 col2" >$13.41</td> 
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
<table id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aa" > 
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
        <th id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aa" class="row_heading level0 row0" >34</th> 
        <th id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aa" class="row_heading level1 row0" >Retribution Axe</th> 
        <td id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aarow0_col0" class="data row0 col0" >$4.14</td> 
        <td id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aarow0_col1" class="data row0 col1" >9</td> 
        <td id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aarow0_col2" class="data row0 col2" >$37.26</td> 
    </tr>    <tr> 
        <th id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aa" class="row_heading level0 row1" >115</th> 
        <th id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aa" class="row_heading level1 row1" >Spectral Diamond Doomblade</th> 
        <td id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aarow1_col0" class="data row1 col0" >$4.25</td> 
        <td id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aarow1_col1" class="data row1 col1" >7</td> 
        <td id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aarow1_col2" class="data row1 col2" >$29.75</td> 
    </tr>    <tr> 
        <th id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aa" class="row_heading level0 row2" >32</th> 
        <th id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aa" class="row_heading level1 row2" >Orenmir</th> 
        <td id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aarow2_col0" class="data row2 col0" >$4.95</td> 
        <td id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aarow2_col1" class="data row2 col1" >6</td> 
        <td id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aarow2_col2" class="data row2 col2" >$29.70</td> 
    </tr>    <tr> 
        <th id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aa" class="row_heading level0 row3" >103</th> 
        <th id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aa" class="row_heading level1 row3" >Singed Scalpel</th> 
        <td id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aarow3_col0" class="data row3 col0" >$4.87</td> 
        <td id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aarow3_col1" class="data row3 col1" >6</td> 
        <td id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aarow3_col2" class="data row3 col2" >$29.22</td> 
    </tr>    <tr> 
        <th id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aa" class="row_heading level0 row4" >107</th> 
        <th id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aa" class="row_heading level1 row4" >Splitter, Foe Of Subtlety</th> 
        <td id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aarow4_col0" class="data row4 col0" >$3.61</td> 
        <td id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aarow4_col1" class="data row4 col1" >8</td> 
        <td id="T_5b1cbcde_8ffb_11e7_b030_8ff3606768aarow4_col2" class="data row4 col2" >$28.88</td> 
    </tr></tbody> 
</table> 




```python

```


```python

```
