
# Pycity Schools Analysis

## ObservedTrend1: Overallpassing score of district  is more than 70%
## ObserbedTrend2:Smaller school size have more passing score than others
## Observedtrend3:Chatter schools  have more passing score than District 



```python
import pandas as pd
import numpy as np
```


```python
file="schools_complete.csv"
file1="students_complete.csv"
student_df=pd.read_csv(file1)
school_df=pd.read_csv(file)
student_df.head()
school_df.head()
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
      <th>School ID</th>
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
  </tbody>
</table>
</div>




```python
 school_df=school_df.rename(columns={"name":"SchoolName"})
school_df=school_df.rename(columns={"size":"School Size"})
school_df
student_df=student_df.rename(columns={"school":"SchoolName"})

student_df["MathPassed"]= student_df['math_score']>=70
student_df["ReadingPassed"]= student_df['reading_score']>=70

student_df.head()
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
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>SchoolName</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>MathPassed</th>
      <th>ReadingPassed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
      <td>True</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>




```python

```


```python
 merged_df=school_df.merge(student_df,how='outer',on='SchoolName')
   # file_original =  file_original.drop_duplicates(subset=None, keep='first', inplace=False)
mergerd_df=merged_df.drop_duplicates(subset=None,keep='first',inplace=False) 
merged_df.head()
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
      <th>School ID</th>
      <th>SchoolName</th>
      <th>type</th>
      <th>School Size</th>
      <th>budget</th>
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>MathPassed</th>
      <th>ReadingPassed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>66</td>
      <td>79</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>94</td>
      <td>61</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>90</td>
      <td>60</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>67</td>
      <td>58</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>97</td>
      <td>84</td>
      <td>True</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



# District Summary


```python
district_df=pd.DataFrame({"TotalSchools":[merged_df['SchoolName'].nunique()],
                         "TotalStudents":[merged_df['Student ID'].nunique()],
                         "TotalBudget":[merged_df.groupby(['SchoolName'])['budget'].max().sum()],
                         "AverageMathScore":[student_df['reading_score'].mean()],
                          "AverageReadingScore":[student_df['reading_score'].mean()],
                         "%PassingMath":[student_df[student_df['math_score']>70].name.count() / student_df['name'].count() *100],
                         "%PassingReading":[student_df[student_df['reading_score']>70].name.count() / student_df['name'].count()*100]})
                                      
district_df["overallPassingRate"]=(district_df["%PassingMath"] + district_df["%PassingReading"]) /2
#district_df[columns="TotalSchools","TotalStudents","TotalBudget","AverageMathScore",
                    # "AverageReadingScore","%PassingMath","%PassingReading","overallPassingRate"]

district_df
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
      <th>%PassingMath</th>
      <th>%PassingReading</th>
      <th>AverageMathScore</th>
      <th>AverageReadingScore</th>
      <th>TotalBudget</th>
      <th>TotalSchools</th>
      <th>TotalStudents</th>
      <th>overallPassingRate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>72.392137</td>
      <td>82.971662</td>
      <td>81.87784</td>
      <td>81.87784</td>
      <td>24649428</td>
      <td>15</td>
      <td>39170</td>
      <td>77.681899</td>
    </tr>
  </tbody>
</table>
</div>



# SchoolSummary


