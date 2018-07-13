
### Heroes Of Pymoli Data Analysis
* Of the 1163 active players, the vast majority are male (84%). There also exists, a smaller, but notable proportion of female players (14%).

* Our peak age demographic falls between 20-24 (44.8%) with secondary groups falling between 15-19 (18.60%) and 25-29 (13.4%).  
-----

### Note
* Instructions have been included for each segment. You do not have to follow them exactly, but they are included to help you think through the steps.


```python
# Dependencies and Setup
import pandas as pd
import numpy as np

# Raw data file
file_to_load = "Resources/purchase_data.csv"

# Read purchasing file and store into pandas data frame
purchase_data = pd.read_csv(file_to_load)
purchase_data.head()
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
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>$3.53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>$1.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>$4.88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>$3.27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>$1.44</td>
    </tr>
  </tbody>
</table>
</div>



## Player Count

* Display the total number of players



```python
purchase_data.columns
```




    Index(['Purchase ID', 'SN', 'Age', 'Gender', 'Item ID', 'Item Name', 'Price'], dtype='object')




```python

SN = purchase_data['SN'].nunique()
SN
```




    576




```python
total_player_count = pd.DataFrame({'Total Players': [SN]}, columns= ["Total Players"])
total_player_count.head()
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
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>576</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Total)

* Run basic calculations to obtain number of unique items, average price, etc.


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame



```python
# Number of Unique Items
# Average Purchase Price
# Total Number of Purchases
#Total Revenue

```


```python
unique_items = purchase_data["Item ID"].nunique()
av_price = purchase_data["Price"].mean()
total_purchases = purchase_data["Item Name"].count()
total_revenue = purchase_data["Price"].sum()

summary_purchasing = pd.DataFrame({"Number of Unique Items": [unique_items], 
                                    "Average Price": [av_price], 
                                    "Number of Purchases": [total_purchases], 
                                    "Total Revenue": [total_revenue]}, 
                                  columns = ["Number of Unique Items", "Average Price", "Number of Purchases", "Total Revenue"])

summary_purchasing.style.format({
    'Average Price': '${:.2f}'.format, 'Total Revenue': '${:.2f}'})

```




<style  type="text/css" >
</style>  
<table id="T_07901e68_86f1_11e8_a4b8_c49ded1446fe" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Number of Unique Items</th> 
        <th class="col_heading level0 col1" >Average Price</th> 
        <th class="col_heading level0 col2" >Number of Purchases</th> 
        <th class="col_heading level0 col3" >Total Revenue</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_07901e68_86f1_11e8_a4b8_c49ded1446felevel0_row0" class="row_heading level0 row0" >0</th> 
        <td id="T_07901e68_86f1_11e8_a4b8_c49ded1446ferow0_col0" class="data row0 col0" >183</td> 
        <td id="T_07901e68_86f1_11e8_a4b8_c49ded1446ferow0_col1" class="data row0 col1" >$3.05</td> 
        <td id="T_07901e68_86f1_11e8_a4b8_c49ded1446ferow0_col2" class="data row0 col2" >780</td> 
        <td id="T_07901e68_86f1_11e8_a4b8_c49ded1446ferow0_col3" class="data row0 col3" >$2379.77</td> 
    </tr></tbody> 
</table> 



## Gender Demographics

* Run basic calculations to obtain number of unique items, average price, etc.


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame



```python
# Percentage and Count of Male Players
# Percentage and Count of Female Players
# Percentage and Count of Other / Non-Disclosed
```


```python
total_gender = purchase_data["Gender"].count()
male = purchase_data["Gender"].value_counts()['Male']
female = purchase_data["Gender"].value_counts()['Female']
non_gender_specific = total_gender - male - female

male_percent = (male/total_gender) * 100
#male_percent = male_percent.map("${:.2f}".format)
female_percent = (female/total_gender) * 100
non_gender_specific_percent = (non_gender_specific/total_gender) * 100
#print(
#    f" % Male: {male_percent}\n % Female: {female_percent}\n % non_specifc: {non_gender_specific}")
```


```python
gender_summary_table = pd.DataFrame({'Percentage of Players': [male_percent, female_percent, non_gender_specific_percent],
                              'Total Count': [male, female, non_gender_specific]}, 
                              index=['Male', 'Female', 'Other/Non-disclosed'])
gender_summary_table
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
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>$83.59</td>
      <td>652</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>$14.49</td>
      <td>113</td>
    </tr>
    <tr>
      <th>Other/Non-disclosed</th>
      <td>$1.92</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>




```python
#gender_summary_table([male_percent] = gender_summary_table[male_percent].map(
#    "{:.2f}%".format)
gender_summary_table.style.format({
    'Percentage of Players': '{:,.2f}'.format})
```




<style  type="text/css" >
</style>  
<table id="T_079a0162_86f1_11e8_98fb_c49ded1446fe" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Percentage of Players</th> 
        <th class="col_heading level0 col1" >Total Count</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_079a0162_86f1_11e8_98fb_c49ded1446felevel0_row0" class="row_heading level0 row0" >Male</th> 
        <td id="T_079a0162_86f1_11e8_98fb_c49ded1446ferow0_col0" class="data row0 col0" >83.59</td> 
        <td id="T_079a0162_86f1_11e8_98fb_c49ded1446ferow0_col1" class="data row0 col1" >652</td> 
    </tr>    <tr> 
        <th id="T_079a0162_86f1_11e8_98fb_c49ded1446felevel0_row1" class="row_heading level0 row1" >Female</th> 
        <td id="T_079a0162_86f1_11e8_98fb_c49ded1446ferow1_col0" class="data row1 col0" >14.49</td> 
        <td id="T_079a0162_86f1_11e8_98fb_c49ded1446ferow1_col1" class="data row1 col1" >113</td> 
    </tr>    <tr> 
        <th id="T_079a0162_86f1_11e8_98fb_c49ded1446felevel0_row2" class="row_heading level0 row2" >Other/Non-disclosed</th> 
        <td id="T_079a0162_86f1_11e8_98fb_c49ded1446ferow2_col0" class="data row2 col0" >1.92</td> 
        <td id="T_079a0162_86f1_11e8_98fb_c49ded1446ferow2_col1" class="data row2 col1" >15</td> 
    </tr></tbody> 
</table> 




```python



```


## Purchasing Analysis (Gender)

* Run basic calculations to obtain purchase count, avg. purchase price, etc. by gender


* For normalized purchasing, divide total purchase value by purchase count, by gender


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
#The below each broken by gender
#     Purchase Count
#     Average Purchase Price
#     Total Purchase Value
#     Normalized Totals
```


```python
purchase_count_female = purchase_data[purchase_data["Gender"] == "Female"]['Price'].count()
purchase_count_male = purchase_data[purchase_data["Gender"] == "Male"]['Price'].count()
purchase_count_other = total_purchases - purchase_count_female - purchase_count_male

ave_female_purchase_price = purchase_data[purchase_data["Gender"] == "Female"]['Price'].mean()
ave_male_purchase_price = purchase_data[purchase_data["Gender"] == "Male"]['Price'].mean()
ave_other_purchase_price = purchase_data[purchase_data["Gender"] == 'non_gender_specific']["Price"].mean()
total_purchases_female = purchase_data[purchase_data["Gender"] == "Female"]["Price"].sum()
total_purchases_male = purchase_data[purchase_data["Gender"] == "Male"]["Price"].sum()
total_purchases_other = purchase_data[purchase_data["Gender"] == "non_gender_specific"]["Price"].sum()
```


```python
total_female_norm = total_purchases_female/female
total_male_norm = total_purchases_male/male
total_other_norm = total_purchases_other/non_gender_specific
```


```python
summary_gender_purchases = pd.DataFrame({'Gender': ["Female", "Male", "Other/Non-Disclosed"], 
                                         'Purchase Count': [purchase_count_female, purchase_count_male, purchase_count_other], 
                                        'Average Purchase Price': [ave_female_purchase_price, ave_male_purchase_price, ave_other_purchase_price],
                                        'Total Purchase Value': [total_purchases_female, total_purchases_male, total_purchases_other], 
                                        'Normalized Totals': [total_female_norm, total_male_norm, total_other_norm]}, 
                                       columns = ["Gender", "Purchase Count", "Average Purchase Price", "Total Purchase Value", "Normalized Totals"]) 
                                        

total_gender_totals = summary_gender_purchases.set_index("Gender")


```


