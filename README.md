### Importing packages and mapping entry files


```python
import pandas as pd
import numpy as np

time = pd.read_csv("Time.csv")
store = pd.read_csv("Store.csv")
sales = pd.read_csv("Sales.csv")
product = pd.read_csv("Product.csv")
customer = pd.read_csv("Customer.csv")
currency = pd.read_csv("CurrencyConversion.csv")
```

### Removing duplicates from time table and adding weekdays


```python
time = time.drop_duplicates()
time['Weekday'] = pd.to_datetime(time['Date'], errors='coerce')
time['Weekday']= time['Weekday'].dt.day_name()
time = time[['MemberId', 'Date', 'MonthName', 'Month', 'QuarterName', 'Quarter', 'Year', 'YearName', 'Weekday']]
time
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
      <th>MemberId</th>
      <th>Date</th>
      <th>MonthName</th>
      <th>Month</th>
      <th>QuarterName</th>
      <th>Quarter</th>
      <th>Year</th>
      <th>YearName</th>
      <th>Weekday</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20200504</td>
      <td>04/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Sunday</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20200505</td>
      <td>05/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Tuesday</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20200506</td>
      <td>06/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20200507</td>
      <td>07/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Sunday</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20200508</td>
      <td>08/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>5</th>
      <td>20200509</td>
      <td>09/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Saturday</td>
    </tr>
    <tr>
      <th>6</th>
      <td>20200510</td>
      <td>10/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>7</th>
      <td>20200511</td>
      <td>11/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Thursday</td>
    </tr>
    <tr>
      <th>8</th>
      <td>20200512</td>
      <td>12/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Saturday</td>
    </tr>
    <tr>
      <th>9</th>
      <td>20200513</td>
      <td>13/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>10</th>
      <td>20200514</td>
      <td>14/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Thursday</td>
    </tr>
    <tr>
      <th>11</th>
      <td>20200515</td>
      <td>15/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>12</th>
      <td>20200516</td>
      <td>16/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Saturday</td>
    </tr>
    <tr>
      <th>13</th>
      <td>20200517</td>
      <td>17/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Sunday</td>
    </tr>
    <tr>
      <th>14</th>
      <td>20200518</td>
      <td>18/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>15</th>
      <td>20200519</td>
      <td>19/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Tuesday</td>
    </tr>
    <tr>
      <th>16</th>
      <td>20200520</td>
      <td>20/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>17</th>
      <td>20200521</td>
      <td>21/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Thursday</td>
    </tr>
    <tr>
      <th>18</th>
      <td>20200522</td>
      <td>22/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20200523</td>
      <td>23/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Saturday</td>
    </tr>
    <tr>
      <th>20</th>
      <td>20200524</td>
      <td>24/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Sunday</td>
    </tr>
    <tr>
      <th>21</th>
      <td>20200525</td>
      <td>25/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>22</th>
      <td>20200526</td>
      <td>26/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Tuesday</td>
    </tr>
    <tr>
      <th>23</th>
      <td>20200527</td>
      <td>27/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>24</th>
      <td>20200528</td>
      <td>28/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Thursday</td>
    </tr>
    <tr>
      <th>25</th>
      <td>20200529</td>
      <td>29/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>26</th>
      <td>20200530</td>
      <td>30/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Saturday</td>
    </tr>
    <tr>
      <th>27</th>
      <td>20200531</td>
      <td>31/05/2020</td>
      <td>May-20</td>
      <td>202005</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Sunday</td>
    </tr>
    <tr>
      <th>28</th>
      <td>20200601</td>
      <td>01/06/2020</td>
      <td>Jun-20</td>
      <td>202006</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>29</th>
      <td>20200602</td>
      <td>02/06/2020</td>
      <td>Jun-20</td>
      <td>202006</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Thursday</td>
    </tr>
    <tr>
      <th>30</th>
      <td>20200603</td>
      <td>03/06/2020</td>
      <td>Jun-20</td>
      <td>202006</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>31</th>
      <td>20200604</td>
      <td>04/06/2020</td>
      <td>Jun-20</td>
      <td>202006</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>32</th>
      <td>20200605</td>
      <td>05/06/2020</td>
      <td>Jun-20</td>
      <td>202006</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>33</th>
      <td>20200606</td>
      <td>06/06/2020</td>
      <td>Jun-20</td>
      <td>202006</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Saturday</td>
    </tr>
  </tbody>
</table>
</div>




```python
time.to_csv('Time_no_duplicates.csv')
```

### Renaming store columns and adding VAT field


```python
store.columns = ['Store', 'Store Name', 'Store Location'] 
vat = ['18%', '18%', '0%']
store['VAT'] = vat
store['VAT float'] = store['VAT'].str.replace('%','').astype(float)/100

store
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
      <th>Store</th>
      <th>Store Name</th>
      <th>Store Location</th>
      <th>VAT</th>
      <th>VAT float</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>18%</td>
      <td>0.18</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
    </tr>
  </tbody>
</table>
</div>




```python
store.to_csv('store_vat_added.csv')
```

### Renaming sales columns


