# Super-Store-Sales-Analysis

# Import Libraries


```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```


```python
import pandas as pd
pd.set_option('display.float_format', lambda x: '%.3f' % x)
```


```python
import warnings
warnings.filterwarnings('ignore')
```

# Loading DataSet


```python
df = pd.read_csv(r'C:\Users\appus\Downloads\superstore_dataset2011-2015.csv',encoding='latin1')
```

# Exploratory Data Analysis and Cleaning


```python
df.head(100)
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
      <th>Row ID</th>
      <th>Order ID</th>
      <th>Order Date</th>
      <th>Ship Date</th>
      <th>Ship Mode</th>
      <th>Customer ID</th>
      <th>Customer Name</th>
      <th>Segment</th>
      <th>City</th>
      <th>State</th>
      <th>...</th>
      <th>Product ID</th>
      <th>Category</th>
      <th>Sub-Category</th>
      <th>Product Name</th>
      <th>Sales</th>
      <th>Quantity</th>
      <th>Discount</th>
      <th>Profit</th>
      <th>Shipping Cost</th>
      <th>Order Priority</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>42433</td>
      <td>AG-2011-2040</td>
      <td>1/1/2011</td>
      <td>6/1/2011</td>
      <td>Standard Class</td>
      <td>TB-11280</td>
      <td>Toby Braunhardt</td>
      <td>Consumer</td>
      <td>Constantine</td>
      <td>Constantine</td>
      <td>...</td>
      <td>OFF-TEN-10000025</td>
      <td>Office Supplies</td>
      <td>Storage</td>
      <td>Tenex Lockers, Blue</td>
      <td>408.300</td>
      <td>2</td>
      <td>0.000</td>
      <td>106.140</td>
      <td>35.460</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>1</th>
      <td>22253</td>
      <td>IN-2011-47883</td>
      <td>1/1/2011</td>
      <td>8/1/2011</td>
      <td>Standard Class</td>
      <td>JH-15985</td>
      <td>Joseph Holt</td>
      <td>Consumer</td>
      <td>Wagga Wagga</td>
      <td>New South Wales</td>
      <td>...</td>
      <td>OFF-SU-10000618</td>
      <td>Office Supplies</td>
      <td>Supplies</td>
      <td>Acme Trimmer, High Speed</td>
      <td>120.366</td>
      <td>3</td>
      <td>0.100</td>
      <td>36.036</td>
      <td>9.720</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>2</th>
      <td>48883</td>
      <td>HU-2011-1220</td>
      <td>1/1/2011</td>
      <td>5/1/2011</td>
      <td>Second Class</td>
      <td>AT-735</td>
      <td>Annie Thurman</td>
      <td>Consumer</td>
      <td>Budapest</td>
      <td>Budapest</td>
      <td>...</td>
      <td>OFF-TEN-10001585</td>
      <td>Office Supplies</td>
      <td>Storage</td>
      <td>Tenex Box, Single Width</td>
      <td>66.120</td>
      <td>4</td>
      <td>0.000</td>
      <td>29.640</td>
      <td>8.170</td>
      <td>High</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11731</td>
      <td>IT-2011-3647632</td>
      <td>1/1/2011</td>
      <td>5/1/2011</td>
      <td>Second Class</td>
      <td>EM-14140</td>
      <td>Eugene Moren</td>
      <td>Home Office</td>
      <td>Stockholm</td>
      <td>Stockholm</td>
      <td>...</td>
      <td>OFF-PA-10001492</td>
      <td>Office Supplies</td>
      <td>Paper</td>
      <td>Enermax Note Cards, Premium</td>
      <td>44.865</td>
      <td>3</td>
      <td>0.500</td>
      <td>-26.055</td>
      <td>4.820</td>
      <td>High</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22255</td>
      <td>IN-2011-47883</td>
      <td>1/1/2011</td>
      <td>8/1/2011</td>
      <td>Standard Class</td>
      <td>JH-15985</td>
      <td>Joseph Holt</td>
      <td>Consumer</td>
      <td>Wagga Wagga</td>
      <td>New South Wales</td>
      <td>...</td>
      <td>FUR-FU-10003447</td>
      <td>Furniture</td>
      <td>Furnishings</td>
      <td>Eldon Light Bulb, Duo Pack</td>
      <td>113.670</td>
      <td>5</td>
      <td>0.100</td>
      <td>37.770</td>
      <td>4.700</td>
      <td>Medium</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>95</th>
      <td>3684</td>
      <td>US-2011-148852</td>
      <td>1/4/2011</td>
      <td>4/4/2011</td>
      <td>Second Class</td>
      <td>VP-21760</td>
      <td>Victoria Pisteka</td>
      <td>Corporate</td>
      <td>Arraiján</td>
      <td>Panama</td>
      <td>...</td>
      <td>OFF-BI-10004305</td>
      <td>Office Supplies</td>
      <td>Binders</td>
      <td>Cardinal Hole Reinforcements, Durable</td>
      <td>10.944</td>
      <td>4</td>
      <td>0.400</td>
      <td>-3.136</td>
      <td>1.370</td>
      <td>High</td>
    </tr>
    <tr>
      <th>96</th>
      <td>2463</td>
      <td>MX-2011-167773</td>
      <td>1/4/2011</td>
      <td>5/4/2011</td>
      <td>Standard Class</td>
      <td>LS-17245</td>
      <td>Lynn Smith</td>
      <td>Consumer</td>
      <td>Bogotá</td>
      <td>Bogota</td>
      <td>...</td>
      <td>OFF-BI-10002222</td>
      <td>Office Supplies</td>
      <td>Binders</td>
      <td>Cardinal Binder Covers, Clear</td>
      <td>15.280</td>
      <td>2</td>
      <td>0.000</td>
      <td>1.960</td>
      <td>1.200</td>
      <td>High</td>
    </tr>
    <tr>
      <th>97</th>
      <td>32670</td>
      <td>US-2011-157021</td>
      <td>1/4/2011</td>
      <td>6/4/2011</td>
      <td>Second Class</td>
      <td>KM-16720</td>
      <td>Kunst Miller</td>
      <td>Consumer</td>
      <td>Vallejo</td>
      <td>California</td>
      <td>...</td>
      <td>OFF-BI-10000042</td>
      <td>Office Supplies</td>
      <td>Binders</td>
      <td>Pressboard Data Binder, Crimson, 12" X 8 1/2"</td>
      <td>17.088</td>
      <td>4</td>
      <td>0.200</td>
      <td>5.554</td>
      <td>0.650</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>98</th>
      <td>39251</td>
      <td>CA-2011-138359</td>
      <td>1/4/2011</td>
      <td>6/4/2011</td>
      <td>Standard Class</td>
      <td>KH-16330</td>
      <td>Katharine Harms</td>
      <td>Corporate</td>
      <td>Revere</td>
      <td>Massachusetts</td>
      <td>...</td>
      <td>OFF-BI-10000145</td>
      <td>Office Supplies</td>
      <td>Binders</td>
      <td>Zipper Ring Binder Pockets</td>
      <td>6.240</td>
      <td>2</td>
      <td>0.000</td>
      <td>3.058</td>
      <td>0.340</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>99</th>
      <td>22375</td>
      <td>ID-2011-77192</td>
      <td>1/4/2011</td>
      <td>5/4/2011</td>
      <td>Standard Class</td>
      <td>RP-19270</td>
      <td>Rachel Payne</td>
      <td>Corporate</td>
      <td>Aew?l-li</td>
      <td>Jeju</td>
      <td>...</td>
      <td>OFF-LA-10001764</td>
      <td>Office Supplies</td>
      <td>Labels</td>
      <td>Avery Round Labels, Adjustable</td>
      <td>10.080</td>
      <td>4</td>
      <td>0.500</td>
      <td>-9.120</td>
      <td>0.320</td>
      <td>Medium</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 24 columns</p>
</div>




```python
df.tail()
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
      <th>Row ID</th>
      <th>Order ID</th>
      <th>Order Date</th>
      <th>Ship Date</th>
      <th>Ship Mode</th>
      <th>Customer ID</th>
      <th>Customer Name</th>
      <th>Segment</th>
      <th>City</th>
      <th>State</th>
      <th>...</th>
      <th>Product ID</th>
      <th>Category</th>
      <th>Sub-Category</th>
      <th>Product Name</th>
      <th>Sales</th>
      <th>Quantity</th>
      <th>Discount</th>
      <th>Profit</th>
      <th>Shipping Cost</th>
      <th>Order Priority</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>51285</th>
      <td>32593</td>
      <td>CA-2014-115427</td>
      <td>31-12-2014</td>
      <td>4/1/2015</td>
      <td>Standard Class</td>
      <td>EB-13975</td>
      <td>Erica Bern</td>
      <td>Corporate</td>
      <td>Fairfield</td>
      <td>California</td>
      <td>...</td>
      <td>OFF-BI-10002103</td>
      <td>Office Supplies</td>
      <td>Binders</td>
      <td>Cardinal Slant-D Ring Binder, Heavy Gauge Vinyl</td>
      <td>13.904</td>
      <td>2</td>
      <td>0.200</td>
      <td>4.519</td>
      <td>0.890</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>51286</th>
      <td>47594</td>
      <td>MO-2014-2560</td>
      <td>31-12-2014</td>
      <td>5/1/2015</td>
      <td>Standard Class</td>
      <td>LP-7095</td>
      <td>Liz Preis</td>
      <td>Consumer</td>
      <td>Agadir</td>
      <td>Souss-Massa-Draâ</td>
      <td>...</td>
      <td>OFF-WIL-10001069</td>
      <td>Office Supplies</td>
      <td>Binders</td>
      <td>Wilson Jones Hole Reinforcements, Clear</td>
      <td>3.990</td>
      <td>1</td>
      <td>0.000</td>
      <td>0.420</td>
      <td>0.490</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>51287</th>
      <td>8857</td>
      <td>MX-2014-110527</td>
      <td>31-12-2014</td>
      <td>2/1/2015</td>
      <td>Second Class</td>
      <td>CM-12190</td>
      <td>Charlotte Melton</td>
      <td>Consumer</td>
      <td>Managua</td>
      <td>Managua</td>
      <td>...</td>
      <td>OFF-LA-10004182</td>
      <td>Office Supplies</td>
      <td>Labels</td>
      <td>Hon Color Coded Labels, 5000 Label Set</td>
      <td>26.400</td>
      <td>3</td>
      <td>0.000</td>
      <td>12.360</td>
      <td>0.350</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>51288</th>
      <td>6852</td>
      <td>MX-2014-114783</td>
      <td>31-12-2014</td>
      <td>6/1/2015</td>
      <td>Standard Class</td>
      <td>TD-20995</td>
      <td>Tamara Dahlen</td>
      <td>Consumer</td>
      <td>Juárez</td>
      <td>Chihuahua</td>
      <td>...</td>
      <td>OFF-LA-10000413</td>
      <td>Office Supplies</td>
      <td>Labels</td>
      <td>Hon Legal Exhibit Labels, Alphabetical</td>
      <td>7.120</td>
      <td>1</td>
      <td>0.000</td>
      <td>0.560</td>
      <td>0.200</td>
      <td>Medium</td>
    </tr>
    <tr>
      <th>51289</th>
      <td>36388</td>
      <td>CA-2014-156720</td>
      <td>31-12-2014</td>
      <td>4/1/2015</td>
      <td>Standard Class</td>
      <td>JM-15580</td>
      <td>Jill Matthias</td>
      <td>Consumer</td>
      <td>Loveland</td>
      <td>Colorado</td>
      <td>...</td>
      <td>OFF-FA-10003472</td>
      <td>Office Supplies</td>
      <td>Fasteners</td>
      <td>Bagged Rubber Bands</td>
      <td>3.024</td>
      <td>3</td>
      <td>0.200</td>
      <td>-0.605</td>
      <td>0.170</td>
      <td>Medium</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 24 columns</p>