```python
groupby_School=merged_df.groupby("SchoolName")
groupby_School_MathPassed = merged_df.groupby(["SchoolName","MathPassed"])

groupby_School_df=pd.DataFrame({"TotalStudents":groupby_School.name.count(),
               "SchoolType":groupby_School.type.max(),
               "TotalSchoolBudget":groupby_School.budget.max(),
               "PerStudentBudget":(groupby_School.budget.max())/ (groupby_School.name.count()),
               "AverageMathScore":groupby_School['math_score'].mean(),
               "AverageReadingScore":groupby_School['reading_score'].mean(),
             
               "%PassingMath":(groupby_School.apply(lambda g: g[g['MathPassed'] == True]).SchoolName.value_counts()/groupby_School['name'].count()) *100,
               "%PassingReading":(groupby_School.apply(lambda g: g[g['ReadingPassed'] == True]).SchoolName.value_counts()/groupby_School['name'].count()) *100})
    
              
groupby_School_df["overallPassingRate"]=(groupby_School_df["%PassingMath"] + groupby_School_df["%PassingReading"]) /2
groupby_School_df

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
      <th>%PassingMath</th>
      <th>%PassingReading</th>
      <th>AverageMathScore</th>
      <th>AverageReadingScore</th>
      <th>PerStudentBudget</th>
      <th>SchoolType</th>
      <th>TotalSchoolBudget</th>
      <th>TotalStudents</th>
      <th>overallPassingRate</th>
    </tr>
    <tr>
      <th>SchoolName</th>
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
      <th>Bailey High School</th>
      <td>66.680064</td>
      <td>81.933280</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>628.0</td>
      <td>District</td>
      <td>3124928</td>
      <td>4976</td>
      <td>74.306672</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>582.0</td>
      <td>Charter</td>
      <td>1081356</td>
      <td>1858</td>
      <td>95.586652</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>639.0</td>
      <td>District</td>
      <td>1884411</td>
      <td>2949</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>644.0</td>
      <td>District</td>
      <td>1763916</td>
      <td>2739</td>
      <td>73.804308</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>625.0</td>
      <td>Charter</td>
      <td>917500</td>
      <td>1468</td>
      <td>95.265668</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>66.752967</td>
      <td>80.862999</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>652.0</td>
      <td>District</td>
      <td>3022020</td>
      <td>4635</td>
      <td>73.807983</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>92.505855</td>
      <td>96.252927</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>581.0</td>
      <td>Charter</td>
      <td>248087</td>
      <td>427</td>
      <td>94.379391</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>65.683922</td>
      <td>81.316421</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>655.0</td>
      <td>District</td>
      <td>1910635</td>
      <td>2917</td>
      <td>73.500171</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>66.057551</td>
      <td>81.222432</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>650.0</td>
      <td>District</td>
      <td>3094650</td>
      <td>4761</td>
      <td>73.639992</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>94.594595</td>
      <td>95.945946</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>609.0</td>
      <td>Charter</td>
      <td>585858</td>
      <td>962</td>
      <td>95.270270</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>637.0</td>
      <td>District</td>
      <td>2547363</td>
      <td>3999</td>
      <td>73.293323</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>93.867121</td>
      <td>95.854628</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>600.0</td>
      <td>Charter</td>
      <td>1056600</td>
      <td>1761</td>
      <td>94.860875</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>93.272171</td>
      <td>97.308869</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>638.0</td>
      <td>Charter</td>
      <td>1043130</td>
      <td>1635</td>
      <td>95.290520</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>93.867718</td>
      <td>96.539641</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>578.0</td>
      <td>Charter</td>
      <td>1319574</td>
      <td>2283</td>
      <td>95.203679</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>93.333333</td>
      <td>96.611111</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>583.0</td>
      <td>Charter</td>
      <td>1049400</td>
      <td>1800</td>
      <td>94.972222</td>
    </tr>
  </tbody>
</table>
</div>



# TopPerformingSchools(ByPassingRate)


```python
 groupby_School_df.sort_values(by="overallPassingRate", ascending=False).head(5)
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
      <th>%PassingMath</th>
      <th>%PassingReading</th>
      <th>AverageMathScore</th>
      <th>AverageReadingScore</th>
      <th>PerStudentBudget</th>
      <th>SchoolType</th>
      <th>TotalSchoolBudget</th>
      <th>TotalStudents</th>
      <th>overallPassingRate</th>
    </tr>
    <tr>
      <th>SchoolName</th>
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
      <th>Cabrera High School</th>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>582.0</td>
      <td>Charter</td>
      <td>1081356</td>
      <td>1858</td>
      <td>95.586652</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>93.272171</td>
      <td>97.308869</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>638.0</td>
      <td>Charter</td>
      <td>1043130</td>
      <td>1635</td>
      <td>95.290520</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>94.594595</td>
      <td>95.945946</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>609.0</td>
      <td>Charter</td>
      <td>585858</td>
      <td>962</td>
      <td>95.270270</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>625.0</td>
      <td>Charter</td>
      <td>917500</td>
      <td>1468</td>
      <td>95.265668</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>93.867718</td>
      <td>96.539641</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>578.0</td>
      <td>Charter</td>
      <td>1319574</td>
      <td>2283</td>
      <td>95.203679</td>
    </tr>
  </tbody>