```python
sales.columns = ['Date', 'Store', 'Product No', 'Customer No', 'QTY']

sales
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
      <th>Date</th>
      <th>Store</th>
      <th>Product No</th>
      <th>Customer No</th>
      <th>QTY</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>04/05/2020</td>
      <td>1</td>
      <td>3</td>
      <td>29</td>
      <td>60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>05/05/2020</td>
      <td>2</td>
      <td>8</td>
      <td>26</td>
      <td>67</td>
    </tr>
    <tr>
      <th>2</th>
      <td>06/05/2020</td>
      <td>3</td>
      <td>5</td>
      <td>12</td>
      <td>68</td>
    </tr>
    <tr>
      <th>3</th>
      <td>07/05/2020</td>
      <td>1</td>
      <td>6</td>
      <td>22</td>
      <td>52</td>
    </tr>
    <tr>
      <th>4</th>
      <td>08/05/2020</td>
      <td>1</td>
      <td>1</td>
      <td>29</td>
      <td>78</td>
    </tr>
    <tr>
      <th>5</th>
      <td>09/05/2020</td>
      <td>2</td>
      <td>9</td>
      <td>23</td>
      <td>82</td>
    </tr>
    <tr>
      <th>6</th>
      <td>10/05/2020</td>
      <td>1</td>
      <td>7</td>
      <td>12</td>
      <td>87</td>
    </tr>
    <tr>
      <th>7</th>
      <td>11/05/2020</td>
      <td>3</td>
      <td>9</td>
      <td>30</td>
      <td>90</td>
    </tr>
    <tr>
      <th>8</th>
      <td>12/05/2020</td>
      <td>2</td>
      <td>4</td>
      <td>9</td>
      <td>66</td>
    </tr>
    <tr>
      <th>9</th>
      <td>13/05/2020</td>
      <td>2</td>
      <td>1</td>
      <td>14</td>
      <td>57</td>
    </tr>
    <tr>
      <th>10</th>
      <td>14/05/2020</td>
      <td>2</td>
      <td>5</td>
      <td>7</td>
      <td>98</td>
    </tr>
    <tr>
      <th>11</th>
      <td>15/05/2020</td>
      <td>2</td>
      <td>9</td>
      <td>16</td>
      <td>59</td>
    </tr>
    <tr>
      <th>12</th>
      <td>16/05/2020</td>
      <td>2</td>
      <td>6</td>
      <td>18</td>
      <td>77</td>
    </tr>
    <tr>
      <th>13</th>
      <td>17/05/2020</td>
      <td>3</td>
      <td>3</td>
      <td>8</td>
      <td>93</td>
    </tr>
    <tr>
      <th>14</th>
      <td>18/05/2020</td>
      <td>1</td>
      <td>10</td>
      <td>21</td>
      <td>63</td>
    </tr>
    <tr>
      <th>15</th>
      <td>19/05/2020</td>
      <td>1</td>
      <td>4</td>
      <td>20</td>
      <td>96</td>
    </tr>
    <tr>
      <th>16</th>
      <td>20/05/2020</td>
      <td>2</td>
      <td>3</td>
      <td>28</td>
      <td>90</td>
    </tr>
    <tr>
      <th>17</th>
      <td>21/05/2020</td>
      <td>2</td>
      <td>3</td>
      <td>1</td>
      <td>79</td>
    </tr>
    <tr>
      <th>18</th>
      <td>22/05/2020</td>
      <td>3</td>
      <td>2</td>
      <td>30</td>
      <td>52</td>
    </tr>
    <tr>
      <th>19</th>
      <td>23/05/2020</td>
      <td>3</td>
      <td>7</td>
      <td>24</td>
      <td>67</td>
    </tr>
    <tr>
      <th>20</th>
      <td>24/05/2020</td>
      <td>3</td>
      <td>10</td>
      <td>8</td>
      <td>83</td>
    </tr>
    <tr>
      <th>21</th>
      <td>25/05/2020</td>
      <td>2</td>
      <td>9</td>
      <td>8</td>
      <td>93</td>
    </tr>
    <tr>
      <th>22</th>
      <td>26/05/2020</td>
      <td>2</td>
      <td>6</td>
      <td>5</td>
      <td>57</td>
    </tr>
    <tr>
      <th>23</th>
      <td>27/05/2020</td>
      <td>2</td>
      <td>1</td>
      <td>30</td>
      <td>89</td>
    </tr>
    <tr>
      <th>24</th>
      <td>28/05/2020</td>
      <td>2</td>
      <td>8</td>
      <td>24</td>
      <td>58</td>
    </tr>
    <tr>
      <th>25</th>
      <td>29/05/2020</td>
      <td>3</td>
      <td>2</td>
      <td>21</td>
      <td>100</td>
    </tr>
    <tr>
      <th>26</th>
      <td>30/05/2020</td>
      <td>3</td>
      <td>7</td>
      <td>28</td>
      <td>77</td>
    </tr>
    <tr>
      <th>27</th>
      <td>31/05/2020</td>
      <td>1</td>
      <td>10</td>
      <td>28</td>
      <td>86</td>
    </tr>
    <tr>
      <th>28</th>
      <td>01/06/2020</td>
      <td>2</td>
      <td>2</td>
      <td>28</td>
      <td>74</td>
    </tr>
    <tr>
      <th>29</th>
      <td>02/06/2020</td>
      <td>1</td>
      <td>7</td>
      <td>5</td>
      <td>83</td>
    </tr>
    <tr>
      <th>30</th>
      <td>03/06/2020</td>
      <td>3</td>
      <td>4</td>
      <td>25</td>
      <td>72</td>
    </tr>
    <tr>
      <th>31</th>
      <td>04/06/2020</td>
      <td>3</td>
      <td>3</td>
      <td>11</td>
      <td>90</td>
    </tr>
    <tr>
      <th>32</th>
      <td>05/06/2020</td>
      <td>3</td>
      <td>6</td>
      <td>30</td>
      <td>64</td>
    </tr>
    <tr>
      <th>33</th>
      <td>06/06/2020</td>
      <td>2</td>
      <td>4</td>
      <td>8</td>
      <td>81</td>
    </tr>
  </tbody>
</table>
</div>




```python
sales.to_csv('sales_renamed.csv')
```

### Printing product table


```python
product
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
      <th>Product No</th>
      <th>Product</th>
      <th>Price</th>
      <th>Currency</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Product A</td>
      <td>26.0</td>
      <td>USD</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Product B</td>
      <td>37.0</td>
      <td>EUR</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Product C</td>
      <td>46.0</td>
      <td>USD</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Product D</td>
      <td>34.0</td>
      <td>USD</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Product E</td>
      <td>11.0</td>
      <td>EUR</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>Product F</td>
      <td>15.0</td>
      <td>EUR</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>Product G</td>
      <td>20.0</td>
      <td>USD</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>Product H</td>
      <td>45.0</td>
      <td>EUR</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>Product I</td>
      <td>31.0</td>
      <td>EUR</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>Product J</td>
      <td>25.0</td>
      <td>USD</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>Product K</td>
      <td>50.0</td>
      <td>EUR</td>
    </tr>
  </tbody>
</table>
</div>



### Printing customer table


```python
customer = customer.rename(columns=lambda x: x.strip())
customer['Customer'] = customer['Customer'].str.replace(' -', '')

customer
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
      <th>Customer No</th>
      <th>Customer</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Customer 001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Customer 002</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Customer 003</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Customer 004</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Customer 005</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>Customer 006</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>Customer 007</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>Customer 008</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>Customer 009</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>Customer 010</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>Customer 011</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>Customer 012</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>Customer 013</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>Customer 014</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>Customer 015</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>Customer 016</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>Customer 017</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>Customer 018</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>Customer 019</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>Customer 020</td>
    </tr>
    <tr>
      <th>20</th>
      <td>21</td>
      <td>Customer 021</td>
    </tr>
    <tr>
      <th>21</th>
      <td>22</td>
      <td>Customer 022</td>
    </tr>
    <tr>
      <th>22</th>
      <td>23</td>
      <td>Customer 023</td>
    </tr>
    <tr>
      <th>23</th>
      <td>24</td>
      <td>Customer 024</td>
    </tr>
    <tr>
      <th>24</th>
      <td>25</td>
      <td>Customer 025</td>
    </tr>
    <tr>
      <th>25</th>
      <td>26</td>
      <td>Customer 026</td>
    </tr>
    <tr>
      <th>26</th>
      <td>27</td>
      <td>Customer 027</td>
    </tr>
    <tr>
      <th>27</th>
      <td>28</td>
      <td>Customer 028</td>
    </tr>
    <tr>
      <th>28</th>
      <td>29</td>
      <td>Customer 029</td>
    </tr>
    <tr>
      <th>29</th>
      <td>30</td>
      <td>Customer 030</td>
    </tr>
  </tbody>
</table>
</div>




```python
sales.to_csv('sales_renamed.csv')
```

### Updading currency table


```python
currency.columns = ['Currency From', 'Currency To', 'Conversion Rate', 'From', 'To']

currency['To'] = 20201130, 20200602, 20201130
currency
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
      <th>Currency From</th>
      <th>Currency To</th>
      <th>Conversion Rate</th>
      <th>From</th>
      <th>To</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>EUR</td>
      <td>EUR</td>
      <td>1.00</td>
      <td>20200101</td>
      <td>20201130</td>
    </tr>
    <tr>
      <th>1</th>
      <td>USD</td>
      <td>EUR</td>
      <td>1.10</td>
      <td>20200101</td>
      <td>20200602</td>
    </tr>
    <tr>
      <th>2</th>
      <td>USD</td>
      <td>EUR</td>
      <td>1.18</td>
      <td>20200603</td>
      <td>20201130</td>
    </tr>
  </tbody>
</table>
</div>




```python
currency.to_csv('currency_renamed.csv')
```

### Creating master merge