</div>




```python
# Shape of the DataSet
```


```python
df.shape
```




    (51290, 24)




```python
# Information About Dataset like Total Rows,Columns 
```


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 51290 entries, 0 to 51289
    Data columns (total 24 columns):
     #   Column          Non-Null Count  Dtype  
    ---  ------          --------------  -----  
     0   Row ID          51290 non-null  int64  
     1   Order ID        51290 non-null  object 
     2   Order Date      51290 non-null  object 
     3   Ship Date       51290 non-null  object 
     4   Ship Mode       51290 non-null  object 
     5   Customer ID     51290 non-null  object 
     6   Customer Name   51290 non-null  object 
     7   Segment         51290 non-null  object 
     8   City            51290 non-null  object 
     9   State           51290 non-null  object 
     10  Country         51290 non-null  object 
     11  Postal Code     9994 non-null   float64
     12  Market          51290 non-null  object 
     13  Region          51290 non-null  object 
     14  Product ID      51290 non-null  object 
     15  Category        51290 non-null  object 
     16  Sub-Category    51290 non-null  object 
     17  Product Name    51290 non-null  object 
     18  Sales           51290 non-null  float64
     19  Quantity        51290 non-null  int64  
     20  Discount        51290 non-null  float64
     21  Profit          51290 non-null  float64
     22  Shipping Cost   51290 non-null  float64
     23  Order Priority  51290 non-null  object 
    dtypes: float64(5), int64(2), object(17)
    memory usage: 9.4+ MB
    