```python
total_gender_totals.style.format({
    'Average Purchase Price': '${:.2f}'.format, 'Total Purchase Value': '${:.2f}'.format, 'Normalized Totals': '${:.2f}'.format})

```




<style  type="text/css" >
</style>  
<table id="T_07a6ca5e_86f1_11e8_8301_c49ded1446fe" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Purchase Count</th> 
        <th class="col_heading level0 col1" >Average Purchase Price</th> 
        <th class="col_heading level0 col2" >Total Purchase Value</th> 
        <th class="col_heading level0 col3" >Normalized Totals</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Gender</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_07a6ca5e_86f1_11e8_8301_c49ded1446felevel0_row0" class="row_heading level0 row0" >Female</th> 
        <td id="T_07a6ca5e_86f1_11e8_8301_c49ded1446ferow0_col0" class="data row0 col0" >113</td> 
        <td id="T_07a6ca5e_86f1_11e8_8301_c49ded1446ferow0_col1" class="data row0 col1" >$3.20</td> 
        <td id="T_07a6ca5e_86f1_11e8_8301_c49ded1446ferow0_col2" class="data row0 col2" >$361.94</td> 
        <td id="T_07a6ca5e_86f1_11e8_8301_c49ded1446ferow0_col3" class="data row0 col3" >$3.20</td> 
    </tr>    <tr> 
        <th id="T_07a6ca5e_86f1_11e8_8301_c49ded1446felevel0_row1" class="row_heading level0 row1" >Male</th> 
        <td id="T_07a6ca5e_86f1_11e8_8301_c49ded1446ferow1_col0" class="data row1 col0" >652</td> 
        <td id="T_07a6ca5e_86f1_11e8_8301_c49ded1446ferow1_col1" class="data row1 col1" >$3.02</td> 
        <td id="T_07a6ca5e_86f1_11e8_8301_c49ded1446ferow1_col2" class="data row1 col2" >$1967.64</td> 
        <td id="T_07a6ca5e_86f1_11e8_8301_c49ded1446ferow1_col3" class="data row1 col3" >$3.02</td> 
    </tr>    <tr> 
        <th id="T_07a6ca5e_86f1_11e8_8301_c49ded1446felevel0_row2" class="row_heading level0 row2" >Other/Non-Disclosed</th> 
        <td id="T_07a6ca5e_86f1_11e8_8301_c49ded1446ferow2_col0" class="data row2 col0" >15</td> 
        <td id="T_07a6ca5e_86f1_11e8_8301_c49ded1446ferow2_col1" class="data row2 col1" >$nan</td> 
        <td id="T_07a6ca5e_86f1_11e8_8301_c49ded1446ferow2_col2" class="data row2 col2" >$0.00</td> 
        <td id="T_07a6ca5e_86f1_11e8_8301_c49ded1446ferow2_col3" class="data row2 col3" >$0.00</td> 
    </tr></tbody> 
</table> 




```python


```

## Age Demographics

* Establish bins for ages


* Categorize the existing players using the age bins. Hint: use pd.cut()


* Calculate the numbers and percentages by age group


* Create a summary data frame to hold the results


* Optional: round the percentage column to two decimal points


* Display Age Demographics Table



```python
# The below each broken into bins of 4 years (i.e. <10, 10-14, 15-19, etc.)
#     Purchase Count
#     Average Purchase Price
#     Total Purchase Value
#     Normalized Totals
```


```python
# Establish bins for ages
age_bins = [0, 9.90, 14.90, 19.90, 24.90, 29.90, 34.90, 39.90, 99999]
group_names = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"]

```


```python
pd.cut(purchase_data["Age"], age_bins, labels=group_names).head()
```




    0    20-24
    1      40+
    2    20-24
    3    20-24
    4    20-24
    Name: Age, dtype: category
    Categories (8, object): [<10 < 10-14 < 15-19 < 20-24 < 25-29 < 30-34 < 35-39 < 40+]




```python
purchase_data[""] = pd.cut(purchase_data["Age"], age_bins, labels=group_names)
purchase_data.head()
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
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>$3.53</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>$1.56</td>
      <td>40+</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>$4.88</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>$3.27</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>$1.44</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Create purchase groupby Total Count
purchase_group = purchase_data.groupby("")




#total_purchase_group = pd.DataFrame(purchase_group["SN"].count())
#total_purchase_group.head()

# Find how many rows fall into each bin
#print(purchase_group["Item ID"].count())

total_purchase_group = purchase_group["Item ID"].count()
df_total_purchase_group = pd.DataFrame({"Total Count": total_purchase_group})
df_total_purchase_group
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
      <th>Total Count</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>23</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>28</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>136</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>365</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>101</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>73</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>41</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Get the average of each column within the GroupBy object

```


```python
# Get the average of each column within the GroupBy object
SN = purchase_data['SN'].nunique()

percentage_of_players = total_purchase_group/SN * 100
#percentage_of_players = purchase_group["Item ID"], total_count_age/SN * 100
#print(percentage_of_players["SN"].nunique()
      
      #/SN * 100


df_percentage_of_players = pd.DataFrame({"Percentage of Players": percentage_of_players})
df_percentage_of_players


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
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>$3.99</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>$4.86</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>$23.61</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>$63.37</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>$17.53</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>$12.67</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>$7.12</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>$2.26</td>
    </tr>
  </tbody>
</table>
</div>




```python
print(df_percentage_of_players, df_total_purchase_group)
```

           Percentage of Players
                                
    <10                    $3.99
    10-14                  $4.86
    15-19                 $23.61
    20-24                 $63.37
    25-29                 $17.53
    30-34                 $12.67
    35-39                  $7.12
    40+                    $2.26        Total Count
                      
    <10             23
    10-14           28
    15-19          136
    20-24          365
    25-29          101
    30-34           73
    35-39           41
    40+             13
    


```python
#df = [df_percentage_of_players, df_total_purchase_group]
#result = pd.merge(df_percentage_of_players, df_total_purchase_group, )
result = df_percentage_of_players.join(df_total_purchase_group)
result
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
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>$3.99</td>
      <td>23</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>$4.86</td>
      <td>28</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>$23.61</td>
      <td>136</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>$63.37</td>
      <td>365</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>$17.53</td>
      <td>101</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>$12.67</td>
      <td>73</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>$7.12</td>
      <td>41</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>$2.26</td>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>




```python
result.style.format({
    'Percentage of Players': '{:,.2f}'.format})
```