</table>
</div>



# BottomPerformingSchools(ByPassingRate)


```python
groupby_School_df.sort_values(by="overallPassingRate", ascending=True).head(5)
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
      <th>%PassingMath</th>
      <th>%PassingReading</th>
      <th>AverageMathScore</th>
      <th>AverageReadingScore</th>
      <th>PerStudentBudget</th>
      <th>SchoolType</th>
      <th>TotalSchoolBudget</th>
      <th>TotalStudents</th>
      <th>overallPassingRate</th>
    </tr>
    <tr>
      <th>SchoolName</th>
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
      <th>Rodriguez High School</th>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>637.0</td>
      <td>District</td>
      <td>2547363</td>
      <td>3999</td>
      <td>73.293323</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>639.0</td>
      <td>District</td>
      <td>1884411</td>
      <td>2949</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>65.683922</td>
      <td>81.316421</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>655.0</td>
      <td>District</td>
      <td>1910635</td>
      <td>2917</td>
      <td>73.500171</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>66.057551</td>
      <td>81.222432</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>650.0</td>
      <td>District</td>
      <td>3094650</td>
      <td>4761</td>
      <td>73.639992</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>644.0</td>
      <td>District</td>
      <td>1763916</td>
      <td>2739</td>
      <td>73.804308</td>
    </tr>
  </tbody>
</table>
</div>



# MathScore byGrade


```python
math_score_by_grade_df=pd.DataFrame({"9th":
                                merged_df[merged_df['grade'] == "9th"].groupby('SchoolName')['math_score'].mean(),
"10th":merged_df[merged_df['grade'] == "10th"].groupby('SchoolName')['math_score'].mean(),
"11th":merged_df[merged_df['grade'] == "11th"].groupby('SchoolName')['math_score'].mean(),
"12th":merged_df[merged_df['grade'] == "12th"].groupby('SchoolName')['math_score'].mean()})
math_score_by_grade_df
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
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
      <th>9th</th>
    </tr>
    <tr>
      <th>SchoolName</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>76.996772</td>
      <td>77.515588</td>
      <td>76.492218</td>
      <td>77.083676</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.154506</td>
      <td>82.765560</td>
      <td>83.277487</td>
      <td>83.094697</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.539974</td>
      <td>76.884344</td>
      <td>77.151369</td>
      <td>76.403037</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.672316</td>
      <td>76.918058</td>
      <td>76.179963</td>
      <td>77.361345</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>84.229064</td>
      <td>83.842105</td>
      <td>83.356164</td>
      <td>82.044010</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>77.337408</td>
      <td>77.136029</td>
      <td>77.186567</td>
      <td>77.438495</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.429825</td>
      <td>85.000000</td>
      <td>82.855422</td>
      <td>83.787402</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>75.908735</td>
      <td>76.446602</td>
      <td>77.225641</td>
      <td>77.027251</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>76.691117</td>
      <td>77.491653</td>
      <td>76.863248</td>
      <td>77.187857</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.372000</td>
      <td>84.328125</td>
      <td>84.121547</td>
      <td>83.625455</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>76.612500</td>
      <td>76.395626</td>
      <td>77.690748</td>
      <td>76.859966</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>82.917411</td>
      <td>83.383495</td>
      <td>83.778976</td>
      <td>83.420755</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.087886</td>
      <td>83.498795</td>
      <td>83.497041</td>
      <td>83.590022</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.724422</td>
      <td>83.195326</td>
      <td>83.035794</td>
      <td>83.085578</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>84.010288</td>
      <td>83.836782</td>
      <td>83.644986</td>
      <td>83.264706</td>
    </tr>
  </tbody>