```python
# Null Values in Dataset
```


```python
df.isnull().sum()
```




    Row ID                0
    Order ID              0
    Order Date            0
    Ship Date             0
    Ship Mode             0
    Customer ID           0
    Customer Name         0
    Segment               0
    City                  0
    State                 0
    Country               0
    Postal Code       41296
    Market                0
    Region                0
    Product ID            0
    Category              0
    Sub-Category          0
    Product Name          0
    Sales                 0
    Quantity              0
    Discount              0
    Profit                0
    Shipping Cost         0
    Order Priority        0
    dtype: int64




```python
# Check Duplicate Data and Drop Them
```


```python
df.duplicated().any()
```




    False




```python
# Statistics of the Dataset
```


```python
df.describe()
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
      <th>Row ID</th>
      <th>Postal Code</th>
      <th>Sales</th>
      <th>Quantity</th>
      <th>Discount</th>
      <th>Profit</th>
      <th>Shipping Cost</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>51290.000</td>
      <td>9994.000</td>
      <td>51290.000</td>
      <td>51290.000</td>
      <td>51290.000</td>
      <td>51290.000</td>
      <td>51290.000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>25645.500</td>
      <td>55190.379</td>
      <td>246.491</td>
      <td>3.477</td>
      <td>0.143</td>
      <td>28.611</td>
      <td>26.376</td>
    </tr>
    <tr>
      <th>std</th>
      <td>14806.292</td>
      <td>32063.693</td>
      <td>487.565</td>
      <td>2.279</td>
      <td>0.212</td>
      <td>174.341</td>
      <td>57.297</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000</td>
      <td>1040.000</td>
      <td>0.444</td>
      <td>1.000</td>
      <td>0.000</td>
      <td>-6599.978</td>
      <td>0.000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>12823.250</td>
      <td>23223.000</td>
      <td>30.759</td>
      <td>2.000</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>2.610</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>25645.500</td>
      <td>56430.500</td>
      <td>85.053</td>
      <td>3.000</td>
      <td>0.000</td>
      <td>9.240</td>
      <td>7.790</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>38467.750</td>
      <td>90008.000</td>
      <td>251.053</td>
      <td>5.000</td>
      <td>0.200</td>
      <td>36.810</td>
      <td>24.450</td>
    </tr>
    <tr>
      <th>max</th>
      <td>51290.000</td>
      <td>99301.000</td>
      <td>22638.480</td>
      <td>14.000</td>
      <td>0.850</td>
      <td>8399.976</td>
      <td>933.570</td>
    </tr>
  </tbody>
</table>
</div>



# Remove Unnecessary Columns


```python
df.columns
```




    Index(['Row ID', 'Order ID', 'Order Date', 'Ship Date', 'Ship Mode',
           'Customer ID', 'Customer Name', 'Segment', 'City', 'State', 'Country',
           'Postal Code', 'Market', 'Region', 'Product ID', 'Category',
           'Sub-Category', 'Product Name', 'Sales', 'Quantity', 'Discount',
           'Profit', 'Shipping Cost', 'Order Priority'],
          dtype='object')




```python
df=df.drop(['Row ID' , 'Order ID' , 'Customer ID' , 'Postal Code'],axis=1)
```


```python
df.columns
```




    Index(['Order Date', 'Ship Date', 'Ship Mode', 'Customer Name', 'Segment',
           'City', 'State', 'Country', 'Market', 'Region', 'Product ID',
           'Category', 'Sub-Category', 'Product Name', 'Sales', 'Quantity',
           'Discount', 'Profit', 'Shipping Cost', 'Order Priority'],
          dtype='object')



# 1 : Technology products Highest Profit Margin Compared to Other Product Categories


```python
cat_profit=df.groupby('Category')['Profit'].sum()
cat_profit.plot(kind='bar')
plt.title("Profit by Category")
plt.xlabel("Category")
plt.ylabel("Total Profit")
plt.show()
```


    
![png](output_24_0.png)
    


# 2 : East region has highest sales compared to other regions


```python
reg_sales=df.groupby('Region')['Sales'].sum()
reg_sales.plot(kind="bar")
plt.title("Total Sales by Region")
plt.xlabel("Region")
plt.ylabel("Total Sales")
plt.show()
```


    
![png](output_26_0.png)
    


# 3 : Sales are higher during certain months of the year


```python
df['Order Month']=pd.DatetimeIndex(df['Order Date']).month