```python
sales_store = sales.merge(store, how='left', on='Store')
sales_store_customer = sales_store.merge(customer, how='left', on='Customer No')
sales_store_customer_product = sales_store_customer.merge(product, how='left', on='Product No')
sales_store_customer_product_time = sales_store_customer_product.merge(time, how='left', on='Date')
sales_store_customer_product_time_currency = sales_store_customer_product_time.merge(currency, how='left', left_on='Currency', right_on='Currency From')
master_merge = sales_store_customer_product_time_currency
master_merge = master_merge.drop(master_merge[(master_merge.Currency == 'USD') & (master_merge.MemberId > master_merge.To)].index)
master_merge = master_merge.drop(master_merge[(master_merge.MemberId < master_merge.From)].index)
master_merge.reset_index(drop=True, inplace=True)

master_merge

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
      <th>Date</th>
      <th>Store</th>
      <th>Product No</th>
      <th>Customer No</th>
      <th>QTY</th>
      <th>Store Name</th>
      <th>Store Location</th>
      <th>VAT</th>
      <th>VAT float</th>
      <th>Customer</th>
      <th>...</th>
      <th>QuarterName</th>
      <th>Quarter</th>
      <th>Year</th>
      <th>YearName</th>
      <th>Weekday</th>
      <th>Currency From</th>
      <th>Currency To</th>
      <th>Conversion Rate</th>
      <th>From</th>
      <th>To</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>04/05/2020</td>
      <td>1</td>
      <td>3</td>
      <td>29</td>
      <td>60</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 029</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Sunday</td>
      <td>USD</td>
      <td>EUR</td>
      <td>1.10</td>
      <td>20200101</td>
      <td>20200602</td>
    </tr>
    <tr>
      <th>1</th>
      <td>05/05/2020</td>
      <td>2</td>
      <td>8</td>
      <td>26</td>
      <td>67</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 026</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Tuesday</td>
      <td>EUR</td>
      <td>EUR</td>
      <td>1.00</td>
      <td>20200101</td>
      <td>20201130</td>
    </tr>
    <tr>
      <th>2</th>
      <td>06/05/2020</td>
      <td>3</td>
      <td>5</td>
      <td>12</td>
      <td>68</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 012</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Friday</td>
      <td>EUR</td>
      <td>EUR</td>
      <td>1.00</td>
      <td>20200101</td>
      <td>20201130</td>
    </tr>
    <tr>
      <th>3</th>
      <td>07/05/2020</td>
      <td>1</td>
      <td>6</td>
      <td>22</td>
      <td>52</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 022</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Sunday</td>
      <td>EUR</td>
      <td>EUR</td>
      <td>1.00</td>
      <td>20200101</td>
      <td>20201130</td>
    </tr>
    <tr>
      <th>4</th>
      <td>08/05/2020</td>
      <td>1</td>
      <td>1</td>
      <td>29</td>
      <td>78</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 029</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Wednesday</td>
      <td>USD</td>
      <td>EUR</td>
      <td>1.10</td>
      <td>20200101</td>
      <td>20200602</td>
    </tr>
    <tr>
      <th>5</th>
      <td>09/05/2020</td>
      <td>2</td>
      <td>9</td>
      <td>23</td>
      <td>82</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 023</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Saturday</td>
      <td>EUR</td>
      <td>EUR</td>
      <td>1.00</td>
      <td>20200101</td>
      <td>20201130</td>
    </tr>
    <tr>
      <th>6</th>
      <td>10/05/2020</td>
      <td>1</td>
      <td>7</td>
      <td>12</td>
      <td>87</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 012</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Monday</td>
      <td>USD</td>
      <td>EUR</td>
      <td>1.10</td>
      <td>20200101</td>
      <td>20200602</td>
    </tr>
    <tr>
      <th>7</th>
      <td>11/05/2020</td>
      <td>3</td>
      <td>9</td>
      <td>30</td>
      <td>90</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 030</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Thursday</td>
      <td>EUR</td>
      <td>EUR</td>
      <td>1.00</td>
      <td>20200101</td>
      <td>20201130</td>
    </tr>
    <tr>
      <th>8</th>
      <td>12/05/2020</td>
      <td>2</td>
      <td>4</td>
      <td>9</td>
      <td>66</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 009</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Saturday</td>
      <td>USD</td>
      <td>EUR</td>
      <td>1.10</td>
      <td>20200101</td>
      <td>20200602</td>
    </tr>
    <tr>
      <th>9</th>
      <td>13/05/2020</td>
      <td>2</td>
      <td>1</td>
      <td>14</td>
      <td>57</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 014</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Wednesday</td>
      <td>USD</td>
      <td>EUR</td>
      <td>1.10</td>
      <td>20200101</td>
      <td>20200602</td>
    </tr>
    <tr>
      <th>10</th>
      <td>14/05/2020</td>
      <td>2</td>
      <td>5</td>
      <td>7</td>
      <td>98</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 007</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Thursday</td>
      <td>EUR</td>
      <td>EUR</td>
      <td>1.00</td>
      <td>20200101</td>
      <td>20201130</td>
    </tr>
    <tr>
      <th>11</th>
      <td>15/05/2020</td>
      <td>2</td>
      <td>9</td>
      <td>16</td>
      <td>59</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 016</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Friday</td>
      <td>EUR</td>
      <td>EUR</td>
      <td>1.00</td>
      <td>20200101</td>
      <td>20201130</td>
    </tr>
    <tr>
      <th>12</th>
      <td>16/05/2020</td>
      <td>2</td>
      <td>6</td>
      <td>18</td>
      <td>77</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 018</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Saturday</td>
      <td>EUR</td>
      <td>EUR</td>
      <td>1.00</td>
      <td>20200101</td>
      <td>20201130</td>
    </tr>
    <tr>
      <th>13</th>
      <td>17/05/2020</td>
      <td>3</td>
      <td>3</td>
      <td>8</td>
      <td>93</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 008</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Sunday</td>
      <td>USD</td>
      <td>EUR</td>
      <td>1.10</td>
      <td>20200101</td>
      <td>20200602</td>
    </tr>
    <tr>
      <th>14</th>
      <td>18/05/2020</td>
      <td>1</td>
      <td>10</td>
      <td>21</td>
      <td>63</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 021</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Monday</td>
      <td>USD</td>
      <td>EUR</td>
      <td>1.10</td>
      <td>20200101</td>
      <td>20200602</td>
    </tr>
    <tr>
      <th>15</th>
      <td>19/05/2020</td>
      <td>1</td>
      <td>4</td>
      <td>20</td>
      <td>96</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 020</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Tuesday</td>
      <td>USD</td>
      <td>EUR</td>
      <td>1.10</td>
      <td>20200101</td>
      <td>20200602</td>
    </tr>
    <tr>
      <th>16</th>
      <td>20/05/2020</td>
      <td>2</td>
      <td>3</td>
      <td>28</td>
      <td>90</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 028</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Wednesday</td>
      <td>USD</td>
      <td>EUR</td>
      <td>1.10</td>
      <td>20200101</td>
      <td>20200602</td>
    </tr>
    <tr>
      <th>17</th>
      <td>21/05/2020</td>
      <td>2</td>
      <td>3</td>
      <td>1</td>
      <td>79</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 001</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Thursday</td>
      <td>USD</td>
      <td>EUR</td>
      <td>1.10</td>
      <td>20200101</td>
      <td>20200602</td>
    </tr>
    <tr>
      <th>18</th>
      <td>22/05/2020</td>
      <td>3</td>
      <td>2</td>
      <td>30</td>
      <td>52</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 030</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Friday</td>
      <td>EUR</td>
      <td>EUR</td>
      <td>1.00</td>
      <td>20200101</td>
      <td>20201130</td>
    </tr>
    <tr>
      <th>19</th>
      <td>23/05/2020</td>
      <td>3</td>
      <td>7</td>
      <td>24</td>
      <td>67</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 024</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Saturday</td>
      <td>USD</td>
      <td>EUR</td>
      <td>1.10</td>
      <td>20200101</td>
      <td>20200602</td>
    </tr>
    <tr>
      <th>20</th>
      <td>24/05/2020</td>
      <td>3</td>
      <td>10</td>
      <td>8</td>
      <td>83</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 008</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Sunday</td>
      <td>USD</td>
      <td>EUR</td>
      <td>1.10</td>
      <td>20200101</td>
      <td>20200602</td>
    </tr>
    <tr>
      <th>21</th>
      <td>25/05/2020</td>
      <td>2</td>
      <td>9</td>
      <td>8</td>
      <td>93</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 008</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Monday</td>
      <td>EUR</td>
      <td>EUR</td>
      <td>1.00</td>
      <td>20200101</td>
      <td>20201130</td>
    </tr>
    <tr>
      <th>22</th>
      <td>26/05/2020</td>
      <td>2</td>
      <td>6</td>
      <td>5</td>
      <td>57</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 005</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Tuesday</td>
      <td>EUR</td>
      <td>EUR</td>
      <td>1.00</td>
      <td>20200101</td>
      <td>20201130</td>
    </tr>
    <tr>
      <th>23</th>
      <td>27/05/2020</td>
      <td>2</td>
      <td>1</td>
      <td>30</td>
      <td>89</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 030</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Wednesday</td>
      <td>USD</td>
      <td>EUR</td>
      <td>1.10</td>
      <td>20200101</td>
      <td>20200602</td>
    </tr>
    <tr>
      <th>24</th>
      <td>28/05/2020</td>
      <td>2</td>
      <td>8</td>
      <td>24</td>
      <td>58</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 024</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Thursday</td>
      <td>EUR</td>
      <td>EUR</td>
      <td>1.00</td>
      <td>20200101</td>
      <td>20201130</td>
    </tr>
    <tr>
      <th>25</th>
      <td>29/05/2020</td>
      <td>3</td>
      <td>2</td>
      <td>21</td>
      <td>100</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 021</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Friday</td>
      <td>EUR</td>
      <td>EUR</td>
      <td>1.00</td>
      <td>20200101</td>
      <td>20201130</td>
    </tr>
    <tr>
      <th>26</th>
      <td>30/05/2020</td>
      <td>3</td>
      <td>7</td>
      <td>28</td>
      <td>77</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 028</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Saturday</td>
      <td>USD</td>
      <td>EUR</td>
      <td>1.10</td>
      <td>20200101</td>
      <td>20200602</td>
    </tr>
    <tr>
      <th>27</th>
      <td>31/05/2020</td>
      <td>1</td>
      <td>10</td>
      <td>28</td>
      <td>86</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 028</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Sunday</td>
      <td>USD</td>
      <td>EUR</td>
      <td>1.10</td>
      <td>20200101</td>
      <td>20200602</td>
    </tr>
    <tr>
      <th>28</th>
      <td>01/06/2020</td>
      <td>2</td>
      <td>2</td>
      <td>28</td>
      <td>74</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 028</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Monday</td>
      <td>EUR</td>
      <td>EUR</td>
      <td>1.00</td>
      <td>20200101</td>
      <td>20201130</td>
    </tr>
    <tr>
      <th>29</th>
      <td>02/06/2020</td>
      <td>1</td>
      <td>7</td>
      <td>5</td>
      <td>83</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 005</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Thursday</td>
      <td>USD</td>
      <td>EUR</td>
      <td>1.10</td>
      <td>20200101</td>
      <td>20200602</td>
    </tr>
    <tr>
      <th>30</th>
      <td>03/06/2020</td>
      <td>3</td>
      <td>4</td>
      <td>25</td>
      <td>72</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 025</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Friday</td>
      <td>USD</td>
      <td>EUR</td>
      <td>1.18</td>
      <td>20200603</td>
      <td>20201130</td>
    </tr>
    <tr>
      <th>31</th>
      <td>04/06/2020</td>
      <td>3</td>
      <td>3</td>
      <td>11</td>
      <td>90</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 011</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Monday</td>
      <td>USD</td>
      <td>EUR</td>
      <td>1.18</td>
      <td>20200603</td>
      <td>20201130</td>
    </tr>
    <tr>
      <th>32</th>
      <td>05/06/2020</td>
      <td>3</td>
      <td>6</td>
      <td>30</td>
      <td>64</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 030</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Wednesday</td>
      <td>EUR</td>
      <td>EUR</td>
      <td>1.00</td>
      <td>20200101</td>
      <td>20201130</td>
    </tr>
    <tr>
      <th>33</th>
      <td>06/06/2020</td>
      <td>2</td>
      <td>4</td>
      <td>8</td>
      <td>81</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 008</td>
      <td>...</td>
      <td>Q2 2020</td>
      <td>20202</td>
      <td>2020</td>
      <td>Year 2020</td>
      <td>Saturday</td>
      <td>USD</td>
      <td>EUR</td>
      <td>1.18</td>
      <td>20200603</td>
      <td>20201130</td>
    </tr>
  </tbody>
</table>
<p>34 rows × 26 columns</p>
</div>



### Updating master merge by adding total EUR gross and net values


```python
master_merge['Price per unit Net'] = master_merge['Price'].round(2)
master_merge['VAT Value'] = (master_merge['Price per unit Net']*master_merge['VAT float']).round(2)
master_merge['Price per unit Gross'] = (master_merge['VAT Value'] + master_merge['Price per unit Net']).round(2)
master_merge['Total Price Net'] = master_merge['Price per unit Net'] * master_merge['QTY']
master_merge['Total Price Gross'] = master_merge['Price per unit Gross'] * master_merge['QTY']
master_merge['Total VAT'] = master_merge['Total Price Gross'] - master_merge['Total Price Net']