</table>
</div>



# Reading Score By Grade


```python
math_score_by_grade_df=pd.DataFrame({"9th":
                                merged_df[merged_df['grade'] == "9th"].groupby('SchoolName')['reading_score'].mean(),
"10th":merged_df[merged_df['grade'] == "10th"].groupby('SchoolName')['reading_score'].mean(),
"11th":merged_df[merged_df['grade'] == "11th"].groupby('SchoolName')['reading_score'].mean(),
"12th":merged_df[merged_df['grade'] == "12th"].groupby('SchoolName')['reading_score'].mean()})
math_score_by_grade_df
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
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
      <th>9th</th>
    </tr>
    <tr>
      <th>SchoolName</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>80.907183</td>
      <td>80.945643</td>
      <td>80.912451</td>
      <td>81.303155</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>84.253219</td>
      <td>83.788382</td>
      <td>84.287958</td>
      <td>83.676136</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>81.408912</td>
      <td>80.640339</td>
      <td>81.384863</td>
      <td>81.198598</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>81.262712</td>
      <td>80.403642</td>
      <td>80.662338</td>
      <td>80.632653</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>83.706897</td>
      <td>84.288089</td>
      <td>84.013699</td>
      <td>83.369193</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>80.660147</td>
      <td>81.396140</td>
      <td>80.857143</td>
      <td>80.866860</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.324561</td>
      <td>83.815534</td>
      <td>84.698795</td>
      <td>83.677165</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>81.512386</td>
      <td>81.417476</td>
      <td>80.305983</td>
      <td>81.290284</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>80.773431</td>
      <td>80.616027</td>
      <td>81.227564</td>
      <td>81.260714</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.612000</td>
      <td>84.335938</td>
      <td>84.591160</td>
      <td>83.807273</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>80.629808</td>
      <td>80.864811</td>
      <td>80.376426</td>
      <td>80.993127</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>83.441964</td>
      <td>84.373786</td>
      <td>82.781671</td>
      <td>84.122642</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>84.254157</td>
      <td>83.585542</td>
      <td>83.831361</td>
      <td>83.728850</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>84.021452</td>
      <td>83.764608</td>
      <td>84.317673</td>
      <td>83.939778</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.812757</td>
      <td>84.156322</td>
      <td>84.073171</td>
      <td>83.833333</td>
    </tr>
  </tbody>
</table>
</div>



# Scores By School Size


```python
school_bins=[0,1000,2000,5000]
names=["  Small(<1000)"," Medium(1000-2000)","Large(2000-5000)"]
p=pd.cut(merged_df["School Size"], bins=school_bins , labels=names)
p1=pd.cut(filtered[merged_df['math_score'] >= 70]["School Size"], bins=school_bins , labels=names)
p2=pd.cut(filtered[merged_df['reading_score'] >= 70]["School Size"], bins=school_bins , labels=names)
scoreBySchoolSize_df=pd.DataFrame({"Average math Score":merged_df.groupby(p).math_score.mean(),
                                  "AverageReadingScore":merged_df.groupby(p).reading_score.mean(),
                                  "%PassingMath":(p1.value_counts()/p.value_counts())*100,
                                  "%PassingReading":(p2.value_counts()/p.value_counts())*100})