<style  type="text/css" >
</style>  
<table id="T_07c49dca_86f1_11e8_a0ba_c49ded1446fe" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Percentage of Players</th> 
        <th class="col_heading level0 col1" >Total Count</th> 
    </tr>    <tr> 
        <th class="index_name level0" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_07c49dca_86f1_11e8_a0ba_c49ded1446felevel0_row0" class="row_heading level0 row0" ><10</th> 
        <td id="T_07c49dca_86f1_11e8_a0ba_c49ded1446ferow0_col0" class="data row0 col0" >3.99</td> 
        <td id="T_07c49dca_86f1_11e8_a0ba_c49ded1446ferow0_col1" class="data row0 col1" >23</td> 
    </tr>    <tr> 
        <th id="T_07c49dca_86f1_11e8_a0ba_c49ded1446felevel0_row1" class="row_heading level0 row1" >10-14</th> 
        <td id="T_07c49dca_86f1_11e8_a0ba_c49ded1446ferow1_col0" class="data row1 col0" >4.86</td> 
        <td id="T_07c49dca_86f1_11e8_a0ba_c49ded1446ferow1_col1" class="data row1 col1" >28</td> 
    </tr>    <tr> 
        <th id="T_07c49dca_86f1_11e8_a0ba_c49ded1446felevel0_row2" class="row_heading level0 row2" >15-19</th> 
        <td id="T_07c49dca_86f1_11e8_a0ba_c49ded1446ferow2_col0" class="data row2 col0" >23.61</td> 
        <td id="T_07c49dca_86f1_11e8_a0ba_c49ded1446ferow2_col1" class="data row2 col1" >136</td> 
    </tr>    <tr> 
        <th id="T_07c49dca_86f1_11e8_a0ba_c49ded1446felevel0_row3" class="row_heading level0 row3" >20-24</th> 
        <td id="T_07c49dca_86f1_11e8_a0ba_c49ded1446ferow3_col0" class="data row3 col0" >63.37</td> 
        <td id="T_07c49dca_86f1_11e8_a0ba_c49ded1446ferow3_col1" class="data row3 col1" >365</td> 
    </tr>    <tr> 
        <th id="T_07c49dca_86f1_11e8_a0ba_c49ded1446felevel0_row4" class="row_heading level0 row4" >25-29</th> 
        <td id="T_07c49dca_86f1_11e8_a0ba_c49ded1446ferow4_col0" class="data row4 col0" >17.53</td> 
        <td id="T_07c49dca_86f1_11e8_a0ba_c49ded1446ferow4_col1" class="data row4 col1" >101</td> 
    </tr>    <tr> 
        <th id="T_07c49dca_86f1_11e8_a0ba_c49ded1446felevel0_row5" class="row_heading level0 row5" >30-34</th> 
        <td id="T_07c49dca_86f1_11e8_a0ba_c49ded1446ferow5_col0" class="data row5 col0" >12.67</td> 
        <td id="T_07c49dca_86f1_11e8_a0ba_c49ded1446ferow5_col1" class="data row5 col1" >73</td> 
    </tr>    <tr> 
        <th id="T_07c49dca_86f1_11e8_a0ba_c49ded1446felevel0_row6" class="row_heading level0 row6" >35-39</th> 
        <td id="T_07c49dca_86f1_11e8_a0ba_c49ded1446ferow6_col0" class="data row6 col0" >7.12</td> 
        <td id="T_07c49dca_86f1_11e8_a0ba_c49ded1446ferow6_col1" class="data row6 col1" >41</td> 
    </tr>    <tr> 
        <th id="T_07c49dca_86f1_11e8_a0ba_c49ded1446felevel0_row7" class="row_heading level0 row7" >40+</th> 
        <td id="T_07c49dca_86f1_11e8_a0ba_c49ded1446ferow7_col0" class="data row7 col0" >2.26</td> 
        <td id="T_07c49dca_86f1_11e8_a0ba_c49ded1446ferow7_col1" class="data row7 col1" >13</td> 
    </tr></tbody> 
</table> 



## Purchasing Analysis (Age)

* Bin the purchase_data data frame by age


* Run basic calculations to obtain purchase count, avg. purchase price, etc. in the table below


* Calculate Normalized Purchasing


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
purchase_data.head()
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
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>$3.53</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>$1.56</td>
      <td>40+</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>$4.88</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>$3.27</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>$1.44</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
purchase_data["Price"].sum()
```




    2379.77




```python
purchase_data["Item Name"].nunique()
```




    179




```python
purchase_group = purchase_data.groupby("")
purchase_group.head(1)

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
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>$3.53</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>$1.56</td>
      <td>40+</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Itheria73</td>
      <td>36</td>
      <td>Male</td>
      <td>169</td>
      <td>Interrogator, Blood Blade of the Queen</td>
      <td>$2.18</td>
      <td>35-39</td>
    </tr>
    <tr>
      <th>19</th>
      <td>19</td>
      <td>Chamalo71</td>
      <td>30</td>
      <td>Male</td>
      <td>89</td>
      <td>Blazefury, Protector of Delusions</td>
      <td>$4.64</td>
      <td>30-34</td>
    </tr>
    <tr>
      <th>25</th>
      <td>25</td>
      <td>Lisirra87</td>
      <td>29</td>
      <td>Male</td>
      <td>178</td>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>$4.23</td>
      <td>25-29</td>
    </tr>
    <tr>
      <th>26</th>
      <td>26</td>
      <td>Lirtossa84</td>
      <td>11</td>
      <td>Male</td>
      <td>71</td>
      <td>Demise</td>
      <td>$1.61</td>
      <td>10-14</td>
    </tr>
    <tr>
      <th>27</th>
      <td>27</td>
      <td>Eusri44</td>
      <td>7</td>
      <td>Male</td>
      <td>96</td>
      <td>Blood-Forged Skeletal Spine</td>
      <td>$3.09</td>
      <td>&lt;10</td>
    </tr>
    <tr>
      <th>30</th>
      <td>30</td>
      <td>Idai61</td>
      <td>19</td>
      <td>Male</td>
      <td>140</td>
      <td>Striker</td>
      <td>$2.94</td>
      <td>15-19</td>
    </tr>
  </tbody>
</table>
</div>




```python
purchase_item_count = purchase_group["Item ID"].count()

purchase_data_count_df = pd.DataFrame({"Purchase Count": purchase_item_count})

purchase_data_count_df.head()
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
      <th>Purchase Count</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>23</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>28</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>136</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>365</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>101</td>
    </tr>
  </tbody>
</table>
</div>




```python
purchase_ave_purch_price = purchase_group["Price"].mean()
purchase_ave_purch_price_df = pd.DataFrame({"Average Purchase Price": purchase_ave_purch_price})

purchase_ave_purch_price_df
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
      <th>Average Purchase Price</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>$3.35</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>$2.96</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>$3.04</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>$3.05</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>$2.90</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>$2.93</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>$3.60</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>$2.94</td>
    </tr>
  </tbody>
</table>
</div>




```python
purchase_total_purch_price = purchase_group["Price"].sum()
purchase_total_purch_price_df = pd.DataFrame({"Total Purchase Value": purchase_total_purch_price})
purchase_total_purch_price_df
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
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>$77.13</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>$82.78</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>$412.89</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>$1,114.06</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>$293.00</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>$214.00</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>$147.67</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>$38.24</td>
    </tr>
  </tbody>
</table>
</div>




```python
ave_purch_price_norm = purchase_total_purch_price/purchase_item_count
ave_purch_price_norm_df = pd.DataFrame({"Normalized Totals": ave_purch_price_norm})

ave_purch_price_norm_df

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
      <th>Normalized Totals</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>$3.35</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>$2.96</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>$3.04</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>$3.05</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>$2.90</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>$2.93</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>$3.60</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>$2.94</td>
    </tr>
  </tbody>
</table>
</div>




```python
print(purchase_data_count_df, purchase_ave_purch_price_df, purchase_total_purch_price_df, ave_purch_price_norm_df)
```

           Purchase Count
                         
    <10                23
    10-14              28
    15-19             136
    20-24             365
    25-29             101
    30-34              73
    35-39              41
    40+                13        Average Purchase Price
                                 
    <10                     $3.35
    10-14                   $2.96
    15-19                   $3.04
    20-24                   $3.05
    25-29                   $2.90
    30-34                   $2.93
    35-39                   $3.60
    40+                     $2.94        Total Purchase Value
                               
    <10                  $77.13
    10-14                $82.78
    15-19               $412.89
    20-24             $1,114.06
    25-29               $293.00
    30-34               $214.00
    35-39               $147.67
    40+                  $38.24        Normalized Totals
                            
    <10                $3.35
    10-14              $2.96
    15-19              $3.04
    20-24              $3.05
    25-29              $2.90
    30-34              $2.93
    35-39              $3.60
    40+                $2.94
    


```python
result1 = purchase_data_count_df.join(purchase_ave_purch_price_df)
result1
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>23</td>
      <td>$3.35</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>28</td>
      <td>$2.96</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>136</td>
      <td>$3.04</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>365</td>
      <td>$3.05</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>101</td>
      <td>$2.90</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>73</td>
      <td>$2.93</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>41</td>
      <td>$3.60</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>13</td>
      <td>$2.94</td>
    </tr>
  </tbody>
</table>
</div>




```python
result2 = purchase_total_purch_price_df.join(ave_purch_price_norm_df)
result2
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
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>$77.13</td>
      <td>$3.35</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>$82.78</td>
      <td>$2.96</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>$412.89</td>
      <td>$3.04</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>$1,114.06</td>
      <td>$3.05</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>$293.00</td>
      <td>$2.90</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>$214.00</td>
      <td>$2.93</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>$147.67</td>
      <td>$3.60</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>$38.24</td>
      <td>$2.94</td>
    </tr>
  </tbody>
</table>
</div>