master_merge['EUR Price per unit Net'] = (master_merge['Conversion Rate']*master_merge['Price']).round(2)
master_merge['EUR VAT Value'] = (master_merge['EUR Price per unit Net']*master_merge['VAT float']).round(2)
master_merge['EUR Price per unit Gross'] = (master_merge['EUR VAT Value'] + master_merge['EUR Price per unit Net']).round(2)
master_merge['EUR Total Price Net'] = master_merge['EUR Price per unit Net'] * master_merge['QTY']
master_merge['EUR Total Price Gross'] = master_merge['EUR Price per unit Gross'] * master_merge['QTY']
master_merge['EUR Total VAT'] = master_merge['EUR Total Price Gross'] - master_merge['EUR Total Price Net']

master_merge
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
      <th>Date</th>
      <th>Store</th>
      <th>Product No</th>
      <th>Customer No</th>
      <th>QTY</th>
      <th>Store Name</th>
      <th>Store Location</th>
      <th>VAT</th>
      <th>VAT float</th>
      <th>Customer</th>
      <th>...</th>
      <th>Price per unit Gross</th>
      <th>Total Price Net</th>
      <th>Total Price Gross</th>
      <th>Total VAT</th>
      <th>EUR Price per unit Net</th>
      <th>EUR VAT Value</th>
      <th>EUR Price per unit Gross</th>
      <th>EUR Total Price Net</th>
      <th>EUR Total Price Gross</th>
      <th>EUR Total VAT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>04/05/2020</td>
      <td>1</td>
      <td>3</td>
      <td>29</td>
      <td>60</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 029</td>
      <td>...</td>
      <td>54.28</td>
      <td>2760.0</td>
      <td>3256.80</td>
      <td>496.80</td>
      <td>50.60</td>
      <td>9.11</td>
      <td>59.71</td>
      <td>3036.00</td>
      <td>3582.60</td>
      <td>546.60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>05/05/2020</td>
      <td>2</td>
      <td>8</td>
      <td>26</td>
      <td>67</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 026</td>
      <td>...</td>
      <td>53.10</td>
      <td>3015.0</td>
      <td>3557.70</td>
      <td>542.70</td>
      <td>45.00</td>
      <td>8.10</td>
      <td>53.10</td>
      <td>3015.00</td>
      <td>3557.70</td>
      <td>542.70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>06/05/2020</td>
      <td>3</td>
      <td>5</td>
      <td>12</td>
      <td>68</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 012</td>
      <td>...</td>
      <td>11.00</td>
      <td>748.0</td>
      <td>748.00</td>
      <td>0.00</td>
      <td>11.00</td>
      <td>0.00</td>
      <td>11.00</td>
      <td>748.00</td>
      <td>748.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>07/05/2020</td>
      <td>1</td>
      <td>6</td>
      <td>22</td>
      <td>52</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 022</td>
      <td>...</td>
      <td>17.70</td>
      <td>780.0</td>
      <td>920.40</td>
      <td>140.40</td>
      <td>15.00</td>
      <td>2.70</td>
      <td>17.70</td>
      <td>780.00</td>
      <td>920.40</td>
      <td>140.40</td>
    </tr>
    <tr>
      <th>4</th>
      <td>08/05/2020</td>
      <td>1</td>
      <td>1</td>
      <td>29</td>
      <td>78</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 029</td>
      <td>...</td>
      <td>30.68</td>
      <td>2028.0</td>
      <td>2393.04</td>
      <td>365.04</td>
      <td>28.60</td>
      <td>5.15</td>
      <td>33.75</td>
      <td>2230.80</td>
      <td>2632.50</td>
      <td>401.70</td>
    </tr>
    <tr>
      <th>5</th>
      <td>09/05/2020</td>
      <td>2</td>
      <td>9</td>
      <td>23</td>
      <td>82</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 023</td>
      <td>...</td>
      <td>36.58</td>
      <td>2542.0</td>
      <td>2999.56</td>
      <td>457.56</td>
      <td>31.00</td>
      <td>5.58</td>
      <td>36.58</td>
      <td>2542.00</td>
      <td>2999.56</td>
      <td>457.56</td>
    </tr>
    <tr>
      <th>6</th>
      <td>10/05/2020</td>
      <td>1</td>
      <td>7</td>
      <td>12</td>
      <td>87</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 012</td>
      <td>...</td>
      <td>23.60</td>
      <td>1740.0</td>
      <td>2053.20</td>
      <td>313.20</td>
      <td>22.00</td>
      <td>3.96</td>
      <td>25.96</td>
      <td>1914.00</td>
      <td>2258.52</td>
      <td>344.52</td>
    </tr>
    <tr>
      <th>7</th>
      <td>11/05/2020</td>
      <td>3</td>
      <td>9</td>
      <td>30</td>
      <td>90</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 030</td>
      <td>...</td>
      <td>31.00</td>
      <td>2790.0</td>
      <td>2790.00</td>
      <td>0.00</td>
      <td>31.00</td>
      <td>0.00</td>
      <td>31.00</td>
      <td>2790.00</td>
      <td>2790.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>8</th>
      <td>12/05/2020</td>
      <td>2</td>
      <td>4</td>
      <td>9</td>
      <td>66</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 009</td>
      <td>...</td>
      <td>40.12</td>
      <td>2244.0</td>
      <td>2647.92</td>
      <td>403.92</td>
      <td>37.40</td>
      <td>6.73</td>
      <td>44.13</td>
      <td>2468.40</td>
      <td>2912.58</td>
      <td>444.18</td>
    </tr>
    <tr>
      <th>9</th>
      <td>13/05/2020</td>
      <td>2</td>
      <td>1</td>
      <td>14</td>
      <td>57</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 014</td>
      <td>...</td>
      <td>30.68</td>
      <td>1482.0</td>
      <td>1748.76</td>
      <td>266.76</td>
      <td>28.60</td>
      <td>5.15</td>
      <td>33.75</td>
      <td>1630.20</td>
      <td>1923.75</td>
      <td>293.55</td>
    </tr>
    <tr>
      <th>10</th>
      <td>14/05/2020</td>
      <td>2</td>
      <td>5</td>
      <td>7</td>
      <td>98</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 007</td>
      <td>...</td>
      <td>12.98</td>
      <td>1078.0</td>
      <td>1272.04</td>
      <td>194.04</td>
      <td>11.00</td>
      <td>1.98</td>
      <td>12.98</td>
      <td>1078.00</td>
      <td>1272.04</td>
      <td>194.04</td>
    </tr>
    <tr>
      <th>11</th>
      <td>15/05/2020</td>
      <td>2</td>
      <td>9</td>
      <td>16</td>
      <td>59</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 016</td>
      <td>...</td>
      <td>36.58</td>
      <td>1829.0</td>
      <td>2158.22</td>
      <td>329.22</td>
      <td>31.00</td>
      <td>5.58</td>
      <td>36.58</td>
      <td>1829.00</td>
      <td>2158.22</td>
      <td>329.22</td>
    </tr>
    <tr>
      <th>12</th>
      <td>16/05/2020</td>
      <td>2</td>
      <td>6</td>
      <td>18</td>
      <td>77</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 018</td>
      <td>...</td>
      <td>17.70</td>
      <td>1155.0</td>
      <td>1362.90</td>
      <td>207.90</td>
      <td>15.00</td>
      <td>2.70</td>
      <td>17.70</td>
      <td>1155.00</td>
      <td>1362.90</td>
      <td>207.90</td>
    </tr>
    <tr>
      <th>13</th>
      <td>17/05/2020</td>
      <td>3</td>
      <td>3</td>
      <td>8</td>
      <td>93</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 008</td>
      <td>...</td>
      <td>46.00</td>
      <td>4278.0</td>
      <td>4278.00</td>
      <td>0.00</td>
      <td>50.60</td>
      <td>0.00</td>
      <td>50.60</td>
      <td>4705.80</td>
      <td>4705.80</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>14</th>
      <td>18/05/2020</td>
      <td>1</td>
      <td>10</td>
      <td>21</td>
      <td>63</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 021</td>
      <td>...</td>
      <td>29.50</td>
      <td>1575.0</td>
      <td>1858.50</td>
      <td>283.50</td>
      <td>27.50</td>
      <td>4.95</td>
      <td>32.45</td>
      <td>1732.50</td>
      <td>2044.35</td>
      <td>311.85</td>
    </tr>
    <tr>
      <th>15</th>
      <td>19/05/2020</td>
      <td>1</td>
      <td>4</td>
      <td>20</td>
      <td>96</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 020</td>
      <td>...</td>
      <td>40.12</td>
      <td>3264.0</td>
      <td>3851.52</td>
      <td>587.52</td>
      <td>37.40</td>
      <td>6.73</td>
      <td>44.13</td>
      <td>3590.40</td>
      <td>4236.48</td>
      <td>646.08</td>
    </tr>
    <tr>
      <th>16</th>
      <td>20/05/2020</td>
      <td>2</td>
      <td>3</td>
      <td>28</td>
      <td>90</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 028</td>
      <td>...</td>
      <td>54.28</td>
      <td>4140.0</td>
      <td>4885.20</td>
      <td>745.20</td>
      <td>50.60</td>
      <td>9.11</td>
      <td>59.71</td>
      <td>4554.00</td>
      <td>5373.90</td>
      <td>819.90</td>
    </tr>
    <tr>
      <th>17</th>
      <td>21/05/2020</td>
      <td>2</td>
      <td>3</td>
      <td>1</td>
      <td>79</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 001</td>
      <td>...</td>
      <td>54.28</td>
      <td>3634.0</td>
      <td>4288.12</td>
      <td>654.12</td>
      <td>50.60</td>
      <td>9.11</td>
      <td>59.71</td>
      <td>3997.40</td>
      <td>4717.09</td>
      <td>719.69</td>
    </tr>
    <tr>
      <th>18</th>
      <td>22/05/2020</td>
      <td>3</td>
      <td>2</td>
      <td>30</td>
      <td>52</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 030</td>
      <td>...</td>
      <td>37.00</td>
      <td>1924.0</td>
      <td>1924.00</td>
      <td>0.00</td>
      <td>37.00</td>
      <td>0.00</td>
      <td>37.00</td>
      <td>1924.00</td>
      <td>1924.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>19</th>
      <td>23/05/2020</td>
      <td>3</td>
      <td>7</td>
      <td>24</td>
      <td>67</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 024</td>
      <td>...</td>
      <td>20.00</td>
      <td>1340.0</td>
      <td>1340.00</td>
      <td>0.00</td>
      <td>22.00</td>
      <td>0.00</td>
      <td>22.00</td>
      <td>1474.00</td>
      <td>1474.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>20</th>
      <td>24/05/2020</td>
      <td>3</td>
      <td>10</td>
      <td>8</td>
      <td>83</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 008</td>
      <td>...</td>
      <td>25.00</td>
      <td>2075.0</td>
      <td>2075.00</td>
      <td>0.00</td>
      <td>27.50</td>
      <td>0.00</td>
      <td>27.50</td>
      <td>2282.50</td>
      <td>2282.50</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>21</th>
      <td>25/05/2020</td>
      <td>2</td>
      <td>9</td>
      <td>8</td>
      <td>93</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 008</td>
      <td>...</td>
      <td>36.58</td>
      <td>2883.0</td>
      <td>3401.94</td>
      <td>518.94</td>
      <td>31.00</td>
      <td>5.58</td>
      <td>36.58</td>
      <td>2883.00</td>
      <td>3401.94</td>
      <td>518.94</td>
    </tr>
    <tr>
      <th>22</th>
      <td>26/05/2020</td>
      <td>2</td>
      <td>6</td>
      <td>5</td>
      <td>57</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 005</td>
      <td>...</td>
      <td>17.70</td>
      <td>855.0</td>
      <td>1008.90</td>
      <td>153.90</td>
      <td>15.00</td>
      <td>2.70</td>
      <td>17.70</td>
      <td>855.00</td>
      <td>1008.90</td>
      <td>153.90</td>
    </tr>
    <tr>
      <th>23</th>
      <td>27/05/2020</td>
      <td>2</td>
      <td>1</td>
      <td>30</td>
      <td>89</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 030</td>
      <td>...</td>
      <td>30.68</td>
      <td>2314.0</td>
      <td>2730.52</td>
      <td>416.52</td>
      <td>28.60</td>
      <td>5.15</td>
      <td>33.75</td>
      <td>2545.40</td>
      <td>3003.75</td>
      <td>458.35</td>
    </tr>
    <tr>
      <th>24</th>
      <td>28/05/2020</td>
      <td>2</td>
      <td>8</td>
      <td>24</td>
      <td>58</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 024</td>
      <td>...</td>
      <td>53.10</td>
      <td>2610.0</td>
      <td>3079.80</td>
      <td>469.80</td>
      <td>45.00</td>
      <td>8.10</td>
      <td>53.10</td>
      <td>2610.00</td>
      <td>3079.80</td>
      <td>469.80</td>
    </tr>
    <tr>
      <th>25</th>
      <td>29/05/2020</td>
      <td>3</td>
      <td>2</td>
      <td>21</td>
      <td>100</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 021</td>
      <td>...</td>
      <td>37.00</td>
      <td>3700.0</td>
      <td>3700.00</td>
      <td>0.00</td>
      <td>37.00</td>
      <td>0.00</td>
      <td>37.00</td>
      <td>3700.00</td>
      <td>3700.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>26</th>
      <td>30/05/2020</td>
      <td>3</td>
      <td>7</td>
      <td>28</td>
      <td>77</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 028</td>
      <td>...</td>
      <td>20.00</td>
      <td>1540.0</td>
      <td>1540.00</td>
      <td>0.00</td>
      <td>22.00</td>
      <td>0.00</td>
      <td>22.00</td>
      <td>1694.00</td>
      <td>1694.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>27</th>
      <td>31/05/2020</td>
      <td>1</td>
      <td>10</td>
      <td>28</td>
      <td>86</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 028</td>
      <td>...</td>
      <td>29.50</td>
      <td>2150.0</td>
      <td>2537.00</td>
      <td>387.00</td>
      <td>27.50</td>
      <td>4.95</td>
      <td>32.45</td>
      <td>2365.00</td>
      <td>2790.70</td>
      <td>425.70</td>
    </tr>
    <tr>
      <th>28</th>
      <td>01/06/2020</td>
      <td>2</td>
      <td>2</td>
      <td>28</td>
      <td>74</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 028</td>
      <td>...</td>
      <td>43.66</td>
      <td>2738.0</td>
      <td>3230.84</td>
      <td>492.84</td>
      <td>37.00</td>
      <td>6.66</td>
      <td>43.66</td>
      <td>2738.00</td>
      <td>3230.84</td>
      <td>492.84</td>
    </tr>
    <tr>
      <th>29</th>
      <td>02/06/2020</td>
      <td>1</td>
      <td>7</td>
      <td>5</td>
      <td>83</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 005</td>
      <td>...</td>
      <td>23.60</td>
      <td>1660.0</td>
      <td>1958.80</td>
      <td>298.80</td>
      <td>22.00</td>
      <td>3.96</td>
      <td>25.96</td>
      <td>1826.00</td>
      <td>2154.68</td>
      <td>328.68</td>
    </tr>
    <tr>
      <th>30</th>
      <td>03/06/2020</td>
      <td>3</td>
      <td>4</td>
      <td>25</td>
      <td>72</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 025</td>
      <td>...</td>
      <td>34.00</td>
      <td>2448.0</td>
      <td>2448.00</td>
      <td>0.00</td>
      <td>40.12</td>
      <td>0.00</td>
      <td>40.12</td>
      <td>2888.64</td>
      <td>2888.64</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>31</th>
      <td>04/06/2020</td>
      <td>3</td>
      <td>3</td>
      <td>11</td>
      <td>90</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 011</td>
      <td>...</td>
      <td>46.00</td>
      <td>4140.0</td>
      <td>4140.00</td>
      <td>0.00</td>
      <td>54.28</td>
      <td>0.00</td>
      <td>54.28</td>
      <td>4885.20</td>
      <td>4885.20</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>32</th>
      <td>05/06/2020</td>
      <td>3</td>
      <td>6</td>
      <td>30</td>
      <td>64</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>0%</td>
      <td>0.00</td>
      <td>Customer 030</td>
      <td>...</td>
      <td>15.00</td>
      <td>960.0</td>
      <td>960.00</td>
      <td>0.00</td>
      <td>15.00</td>
      <td>0.00</td>
      <td>15.00</td>
      <td>960.00</td>
      <td>960.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>33</th>
      <td>06/06/2020</td>
      <td>2</td>
      <td>4</td>
      <td>8</td>
      <td>81</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>18%</td>
      <td>0.18</td>
      <td>Customer 008</td>
      <td>...</td>
      <td>40.12</td>
      <td>2754.0</td>
      <td>3249.72</td>
      <td>495.72</td>
      <td>40.12</td>
      <td>7.22</td>
      <td>47.34</td>
      <td>3249.72</td>
      <td>3834.54</td>
      <td>584.82</td>
    </tr>
  </tbody>