scoreBySchoolSize_df.sort_index(ascending=True)
```

    C:\Users\nagalakshmi\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:4: UserWarning: Boolean Series key will be reindexed to match DataFrame index.
    C:\Users\nagalakshmi\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:5: UserWarning: Boolean Series key will be reindexed to match DataFrame index.
    




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
      <th>%PassingMath</th>
      <th>%PassingReading</th>
      <th>Average math Score</th>
      <th>AverageReadingScore</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Small(&lt;1000)</th>
      <td>93.952484</td>
      <td>90.136789</td>
      <td>83.828654</td>
      <td>83.974082</td>
    </tr>
    <tr>
      <th>Medium(1000-2000)</th>
      <td>93.616522</td>
      <td>90.624267</td>
      <td>83.372682</td>
      <td>83.867989</td>
    </tr>
    <tr>
      <th>Large(2000-5000)</th>
      <td>68.652380</td>
      <td>56.574046</td>
      <td>77.477597</td>
      <td>81.198674</td>
    </tr>
  </tbody>
</table>
</div>



# ScoresBySchoolSpending


```python
budget_bins=[0,1000000,2000000,3000000,4000000]
budget_names=[" <$1000000","$1000000-200000","$200000-3000000",">$300000"]
budgetGroup=pd.cut(merged_df["budget"], bins=budget_bins , labels=budget_names)
groupb = merged_df.groupby(budgetGroup)

p1=pd.cut(merged_df[merged_df['math_score'] >= 70]["budget"], bins=budget_bins , labels=budget_names)
p2=pd.cut(merged_df[merged_df['reading_score'] >= 70]["budget"], bins=budget_bins , labels=budget_names)
scoreBySchoolSize_df=pd.DataFrame({"Average Math Score":groupb.math_score.mean(),
                                  "Average Reading Score":groupb.reading_score.mean(),
                                  "%PassingMath":(p1.value_counts()/budgetGroup.value_counts())*100,
                                  "%PassingReading":(p2.value_counts()/budgetGroup.value_counts())*100})
scoreBySchoolSize_df#.#sort_values(by ="budget")
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
      <th>%PassingMath</th>
      <th>%PassingReading</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;$1000000</th>
      <td>93.664683</td>
      <td>96.604830</td>
      <td>83.583479</td>
      <td>83.893245</td>
    </tr>
    <tr>
      <th>$1000000-200000</th>
      <td>80.721213</td>
      <td>88.897559</td>
      <td>80.213577</td>
      <td>82.529094</td>
    </tr>
    <tr>
      <th>$200000-3000000</th>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>76.842711</td>
      <td>80.744686</td>
    </tr>
    <tr>
      <th>&gt;$300000</th>
      <td>66.497356</td>
      <td>81.352630</td>
      <td>77.134219</td>
      <td>80.979474</td>
    </tr>
  </tbody>
</table>
</div>



# Scores By SchoolsType


```python
group_type_df=merged_df.groupby("type")
#group_type.head()
group_type_df = pd.DataFrame({"AveragemathScore":group_type_df.math_score.mean(),
                              "AverageReadingScore":group_type_df.reading_score.mean(),
                              "%PassingMath":(group_type_df.apply(lambda g: g[g['MathPassed'] == True]).type.value_counts()/group_type_df['name'].count()) *100,
                             "%PassingReading":(group_type_df.apply(lambda g: g[g['ReadingPassed'] == True]).type.value_counts()/group_type_df['name'].count()) *100
                             })
group_type_df["overallPassingRate"]=(group_type_df["%PassingMath"] + group_type_df["%PassingReading"])/2
group_type_df                                                                               
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
      <th>%PassingMath</th>
      <th>%PassingReading</th>
      <th>AverageReadingScore</th>
      <th>AveragemathScore</th>
      <th>overallPassingRate</th>
    </tr>
    <tr>
      <th>type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Charter</th>
      <td>93.701821</td>
      <td>96.645891</td>
      <td>83.902821</td>
      <td>83.406183</td>
      <td>95.173856</td>
    </tr>
    <tr>
      <th>District</th>
      <td>66.518387</td>
      <td>80.905249</td>
      <td>80.962485</td>
      <td>76.987026</td>
      <td>73.711818</td>
    </tr>
  </tbody>
</table>
</div>