```python
complete_result = result1.join(result2)
complete_result
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>23</td>
      <td>$3.35</td>
      <td>$77.13</td>
      <td>$3.35</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>28</td>
      <td>$2.96</td>
      <td>$82.78</td>
      <td>$2.96</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>136</td>
      <td>$3.04</td>
      <td>$412.89</td>
      <td>$3.04</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>365</td>
      <td>$3.05</td>
      <td>$1,114.06</td>
      <td>$3.05</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>101</td>
      <td>$2.90</td>
      <td>$293.00</td>
      <td>$2.90</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>73</td>
      <td>$2.93</td>
      <td>$214.00</td>
      <td>$2.93</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>41</td>
      <td>$3.60</td>
      <td>$147.67</td>
      <td>$3.60</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>13</td>
      <td>$2.94</td>
      <td>$38.24</td>
      <td>$2.94</td>
    </tr>
  </tbody>
</table>
</div>




```python
complete_result.style.format({
    'Average Purchase Price': '${:.2f}'.format, 'Total Purchase Value': '${:.2f}'.format, 'Normalized Totals': '${:.2f}'.format})

```




<style  type="text/css" >
</style>  
<table id="T_07f21e4a_86f1_11e8_93fc_c49ded1446fe" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Purchase Count</th> 
        <th class="col_heading level0 col1" >Average Purchase Price</th> 
        <th class="col_heading level0 col2" >Total Purchase Value</th> 
        <th class="col_heading level0 col3" >Normalized Totals</th> 
    </tr>    <tr> 
        <th class="index_name level0" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_07f21e4a_86f1_11e8_93fc_c49ded1446felevel0_row0" class="row_heading level0 row0" ><10</th> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow0_col0" class="data row0 col0" >23</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow0_col1" class="data row0 col1" >$3.35</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow0_col2" class="data row0 col2" >$77.13</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow0_col3" class="data row0 col3" >$3.35</td> 
    </tr>    <tr> 
        <th id="T_07f21e4a_86f1_11e8_93fc_c49ded1446felevel0_row1" class="row_heading level0 row1" >10-14</th> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow1_col0" class="data row1 col0" >28</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow1_col1" class="data row1 col1" >$2.96</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow1_col2" class="data row1 col2" >$82.78</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow1_col3" class="data row1 col3" >$2.96</td> 
    </tr>    <tr> 
        <th id="T_07f21e4a_86f1_11e8_93fc_c49ded1446felevel0_row2" class="row_heading level0 row2" >15-19</th> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow2_col0" class="data row2 col0" >136</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow2_col1" class="data row2 col1" >$3.04</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow2_col2" class="data row2 col2" >$412.89</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow2_col3" class="data row2 col3" >$3.04</td> 
    </tr>    <tr> 
        <th id="T_07f21e4a_86f1_11e8_93fc_c49ded1446felevel0_row3" class="row_heading level0 row3" >20-24</th> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow3_col0" class="data row3 col0" >365</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow3_col1" class="data row3 col1" >$3.05</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow3_col2" class="data row3 col2" >$1114.06</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow3_col3" class="data row3 col3" >$3.05</td> 
    </tr>    <tr> 
        <th id="T_07f21e4a_86f1_11e8_93fc_c49ded1446felevel0_row4" class="row_heading level0 row4" >25-29</th> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow4_col0" class="data row4 col0" >101</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow4_col1" class="data row4 col1" >$2.90</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow4_col2" class="data row4 col2" >$293.00</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow4_col3" class="data row4 col3" >$2.90</td> 
    </tr>    <tr> 
        <th id="T_07f21e4a_86f1_11e8_93fc_c49ded1446felevel0_row5" class="row_heading level0 row5" >30-34</th> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow5_col0" class="data row5 col0" >73</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow5_col1" class="data row5 col1" >$2.93</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow5_col2" class="data row5 col2" >$214.00</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow5_col3" class="data row5 col3" >$2.93</td> 
    </tr>    <tr> 
        <th id="T_07f21e4a_86f1_11e8_93fc_c49ded1446felevel0_row6" class="row_heading level0 row6" >35-39</th> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow6_col0" class="data row6 col0" >41</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow6_col1" class="data row6 col1" >$3.60</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow6_col2" class="data row6 col2" >$147.67</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow6_col3" class="data row6 col3" >$3.60</td> 
    </tr>    <tr> 
        <th id="T_07f21e4a_86f1_11e8_93fc_c49ded1446felevel0_row7" class="row_heading level0 row7" >40+</th> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow7_col0" class="data row7 col0" >13</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow7_col1" class="data row7 col1" >$2.94</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow7_col2" class="data row7 col2" >$38.24</td> 
        <td id="T_07f21e4a_86f1_11e8_93fc_c49ded1446ferow7_col3" class="data row7 col3" >$2.94</td> 
    </tr></tbody> 
</table> 



## Top Spenders

* Run basic calculations to obtain the results in the table below


* Create a summary data frame to hold the results


* Sort the total purchase value column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
# Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
#     SN
#     Purchase Count
#     Average Purchase Price
#     Total Purchase Value
```


```python
purchase_group.head(1)
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
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>$3.53</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>$1.56</td>
      <td>40+</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Itheria73</td>
      <td>36</td>
      <td>Male</td>
      <td>169</td>
      <td>Interrogator, Blood Blade of the Queen</td>
      <td>$2.18</td>
      <td>35-39</td>
    </tr>
    <tr>
      <th>19</th>
      <td>19</td>
      <td>Chamalo71</td>
      <td>30</td>
      <td>Male</td>
      <td>89</td>
      <td>Blazefury, Protector of Delusions</td>
      <td>$4.64</td>
      <td>30-34</td>
    </tr>
    <tr>
      <th>25</th>
      <td>25</td>
      <td>Lisirra87</td>
      <td>29</td>
      <td>Male</td>
      <td>178</td>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>$4.23</td>
      <td>25-29</td>
    </tr>
    <tr>
      <th>26</th>
      <td>26</td>
      <td>Lirtossa84</td>
      <td>11</td>
      <td>Male</td>
      <td>71</td>
      <td>Demise</td>
      <td>$1.61</td>
      <td>10-14</td>
    </tr>
    <tr>
      <th>27</th>
      <td>27</td>
      <td>Eusri44</td>
      <td>7</td>
      <td>Male</td>
      <td>96</td>
      <td>Blood-Forged Skeletal Spine</td>
      <td>$3.09</td>
      <td>&lt;10</td>
    </tr>
    <tr>
      <th>30</th>
      <td>30</td>
      <td>Idai61</td>
      <td>19</td>
      <td>Male</td>
      <td>140</td>
      <td>Striker</td>
      <td>$2.94</td>
      <td>15-19</td>
    </tr>
  </tbody>
</table>
</div>




```python
#SN_name = purchase_group["SN"].nunique()

#purchase_data_count_df = pd.DataFrame({"Purchase Count": purchase_item_count})

#purchase_data_count_df.head()

```


```python
purchase_data = pd.read_csv(file_to_load)
purchase_data.head()

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
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>$3.53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>$1.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>$4.88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>$3.27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>$1.44</td>
    </tr>
  </tbody>
</table>
</div>




