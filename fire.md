
# **Team Entrepreneur**

---

# **Exploratory Data Analysis on Fire Dataset**

## About the Dataset

- Data is taken from [Fao website](https://www.fao.org/faostat/en/#data/GI). All countries available were selected and Year: 1990 to 2019.

## Steps performed

## 1. Import Libraries

- Import necessary libraries

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

## 2. Import dataset

- Import dataset and check dataset

```python
df= pd.read_csv('fires_data_11-29-2021.csv')
df.head()
```

## 3. Shape of dataset

- Check Shape of data

```python
row, cols= df.shape
print("Number of rows:", row)
print("Number of columns:", cols)
```
Dataset has 47649 rows and 17 columns

## 4. Check data types

- Check data types of each column

```python
df.dtypes
```

## 5. Check missing values

- Check missing values in each column

```python
df.isnull().sum()
```

- Only one column (Note) has missing values

## 6. Dropping unnecessary columns

- Drop unnecessary columns and making changes in the dataset

```python
df.drop(['Note','Domain Code','Element Code','Item Code','Flag Description','Flag','Source Code'], axis=1, inplace=True)
```

## 7. Data Structure of dataset

- Check data structure of dataset

```python
df.info()
```

- Data has RangeIndex: 47649 entries, starting from 0 to 47648

- Data has total 10 columns

- dtypes of columns are one float64, two int64 and seven object

- Memory usage of the data is 3.6 MB

## 8. Summery of dataset

- Summery of dataset

```python
df.describe()
```

## 9. Unique values in each column

- Unique values in each column

```python
df.nunique()
```

- 238 Countries
- 30 Years
- 7 Items

## 10. Value counts

- Value counts of Item column

```python
df['Item'].value_counts()
```

Seven different items are available in the dataset and their count are:

>Humid tropical forest    6807
>
>Other forest             6807
>
>Closed shrubland         6807
>
>Grassland                6807
>
>Open shrubland           6807
>
>Savanna                  6807
>
>Woody savanna            6807

# **Insights of Datasets**

## 1. Land affected by fires yearly

```python
s=df.groupby(["Year"]).sum().sort_values(by="Value", ascending=False).head(30)
s
```

|Year  | Value
|:-------|-----:|
| 2012 | 8.320688e+08|
|2007	| 8.303040e+08|
|2011	| 8.294422e+08|
|2002	| 8.285003e+08|
|2004	| 8.227932e+08|
|2005	| 7.998101e+08|
|2003	| 7.846035e+08|
|2006	| 7.715579e+08|
|2010	| 7.536716e+08|
|2008	|	7.461368e+08|
|2001	|	7.394390e+08|
|2017	|	7.011378e+08|
|2015	|	6.869739e+08|
|2014	|	6.793501e+08|
|2009	|	6.761442e+08|
|1995	|	6.640982e+08|
|1994	|	6.640982e+08|
|1993	|	6.640982e+08|
|1992	|	6.640982e+08|
|1990	|	6.640982e+08|
|1991	|	6.640982e+08|
|2016	|	6.469105e+08|
|2013	|	6.379084e+08|
|2018	|	6.311982e+08|
|2019	|	6.064821e+08|
|1998| 3.534771e+08|
|2000|	3.421322e+08|
|1999|	3.396431e+08|
|1996|	3.087709e+08|
|1997|	3.022354e+08|

- The highest value is in year **2012** value of **8.320688e+08**
- The lowest value is in year **1997** value of **3.022354e+08**


### Graphical Representation land affected by fires yearly

```python
plt.figure(figsize=(5,3), dpi=150, linewidth=2)
sns.barplot(x=s.index,y='Value',data=s, palette="winter")
plt.xticks(rotation=90)
plt.title('Land affected by fires yearly')
```

![](Land%20affected%20yearly.png)


## 2. Top 10 countries affected by fires

```python

```python
a=df.groupby(["Area"]).sum().sort_values(by="Value", ascending=False).head(30)
a
```

|Area  | Value|
|:-------|-----:|
|Australia	|2.650662e+09|
|Angola	|	1.927834e+09|
|Democratic Republic of the Congo|	1.698499e+09|
|Sudan (former)	|	1.304401e+09|
|Zambia	|	1.204405e+09|
|Mozambique	|	1.040799e+09|
|Central African Republic|	9.843985e+08|
|Brazil	|	8.904736e+08|
|United Republic of Tanzania	|	6.783696e+08|
|Russian Federation	|	4.573399e+08|

- Australia has the highest value of **2.650662e+09**

### Graphical Representation of top 10 countries affected by fires

```python
plt.figure(figsize=(5,3), dpi=150, linewidth=2)
sns.barplot(x=a.index,y='Value',data=a)
plt.xticks(rotation=90)
plt.title('Top 10 Countries affected by fires')
```

![](Country%20affected.png)


## 3.Item type burned by fire over years

- Item type burned by fire over years

```python
b=df.groupby(["Item"]).sum().sort_values(by="Value", ascending=False)
b
```
|Item  | Value|
|:-------|-----:|
|Savanna	|	7.831523e+09|
|Grassland	|	6.801505e+09|
|Woody savanna	|	1.957280e+09|
|Open shrubland	|	1.365417e+09|
|Humid tropical forest	|	1.132681e+09|
|Other forest	|	4.478974e+08|
|Closed shrubland	|	9.897531e+07 |

- Savanna is most burned item type with value of **7.831523e+09**

- Closed shrubland is least burned item type with value of **9.897531e+07**


### Graphical Representation of item type affected by fire

```python
plt.figure(figsize=(5,3), dpi=150)
sns.barplot(x=b.index,y='Value',data=b)
plt.xticks(rotation=90)
plt.title("Item type affected by fires")
```

![](Item%20affected.png)


## 4. Maximum area burned in a year in a country

- Maximum area burned in a year in a country

```python
df.groupby(["Year","Area"]).sum().sort_values(by="Value", ascending=False).head(10)
```
|Year |Area  | Value|
|:-------|------|-----:|
2001|	Australia	|	1.840483e+08|
2012|	Australia	|	1.783090e+08|
2011|	Australia	|	1.737702e+08|
2002|	Australia	|	1.530490e+08|
2004|	Australia	|	1.255536e+08|
2006|	Australia	|	1.134671e+08|
2007|	Australia	|	1.025287e+08|
2018|	Australia	|	1.013396e+08|
2017|	Australia	|	9.615384e+07|
2014|	Australia	|   9.246523e+07|

- For most Forest and Savanna burned in a year in a country Australia has 10 top values of the burned area in a country in a year.

## 5. Item type burned most in a year

- Item type burned most in a year

```python
df.groupby(["Year","Item"]).sum().sort_values(by="Value", ascending=False).head(10)
```
|Year |Item  | Value|
|:-------|------|-----:|
2005|	Savanna	|	3.487667e+08
2003|	Savanna	|	3.414789e+08
2007|	Savanna	|	3.294614e+08
2004|	Grassland	|	3.285651e+08
2002|	Grassland	|	3.209670e+08
2007|	Grassland	|	3.209456e+08
2008|	Savanna	|	3.151744e+08
2010|	Savanna	|	3.136204e+08
2004|	Savanna	|	3.135659e+08
2005|	Grassland	|	3.107788e+08


- For most Forest and Savanna burned in a year Savanna has the highest value of **3.487667e+08** in year **2005**

## 6. Which type of item is burned most in a year and in which country

```python
df.groupby(["Year","Area","Item"]).sum().sort_values(by="Value", ascending=False).head(10)
```

|Year |Area  | Item | Value|
|:-------|------|-----:|-----:|
2011|	Australia	|Open shrubland	|	1.052085e+08
2012|	Australia	|Open shrubland	|	9.431891e+07
2001|	Australia	|Open shrubland	|	9.156779e+07
2002|	Australia	|Open shrubland	|	8.998342e+07
2001|	Australia	|Grassland	|	7.639979e+07
2004|	Australia	|Grassland	|	6.797964e+07
2012|	Australia	|Grassland	|	6.456851e+07
2011|	Australia	|Grassland	|	5.287709e+07
2017|	Australia	|Open shrubland	|	5.209256e+07
2006|	Australia	|Grassland	|	5.006097e+07

- For most Forest and Savanna burned in a year in a country Open shrubland has the highest value of **1.052085e+08** in year **2011** in Australia

- Open shrubland and Grassland are most burned item type in a year in a country.

- Both item type are most burned Australia in a year.

# **Continent Analysis**
## 1. Create Continent Column

```python
#Adding a new column of Continent 
#pip install pycountry_convert
#Making new columns of Continent for Visualization

import pycountry_convert as pc
def country_to_continent(country_name):
    country_alpha2 = pc.country_name_to_country_alpha2(country_name)
    country_continent_code = pc.country_alpha2_to_continent_code(country_alpha2)
    country_continent_name = pc.convert_continent_code_to_continent_name(country_continent_code)
    return country_continent_name
# Example
# country_name = 'Chagos Archipelago'
# print(country_to_continent(country_name))
continent=[]
for i in df['Area']:
    
   if i=='Chagos Archipelago':
       continent.append('Africa')
       
   elif i=='Western Sahara':
       continent.append('Africa')
   elif i=='Channel Islands'  :
       continent.append('Europe')
   elif i=='China, Hong Kong SAR'  :
       continent.append('Asia')
   elif i=='China, Macao SAR'  :
       continent.append('Asia')
   elif i=='China, mainland'  :
       continent.append('Asia')
   elif i=='China, Taiwan Province of'  :
       continent.append('Asia')
   elif i=='French Guyana'  :
       continent.append('South America')
   elif i=='French Southern Territories'  :
       continent.append('Antarctica')
   elif i=='Heard and McDonald Islands'  :
       continent.append('Antarctica')
   elif i=='Holy See'  :
       continent.append('Europe')
   elif i=='Iran (Islamic Republic of)'  :
       continent.append('Asia')
   elif i=='Johnston Island'  :
       continent.append('Oceania')
   elif i=='Micronesia (Federated States of)'  :
       continent.append('Oceania')
   elif i=='Midway Island'  :
       continent.append('North America')
   elif i=='Netherlands Antilles (former)'  :
       continent.append('Europe')
   elif i=='Pitcairn'  :
       continent.append('Oceania')
   elif i=='Wake Island'  :
       continent.append('Oceania')
   elif i=='Wallis and Futuna Islands'  :
       continent.append('Oceania')
   elif i=='Republic of Korea'  :
       continent.append('Asia')
   elif i=='Serbia and Montenegro'  :
       continent.append('Europe')
   elif i=='Sudan (former)'  :
       continent.append('Asia')
   elif i=='Timor-Leste'  :
       continent.append('Asia')
   elif i=='Venezuela (Bolivarian Republic of)'  :
       continent.append('South America')
   elif i=='Antarctica' :
       continent.append('Antarctica')
   elif i=='Bolivia (Plurinational State of)' :
       continent.append('South America')
   elif i=='Belgium-Luxembourg' :
       continent.append('Europe')
   elif i=='Czechoslovakia' :
       continent.append('Europe')
   elif i=='Ethiopia PDR' :
       continent.append('Africa')
   elif i=='Pacific Islands Trust Territory' :
       continent.append('Asia')
   elif i=='Svalbard and Jan Mayen Islands' :
       continent.append('Europe')
   elif i=='USSR' :
       continent.append('Asia')
   elif i=='Yugoslav SFR' :
       continent.append('Europe')
   else:
      continent.append(country_to_continent(i))

df["continent"]=continent
```
## 1. Continent Names

```python
df['continent'].unique()
```
- Asia, Europe, Africa, Oceania, North America,
       South America

## 2. Most land affected by fire in a continent

```python
con_fire=df.groupby(["continent"]).sum().sort_values(by="Value", ascending=False)
plt.figure(figsize=(15,8), dpi=150, linewidth=2)
sns.barplot(x=con_fire.index,y='Value',data=con_fire)
plt.xticks(rotation=90)
```

![](most%20continent%20affected.png)
  
- The most affected continent is Africa and the least one is North America.

## 2. Maximum area burned in a year in a continent

```python
a_con_fire=df.groupby(["Year","continent"]).sum().sort_values(by="Value", ascending=False).head(10)
a_con_fire
```
|Year| Continent | Value|
|:-----|:--------|:------|	
2005	|Africa	|5.102612e+08
2012	|Africa	|5.075348e+08
2013	|Africa	|4.898559e+08
2016	|Africa	|4.887990e+08
2003	|Africa	|4.803761e+08
2011	|Africa	|4.767006e+08
2010	|Africa	|4.760484e+08
2008	|Africa	|4.719482e+08
2007	|Africa	|4.705869e+08
2015	|Africa	|4.694914e+08

- The top affected year is 2005 w.r.t. continent.

## 3. Item burned in a continent in a year

```python
df.groupby(["Year","continent","Item"]).sum().sort_values(by="Value", ascending=False).head(10)
```
|Year	|continent	|Item |Value
|:-----|:------|:-------|:-------|	
2005	|Africa	|Savanna	|2.437630e+08
2016	|Africa	|Savanna	|2.414008e+08
2003	|Africa	|Savanna	|2.374897e+08
2013	|Africa	|Savanna	|2.350593e+08
2012	|Africa	|Savanna	|2.348181e+08
2015	|Africa	|Savanna	|2.299518e+08
2017	|Africa	|Savanna	|2.258347e+08
2014	|Africa	|Savanna	|2.232819e+08
2008	|Africa	|Savanna	|2.203084e+08
2018	|Africa	|Savanna	|2.186234e+08

- The most affected item by fire is **Savanna** in **2005** in **Africa** with value **2.437630e+08**.

## 4. Graphical representation w.r.t Continents

```python
plt.figure(figsize=(15,8), dpi=150)
sns.set(font_scale=1)
sns.set_style("whitegrid")
sns.lineplot(x="Year",y="Value",hue="continent",style="Item",data=df)
```
![](Item%20affected%20continents.png)

- Above graph is visualized to show the fires by year and continent with the style of line for the item type.
- Africa has the most area covered by fires under item 'Savanna' and in year 2005.

# **Selected countries Analysis**

## 1.Select countries

- Select countries

```python
df_selected = df[df["Area"].isin(["India", "Afghanistan", "Pakistan","Bangladesh"])]
```

- Afganistan, India, Pakistan and Bangladesh are the selected countries in south Asia

| Area | Value|
|:-------|------:|
India	|	6.546250e+07
Bangladesh	| 2.536032e+06
Pakistan	|	1.015368e+06
Afghanistan	|	1.004836e+06


- From the above analysis we can say that India is the most affected country from Selected countries in south Asia with value of **6.546250e+07**

- Afghanistan is least affected country from Selected countries in south Asia with value of **1.004836e+06**

## 2. Item type burned by fire in selected countries

- Item type burned by fire in selected countries

```python
df_selected.groupby(["Item"]).sum().sort_values(by="Value", ascending=False).head(10)
```

|Item  | Value|
|:-------|-----:|
Other forest	|	2.952522e+07
Woody savanna	|	1.180380e+07
Humid tropical forest	|	1.146947e+07
Grassland	|	9.088783e+06
Savanna	|	7.766206e+06
Open shrubland	|	3.090104e+05
Closed shrubland	|	5.624728e+04

- From the selected countries in south Asia, the most burned item type is **Other forest** with value of **2.952522e+07**

- Least burned item type is **Closed shrubland** with value of **5.624728e+04**

## 3. Most burned area in selected countries in a year

- Most burned area in selected countries in a year

```python
df_selected.groupby("Year").sum().sort_values(by="Value", ascending=False)
```

|Year |Value|
|:-------|-----:|
2009	|	5.714089e+06
2012	|	5.213439e+06
2010	|	4.137277e+06
2017	|	3.678856e+06
2018	|	3.413934e+06
2004	|	3.287813e+06
2007	|	2.961845e+06
2013	|	2.921003e+06
2014	|	2.766442e+06
2016	|	2.717386e+06
2008	|	2.498098e+06
2011	|	2.491687e+06
1995	|	2.338895e+06
1994	|	2.338895e+06
1993	|	2.338895e+06
1991	|	2.338895e+06
1992	|	2.338895e+06
1990	|	2.338895e+06
2006	|	2.243740e+06
2003	|	2.178761e+06
2019	|	1.923328e+06
2015	|	1.897175e+06
2005	|	1.862174e+06
2001	|	1.099192e+06
2002	|	6.803164e+05
1999	|	6.271583e+05
1998	|	4.767263e+05
1996	|	4.493037e+05
2000	|	4.126897e+05
1997	|	3.329337e+05

- From the above table it is clear the most area burned in a year is in year **2009** with value of **5.714089e+06**

- Minimum area burned in a year is in year **1997** with value of **3.329337e+05**

## 4. Graphical analysis of selected countries

- Graphical analysis of selected countries

```python
plt.figure(figsize=(15,8), dpi=150)
sns.set(font_scale=1)
sns.set_style("whitegrid")
sns.lineplot(x="Year",y="Value",hue="Area",style="Item",data=df_selected)
plt.title("Fires by year and area")
```

![](Selected%20countries.png)

- Above graph is visualized to show the fires by year and area of selected countries with the style of line for the item type.
- India has the most area covered by fires under item 'Other Forest' and in year 2009.


# **Conclusion**

- As far as the whole data is concerned, 
  - Australia is the top country having maximum area of fire.
  - Savanna is the top item having maximum area under fire.
  - 2012 is the leading year having maximum area under fire.
- In Continent Analysis,
  - The most affected continent is Africa and the least one is North America.
  - Year wise 2005 is most affected by fires.
  - Africa has the most area covered by fires under item 'Savanna' and in year 2005.
- For selected countries, India, Afghanistan, Pakistan and Bangladesh,
  - India is most affected country by fires and Afghanistan is the least affected one.
  - Item affected most is other forest while least affected one is closed shrubland.
  - The most affected year by fires w.r.t is 2009 while the least affected one is 1997.