</table>
<p>34 rows × 38 columns</p>
</div>




```python
master_merge.to_csv('Master_merge.csv')
```

### Total Revenue


```python
master_merge['Price per unit Net'] = master_merge['Price'].sum()
revenue = master_merge[['Date','Store Name', 'Store Location','EUR Price per unit Net', \
                        'EUR VAT Value', 'EUR Price per unit Gross','QTY', 'EUR Total Price Net', \
                        'EUR Total Price Gross', 'EUR Total VAT']]

revenue.at['Total', 'EUR Total Price Net'] = revenue['EUR Total Price Net'].sum()
revenue.at['Total', 'EUR Total Price Gross'] = revenue['EUR Total Price Gross'].sum()
revenue.at['Total', 'EUR Total VAT'] = revenue['EUR Total VAT'].sum()
revenue.at['Total', 'QTY'] = revenue['QTY'].sum()

revenue
```

    /Users/edwardkolodziejski/opt/anaconda3/lib/python3.8/site-packages/pandas/core/frame.py:3041: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      self.loc[index, col] = value





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
      <th>Date</th>
      <th>Store Name</th>
      <th>Store Location</th>
      <th>EUR Price per unit Net</th>
      <th>EUR VAT Value</th>
      <th>EUR Price per unit Gross</th>
      <th>QTY</th>
      <th>EUR Total Price Net</th>
      <th>EUR Total Price Gross</th>
      <th>EUR Total VAT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>04/05/2020</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>50.60</td>
      <td>9.11</td>
      <td>59.71</td>
      <td>60.0</td>
      <td>3036.00</td>
      <td>3582.60</td>
      <td>546.60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>05/05/2020</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>45.00</td>
      <td>8.10</td>
      <td>53.10</td>
      <td>67.0</td>
      <td>3015.00</td>
      <td>3557.70</td>
      <td>542.70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>06/05/2020</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>11.00</td>
      <td>0.00</td>
      <td>11.00</td>
      <td>68.0</td>
      <td>748.00</td>
      <td>748.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>07/05/2020</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>15.00</td>
      <td>2.70</td>
      <td>17.70</td>
      <td>52.0</td>
      <td>780.00</td>
      <td>920.40</td>
      <td>140.40</td>
    </tr>
    <tr>
      <th>4</th>
      <td>08/05/2020</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>28.60</td>
      <td>5.15</td>
      <td>33.75</td>
      <td>78.0</td>
      <td>2230.80</td>
      <td>2632.50</td>
      <td>401.70</td>
    </tr>
    <tr>
      <th>5</th>
      <td>09/05/2020</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>31.00</td>
      <td>5.58</td>
      <td>36.58</td>
      <td>82.0</td>
      <td>2542.00</td>
      <td>2999.56</td>
      <td>457.56</td>
    </tr>
    <tr>
      <th>6</th>
      <td>10/05/2020</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>22.00</td>
      <td>3.96</td>
      <td>25.96</td>
      <td>87.0</td>
      <td>1914.00</td>
      <td>2258.52</td>
      <td>344.52</td>
    </tr>
    <tr>
      <th>7</th>
      <td>11/05/2020</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>31.00</td>
      <td>0.00</td>
      <td>31.00</td>
      <td>90.0</td>
      <td>2790.00</td>
      <td>2790.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>8</th>
      <td>12/05/2020</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>37.40</td>
      <td>6.73</td>
      <td>44.13</td>
      <td>66.0</td>
      <td>2468.40</td>
      <td>2912.58</td>
      <td>444.18</td>
    </tr>
    <tr>
      <th>9</th>
      <td>13/05/2020</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>28.60</td>
      <td>5.15</td>
      <td>33.75</td>
      <td>57.0</td>
      <td>1630.20</td>
      <td>1923.75</td>
      <td>293.55</td>
    </tr>
    <tr>
      <th>10</th>
      <td>14/05/2020</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>11.00</td>
      <td>1.98</td>
      <td>12.98</td>
      <td>98.0</td>
      <td>1078.00</td>
      <td>1272.04</td>
      <td>194.04</td>
    </tr>
    <tr>
      <th>11</th>
      <td>15/05/2020</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>31.00</td>
      <td>5.58</td>
      <td>36.58</td>
      <td>59.0</td>
      <td>1829.00</td>
      <td>2158.22</td>
      <td>329.22</td>
    </tr>
    <tr>
      <th>12</th>
      <td>16/05/2020</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>15.00</td>
      <td>2.70</td>
      <td>17.70</td>
      <td>77.0</td>
      <td>1155.00</td>
      <td>1362.90</td>
      <td>207.90</td>
    </tr>
    <tr>
      <th>13</th>
      <td>17/05/2020</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>50.60</td>
      <td>0.00</td>
      <td>50.60</td>
      <td>93.0</td>
      <td>4705.80</td>
      <td>4705.80</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>14</th>
      <td>18/05/2020</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>27.50</td>
      <td>4.95</td>
      <td>32.45</td>
      <td>63.0</td>
      <td>1732.50</td>
      <td>2044.35</td>
      <td>311.85</td>
    </tr>
    <tr>
      <th>15</th>
      <td>19/05/2020</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>37.40</td>
      <td>6.73</td>
      <td>44.13</td>
      <td>96.0</td>
      <td>3590.40</td>
      <td>4236.48</td>
      <td>646.08</td>
    </tr>
    <tr>
      <th>16</th>
      <td>20/05/2020</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>50.60</td>
      <td>9.11</td>
      <td>59.71</td>
      <td>90.0</td>
      <td>4554.00</td>
      <td>5373.90</td>
      <td>819.90</td>
    </tr>
    <tr>
      <th>17</th>
      <td>21/05/2020</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>50.60</td>
      <td>9.11</td>
      <td>59.71</td>
      <td>79.0</td>
      <td>3997.40</td>
      <td>4717.09</td>
      <td>719.69</td>
    </tr>
    <tr>
      <th>18</th>
      <td>22/05/2020</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>37.00</td>
      <td>0.00</td>
      <td>37.00</td>
      <td>52.0</td>
      <td>1924.00</td>
      <td>1924.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>19</th>
      <td>23/05/2020</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>22.00</td>
      <td>0.00</td>
      <td>22.00</td>
      <td>67.0</td>
      <td>1474.00</td>
      <td>1474.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>20</th>
      <td>24/05/2020</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>27.50</td>
      <td>0.00</td>
      <td>27.50</td>
      <td>83.0</td>
      <td>2282.50</td>
      <td>2282.50</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>21</th>
      <td>25/05/2020</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>31.00</td>
      <td>5.58</td>
      <td>36.58</td>
      <td>93.0</td>
      <td>2883.00</td>
      <td>3401.94</td>
      <td>518.94</td>
    </tr>
    <tr>
      <th>22</th>
      <td>26/05/2020</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>15.00</td>
      <td>2.70</td>
      <td>17.70</td>
      <td>57.0</td>
      <td>855.00</td>
      <td>1008.90</td>
      <td>153.90</td>
    </tr>
    <tr>
      <th>23</th>
      <td>27/05/2020</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>28.60</td>
      <td>5.15</td>
      <td>33.75</td>
      <td>89.0</td>
      <td>2545.40</td>
      <td>3003.75</td>
      <td>458.35</td>
    </tr>
    <tr>
      <th>24</th>
      <td>28/05/2020</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>45.00</td>
      <td>8.10</td>
      <td>53.10</td>
      <td>58.0</td>
      <td>2610.00</td>
      <td>3079.80</td>
      <td>469.80</td>
    </tr>
    <tr>
      <th>25</th>
      <td>29/05/2020</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>37.00</td>
      <td>0.00</td>
      <td>37.00</td>
      <td>100.0</td>
      <td>3700.00</td>
      <td>3700.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>26</th>
      <td>30/05/2020</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>22.00</td>
      <td>0.00</td>
      <td>22.00</td>
      <td>77.0</td>
      <td>1694.00</td>
      <td>1694.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>27</th>
      <td>31/05/2020</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>27.50</td>
      <td>4.95</td>
      <td>32.45</td>
      <td>86.0</td>
      <td>2365.00</td>
      <td>2790.70</td>
      <td>425.70</td>
    </tr>
    <tr>
      <th>28</th>
      <td>01/06/2020</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>37.00</td>
      <td>6.66</td>
      <td>43.66</td>
      <td>74.0</td>
      <td>2738.00</td>
      <td>3230.84</td>
      <td>492.84</td>
    </tr>
    <tr>
      <th>29</th>
      <td>02/06/2020</td>
      <td>Brand New Store</td>
      <td>Berlin</td>
      <td>22.00</td>
      <td>3.96</td>
      <td>25.96</td>
      <td>83.0</td>
      <td>1826.00</td>
      <td>2154.68</td>
      <td>328.68</td>
    </tr>
    <tr>
      <th>30</th>
      <td>03/06/2020</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>40.12</td>
      <td>0.00</td>
      <td>40.12</td>
      <td>72.0</td>
      <td>2888.64</td>
      <td>2888.64</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>31</th>
      <td>04/06/2020</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>54.28</td>
      <td>0.00</td>
      <td>54.28</td>
      <td>90.0</td>
      <td>4885.20</td>
      <td>4885.20</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>32</th>
      <td>05/06/2020</td>
      <td>TOP Store</td>
      <td>Leipzig</td>
      <td>15.00</td>
      <td>0.00</td>
      <td>15.00</td>
      <td>64.0</td>
      <td>960.00</td>
      <td>960.00</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>33</th>
      <td>06/06/2020</td>
      <td>Vintage Store</td>
      <td>Leipzig</td>
      <td>40.12</td>
      <td>7.22</td>
      <td>47.34</td>
      <td>81.0</td>
      <td>3249.72</td>
      <td>3834.54</td>
      <td>584.82</td>
    </tr>
    <tr>
      <th>Total</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2588.0</td>
      <td>82676.96</td>
      <td>92509.88</td>
      <td>9832.92</td>
    </tr>
  </tbody>