```python
purchase_group_df = purchase_data.groupby("SN")
purchase_group_df.head(2)


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
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>$3.53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>$1.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>$4.88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>$3.27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>$1.44</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Yalae81</td>
      <td>22</td>
      <td>Male</td>
      <td>81</td>
      <td>Dreamkiss</td>
      <td>$3.61</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Itheria73</td>
      <td>36</td>
      <td>Male</td>
      <td>169</td>
      <td>Interrogator, Blood Blade of the Queen</td>
      <td>$2.18</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>Iskjaskst81</td>
      <td>20</td>
      <td>Male</td>
      <td>162</td>
      <td>Abyssal Shard</td>
      <td>$2.67</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Undjask33</td>
      <td>22</td>
      <td>Male</td>
      <td>21</td>
      <td>Souleater</td>
      <td>$1.10</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Chanosian48</td>
      <td>35</td>
      <td>Other / Non-Disclosed</td>
      <td>136</td>
      <td>Ghastly Adamantite Protector</td>
      <td>$3.58</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>Inguron55</td>
      <td>23</td>
      <td>Male</td>
      <td>95</td>
      <td>Singed Onyx Warscythe</td>
      <td>$4.74</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>Haisrisuir60</td>
      <td>23</td>
      <td>Male</td>
      <td>162</td>
      <td>Abyssal Shard</td>
      <td>$2.67</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>Saelaephos52</td>
      <td>21</td>
      <td>Male</td>
      <td>116</td>
      <td>Renewed Skeletal Katana</td>
      <td>$4.18</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>Assjaskan73</td>
      <td>22</td>
      <td>Male</td>
      <td>4</td>
      <td>Bloodlord's Fetish</td>
      <td>$1.70</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>Saesrideu94</td>
      <td>35</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>$4.86</td>
    </tr>
    <tr>
      <th>15</th>
      <td>15</td>
      <td>Lisassa64</td>
      <td>21</td>
      <td>Female</td>
      <td>98</td>
      <td>Deadline, Voice Of Subtlety</td>
      <td>$2.89</td>
    </tr>
    <tr>
      <th>16</th>
      <td>16</td>
      <td>Lisirra25</td>
      <td>20</td>
      <td>Male</td>
      <td>40</td>
      <td>Second Chance</td>
      <td>$2.52</td>
    </tr>
    <tr>
      <th>17</th>
      <td>17</td>
      <td>Zontibe81</td>
      <td>21</td>
      <td>Male</td>
      <td>161</td>
      <td>Devine</td>
      <td>$1.76</td>
    </tr>
    <tr>
      <th>18</th>
      <td>18</td>
      <td>Reunasu60</td>
      <td>22</td>
      <td>Female</td>
      <td>82</td>
      <td>Nirvana</td>
      <td>$4.90</td>
    </tr>
    <tr>
      <th>19</th>
      <td>19</td>
      <td>Chamalo71</td>
      <td>30</td>
      <td>Male</td>
      <td>89</td>
      <td>Blazefury, Protector of Delusions</td>
      <td>$4.64</td>
    </tr>
    <tr>
      <th>20</th>
      <td>20</td>
      <td>Iathenudil29</td>
      <td>20</td>
      <td>Male</td>
      <td>57</td>
      <td>Despair, Favor of Due Diligence</td>
      <td>$4.60</td>
    </tr>
    <tr>
      <th>21</th>
      <td>21</td>
      <td>Phiarithdeu40</td>
      <td>20</td>
      <td>Male</td>
      <td>168</td>
      <td>Sun Strike, Jaws of Twisted Visions</td>
      <td>$1.48</td>
    </tr>
    <tr>
      <th>22</th>
      <td>22</td>
      <td>Siarithria38</td>
      <td>38</td>
      <td>Other / Non-Disclosed</td>
      <td>24</td>
      <td>Warped Fetish</td>
      <td>$3.81</td>
    </tr>
    <tr>
      <th>23</th>
      <td>23</td>
      <td>Eyrian71</td>
      <td>40</td>
      <td>Male</td>
      <td>151</td>
      <td>Severance</td>
      <td>$3.40</td>
    </tr>
    <tr>
      <th>24</th>
      <td>24</td>
      <td>Siala43</td>
      <td>30</td>
      <td>Male</td>
      <td>141</td>
      <td>Persuasion</td>
      <td>$3.19</td>
    </tr>
    <tr>
      <th>25</th>
      <td>25</td>
      <td>Lisirra87</td>
      <td>29</td>
      <td>Male</td>
      <td>178</td>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>$4.23</td>
    </tr>
    <tr>
      <th>26</th>
      <td>26</td>
      <td>Lirtossa84</td>
      <td>11</td>
      <td>Male</td>
      <td>71</td>
      <td>Demise</td>
      <td>$1.61</td>
    </tr>
    <tr>
      <th>27</th>
      <td>27</td>
      <td>Eusri44</td>
      <td>7</td>
      <td>Male</td>
      <td>96</td>
      <td>Blood-Forged Skeletal Spine</td>
      <td>$3.09</td>
    </tr>
    <tr>
      <th>28</th>
      <td>28</td>
      <td>Aela59</td>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>$4.32</td>
    </tr>
    <tr>
      <th>29</th>
      <td>29</td>
      <td>Tyida79</td>
      <td>24</td>
      <td>Male</td>
      <td>37</td>
      <td>Shadow Strike, Glory of Ending Hope</td>
      <td>$3.16</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>744</th>
      <td>744</td>
      <td>Chanastst38</td>
      <td>22</td>
      <td>Male</td>
      <td>94</td>
      <td>Mourning Blade</td>
      <td>$3.49</td>
    </tr>
    <tr>
      <th>745</th>
      <td>745</td>
      <td>Chanista95</td>
      <td>39</td>
      <td>Male</td>
      <td>37</td>
      <td>Shadow Strike, Glory of Ending Hope</td>
      <td>$3.16</td>
    </tr>
    <tr>
      <th>746</th>
      <td>746</td>
      <td>Aellyria80</td>
      <td>23</td>
      <td>Male</td>
      <td>159</td>
      <td>Oathbreaker, Spellblade of Trials</td>
      <td>$3.08</td>
    </tr>
    <tr>
      <th>747</th>
      <td>747</td>
      <td>Siarithria38</td>
      <td>38</td>
      <td>Other / Non-Disclosed</td>
      <td>146</td>
      <td>Warped Iron Scimitar</td>
      <td>$3.10</td>
    </tr>
    <tr>
      <th>748</th>
      <td>748</td>
      <td>Rastynusuir31</td>
      <td>20</td>
      <td>Male</td>
      <td>55</td>
      <td>Vindictive Glass Edge</td>
      <td>$2.27</td>
    </tr>
    <tr>
      <th>749</th>
      <td>749</td>
      <td>Chanossanya44</td>
      <td>20</td>
      <td>Male</td>
      <td>53</td>
      <td>Vengeance Cleaver</td>
      <td>$2.05</td>
    </tr>
    <tr>
      <th>750</th>
      <td>750</td>
      <td>Iljask75</td>
      <td>22</td>
      <td>Male</td>
      <td>167</td>
      <td>Malice, Legacy of the Queen</td>
      <td>$3.61</td>
    </tr>
    <tr>
      <th>751</th>
      <td>751</td>
      <td>Lisjaskan36</td>
      <td>11</td>
      <td>Male</td>
      <td>180</td>
      <td>Stormcaller</td>
      <td>$3.36</td>
    </tr>
    <tr>
      <th>752</th>
      <td>752</td>
      <td>Mindjasksya61</td>
      <td>17</td>
      <td>Male</td>
      <td>112</td>
      <td>Worldbreaker</td>
      <td>$2.60</td>
    </tr>
    <tr>
      <th>753</th>
      <td>753</td>
      <td>Frichirranya75</td>
      <td>36</td>
      <td>Male</td>
      <td>178</td>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>$4.23</td>
    </tr>
    <tr>
      <th>754</th>
      <td>754</td>
      <td>Pheosurllorin41</td>
      <td>23</td>
      <td>Female</td>
      <td>79</td>
      <td>Alpha, Oath of Zeal</td>
      <td>$4.05</td>
    </tr>
    <tr>
      <th>756</th>
      <td>756</td>
      <td>Ilast79</td>
      <td>20</td>
      <td>Male</td>
      <td>73</td>
      <td>Ritual Mace</td>
      <td>$2.05</td>
    </tr>
    <tr>
      <th>757</th>
      <td>757</td>
      <td>Eratiel90</td>
      <td>18</td>
      <td>Male</td>
      <td>57</td>
      <td>Despair, Favor of Due Diligence</td>
      <td>$4.60</td>
    </tr>
    <tr>
      <th>759</th>
      <td>759</td>
      <td>Tyaelorap29</td>
      <td>25</td>
      <td>Male</td>
      <td>72</td>
      <td>Winter's Bite</td>
      <td>$3.77</td>
    </tr>
    <tr>
      <th>760</th>
      <td>760</td>
      <td>Aithelis62</td>
      <td>21</td>
      <td>Male</td>
      <td>44</td>
      <td>Bonecarvin Battle Axe</td>
      <td>$2.38</td>
    </tr>
    <tr>
      <th>761</th>
      <td>761</td>
      <td>Assim27</td>
      <td>45</td>
      <td>Male</td>
      <td>17</td>
      <td>Lazarus, Terror of the Earth</td>
      <td>$1.70</td>
    </tr>
    <tr>
      <th>762</th>
      <td>762</td>
      <td>Asur53</td>
      <td>26</td>
      <td>Male</td>
      <td>110</td>
      <td>Suspension</td>
      <td>$1.44</td>
    </tr>
    <tr>
      <th>765</th>
      <td>765</td>
      <td>Irith83</td>
      <td>18</td>
      <td>Male</td>
      <td>130</td>
      <td>Alpha</td>
      <td>$2.07</td>
    </tr>
    <tr>
      <th>766</th>
      <td>766</td>
      <td>Aelastirin39</td>
      <td>23</td>
      <td>Male</td>
      <td>58</td>
      <td>Freak's Bite, Favor of Holy Might</td>
      <td>$4.14</td>
    </tr>
    <tr>
      <th>767</th>
      <td>767</td>
      <td>Ilmol66</td>
      <td>8</td>
      <td>Female</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>$4.88</td>
    </tr>
    <tr>
      <th>768</th>
      <td>768</td>
      <td>Assassasta79</td>
      <td>38</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>$4.88</td>
    </tr>
    <tr>
      <th>769</th>
      <td>769</td>
      <td>Ilosian36</td>
      <td>15</td>
      <td>Male</td>
      <td>145</td>
      <td>Fiery Glass Crusader</td>
      <td>$4.58</td>
    </tr>
    <tr>
      <th>770</th>
      <td>770</td>
      <td>Lirtosia63</td>
      <td>34</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>$1.02</td>
    </tr>
    <tr>
      <th>771</th>
      <td>771</td>
      <td>Iskossasda43</td>
      <td>16</td>
      <td>Male</td>
      <td>25</td>
      <td>Hero Cane</td>
      <td>$4.35</td>
    </tr>
    <tr>
      <th>773</th>
      <td>773</td>
      <td>Hala31</td>
      <td>21</td>
      <td>Male</td>
      <td>19</td>
      <td>Pursuit, Cudgel of Necromancy</td>
      <td>$1.02</td>
    </tr>
    <tr>
      <th>774</th>
      <td>774</td>
      <td>Jiskjask80</td>
      <td>11</td>
      <td>Male</td>
      <td>101</td>
      <td>Final Critic</td>
      <td>$4.19</td>
    </tr>
    <tr>
      <th>775</th>
      <td>775</td>
      <td>Aethedru70</td>
      <td>21</td>
      <td>Female</td>
      <td>60</td>
      <td>Wolf</td>
      <td>$3.54</td>
    </tr>
    <tr>
      <th>777</th>
      <td>777</td>
      <td>Yathecal72</td>
      <td>20</td>
      <td>Male</td>
      <td>67</td>
      <td>Celeste, Incarnation of the Corrupted</td>
      <td>$3.46</td>
    </tr>
    <tr>
      <th>778</th>
      <td>778</td>
      <td>Sisur91</td>
      <td>7</td>
      <td>Male</td>
      <td>101</td>
      <td>Final Critic</td>
      <td>$4.19</td>
    </tr>
    <tr>
      <th>779</th>
      <td>779</td>
      <td>Ennrian78</td>
      <td>24</td>
      <td>Male</td>
      <td>50</td>
      <td>Dawn</td>
      <td>$4.60</td>
    </tr>
  </tbody>
</table>
<p>738 rows × 7 columns</p>
</div>




```python
#purchase_group_SN = purchase_group_df["SN"].nunique()
purchase_count_items_df = purchase_group_df["Item Name"].count()
purchase_ave_price_df = purchase_group_df["Price"].mean()
purchase_total_price_df = purchase_group_df["Price"].sum()
#purchase_item_count = purchase_group["Item ID"].count()
```


```python