month_sales=df.groupby('Order Month')['Sales'].sum()
month_sales.plot(kind='line')
plt.title("Total Sales by Month")
plt.xlabel("Month")
plt.ylabel("Total Sales")
plt.show()
```


    
![png](output_28_0.png)
    


 # 4 : The company's profit is more on weekdays than on weekends


```python
df['Order Day']=pd.DatetimeIndex(df['Order Date']).day_name()

day_profit=df.groupby('Order Day')['Profit'].sum()
day_profit.plot(kind="bar")
plt.title("Total Profit by the day of the week")
plt.xlabel("Day of the week")
plt.ylabel("Total Profit")
plt.show()
```


    
![png](output_30_0.png)
    



```python
plt.style.use("fivethirtyeight")
slices =cat_profit=df.groupby('Category')['Profit'].sum()
cat_profit.plot(kind='bar')
plt.title("Profit by Category")
plt.xlabel("Category")
plt.ylabel("Total Profit")
plt.show()
```


    
![png](output_31_0.png)
    



```python
df['Category'].value_counts().plot(kind="pie",autopct="%1.2f%%")
plt.title(' Overall CategoryList')
plt.ylabel('')  
plt.show()
```


    
![png](output_32_0.png)
    



```python

```


```python

```


```python

```


```python

```