</table>
</div>




```python
revenue.to_csv('Revenue.csv')
```

### Revenue by store


```python
revenue_by_store = revenue.groupby(['Store Name']).sum().round(2)
revenue_by_store = revenue_by_store[['QTY','EUR Total Price Net', 'EUR Total Price Gross', 'EUR Total VAT']]
revenue_by_store
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
      <th>QTY</th>
      <th>EUR Total Price Net</th>
      <th>EUR Total Price Gross</th>
      <th>EUR Total VAT</th>
    </tr>
    <tr>
      <th>Store Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Brand New Store</th>
      <td>605.0</td>
      <td>17474.70</td>
      <td>20620.23</td>
      <td>3145.53</td>
    </tr>
    <tr>
      <th>TOP Store</th>
      <td>856.0</td>
      <td>28052.14</td>
      <td>28052.14</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>Vintage Store</th>
      <td>1127.0</td>
      <td>37150.12</td>
      <td>43837.51</td>
      <td>6687.39</td>
    </tr>
  </tbody>
</table>
</div>




```python
revenue_by_store.to_csv('Revenue_by_store.csv')
```

### Sales by product


```python
total_products = master_merge[['Product', 'QTY', 'EUR Total Price Net','EUR Total Price Gross', 'EUR Total VAT']]
total_products = total_products.groupby(['Product']).sum().sort_values(by=['QTY'], ascending=False)
total_products
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
      <th>QTY</th>
      <th>EUR Total Price Net</th>
      <th>EUR Total Price Gross</th>
      <th>EUR Total VAT</th>
    </tr>
    <tr>
      <th>Product</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Product C</th>
      <td>412</td>
      <td>21178.40</td>
      <td>23264.59</td>
      <td>2086.19</td>
    </tr>
    <tr>
      <th>Product I</th>
      <td>324</td>
      <td>10044.00</td>
      <td>11349.72</td>
      <td>1305.72</td>
    </tr>
    <tr>
      <th>Product D</th>
      <td>315</td>
      <td>12197.16</td>
      <td>13872.24</td>
      <td>1675.08</td>
    </tr>
    <tr>
      <th>Product G</th>
      <td>314</td>
      <td>6908.00</td>
      <td>7581.20</td>
      <td>673.20</td>
    </tr>
    <tr>
      <th>Product F</th>
      <td>250</td>
      <td>3750.00</td>
      <td>4252.20</td>
      <td>502.20</td>
    </tr>
    <tr>
      <th>Product J</th>
      <td>232</td>
      <td>6380.00</td>
      <td>7117.55</td>
      <td>737.55</td>
    </tr>
    <tr>
      <th>Product B</th>
      <td>226</td>
      <td>8362.00</td>
      <td>8854.84</td>
      <td>492.84</td>
    </tr>
    <tr>
      <th>Product A</th>
      <td>224</td>
      <td>6406.40</td>
      <td>7560.00</td>
      <td>1153.60</td>
    </tr>
    <tr>
      <th>Product E</th>
      <td>166</td>
      <td>1826.00</td>
      <td>2020.04</td>
      <td>194.04</td>
    </tr>
    <tr>
      <th>Product H</th>
      <td>125</td>
      <td>5625.00</td>
      <td>6637.50</td>
      <td>1012.50</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_products.to_csv('Total_products.csv')