purchase_data_SN_df = pd.DataFrame({"Purchase Count": purchase_count_items_df, 
                                    "Average Purchase Price": purchase_ave_price_df, 
                                    "Total Purchase Value": purchase_total_price_df})


purchase_data_SN_df.head()

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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
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
      <th>Adairialis76</th>
      <td>1</td>
      <td>$2.28</td>
      <td>$2.28</td>
    </tr>
    <tr>
      <th>Adastirin33</th>
      <td>1</td>
      <td>$4.48</td>
      <td>$4.48</td>
    </tr>
    <tr>
      <th>Aeda94</th>
      <td>1</td>
      <td>$4.91</td>
      <td>$4.91</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>1</td>
      <td>$4.32</td>
      <td>$4.32</td>
    </tr>
    <tr>
      <th>Aelaria33</th>
      <td>1</td>
      <td>$1.79</td>
      <td>$1.79</td>
    </tr>
  </tbody>
</table>
</div>




```python
decending_form = purchase_data_SN_df.sort_values(['Total Purchase Value'], ascending=[False])
decending_form.head()
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
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
      <th>Lisosia93</th>
      <td>5</td>
      <td>$3.79</td>
      <td>$18.96</td>
    </tr>
    <tr>
      <th>Idastidru52</th>
      <td>4</td>
      <td>$3.86</td>
      <td>$15.45</td>
    </tr>
    <tr>
      <th>Chamjask73</th>
      <td>3</td>
      <td>$4.61</td>
      <td>$13.83</td>
    </tr>
    <tr>
      <th>Iral74</th>
      <td>4</td>
      <td>$3.40</td>
      <td>$13.62</td>
    </tr>
    <tr>
      <th>Iskadarya95</th>
      <td>3</td>
      <td>$4.37</td>
      <td>$13.10</td>
    </tr>
  </tbody>
</table>
</div>



## Most Popular Items

* Retrieve the Item ID, Item Name, and Item Price columns


* Group by Item ID and Item Name. Perform calculations to obtain purchase count, item price, and total purchase value


* Create a summary data frame to hold the results


* Sort the purchase count column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
# Identify the 5 most popular items by purchase count, then list (in a table):
#     Item ID
#     Item Name
#     Purchase Count
#     Item Price
#     Total Purchase Value
```


```python
#pd.options.display.float_format = '${:,.2f}'.format
```


```python
purchase_group.head(0)
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
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
purchase_data_pop = pd.read_csv(file_to_load)

```


```python
item_group_df = purchase_data_pop.groupby(["Item ID", "Item Name"])
item_group_df.head(2)
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
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>$3.53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>$1.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>$4.88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>$3.27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>$1.44</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Yalae81</td>
      <td>22</td>
      <td>Male</td>
      <td>81</td>
      <td>Dreamkiss</td>
      <td>$3.61</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Itheria73</td>
      <td>36</td>
      <td>Male</td>
      <td>169</td>
      <td>Interrogator, Blood Blade of the Queen</td>
      <td>$2.18</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>Iskjaskst81</td>
      <td>20</td>
      <td>Male</td>
      <td>162</td>
      <td>Abyssal Shard</td>
      <td>$2.67</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Undjask33</td>
      <td>22</td>
      <td>Male</td>
      <td>21</td>
      <td>Souleater</td>
      <td>$1.10</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Chanosian48</td>
      <td>35</td>
      <td>Other / Non-Disclosed</td>
      <td>136</td>
      <td>Ghastly Adamantite Protector</td>
      <td>$3.58</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>Inguron55</td>
      <td>23</td>
      <td>Male</td>
      <td>95</td>
      <td>Singed Onyx Warscythe</td>
      <td>$4.74</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>Haisrisuir60</td>
      <td>23</td>
      <td>Male</td>
      <td>162</td>
      <td>Abyssal Shard</td>
      <td>$2.67</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>Saelaephos52</td>
      <td>21</td>
      <td>Male</td>
      <td>116</td>
      <td>Renewed Skeletal Katana</td>
      <td>$4.18</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>Assjaskan73</td>
      <td>22</td>
      <td>Male</td>
      <td>4</td>
      <td>Bloodlord's Fetish</td>
      <td>$1.70</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>Saesrideu94</td>
      <td>35</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>$4.86</td>
    </tr>
    <tr>
      <th>15</th>
      <td>15</td>
      <td>Lisassa64</td>
      <td>21</td>
      <td>Female</td>
      <td>98</td>
      <td>Deadline, Voice Of Subtlety</td>
      <td>$2.89</td>
    </tr>
    <tr>
      <th>16</th>
      <td>16</td>
      <td>Lisirra25</td>
      <td>20</td>
      <td>Male</td>
      <td>40</td>
      <td>Second Chance</td>
      <td>$2.52</td>
    </tr>
    <tr>
      <th>17</th>
      <td>17</td>
      <td>Zontibe81</td>
      <td>21</td>
      <td>Male</td>
      <td>161</td>
      <td>Devine</td>
      <td>$1.76</td>
    </tr>
    <tr>
      <th>18</th>
      <td>18</td>
      <td>Reunasu60</td>
      <td>22</td>
      <td>Female</td>
      <td>82</td>
      <td>Nirvana</td>
      <td>$4.90</td>
    </tr>
    <tr>
      <th>19</th>
      <td>19</td>
      <td>Chamalo71</td>
      <td>30</td>
      <td>Male</td>
      <td>89</td>
      <td>Blazefury, Protector of Delusions</td>
      <td>$4.64</td>
    </tr>
    <tr>
      <th>20</th>
      <td>20</td>
      <td>Iathenudil29</td>
      <td>20</td>
      <td>Male</td>
      <td>57</td>
      <td>Despair, Favor of Due Diligence</td>
      <td>$4.60</td>
    </tr>
    <tr>
      <th>21</th>
      <td>21</td>
      <td>Phiarithdeu40</td>
      <td>20</td>
      <td>Male</td>
      <td>168</td>
      <td>Sun Strike, Jaws of Twisted Visions</td>
      <td>$1.48</td>
    </tr>
    <tr>
      <th>22</th>
      <td>22</td>
      <td>Siarithria38</td>
      <td>38</td>
      <td>Other / Non-Disclosed</td>
      <td>24</td>
      <td>Warped Fetish</td>
      <td>$3.81</td>
    </tr>
    <tr>
      <th>23</th>
      <td>23</td>
      <td>Eyrian71</td>
      <td>40</td>
      <td>Male</td>
      <td>151</td>
      <td>Severance</td>
      <td>$3.40</td>
    </tr>
    <tr>
      <th>24</th>
      <td>24</td>
      <td>Siala43</td>
      <td>30</td>
      <td>Male</td>
      <td>141</td>
      <td>Persuasion</td>
      <td>$3.19</td>
    </tr>
    <tr>
      <th>25</th>
      <td>25</td>
      <td>Lisirra87</td>
      <td>29</td>
      <td>Male</td>
      <td>178</td>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>$4.23</td>
    </tr>
    <tr>
      <th>26</th>
      <td>26</td>
      <td>Lirtossa84</td>
      <td>11</td>
      <td>Male</td>
      <td>71</td>
      <td>Demise</td>
      <td>$1.61</td>
    </tr>
    <tr>
      <th>27</th>
      <td>27</td>
      <td>Eusri44</td>
      <td>7</td>
      <td>Male</td>
      <td>96</td>
      <td>Blood-Forged Skeletal Spine</td>
      <td>$3.09</td>
    </tr>
    <tr>
      <th>28</th>
      <td>28</td>
      <td>Aela59</td>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>$4.32</td>
    </tr>
    <tr>
      <th>29</th>
      <td>29</td>
      <td>Tyida79</td>
      <td>24</td>
      <td>Male</td>
      <td>37</td>
      <td>Shadow Strike, Glory of Ending Hope</td>
      <td>$3.16</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>566</th>
      <td>566</td>
      <td>Ardonmol96</td>
      <td>20</td>
      <td>Male</td>
      <td>31</td>
      <td>Trickster</td>
      <td>$1.55</td>
    </tr>
    <tr>
      <th>570</th>
      <td>570</td>
      <td>Chadossa56</td>
      <td>20</td>
      <td>Male</td>
      <td>69</td>
      <td>Frenzy, Defender of the Harvest</td>
      <td>$1.98</td>
    </tr>
    <tr>
      <th>583</th>
      <td>583</td>
      <td>Aeralstical35</td>
      <td>20</td>
      <td>Male</td>
      <td>49</td>
      <td>The Oculus, Token of Lost Worlds</td>
      <td>$2.96</td>
    </tr>
    <tr>
      <th>584</th>
      <td>584</td>
      <td>Aelin32</td>
      <td>20</td>
      <td>Male</td>
      <td>115</td>
      <td>Spectral Diamond Doomblade</td>
      <td>$2.04</td>
    </tr>
    <tr>
      <th>589</th>
      <td>589</td>
      <td>Seolollo93</td>
      <td>30</td>
      <td>Male</td>
      <td>106</td>
      <td>Crying Steel Sickle</td>
      <td>$3.41</td>
    </tr>
    <tr>
      <th>595</th>
      <td>595</td>
      <td>Yathedeu43</td>
      <td>22</td>
      <td>Male</td>
      <td>55</td>
      <td>Vindictive Glass Edge</td>
      <td>$2.27</td>
    </tr>
    <tr>
      <th>597</th>
      <td>597</td>
      <td>Quinarap53</td>
      <td>15</td>
      <td>Male</td>
      <td>86</td>
      <td>Stormfury Lantern</td>
      <td>$2.27</td>
    </tr>
    <tr>
      <th>598</th>
      <td>598</td>
      <td>Halaecal66</td>
      <td>22</td>
      <td>Male</td>
      <td>111</td>
      <td>Misery's End</td>
      <td>$4.89</td>
    </tr>
    <tr>
      <th>608</th>
      <td>608</td>
      <td>Leyirra83</td>
      <td>24</td>
      <td>Female</td>
      <td>132</td>
      <td>Persuasion</td>
      <td>$3.33</td>
    </tr>
    <tr>
      <th>611</th>
      <td>611</td>
      <td>Chamjaskya75</td>
      <td>16</td>
      <td>Male</td>
      <td>176</td>
      <td>Relentless Iron Skewer</td>
      <td>$2.84</td>
    </tr>
    <tr>
      <th>618</th>
      <td>618</td>
      <td>Aisurdru79</td>
      <td>29</td>
      <td>Female</td>
      <td>183</td>
      <td>Dragon's Greatsword</td>
      <td>$1.09</td>
    </tr>
    <tr>
      <th>619</th>
      <td>619</td>
      <td>Quanenrian83</td>
      <td>15</td>
      <td>Male</td>
      <td>55</td>
      <td>Vindictive Glass Edge</td>
      <td>$2.27</td>
    </tr>
    <tr>
      <th>621</th>
      <td>621</td>
      <td>Seosrim97</td>
      <td>20</td>
      <td>Male</td>
      <td>26</td>
      <td>Unholy Wand</td>
      <td>$1.12</td>
    </tr>
    <tr>
      <th>642</th>
      <td>642</td>
      <td>Chamadarsda63</td>
      <td>23</td>
      <td>Male</td>
      <td>127</td>
      <td>Heartseeker, Reaver of Souls</td>
      <td>$3.92</td>
    </tr>
    <tr>
      <th>647</th>
      <td>647</td>
      <td>Chadjask85</td>
      <td>24</td>
      <td>Male</td>
      <td>61</td>
      <td>Ragnarok</td>
      <td>$3.87</td>
    </tr>
    <tr>
      <th>649</th>
      <td>649</td>
      <td>Iskim66</td>
      <td>15</td>
      <td>Male</td>
      <td>67</td>
      <td>Celeste, Incarnation of the Corrupted</td>
      <td>$3.46</td>
    </tr>
    <tr>
      <th>651</th>
      <td>651</td>
      <td>Lirtilsa72</td>
      <td>24</td>
      <td>Male</td>
      <td>132</td>
      <td>Persuasion</td>
      <td>$3.33</td>
    </tr>
    <tr>
      <th>656</th>
      <td>656</td>
      <td>Ethrasyon38</td>
      <td>26</td>
      <td>Male</td>
      <td>115</td>
      <td>Spectral Diamond Doomblade</td>
      <td>$2.04</td>
    </tr>
    <tr>
      <th>664</th>
      <td>664</td>
      <td>Chamistast30</td>
      <td>31</td>
      <td>Male</td>
      <td>47</td>
      <td>Alpha, Reach of Ending Hope</td>
      <td>$3.58</td>
    </tr>
    <tr>
      <th>673</th>
      <td>673</td>
      <td>Idacal95</td>
      <td>30</td>
      <td>Male</td>
      <td>130</td>
      <td>Alpha</td>
      <td>$2.07</td>
    </tr>
    <tr>
      <th>681</th>
      <td>681</td>
      <td>Yalaeria91</td>
      <td>33</td>
      <td>Male</td>
      <td>28</td>
      <td>Flux, Destroyer of Due Diligence</td>
      <td>$1.06</td>
    </tr>
    <tr>
      <th>698</th>
      <td>698</td>
      <td>Yarithrin84</td>
      <td>30</td>
      <td>Female</td>
      <td>58</td>
      <td>Freak's Bite, Favor of Holy Might</td>
      <td>$4.14</td>
    </tr>
    <tr>
      <th>699</th>
      <td>699</td>
      <td>Tyaelly53</td>
      <td>17</td>
      <td>Female</td>
      <td>130</td>
      <td>Alpha</td>
      <td>$2.07</td>
    </tr>
    <tr>
      <th>700</th>
      <td>700</td>
      <td>Chanosia60</td>
      <td>31</td>
      <td>Male</td>
      <td>90</td>
      <td>Betrayer</td>
      <td>$2.94</td>
    </tr>
    <tr>
      <th>717</th>
      <td>717</td>
      <td>Chanilsast61</td>
      <td>30</td>
      <td>Male</td>
      <td>177</td>
      <td>Winterthorn, Defender of Shifting Worlds</td>
      <td>$2.08</td>
    </tr>
    <tr>
      <th>719</th>
      <td>719</td>
      <td>Sundassa93</td>
      <td>16</td>
      <td>Male</td>
      <td>158</td>
      <td>Darkheart, Butcher of the Champion</td>
      <td>$2.45</td>
    </tr>
    <tr>
      <th>723</th>
      <td>723</td>
      <td>Lisista54</td>
      <td>21</td>
      <td>Male</td>
      <td>177</td>
      <td>Winterthorn, Defender of Shifting Worlds</td>
      <td>$2.08</td>
    </tr>
    <tr>
      <th>727</th>
      <td>727</td>
      <td>Yathecal82</td>
      <td>20</td>
      <td>Female</td>
      <td>104</td>
      <td>Gladiator's Glaive</td>
      <td>$1.93</td>
    </tr>
    <tr>
      <th>740</th>
      <td>740</td>
      <td>Reunasu60</td>
      <td>22</td>
      <td>Female</td>
      <td>127</td>
      <td>Heartseeker, Reaver of Souls</td>
      <td>$3.92</td>
    </tr>
    <tr>
      <th>751</th>
      <td>751</td>
      <td>Lisjaskan36</td>
      <td>11</td>
      <td>Male</td>
      <td>180</td>
      <td>Stormcaller</td>
      <td>$3.36</td>
    </tr>
  </tbody>
</table>
<p>354 rows × 7 columns</p>
</div>




```python
#item_name_df = item_group_df["Item Name"].unique()