```

### Sales by weekdays


```python
sales_by_weekday = master_merge[['Weekday','Product', 'QTY', 'EUR Total Price Net', \
                                'EUR Total Price Gross', 'EUR Total VAT']]
sales_by_weekday = sales_by_weekday.groupby(['Weekday']).sum().sort_values(by=['QTY'], ascending=False)
sales_by_weekday
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
      <th>QTY</th>
      <th>EUR Total Price Net</th>
      <th>EUR Total Price Gross</th>
      <th>EUR Total VAT</th>
    </tr>
    <tr>
      <th>Weekday</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Saturday</th>
      <td>450</td>
      <td>12583.12</td>
      <td>14277.58</td>
      <td>1694.46</td>
    </tr>
    <tr>
      <th>Thursday</th>
      <td>408</td>
      <td>12301.40</td>
      <td>14013.61</td>
      <td>1712.21</td>
    </tr>
    <tr>
      <th>Monday</th>
      <td>407</td>
      <td>14152.70</td>
      <td>15820.85</td>
      <td>1668.15</td>
    </tr>
    <tr>
      <th>Wednesday</th>
      <td>378</td>
      <td>11920.40</td>
      <td>13893.90</td>
      <td>1973.50</td>
    </tr>
    <tr>
      <th>Sunday</th>
      <td>374</td>
      <td>13169.30</td>
      <td>14282.00</td>
      <td>1112.70</td>
    </tr>
    <tr>
      <th>Friday</th>
      <td>351</td>
      <td>11089.64</td>
      <td>11418.86</td>
      <td>329.22</td>
    </tr>
    <tr>
      <th>Tuesday</th>
      <td>220</td>
      <td>7460.40</td>
      <td>8803.08</td>
      <td>1342.68</td>
    </tr>
  </tbody>
</table>
</div>




```python
sales_by_weekday.to_csv('Sales_by_weekday.csv')
```