#item_name_df.head()

```


```python
#item_name_df["Item Name"] = item_name_df["Item Name"].str.strip('[]')
#item_name_df_no = item_name_df.strip('[]')
#item_name_df_no
```


```python
purchase_counts_items_df = item_group_df["Item ID"].count()
purchase_counts_items_df.head()
```




    Item ID  Item Name         
    0        Splinter              4
    1        Crucifer              3
    2        Verdict               6
    3        Phantomlight          6
    4        Bloodlord's Fetish    5
    Name: Item ID, dtype: int64




```python
purchase_ave_prices_df = item_group_df["Price"].mean()
purchase_ave_prices_df.head()
```




    Item ID  Item Name         
    0        Splinter             $1.28
    1        Crucifer             $3.26
    2        Verdict              $2.48
    3        Phantomlight         $2.49
    4        Bloodlord's Fetish   $1.70
    Name: Price, dtype: float64




```python
#purchase_ave_price_df.style.format({'Item Price': '${:.2f}'.format})
```


```python
total_prices_df = item_group_df["Price"].sum()
total_prices_df.head()
```




    Item ID  Item Name         
    0        Splinter              $5.12
    1        Crucifer              $9.78
    2        Verdict              $14.88
    3        Phantomlight         $14.94
    4        Bloodlord's Fetish    $8.50
    Name: Price, dtype: float64




```python
#total_prices_df.style.format({'Total Purchase Value': '${:.2f}'.format})
```


```python
popular_items = pd.DataFrame({"Purchase Count":  purchase_counts_items_df, 
                              "Item Price": purchase_ave_prices_df, 
                              "Total Purchase Value": total_prices_df})
popular_items.head()
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
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <th>Splinter</th>
      <td>4</td>
      <td>$1.28</td>
      <td>$5.12</td>
    </tr>
    <tr>
      <th>1</th>
      <th>Crucifer</th>
      <td>3</td>
      <td>$3.26</td>
      <td>$9.78</td>
    </tr>
    <tr>
      <th>2</th>
      <th>Verdict</th>
      <td>6</td>
      <td>$2.48</td>
      <td>$14.88</td>
    </tr>
    <tr>
      <th>3</th>
      <th>Phantomlight</th>
      <td>6</td>
      <td>$2.49</td>
      <td>$14.94</td>
    </tr>
    <tr>
      <th>4</th>
      <th>Bloodlord's Fetish</th>
      <td>5</td>
      <td>$1.70</td>
      <td>$8.50</td>
    </tr>
  </tbody>
</table>
</div>




```python
decending_form_total_pop = popular_items.sort_values(['Purchase Count'], ascending=[False])
decending_form_total_pop.head()
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
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>178</th>
      <th>Oathbreaker, Last Hope of the Breaking Storm</th>
      <td>12</td>
      <td>$4.23</td>
      <td>$50.76</td>
    </tr>
    <tr>
      <th>145</th>
      <th>Fiery Glass Crusader</th>
      <td>9</td>
      <td>$4.58</td>
      <td>$41.22</td>
    </tr>
    <tr>
      <th>108</th>
      <th>Extraction, Quickblade Of Trembling Hands</th>
      <td>9</td>
      <td>$3.53</td>
      <td>$31.77</td>
    </tr>
    <tr>
      <th>82</th>
      <th>Nirvana</th>
      <td>9</td>
      <td>$4.90</td>
      <td>$44.10</td>
    </tr>
    <tr>
      <th>19</th>
      <th>Pursuit, Cudgel of Necromancy</th>
      <td>8</td>
      <td>$1.02</td>
      <td>$8.16</td>
    </tr>
  </tbody>
</table>
</div>




```python
decending_form_total_pop = popular_items.sort_values(['Total Purchase Value'], ascending=[False])
decending_form_total_pop.head()
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
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>178</th>
      <th>Oathbreaker, Last Hope of the Breaking Storm</th>
      <td>12</td>
      <td>$4.23</td>
      <td>$50.76</td>
    </tr>
    <tr>
      <th>82</th>
      <th>Nirvana</th>
      <td>9</td>
      <td>$4.90</td>
      <td>$44.10</td>
    </tr>
    <tr>
      <th>145</th>
      <th>Fiery Glass Crusader</th>
      <td>9</td>
      <td>$4.58</td>
      <td>$41.22</td>
    </tr>
    <tr>
      <th>92</th>
      <th>Final Critic</th>
      <td>8</td>
      <td>$4.88</td>
      <td>$39.04</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <td>8</td>
      <td>$4.35</td>
      <td>$34.80</td>
    </tr>
  </tbody>
</table>
</div>



## Most Profitable Items

* Sort the above table by total purchase value in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the data frame




```python
# Identify the 5 most profitable items by total purchase value, then list (in a table):
#     Item ID
#     Item Name
#     Purchase Count
#     Item Price
#     Total Purchase Value
```


```python
# As final considerations:


# You must use the Pandas Library and the Jupyter Notebook.
# You must submit a link to your Jupyter Notebook with the viewable Data Frames.
# You must include an exported markdown version of your Notebook called  README.md in your GitHub repository.
# You must include a written description of three observable trends based on the data.
# See Example Solution for a reference on expected format.
```
