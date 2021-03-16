
# Project 2: Breakout Strategy
## Instructions
Each problem consists of a function to implement and instructions on how to implement the function.  The parts of the function that need to be implemented are marked with a `# TODO` comment. After implementing the function, run the cell to test it against the unit tests we've provided. For each problem, we provide one or more unit tests from our `project_tests` package. These unit tests won't tell you if your answer is correct, but will warn you of any major errors. Your code will be checked for the correct solution when you submit it to Udacity.

## Packages
When you implement the functions, you'll only need to you use the packages you've used in the classroom, like [Pandas](https://pandas.pydata.org/) and [Numpy](http://www.numpy.org/). These packages will be imported for you. We recommend you don't add any import statements, otherwise the grader might not be able to run your code.

The other packages that we're importing are `helper`, `project_helper`, and `project_tests`. These are custom packages built to help you solve the problems.  The `helper` and `project_helper` module contains utility functions and graph functions. The `project_tests` contains the unit tests for all the problems.

### Install Packages


```python
import sys
!{sys.executable} -m pip install -r requirements.txt
```

    Requirement already satisfied: colour==0.1.5 in /opt/conda/lib/python3.6/site-packages (from -r requirements.txt (line 1)) (0.1.5)
    Requirement already satisfied: cvxpy==1.0.3 in /opt/conda/lib/python3.6/site-packages (from -r requirements.txt (line 2)) (1.0.3)
    Requirement already satisfied: cycler==0.10.0 in /opt/conda/lib/python3.6/site-packages/cycler-0.10.0-py3.6.egg (from -r requirements.txt (line 3)) (0.10.0)
    Requirement already satisfied: numpy==1.13.3 in /opt/conda/lib/python3.6/site-packages (from -r requirements.txt (line 4)) (1.13.3)
    Requirement already satisfied: pandas==0.21.1 in /opt/conda/lib/python3.6/site-packages (from -r requirements.txt (line 5)) (0.21.1)
    Requirement already satisfied: plotly==2.2.3 in /opt/conda/lib/python3.6/site-packages (from -r requirements.txt (line 6)) (2.2.3)
    Requirement already satisfied: pyparsing==2.2.0 in /opt/conda/lib/python3.6/site-packages (from -r requirements.txt (line 7)) (2.2.0)
    Requirement already satisfied: python-dateutil==2.6.1 in /opt/conda/lib/python3.6/site-packages (from -r requirements.txt (line 8)) (2.6.1)
    Requirement already satisfied: pytz==2017.3 in /opt/conda/lib/python3.6/site-packages (from -r requirements.txt (line 9)) (2017.3)
    Requirement already satisfied: requests==2.18.4 in /opt/conda/lib/python3.6/site-packages (from -r requirements.txt (line 10)) (2.18.4)
    Requirement already satisfied: scipy==1.0.0 in /opt/conda/lib/python3.6/site-packages (from -r requirements.txt (line 11)) (1.0.0)
    Requirement already satisfied: scikit-learn==0.19.1 in /opt/conda/lib/python3.6/site-packages (from -r requirements.txt (line 12)) (0.19.1)
    Requirement already satisfied: six==1.11.0 in /opt/conda/lib/python3.6/site-packages (from -r requirements.txt (line 13)) (1.11.0)
    Requirement already satisfied: tqdm==4.19.5 in /opt/conda/lib/python3.6/site-packages (from -r requirements.txt (line 14)) (4.19.5)
    Requirement already satisfied: zipline==1.2.0 in /opt/conda/lib/python3.6/site-packages (from -r requirements.txt (line 15)) (1.2.0)
    Requirement already satisfied: scs>=1.1.3 in /opt/conda/lib/python3.6/site-packages (from cvxpy==1.0.3->-r requirements.txt (line 2)) (2.1.2)
    Requirement already satisfied: osqp in /opt/conda/lib/python3.6/site-packages (from cvxpy==1.0.3->-r requirements.txt (line 2)) (0.6.2.post0)
    Requirement already satisfied: toolz in /opt/conda/lib/python3.6/site-packages (from cvxpy==1.0.3->-r requirements.txt (line 2)) (0.8.2)
    Requirement already satisfied: ecos>=2 in /opt/conda/lib/python3.6/site-packages (from cvxpy==1.0.3->-r requirements.txt (line 2)) (2.0.7.post1)
    Requirement already satisfied: multiprocess in /opt/conda/lib/python3.6/site-packages (from cvxpy==1.0.3->-r requirements.txt (line 2)) (0.70.11.1)
    Requirement already satisfied: fastcache in /opt/conda/lib/python3.6/site-packages (from cvxpy==1.0.3->-r requirements.txt (line 2)) (1.0.2)
    Requirement already satisfied: decorator>=4.0.6 in /opt/conda/lib/python3.6/site-packages (from plotly==2.2.3->-r requirements.txt (line 6)) (4.0.11)
    Requirement already satisfied: nbformat>=4.2 in /opt/conda/lib/python3.6/site-packages (from plotly==2.2.3->-r requirements.txt (line 6)) (4.4.0)
    Requirement already satisfied: chardet<3.1.0,>=3.0.2 in /opt/conda/lib/python3.6/site-packages (from requests==2.18.4->-r requirements.txt (line 10)) (3.0.4)
    Requirement already satisfied: idna<2.7,>=2.5 in /opt/conda/lib/python3.6/site-packages (from requests==2.18.4->-r requirements.txt (line 10)) (2.6)
    Requirement already satisfied: urllib3<1.23,>=1.21.1 in /opt/conda/lib/python3.6/site-packages (from requests==2.18.4->-r requirements.txt (line 10)) (1.22)
    Requirement already satisfied: certifi>=2017.4.17 in /opt/conda/lib/python3.6/site-packages (from requests==2.18.4->-r requirements.txt (line 10)) (2019.11.28)
    Requirement already satisfied: numexpr>=2.6.1 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (2.6.4)
    Requirement already satisfied: bottleneck>=1.0.0 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (1.3.2)
    Requirement already satisfied: networkx<2.0,>=1.9.1 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (1.11)
    Requirement already satisfied: patsy>=0.4.0 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (0.4.1)
    Requirement already satisfied: MarkupSafe>=0.23 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (1.0)
    Requirement already satisfied: alembic>=0.7.7 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (1.5.7)
    Requirement already satisfied: pip>=7.1.0 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (18.1)
    Requirement already satisfied: Mako>=1.0.1 in /opt/conda/lib/python3.6/site-packages/Mako-1.0.7-py3.6.egg (from zipline==1.2.0->-r requirements.txt (line 15)) (1.0.7)
    Requirement already satisfied: pandas-datareader<0.6,>=0.2.1 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (0.5.0)
    Requirement already satisfied: statsmodels>=0.6.1 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (0.8.0)
    Requirement already satisfied: intervaltree>=2.1.0 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (3.1.0)
    Requirement already satisfied: Logbook>=0.12.5 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (1.5.3)
    Requirement already satisfied: Cython>=0.25.2 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (0.29.7)
    Requirement already satisfied: setuptools>18.0 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (38.4.0)
    Requirement already satisfied: requests-file>=1.4.1 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (1.5.1)
    Requirement already satisfied: cyordereddict>=0.2.2 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (1.0.0)
    Requirement already satisfied: sortedcontainers>=1.4.4 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (2.3.0)
    Requirement already satisfied: click>=4.0.0 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (6.7)
    Requirement already satisfied: empyrical>=0.4.2 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (0.5.5)
    Requirement already satisfied: contextlib2>=0.4.0 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (0.6.0.post1)
    Requirement already satisfied: sqlalchemy>=1.0.8 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (1.1.13)
    Requirement already satisfied: lru-dict>=1.1.4 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (1.1.7)
    Requirement already satisfied: multipledispatch>=0.4.8 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (0.6.0)
    Requirement already satisfied: bcolz<1,>=0.12.1 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (0.12.1)
    Requirement already satisfied: tables>=3.3.0 in /opt/conda/lib/python3.6/site-packages (from zipline==1.2.0->-r requirements.txt (line 15)) (3.6.1)
    Requirement already satisfied: qdldl in /opt/conda/lib/python3.6/site-packages (from osqp->cvxpy==1.0.3->-r requirements.txt (line 2)) (0.1.5.post0)
    Requirement already satisfied: dill>=0.3.3 in /opt/conda/lib/python3.6/site-packages (from multiprocess->cvxpy==1.0.3->-r requirements.txt (line 2)) (0.3.3)
    Requirement already satisfied: jupyter-core in /opt/conda/lib/python3.6/site-packages (from nbformat>=4.2->plotly==2.2.3->-r requirements.txt (line 6)) (4.4.0)
    Requirement already satisfied: ipython-genutils in /opt/conda/lib/python3.6/site-packages (from nbformat>=4.2->plotly==2.2.3->-r requirements.txt (line 6)) (0.2.0)
    Requirement already satisfied: jsonschema!=2.5.0,>=2.4 in /opt/conda/lib/python3.6/site-packages (from nbformat>=4.2->plotly==2.2.3->-r requirements.txt (line 6)) (2.6.0)
    Requirement already satisfied: traitlets>=4.1 in /opt/conda/lib/python3.6/site-packages (from nbformat>=4.2->plotly==2.2.3->-r requirements.txt (line 6)) (4.3.2)
    Requirement already satisfied: python-editor>=0.3 in /opt/conda/lib/python3.6/site-packages (from alembic>=0.7.7->zipline==1.2.0->-r requirements.txt (line 15)) (1.0.4)
    Requirement already satisfied: requests-ftp in /opt/conda/lib/python3.6/site-packages (from pandas-datareader<0.6,>=0.2.1->zipline==1.2.0->-r requirements.txt (line 15)) (0.3.1)


### Load Packages


```python
import pandas as pd
import numpy as np
import helper
import project_helper
import project_tests
```


<script>requirejs.config({paths: { 'plotly': ['https://cdn.plot.ly/plotly-latest.min']},});if(!window.Plotly) {{require(['plotly'],function(plotly) {window.Plotly=plotly;});}}</script>


## Market Data
### Load Data
While using real data will give you hands on experience, it's doesn't cover all the topics we try to condense in one project. We'll solve this by creating new stocks. We've create a scenario where companies mining [Terbium](https://en.wikipedia.org/wiki/Terbium) are making huge profits. All the companies in this sector of the market are made up. They represent a sector with large growth that will be used for demonstration latter in this project.


```python
df_original = pd.read_csv('../../data/project_2/eod-quotemedia.csv', parse_dates=['date'], index_col=False)

# Add TB sector to the market
df = df_original
df = pd.concat([df] + project_helper.generate_tb_sector(df[df['ticker'] == 'AAPL']['date']), ignore_index=True)

close = df.reset_index().pivot(index='date', columns='ticker', values='adj_close')
high = df.reset_index().pivot(index='date', columns='ticker', values='adj_high')
low = df.reset_index().pivot(index='date', columns='ticker', values='adj_low')

print('Loaded Data')
```

    Loaded Data


### View Data
To see what one of these 2-d matrices looks like, let's take a look at the closing prices matrix.


```python
close
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
      <th>ticker</th>
      <th>A</th>
      <th>AAL</th>
      <th>AAP</th>
      <th>AAPL</th>
      <th>ABBV</th>
      <th>ABC</th>
      <th>ABT</th>
      <th>ACN</th>
      <th>ADBE</th>
      <th>ADI</th>
      <th>...</th>
      <th>XL</th>
      <th>XLNX</th>
      <th>XOM</th>
      <th>XRAY</th>
      <th>XRX</th>
      <th>XYL</th>
      <th>YUM</th>
      <th>ZBH</th>
      <th>ZION</th>
      <th>ZTS</th>
    </tr>
    <tr>
      <th>date</th>
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
      <th>2013-07-01</th>
      <td>29.99418563</td>
      <td>16.17609308</td>
      <td>81.13821681</td>
      <td>53.10917319</td>
      <td>34.92447839</td>
      <td>50.86319750</td>
      <td>31.42538772</td>
      <td>64.69409505</td>
      <td>46.23500000</td>
      <td>39.91336014</td>
      <td>...</td>
      <td>27.66879066</td>
      <td>35.28892781</td>
      <td>76.32080247</td>
      <td>40.02387348</td>
      <td>22.10666494</td>
      <td>25.75338607</td>
      <td>45.48038323</td>
      <td>71.89882693</td>
      <td>27.85858718</td>
      <td>29.44789315</td>
    </tr>
    <tr>
      <th>2013-07-02</th>
      <td>29.65013670</td>
      <td>15.81983388</td>
      <td>80.72207258</td>
      <td>54.31224742</td>
      <td>35.42807578</td>
      <td>50.69676639</td>
      <td>31.27288084</td>
      <td>64.71204071</td>
      <td>46.03000000</td>
      <td>39.86057632</td>
      <td>...</td>
      <td>27.54228410</td>
      <td>35.05903252</td>
      <td>76.60816761</td>
      <td>39.96552964</td>
      <td>22.08273998</td>
      <td>25.61367511</td>
      <td>45.40266113</td>
      <td>72.93417195</td>
      <td>28.03893238</td>
      <td>28.57244125</td>
    </tr>
    <tr>
      <th>2013-07-03</th>
      <td>29.70518453</td>
      <td>16.12794994</td>
      <td>81.23729877</td>
      <td>54.61204262</td>
      <td>35.44486235</td>
      <td>50.93716689</td>
      <td>30.72565028</td>
      <td>65.21451912</td>
      <td>46.42000000</td>
      <td>40.18607651</td>
      <td>...</td>
      <td>27.33445191</td>
      <td>35.28008569</td>
      <td>76.65042719</td>
      <td>40.00442554</td>
      <td>22.20236479</td>
      <td>25.73475794</td>
      <td>46.06329899</td>
      <td>72.30145844</td>
      <td>28.18131017</td>
      <td>28.16838652</td>
    </tr>
    <tr>
      <th>2013-07-05</th>
      <td>30.43456826</td>
      <td>16.21460758</td>
      <td>81.82188233</td>
      <td>54.17338125</td>
      <td>35.85613355</td>
      <td>51.37173702</td>
      <td>31.32670680</td>
      <td>66.07591068</td>
      <td>47.00000000</td>
      <td>40.65233352</td>
      <td>...</td>
      <td>27.69589920</td>
      <td>35.80177117</td>
      <td>77.39419581</td>
      <td>40.67537968</td>
      <td>22.58516418</td>
      <td>26.06075017</td>
      <td>46.41304845</td>
      <td>73.16424628</td>
      <td>29.39626730</td>
      <td>29.02459772</td>
    </tr>
    <tr>
      <th>2013-07-08</th>
      <td>30.52402098</td>
      <td>16.31089385</td>
      <td>82.95141667</td>
      <td>53.86579916</td>
      <td>36.66188936</td>
      <td>52.03746147</td>
      <td>31.76628544</td>
      <td>66.82065546</td>
      <td>46.62500000</td>
      <td>40.25645492</td>
      <td>...</td>
      <td>27.98505704</td>
      <td>35.20050655</td>
      <td>77.96892611</td>
      <td>40.64620776</td>
      <td>22.48946433</td>
      <td>26.22840332</td>
      <td>46.95062632</td>
      <td>73.89282298</td>
      <td>29.57661249</td>
      <td>29.76536472</td>
    </tr>
    <tr>
      <th>2013-07-09</th>
      <td>30.68916447</td>
      <td>16.71529618</td>
      <td>82.43619048</td>
      <td>54.81320389</td>
      <td>36.35973093</td>
      <td>51.69535307</td>
      <td>31.16522893</td>
      <td>66.48866080</td>
      <td>47.26000000</td>
      <td>40.69632003</td>
      <td>...</td>
      <td>28.31939579</td>
      <td>35.50113886</td>
      <td>78.89018496</td>
      <td>40.80179133</td>
      <td>22.48946433</td>
      <td>26.58233774</td>
      <td>47.28094525</td>
      <td>73.70108798</td>
      <td>28.91218282</td>
      <td>29.80384612</td>
    </tr>
    <tr>
      <th>2013-07-10</th>
      <td>31.17771395</td>
      <td>16.53235227</td>
      <td>81.99032166</td>
      <td>54.60295791</td>
      <td>36.85493502</td>
      <td>52.28710814</td>
      <td>31.16522893</td>
      <td>66.71298151</td>
      <td>47.25000000</td>
      <td>41.10979324</td>
      <td>...</td>
      <td>27.95794850</td>
      <td>36.39419366</td>
      <td>78.45068533</td>
      <td>40.71427558</td>
      <td>22.96796358</td>
      <td>26.98284247</td>
      <td>47.08340158</td>
      <td>74.00785631</td>
      <td>28.32368796</td>
      <td>29.86156823</td>
    </tr>
    <tr>
      <th>2013-07-11</th>
      <td>31.45983407</td>
      <td>16.72492481</td>
      <td>82.00022986</td>
      <td>55.45406479</td>
      <td>37.08155384</td>
      <td>53.72026495</td>
      <td>31.85599537</td>
      <td>67.47567196</td>
      <td>47.99000000</td>
      <td>42.22705062</td>
      <td>...</td>
      <td>28.50011944</td>
      <td>37.00430040</td>
      <td>78.83102155</td>
      <td>41.01571874</td>
      <td>23.23113816</td>
      <td>27.03872686</td>
      <td>46.54333492</td>
      <td>74.93774876</td>
      <td>27.84909533</td>
      <td>29.74612402</td>
    </tr>
    <tr>
      <th>2013-07-12</th>
      <td>31.48047700</td>
      <td>16.90786872</td>
      <td>81.91105609</td>
      <td>55.35309481</td>
      <td>38.15724076</td>
      <td>53.98840397</td>
      <td>31.81096287</td>
      <td>67.76280247</td>
      <td>48.39000000</td>
      <td>42.53495620</td>
      <td>...</td>
      <td>28.92482002</td>
      <td>38.00346072</td>
      <td>78.94089646</td>
      <td>40.83096325</td>
      <td>23.49431274</td>
      <td>27.08529718</td>
      <td>45.96422730</td>
      <td>75.68549560</td>
      <td>28.44708204</td>
      <td>30.15979909</td>
    </tr>
    <tr>
      <th>2013-07-15</th>
      <td>31.72819223</td>
      <td>17.10044125</td>
      <td>82.61453801</td>
      <td>55.47379158</td>
      <td>37.79303181</td>
      <td>53.84971137</td>
      <td>31.95506689</td>
      <td>68.41781897</td>
      <td>48.12000000</td>
      <td>42.57894271</td>
      <td>...</td>
      <td>29.27723113</td>
      <td>38.17146113</td>
      <td>78.81411772</td>
      <td>40.84068723</td>
      <td>23.54216266</td>
      <td>27.06666905</td>
      <td>46.69299195</td>
      <td>76.27027369</td>
      <td>28.77929688</td>
      <td>30.38106716</td>
    </tr>
    <tr>
      <th>2013-07-16</th>
      <td>31.59057266</td>
      <td>17.28338516</td>
      <td>81.62371841</td>
      <td>55.83133953</td>
      <td>37.10696377</td>
      <td>53.88669607</td>
      <td>32.15320992</td>
      <td>67.55642741</td>
      <td>47.48500000</td>
      <td>42.68451033</td>
      <td>...</td>
      <td>29.04229039</td>
      <td>38.27314559</td>
      <td>78.85637730</td>
      <td>40.86013517</td>
      <td>23.27898808</td>
      <td>26.61959399</td>
      <td>46.56936223</td>
      <td>76.81670381</td>
      <td>28.06740794</td>
      <td>29.97701243</td>
    </tr>
    <tr>
      <th>2013-07-17</th>
      <td>31.38414330</td>
      <td>17.76481650</td>
      <td>80.74188897</td>
      <td>55.84626440</td>
      <td>37.23401341</td>
      <td>54.06237335</td>
      <td>32.26128793</td>
      <td>67.43978064</td>
      <td>48.04000000</td>
      <td>42.80767257</td>
      <td>...</td>
      <td>29.18686931</td>
      <td>38.48977769</td>
      <td>78.99160796</td>
      <td>40.93792696</td>
      <td>23.18328823</td>
      <td>26.66616431</td>
      <td>46.45874617</td>
      <td>78.30261578</td>
      <td>28.06740794</td>
      <td>29.81346647</td>
    </tr>
    <tr>
      <th>2013-07-18</th>
      <td>31.58369168</td>
      <td>17.73593062</td>
      <td>81.74261676</td>
      <td>56.03418797</td>
      <td>37.53893253</td>
      <td>53.91443458</td>
      <td>32.15320992</td>
      <td>67.69101984</td>
      <td>48.19000000</td>
      <td>42.52615889</td>
      <td>...</td>
      <td>29.55735279</td>
      <td>40.52346684</td>
      <td>79.76918424</td>
      <td>41.22964615</td>
      <td>23.49431274</td>
      <td>26.94558622</td>
      <td>46.97929234</td>
      <td>78.81069986</td>
      <td>28.77929688</td>
      <td>29.64992051</td>
    </tr>
    <tr>
      <th>2013-07-19</th>
      <td>31.79012104</td>
      <td>17.55298671</td>
      <td>81.45527908</td>
      <td>55.15063572</td>
      <td>37.70833205</td>
      <td>54.37674323</td>
      <td>32.30632044</td>
      <td>67.49361761</td>
      <td>48.07000000</td>
      <td>42.20945601</td>
      <td>...</td>
      <td>29.71096789</td>
      <td>40.54999322</td>
      <td>80.43688561</td>
      <td>41.24909410</td>
      <td>23.20721320</td>
      <td>26.81518933</td>
      <td>46.90121042</td>
      <td>81.16898043</td>
      <td>28.99760949</td>
      <td>29.09194018</td>
    </tr>
    <tr>
      <th>2013-07-22</th>
      <td>32.20297975</td>
      <td>17.47595770</td>
      <td>81.99032166</td>
      <td>55.32713852</td>
      <td>38.08948096</td>
      <td>54.54317435</td>
      <td>32.24327493</td>
      <td>67.29621538</td>
      <td>48.28000000</td>
      <td>42.17426681</td>
      <td>...</td>
      <td>29.84651063</td>
      <td>40.59420386</td>
      <td>80.14952046</td>
      <td>41.49219343</td>
      <td>23.47038778</td>
      <td>26.88970184</td>
      <td>46.50429396</td>
      <td>81.02518181</td>
      <td>29.27287321</td>
      <td>29.12080123</td>
    </tr>
    <tr>
      <th>2013-07-23</th>
      <td>31.97590746</td>
      <td>17.37967143</td>
      <td>81.94078068</td>
      <td>54.37713815</td>
      <td>37.53046256</td>
      <td>53.28569482</td>
      <td>33.03584705</td>
      <td>66.62325323</td>
      <td>48.07000000</td>
      <td>42.56134810</td>
      <td>...</td>
      <td>29.13265221</td>
      <td>40.52346684</td>
      <td>80.46224136</td>
      <td>41.32688588</td>
      <td>23.42253785</td>
      <td>26.74067682</td>
      <td>45.82758393</td>
      <td>81.00601167</td>
      <td>28.38063907</td>
      <td>28.91877387</td>
    </tr>
    <tr>
      <th>2013-07-24</th>
      <td>32.17545584</td>
      <td>17.81295964</td>
      <td>80.78152175</td>
      <td>57.17003539</td>
      <td>36.96297418</td>
      <td>52.49052395</td>
      <td>32.82869752</td>
      <td>66.14769330</td>
      <td>47.80000000</td>
      <td>42.42938857</td>
      <td>...</td>
      <td>28.73506019</td>
      <td>40.24051879</td>
      <td>80.28475112</td>
      <td>41.15185437</td>
      <td>23.51823770</td>
      <td>26.62890805</td>
      <td>46.49128030</td>
      <td>80.56503316</td>
      <td>28.53250871</td>
      <td>28.76484826</td>
    </tr>
    <tr>
      <th>2013-07-25</th>
      <td>32.10664605</td>
      <td>18.13070432</td>
      <td>81.46518728</td>
      <td>56.90917464</td>
      <td>37.47117273</td>
      <td>53.26720248</td>
      <td>32.94578204</td>
      <td>65.62726924</td>
      <td>47.79000000</td>
      <td>42.88684829</td>
      <td>...</td>
      <td>29.02421802</td>
      <td>41.05399445</td>
      <td>80.26784729</td>
      <td>40.91847901</td>
      <td>23.44646282</td>
      <td>26.85244558</td>
      <td>46.91422407</td>
      <td>79.47217195</td>
      <td>28.19080202</td>
      <td>29.36130999</td>
    </tr>
    <tr>
      <th>2013-07-26</th>
      <td>31.37726233</td>
      <td>18.38104862</td>
      <td>81.88133151</td>
      <td>57.23233050</td>
      <td>37.93702140</td>
      <td>54.06237335</td>
      <td>33.12591207</td>
      <td>65.60932358</td>
      <td>47.64000000</td>
      <td>42.71969954</td>
      <td>...</td>
      <td>29.11457985</td>
      <td>40.83294128</td>
      <td>80.11571280</td>
      <td>40.98654682</td>
      <td>23.18328823</td>
      <td>26.70342056</td>
      <td>48.15052124</td>
      <td>80.98684153</td>
      <td>28.04842424</td>
      <td>29.27472684</td>
    </tr>
    <tr>
      <th>2013-07-29</th>
      <td>31.19835688</td>
      <td>18.51584940</td>
      <td>81.57417743</td>
      <td>58.11484449</td>
      <td>38.16571074</td>
      <td>53.98840397</td>
      <td>33.08988606</td>
      <td>64.93636143</td>
      <td>47.17000000</td>
      <td>42.66691573</td>
      <td>...</td>
      <td>28.92482002</td>
      <td>40.38199282</td>
      <td>79.47336717</td>
      <td>40.93792696</td>
      <td>23.08758839</td>
      <td>26.50782523</td>
      <td>47.83819353</td>
      <td>80.16240164</td>
      <td>27.71620940</td>
      <td>28.94763492</td>
    </tr>
    <tr>
      <th>2013-07-30</th>
      <td>30.86118893</td>
      <td>18.48696352</td>
      <td>81.43546269</td>
      <td>58.83253602</td>
      <td>37.86079161</td>
      <td>53.84046520</td>
      <td>33.21597708</td>
      <td>66.16563896</td>
      <td>47.36000000</td>
      <td>43.04519972</td>
      <td>...</td>
      <td>28.38264907</td>
      <td>40.88599404</td>
      <td>79.28742502</td>
      <td>41.08378656</td>
      <td>23.06366342</td>
      <td>23.78811863</td>
      <td>47.53237266</td>
      <td>79.55844670</td>
      <td>27.77316051</td>
      <td>28.96206545</td>
    </tr>
    <tr>
      <th>2013-07-31</th>
      <td>30.77861719</td>
      <td>18.63139292</td>
      <td>81.73270857</td>
      <td>58.73000866</td>
      <td>38.52144972</td>
      <td>53.87744989</td>
      <td>32.99081455</td>
      <td>66.22844876</td>
      <td>47.28000000</td>
      <td>43.44107832</td>
      <td>...</td>
      <td>28.32843198</td>
      <td>41.28388974</td>
      <td>79.23671352</td>
      <td>41.69639686</td>
      <td>23.20721320</td>
      <td>23.21996075</td>
      <td>47.44778390</td>
      <td>80.02819050</td>
      <td>28.13385091</td>
      <td>28.74031861</td>
    </tr>
    <tr>
      <th>2013-08-01</th>
      <td>31.68002538</td>
      <td>18.66027880</td>
      <td>82.66407899</td>
      <td>59.26808264</td>
      <td>38.32664028</td>
      <td>54.36749706</td>
      <td>33.17995107</td>
      <td>67.16162295</td>
      <td>47.70000000</td>
      <td>43.93372725</td>
      <td>...</td>
      <td>28.97000093</td>
      <td>41.69062757</td>
      <td>78.37461808</td>
      <td>41.71584481</td>
      <td>23.70963740</td>
      <td>23.46212640</td>
      <td>48.08545297</td>
      <td>80.97725310</td>
      <td>28.61793539</td>
      <td>29.07775945</td>
    </tr>
    <tr>
      <th>2013-08-02</th>
      <td>31.91397865</td>
      <td>18.21736196</td>
      <td>82.70371177</td>
      <td>60.02912118</td>
      <td>38.38593011</td>
      <td>54.07161953</td>
      <td>33.09889256</td>
      <td>66.92832940</td>
      <td>47.45000000</td>
      <td>43.87214613</td>
      <td>...</td>
      <td>28.87060292</td>
      <td>41.12473146</td>
      <td>77.71536862</td>
      <td>41.78391262</td>
      <td>23.92496206</td>
      <td>23.53663891</td>
      <td>48.40428750</td>
      <td>80.52668616</td>
      <td>28.61793539</td>
      <td>29.82977047</td>
    </tr>
    <tr>
      <th>2013-08-05</th>
      <td>31.61121560</td>
      <td>18.45807764</td>
      <td>82.64426260</td>
      <td>60.92591114</td>
      <td>37.86926159</td>
      <td>54.58015904</td>
      <td>32.82869752</td>
      <td>66.60530757</td>
      <td>47.63000000</td>
      <td>43.61702437</td>
      <td>...</td>
      <td>28.60855363</td>
      <td>41.00978381</td>
      <td>77.41109964</td>
      <td>41.52136535</td>
      <td>24.09243679</td>
      <td>23.54595298</td>
      <td>48.68408107</td>
      <td>80.46916901</td>
      <td>28.39962278</td>
      <td>30.12864664</td>
    </tr>
    <tr>
      <th>2013-08-06</th>
      <td>31.70754930</td>
      <td>18.21736196</td>
      <td>82.41637409</td>
      <td>60.38082896</td>
      <td>38.01325118</td>
      <td>54.23805064</td>
      <td>32.51346997</td>
      <td>65.72597036</td>
      <td>47.39000000</td>
      <td>43.47626753</td>
      <td>...</td>
      <td>28.34650434</td>
      <td>40.50305117</td>
      <td>77.30967665</td>
      <td>41.40467767</td>
      <td>23.85318717</td>
      <td>23.68566393</td>
      <td>48.15052124</td>
      <td>79.56803513</td>
      <td>27.88706274</td>
      <td>30.01295264</td>
    </tr>
    <tr>
      <th>2013-08-07</th>
      <td>31.84516887</td>
      <td>18.16921883</td>
      <td>81.53454465</td>
      <td>60.34578796</td>
      <td>37.75068193</td>
      <td>54.31202002</td>
      <td>32.36035945</td>
      <td>65.50164964</td>
      <td>47.10000000</td>
      <td>43.23874037</td>
      <td>...</td>
      <td>28.19288924</td>
      <td>40.52972131</td>
      <td>77.19980174</td>
      <td>41.22964615</td>
      <td>23.61393755</td>
      <td>23.19201856</td>
      <td>48.07243931</td>
      <td>79.17498438</td>
      <td>27.57383161</td>
      <td>30.11900548</td>
    </tr>
    <tr>
      <th>2013-08-08</th>
      <td>31.54928679</td>
      <td>18.27513373</td>
      <td>80.90042011</td>
      <td>60.22638901</td>
      <td>38.16571074</td>
      <td>55.11643707</td>
      <td>32.35135295</td>
      <td>65.48370398</td>
      <td>47.51000000</td>
      <td>43.19475386</td>
      <td>...</td>
      <td>28.02120177</td>
      <td>40.52083127</td>
      <td>77.57168605</td>
      <td>41.57970919</td>
      <td>23.87711213</td>
      <td>23.26653107</td>
      <td>48.21558951</td>
      <td>79.84604489</td>
      <td>28.01994868</td>
      <td>30.11900548</td>
    </tr>
    <tr>
      <th>2013-08-09</th>
      <td>31.80388300</td>
      <td>17.90924591</td>
      <td>82.40646589</td>
      <td>59.36939001</td>
      <td>37.86926159</td>
      <td>55.00548300</td>
      <td>32.32433344</td>
      <td>65.97720956</td>
      <td>47.18000000</td>
      <td>43.10678084</td>
      <td>...</td>
      <td>27.86758667</td>
      <td>40.27190997</td>
      <td>77.20825366</td>
      <td>41.39495370</td>
      <td>23.99673694</td>
      <td>23.26653107</td>
      <td>48.41079433</td>
      <td>79.15581519</td>
      <td>27.99147312</td>
      <td>29.80084697</td>
    </tr>
    <tr>
      <th>2013-08-12</th>
      <td>31.96214550</td>
      <td>18.12107570</td>
      <td>81.69307578</td>
      <td>61.05595360</td>
      <td>38.14877079</td>
      <td>54.24729681</td>
      <td>32.33333995</td>
      <td>65.31322023</td>
      <td>47.20000000</td>
      <td>43.46747023</td>
      <td>...</td>
      <td>27.76818866</td>
      <td>40.35192038</td>
      <td>76.50187303</td>
      <td>41.53108932</td>
      <td>24.28383649</td>
      <td>23.12682011</td>
      <td>48.45634212</td>
      <td>78.90656401</td>
      <td>28.10537535</td>
      <td>29.24165929</td>
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
      <th>2017-05-19</th>
      <td>55.50327007</td>
      <td>44.83282860</td>
      <td>151.06072036</td>
      <td>150.70113045</td>
      <td>63.42995100</td>
      <td>87.59994036</td>
      <td>42.31486674</td>
      <td>118.75601310</td>
      <td>136.43000000</td>
      <td>79.14250576</td>
      <td>...</td>
      <td>40.43133035</td>
      <td>65.31985198</td>
      <td>78.78898294</td>
      <td>61.13598414</td>
      <td>26.81497802</td>
      <td>51.24320268</td>
      <td>68.90686651</td>
      <td>116.46112494</td>
      <td>39.54646594</td>
      <td>59.92967369</td>
    </tr>
    <tr>
      <th>2017-05-22</th>
      <td>55.45382835</td>
      <td>45.81435227</td>
      <td>146.97179877</td>
      <td>151.61679784</td>
      <td>63.29454092</td>
      <td>87.91434122</td>
      <td>42.87370534</td>
      <td>120.45421034</td>
      <td>138.86000000</td>
      <td>79.97056004</td>
      <td>...</td>
      <td>40.86051697</td>
      <td>66.15263846</td>
      <td>79.13518133</td>
      <td>62.09836493</td>
      <td>26.73836380</td>
      <td>51.49936943</td>
      <td>69.83126290</td>
      <td>116.57989212</td>
      <td>39.65494752</td>
      <td>59.92967369</td>
    </tr>
    <tr>
      <th>2017-05-23</th>
      <td>58.00502088</td>
      <td>46.26049939</td>
      <td>140.27992953</td>
      <td>151.42972601</td>
      <td>63.68142686</td>
      <td>87.62941544</td>
      <td>42.82468441</td>
      <td>119.90450488</td>
      <td>139.52000000</td>
      <td>79.84391644</td>
      <td>...</td>
      <td>41.31896631</td>
      <td>62.67453024</td>
      <td>79.41406336</td>
      <td>62.65396622</td>
      <td>26.62344247</td>
      <td>52.19890171</td>
      <td>69.74275686</td>
      <td>116.59968666</td>
      <td>40.76934918</td>
      <td>61.04261076</td>
    </tr>
    <tr>
      <th>2017-05-24</th>
      <td>58.56865644</td>
      <td>46.36955757</td>
      <td>132.66057320</td>
      <td>150.97681525</td>
      <td>63.76847620</td>
      <td>88.39576754</td>
      <td>42.67762162</td>
      <td>119.70818149</td>
      <td>141.12000000</td>
      <td>79.99978549</td>
      <td>...</td>
      <td>41.61159355</td>
      <td>63.13501218</td>
      <td>79.13518133</td>
      <td>62.23726525</td>
      <td>26.89159225</td>
      <td>52.01106475</td>
      <td>70.75565928</td>
      <td>117.87643393</td>
      <td>40.13818363</td>
      <td>61.90712437</td>
    </tr>
    <tr>
      <th>2017-05-25</th>
      <td>58.63787484</td>
      <td>47.60885514</td>
      <td>131.61341035</td>
      <td>151.49864721</td>
      <td>64.14569000</td>
      <td>89.51582062</td>
      <td>43.08939743</td>
      <td>120.83704093</td>
      <td>142.85000000</td>
      <td>80.21410542</td>
      <td>...</td>
      <td>42.29439045</td>
      <td>64.10496348</td>
      <td>78.61588375</td>
      <td>62.57459460</td>
      <td>26.77667091</td>
      <td>51.53652928</td>
      <td>70.93267135</td>
      <td>118.07437924</td>
      <td>40.31569894</td>
      <td>62.18535864</td>
    </tr>
    <tr>
      <th>2017-05-26</th>
      <td>58.84553005</td>
      <td>48.32269053</td>
      <td>133.79749286</td>
      <td>151.24265417</td>
      <td>63.89421413</td>
      <td>89.40774532</td>
      <td>43.83451556</td>
      <td>120.63090138</td>
      <td>141.89000000</td>
      <td>80.67197073</td>
      <td>...</td>
      <td>42.23586500</td>
      <td>64.51645797</td>
      <td>78.42355131</td>
      <td>62.22734380</td>
      <td>26.81497802</td>
      <td>50.82472608</td>
      <td>70.89333534</td>
      <td>118.00509838</td>
      <td>39.89163460</td>
      <td>62.21516946</td>
    </tr>
    <tr>
      <th>2017-05-30</th>
      <td>59.69592756</td>
      <td>47.54936885</td>
      <td>132.63065426</td>
      <td>151.30172949</td>
      <td>63.85552554</td>
      <td>89.43722040</td>
      <td>44.11883696</td>
      <td>121.49472426</td>
      <td>142.41000000</td>
      <td>82.61059193</td>
      <td>...</td>
      <td>42.33340741</td>
      <td>64.38909063</td>
      <td>77.99080333</td>
      <td>62.12812929</td>
      <td>27.12143491</td>
      <td>51.20039999</td>
      <td>71.20802347</td>
      <td>117.21331713</td>
      <td>39.31964082</td>
      <td>61.86737662</td>
    </tr>
    <tr>
      <th>2017-05-31</th>
      <td>59.66626253</td>
      <td>47.99551598</td>
      <td>133.26892494</td>
      <td>150.40575387</td>
      <td>63.85552554</td>
      <td>90.16427240</td>
      <td>44.76591323</td>
      <td>122.18185609</td>
      <td>141.86000000</td>
      <td>83.54580618</td>
      <td>...</td>
      <td>42.61628041</td>
      <td>65.35904193</td>
      <td>77.41380602</td>
      <td>63.02105992</td>
      <td>27.08312780</td>
      <td>51.54641544</td>
      <td>71.43420556</td>
      <td>117.98530385</td>
      <td>39.51688006</td>
      <td>61.88725050</td>
    </tr>
    <tr>
      <th>2017-06-01</th>
      <td>60.05190791</td>
      <td>48.63003633</td>
      <td>136.72954883</td>
      <td>150.81928108</td>
      <td>64.52290380</td>
      <td>91.51030109</td>
      <td>45.19729742</td>
      <td>122.98678196</td>
      <td>141.38000000</td>
      <td>80.08746182</td>
      <td>...</td>
      <td>42.54800072</td>
      <td>65.30025701</td>
      <td>77.60613845</td>
      <td>63.55681830</td>
      <td>27.19804914</td>
      <td>51.84300011</td>
      <td>72.60445204</td>
      <td>121.40975776</td>
      <td>39.99025421</td>
      <td>62.24498027</td>
    </tr>
    <tr>
      <th>2017-06-02</th>
      <td>60.13101466</td>
      <td>49.09601221</td>
      <td>137.42765739</td>
      <td>153.05429719</td>
      <td>65.04519983</td>
      <td>91.94260228</td>
      <td>45.58946486</td>
      <td>123.42850956</td>
      <td>143.48000000</td>
      <td>78.82102586</td>
      <td>...</td>
      <td>42.21635651</td>
      <td>65.52559923</td>
      <td>76.45214383</td>
      <td>63.94375491</td>
      <td>27.12143491</td>
      <td>52.39662482</td>
      <td>72.76179611</td>
      <td>122.66671050</td>
      <td>39.54646594</td>
      <td>62.10586314</td>
    </tr>
    <tr>
      <th>2017-06-05</th>
      <td>59.72559259</td>
      <td>49.31412858</td>
      <td>135.20368297</td>
      <td>151.55772252</td>
      <td>65.29667569</td>
      <td>91.68715157</td>
      <td>45.70711509</td>
      <td>124.25306776</td>
      <td>143.59000000</td>
      <td>76.71679380</td>
      <td>...</td>
      <td>41.72864445</td>
      <td>65.79013140</td>
      <td>77.04837438</td>
      <td>63.39807508</td>
      <td>26.73836380</td>
      <td>52.59434793</td>
      <td>72.96831019</td>
      <td>122.65681324</td>
      <td>39.90149656</td>
      <td>62.27479108</td>
    </tr>
    <tr>
      <th>2017-06-06</th>
      <td>59.42894229</td>
      <td>49.31412858</td>
      <td>130.94522072</td>
      <td>152.06970859</td>
      <td>65.64487304</td>
      <td>90.08567218</td>
      <td>45.45220625</td>
      <td>124.00766354</td>
      <td>143.03000000</td>
      <td>78.03193884</td>
      <td>...</td>
      <td>41.48478841</td>
      <td>66.24081585</td>
      <td>78.09658617</td>
      <td>63.05082428</td>
      <td>26.81497802</td>
      <td>52.09015400</td>
      <td>73.08631824</td>
      <td>122.89434761</td>
      <td>39.70425733</td>
      <td>62.58283617</td>
    </tr>
    <tr>
      <th>2017-06-07</th>
      <td>59.95302448</td>
      <td>50.42453920</td>
      <td>130.26705812</td>
      <td>152.97553010</td>
      <td>66.49602213</td>
      <td>90.32147283</td>
      <td>45.64828997</td>
      <td>124.22361925</td>
      <td>143.62000000</td>
      <td>79.18147302</td>
      <td>...</td>
      <td>41.45552569</td>
      <td>66.49555053</td>
      <td>77.80808751</td>
      <td>63.10043153</td>
      <td>26.96820647</td>
      <td>52.85138798</td>
      <td>73.02731422</td>
      <td>123.07249839</td>
      <td>39.90149656</td>
      <td>62.86107043</td>
    </tr>
    <tr>
      <th>2017-06-08</th>
      <td>59.47838401</td>
      <td>50.98965889</td>
      <td>125.57975776</td>
      <td>152.60138644</td>
      <td>66.50569428</td>
      <td>89.96777186</td>
      <td>45.80515695</td>
      <td>123.85060483</td>
      <td>142.63000000</td>
      <td>80.75863709</td>
      <td>...</td>
      <td>41.18240693</td>
      <td>66.69150029</td>
      <td>77.52920548</td>
      <td>62.95160976</td>
      <td>26.81497802</td>
      <td>52.97002185</td>
      <td>72.74212810</td>
      <td>123.88407418</td>
      <td>40.81865898</td>
      <td>62.18535864</td>
    </tr>
    <tr>
      <th>2017-06-09</th>
      <td>58.54887976</td>
      <td>49.83959075</td>
      <td>128.01316475</td>
      <td>146.68400898</td>
      <td>67.38585980</td>
      <td>90.48849829</td>
      <td>46.36399555</td>
      <td>123.50703891</td>
      <td>138.05000000</td>
      <td>76.99695384</td>
      <td>...</td>
      <td>41.52380538</td>
      <td>64.07557102</td>
      <td>78.98131538</td>
      <td>62.84247379</td>
      <td>26.58513535</td>
      <td>53.35558192</td>
      <td>71.88656975</td>
      <td>123.72571793</td>
      <td>41.75554533</td>
      <td>62.19529558</td>
    </tr>
    <tr>
      <th>2017-06-12</th>
      <td>58.33133621</td>
      <td>49.05635469</td>
      <td>130.59616644</td>
      <td>143.17887358</td>
      <td>67.25044972</td>
      <td>90.74394899</td>
      <td>46.24634532</td>
      <td>123.97821503</td>
      <td>137.25000000</td>
      <td>78.11370356</td>
      <td>...</td>
      <td>41.13363573</td>
      <td>62.92926493</td>
      <td>79.75064513</td>
      <td>62.25710816</td>
      <td>27.04482069</td>
      <td>53.40501269</td>
      <td>70.71632326</td>
      <td>123.71582066</td>
      <td>42.33740107</td>
      <td>61.45996216</td>
    </tr>
    <tr>
      <th>2017-06-13</th>
      <td>58.61809816</td>
      <td>49.02661155</td>
      <td>131.27432905</td>
      <td>144.33084223</td>
      <td>67.38585980</td>
      <td>91.37275071</td>
      <td>46.53066671</td>
      <td>124.73406004</td>
      <td>139.09000000</td>
      <td>79.57331502</td>
      <td>...</td>
      <td>41.54331386</td>
      <td>63.46812677</td>
      <td>79.77949499</td>
      <td>62.78294509</td>
      <td>26.85328513</td>
      <td>53.17763111</td>
      <td>71.46370757</td>
      <td>124.18099215</td>
      <td>42.53464030</td>
      <td>61.67360633</td>
    </tr>
    <tr>
      <th>2017-06-14</th>
      <td>58.71698159</td>
      <td>48.96712526</td>
      <td>130.23713918</td>
      <td>142.92288054</td>
      <td>68.20799244</td>
      <td>92.25700314</td>
      <td>46.70714206</td>
      <td>124.91075109</td>
      <td>138.25000000</td>
      <td>79.28922957</td>
      <td>...</td>
      <td>41.97472897</td>
      <td>63.56610164</td>
      <td>78.92361565</td>
      <td>63.22941040</td>
      <td>26.54682824</td>
      <td>53.04911109</td>
      <td>71.82756572</td>
      <td>124.30965660</td>
      <td>42.63325991</td>
      <td>61.94235833</td>
    </tr>
    <tr>
      <th>2017-06-15</th>
      <td>58.54887976</td>
      <td>48.68952261</td>
      <td>130.79562603</td>
      <td>142.06628846</td>
      <td>68.28536963</td>
      <td>92.77772957</td>
      <td>47.17774299</td>
      <td>124.69479537</td>
      <td>137.52000000</td>
      <td>78.12349961</td>
      <td>...</td>
      <td>42.63165652</td>
      <td>63.54650667</td>
      <td>79.10633146</td>
      <td>62.81270944</td>
      <td>26.61386569</td>
      <td>53.34569576</td>
      <td>71.40470355</td>
      <td>124.54719098</td>
      <td>42.27822930</td>
      <td>62.10161877</td>
    </tr>
    <tr>
      <th>2017-06-16</th>
      <td>58.84553005</td>
      <td>48.37226243</td>
      <td>129.80830106</td>
      <td>140.07741950</td>
      <td>68.72061632</td>
      <td>90.91097444</td>
      <td>47.26598066</td>
      <td>125.21505233</td>
      <td>137.84000000</td>
      <td>78.40758506</td>
      <td>...</td>
      <td>43.18073029</td>
      <td>63.42893681</td>
      <td>80.28917595</td>
      <td>63.19964605</td>
      <td>27.29381692</td>
      <td>53.43467116</td>
      <td>71.57188162</td>
      <td>124.62636910</td>
      <td>42.49519245</td>
      <td>62.26087921</td>
    </tr>
    <tr>
      <th>2017-06-19</th>
      <td>59.87391774</td>
      <td>49.23481354</td>
      <td>129.24981421</td>
      <td>144.08469508</td>
      <td>69.00110863</td>
      <td>92.10962773</td>
      <td>47.93266531</td>
      <td>125.42119188</td>
      <td>140.35000000</td>
      <td>78.73085471</td>
      <td>...</td>
      <td>43.23955963</td>
      <td>64.56544541</td>
      <td>79.58716256</td>
      <td>63.47744669</td>
      <td>27.57154347</td>
      <td>53.55330503</td>
      <td>72.70279208</td>
      <td>125.78434918</td>
      <td>42.76146542</td>
      <td>62.73866054</td>
    </tr>
    <tr>
      <th>2017-06-20</th>
      <td>59.65637419</td>
      <td>47.61876952</td>
      <td>123.24608056</td>
      <td>142.77519225</td>
      <td>68.88504285</td>
      <td>91.61837639</td>
      <td>47.81501508</td>
      <td>124.20398692</td>
      <td>140.91000000</td>
      <td>77.58471685</td>
      <td>...</td>
      <td>43.33760851</td>
      <td>63.93840619</td>
      <td>79.15441457</td>
      <td>62.85239525</td>
      <td>27.13101169</td>
      <td>53.26660652</td>
      <td>72.68312408</td>
      <td>125.91301364</td>
      <td>42.36698695</td>
      <td>62.70879921</td>
    </tr>
    <tr>
      <th>2017-06-21</th>
      <td>59.12240366</td>
      <td>48.01534474</td>
      <td>119.84529455</td>
      <td>143.62193844</td>
      <td>69.00110863</td>
      <td>93.94690777</td>
      <td>47.61893136</td>
      <td>124.77332472</td>
      <td>144.24000000</td>
      <td>78.34880876</td>
      <td>...</td>
      <td>43.15131563</td>
      <td>64.78099015</td>
      <td>78.31776847</td>
      <td>63.26909621</td>
      <td>26.70005669</td>
      <td>52.93047722</td>
      <td>73.16499028</td>
      <td>127.43719255</td>
      <td>41.74568337</td>
      <td>62.70879921</td>
    </tr>
    <tr>
      <th>2017-06-22</th>
      <td>59.93324780</td>
      <td>48.55072128</td>
      <td>120.43399427</td>
      <td>143.38563718</td>
      <td>70.78078399</td>
      <td>94.68378480</td>
      <td>48.30522438</td>
      <td>119.83579169</td>
      <td>143.69000000</td>
      <td>79.66147947</td>
      <td>...</td>
      <td>42.42575385</td>
      <td>65.23167459</td>
      <td>77.97157008</td>
      <td>63.32862492</td>
      <td>26.78624769</td>
      <td>53.23694805</td>
      <td>73.30266633</td>
      <td>128.29986262</td>
      <td>41.71609749</td>
      <td>63.21644187</td>
    </tr>
    <tr>
      <th>2017-06-23</th>
      <td>59.10262697</td>
      <td>48.21363235</td>
      <td>119.47610998</td>
      <td>144.02561977</td>
      <td>70.25848796</td>
      <td>94.14340831</td>
      <td>48.11894484</td>
      <td>120.48365885</td>
      <td>145.41000000</td>
      <td>79.88678863</td>
      <td>...</td>
      <td>42.56302230</td>
      <td>66.16243594</td>
      <td>78.48125104</td>
      <td>63.33854637</td>
      <td>27.23635625</td>
      <td>53.71148352</td>
      <td>73.57801845</td>
      <td>128.00239018</td>
      <td>41.35120491</td>
      <td>62.48981610</td>
    </tr>
    <tr>
      <th>2017-06-26</th>
      <td>58.57854478</td>
      <td>48.36234805</td>
      <td>121.52159207</td>
      <td>143.57270901</td>
      <td>70.35520945</td>
      <td>94.31043377</td>
      <td>47.95227368</td>
      <td>120.09101209</td>
      <td>144.96000000</td>
      <td>78.92677572</td>
      <td>...</td>
      <td>42.76892496</td>
      <td>65.99587865</td>
      <td>78.12543603</td>
      <td>63.56673975</td>
      <td>27.95461459</td>
      <td>54.05749897</td>
      <td>73.49934641</td>
      <td>127.97264293</td>
      <td>41.75554533</td>
      <td>62.43009343</td>
    </tr>
    <tr>
      <th>2017-06-27</th>
      <td>58.22256443</td>
      <td>48.08474540</td>
      <td>121.69121741</td>
      <td>141.51491885</td>
      <td>70.01668424</td>
      <td>93.85848253</td>
      <td>47.71697322</td>
      <td>119.94376955</td>
      <td>142.54000000</td>
      <td>76.54633554</td>
      <td>...</td>
      <td>43.14151074</td>
      <td>63.78164638</td>
      <td>78.00041995</td>
      <td>63.92391201</td>
      <td>27.75350225</td>
      <td>53.87954816</td>
      <td>72.74212810</td>
      <td>127.16946735</td>
      <td>41.95278457</td>
      <td>62.46990854</td>
    </tr>
    <tr>
      <th>2017-06-28</th>
      <td>58.73675827</td>
      <td>48.82832394</td>
      <td>116.45278767</td>
      <td>143.58255490</td>
      <td>70.52930812</td>
      <td>94.69360982</td>
      <td>47.53069368</td>
      <td>121.46527575</td>
      <td>143.81000000</td>
      <td>77.58471685</td>
      <td>...</td>
      <td>43.30819385</td>
      <td>64.67321778</td>
      <td>78.40431807</td>
      <td>64.82428373</td>
      <td>28.28980181</td>
      <td>54.34419748</td>
      <td>72.91914017</td>
      <td>127.42727680</td>
      <td>42.37684891</td>
      <td>62.65903032</td>
    </tr>
    <tr>
      <th>2017-06-29</th>
      <td>58.27398382</td>
      <td>49.19515602</td>
      <td>115.79424221</td>
      <td>141.46568942</td>
      <td>70.10373358</td>
      <td>94.08445815</td>
      <td>47.77579833</td>
      <td>120.72906307</td>
      <td>141.24000000</td>
      <td>76.15449354</td>
      <td>...</td>
      <td>43.27877918</td>
      <td>62.88027749</td>
      <td>77.60613845</td>
      <td>64.10898129</td>
      <td>28.12560699</td>
      <td>54.27499439</td>
      <td>72.23075989</td>
      <td>126.81250043</td>
      <td>43.38276899</td>
      <td>62.21111032</td>
    </tr>
    <tr>
      <th>2017-06-30</th>
      <td>58.77942143</td>
      <td>49.88916265</td>
      <td>116.33305213</td>
      <td>141.80044954</td>
      <td>70.13275003</td>
      <td>92.87597984</td>
      <td>47.65814810</td>
      <td>121.40637874</td>
      <td>141.44000000</td>
      <td>76.21326984</td>
      <td>...</td>
      <td>42.94541296</td>
      <td>63.01744232</td>
      <td>77.63498832</td>
      <td>64.41695873</td>
      <td>27.74892476</td>
      <td>54.79896064</td>
      <td>72.53561401</td>
      <td>127.31820357</td>
      <td>43.30387330</td>
      <td>62.09166499</td>
    </tr>
  </tbody>
</table>
<p>1009 rows × 519 columns</p>
</div>



### Stock Example
Let's see what a single stock looks like from the closing prices. For this example and future display examples in this project, we'll use Apple's stock (AAPL). If we tried to graph all the stocks, it would be too much information.


```python
apple_ticker = 'AAPL'
project_helper.plot_stock(close[apple_ticker], '{} Stock'.format(apple_ticker))
```


<div id="1ad2c2d2-5749-418b-9c46-6282732e4546" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("1ad2c2d2-5749-418b-9c46-6282732e4546", [{"type": "scatter", "name": "Index", "x": ["2013-07-01", "2013-07-02", "2013-07-03", "2013-07-05", "2013-07-08", "2013-07-09", "2013-07-10", "2013-07-11", "2013-07-12", "2013-07-15", "2013-07-16", "2013-07-17", "2013-07-18", "2013-07-19", "2013-07-22", "2013-07-23", "2013-07-24", "2013-07-25", "2013-07-26", "2013-07-29", "2013-07-30", "2013-07-31", "2013-08-01", "2013-08-02", "2013-08-05", "2013-08-06", "2013-08-07", "2013-08-08", "2013-08-09", "2013-08-12", "2013-08-13", "2013-08-14", "2013-08-15", "2013-08-16", "2013-08-19", "2013-08-20", "2013-08-21", "2013-08-22", "2013-08-23", "2013-08-26", "2013-08-27", "2013-08-28", "2013-08-29", "2013-08-30", "2013-09-03", "2013-09-04", "2013-09-05", "2013-09-06", "2013-09-09", "2013-09-10", "2013-09-11", "2013-09-12", "2013-09-13", "2013-09-16", "2013-09-17", "2013-09-18", "2013-09-19", "2013-09-20", "2013-09-23", "2013-09-24", "2013-09-25", "2013-09-26", "2013-09-27", "2013-09-30", "2013-10-01", "2013-10-02", "2013-10-03", "2013-10-04", "2013-10-07", "2013-10-08", "2013-10-09", "2013-10-10", "2013-10-11", "2013-10-14", "2013-10-15", "2013-10-16", "2013-10-17", "2013-10-18", "2013-10-21", "2013-10-22", "2013-10-23", "2013-10-24", "2013-10-25", "2013-10-28", "2013-10-29", "2013-10-30", "2013-10-31", "2013-11-01", "2013-11-04", "2013-11-05", "2013-11-06", "2013-11-07", "2013-11-08", "2013-11-11", "2013-11-12", "2013-11-13", "2013-11-14", "2013-11-15", "2013-11-18", "2013-11-19", "2013-11-20", "2013-11-21", "2013-11-22", "2013-11-25", "2013-11-26", "2013-11-27", "2013-11-29", "2013-12-02", "2013-12-03", "2013-12-04", "2013-12-05", "2013-12-06", "2013-12-09", "2013-12-10", "2013-12-11", "2013-12-12", "2013-12-13", "2013-12-16", "2013-12-17", "2013-12-18", "2013-12-19", "2013-12-20", "2013-12-23", "2013-12-24", "2013-12-26", "2013-12-27", "2013-12-30", "2013-12-31", "2014-01-02", "2014-01-03", "2014-01-06", "2014-01-07", "2014-01-08", "2014-01-09", "2014-01-10", "2014-01-13", "2014-01-14", "2014-01-15", "2014-01-16", "2014-01-17", "2014-01-21", "2014-01-22", "2014-01-23", "2014-01-24", "2014-01-27", "2014-01-28", "2014-01-29", "2014-01-30", "2014-01-31", "2014-02-03", "2014-02-04", "2014-02-05", "2014-02-06", "2014-02-07", "2014-02-10", "2014-02-11", "2014-02-12", "2014-02-13", "2014-02-14", "2014-02-18", "2014-02-19", "2014-02-20", "2014-02-21", "2014-02-24", "2014-02-25", "2014-02-26", "2014-02-27", "2014-02-28", "2014-03-03", "2014-03-04", "2014-03-05", "2014-03-06", "2014-03-07", "2014-03-10", "2014-03-11", "2014-03-12", "2014-03-13", "2014-03-14", "2014-03-17", "2014-03-18", "2014-03-19", "2014-03-20", "2014-03-21", "2014-03-24", "2014-03-25", "2014-03-26", "2014-03-27", "2014-03-28", "2014-03-31", "2014-04-01", "2014-04-02", "2014-04-03", "2014-04-04", "2014-04-07", "2014-04-08", "2014-04-09", "2014-04-10", "2014-04-11", "2014-04-14", "2014-04-15", "2014-04-16", "2014-04-17", "2014-04-21", "2014-04-22", "2014-04-23", "2014-04-24", "2014-04-25", "2014-04-28", "2014-04-29", "2014-04-30", "2014-05-01", "2014-05-02", "2014-05-05", "2014-05-06", "2014-05-07", "2014-05-08", "2014-05-09", "2014-05-12", "2014-05-13", "2014-05-14", "2014-05-15", "2014-05-16", "2014-05-19", "2014-05-20", "2014-05-21", "2014-05-22", "2014-05-23", "2014-05-27", "2014-05-28", "2014-05-29", "2014-05-30", "2014-06-02", "2014-06-03", "2014-06-04", "2014-06-05", "2014-06-06", "2014-06-09", "2014-06-10", "2014-06-11", "2014-06-12", "2014-06-13", "2014-06-16", "2014-06-17", "2014-06-18", "2014-06-19", "2014-06-20", "2014-06-23", "2014-06-24", "2014-06-25", "2014-06-26", "2014-06-27", "2014-06-30", "2014-07-01", "2014-07-02", "2014-07-03", "2014-07-07", "2014-07-08", "2014-07-09", "2014-07-10", "2014-07-11", "2014-07-14", "2014-07-15", "2014-07-16", "2014-07-17", "2014-07-18", "2014-07-21", "2014-07-22", "2014-07-23", "2014-07-24", "2014-07-25", "2014-07-28", "2014-07-29", "2014-07-30", "2014-07-31", "2014-08-01", "2014-08-04", "2014-08-05", "2014-08-06", "2014-08-07", "2014-08-08", "2014-08-11", "2014-08-12", "2014-08-13", "2014-08-14", "2014-08-15", "2014-08-18", "2014-08-19", "2014-08-20", "2014-08-21", "2014-08-22", "2014-08-25", "2014-08-26", "2014-08-27", "2014-08-28", "2014-08-29", "2014-09-02", "2014-09-03", "2014-09-04", "2014-09-05", "2014-09-08", "2014-09-09", "2014-09-10", "2014-09-11", "2014-09-12", "2014-09-15", "2014-09-16", "2014-09-17", "2014-09-18", "2014-09-19", "2014-09-22", "2014-09-23", "2014-09-24", "2014-09-25", "2014-09-26", "2014-09-29", "2014-09-30", "2014-10-01", "2014-10-02", "2014-10-03", "2014-10-06", "2014-10-07", "2014-10-08", "2014-10-09", "2014-10-10", "2014-10-13", "2014-10-14", "2014-10-15", "2014-10-16", "2014-10-17", "2014-10-20", "2014-10-21", "2014-10-22", "2014-10-23", "2014-10-24", "2014-10-27", "2014-10-28", "2014-10-29", "2014-10-30", "2014-10-31", "2014-11-03", "2014-11-04", "2014-11-05", "2014-11-06", "2014-11-07", "2014-11-10", "2014-11-11", "2014-11-12", "2014-11-13", "2014-11-14", "2014-11-17", "2014-11-18", "2014-11-19", "2014-11-20", "2014-11-21", "2014-11-24", "2014-11-25", "2014-11-26", "2014-11-28", "2014-12-01", "2014-12-02", "2014-12-03", "2014-12-04", "2014-12-05", "2014-12-08", "2014-12-09", "2014-12-10", "2014-12-11", "2014-12-12", "2014-12-15", "2014-12-16", "2014-12-17", "2014-12-18", "2014-12-19", "2014-12-22", "2014-12-23", "2014-12-24", "2014-12-26", "2014-12-29", "2014-12-30", "2014-12-31", "2015-01-02", "2015-01-05", "2015-01-06", "2015-01-07", "2015-01-08", "2015-01-09", "2015-01-12", "2015-01-13", "2015-01-14", "2015-01-15", "2015-01-16", "2015-01-20", "2015-01-21", "2015-01-22", "2015-01-23", "2015-01-26", "2015-01-27", "2015-01-28", "2015-01-29", "2015-01-30", "2015-02-02", "2015-02-03", "2015-02-04", "2015-02-05", "2015-02-06", "2015-02-09", "2015-02-10", "2015-02-11", "2015-02-12", "2015-02-13", "2015-02-17", "2015-02-18", "2015-02-19", "2015-02-20", "2015-02-23", "2015-02-24", "2015-02-25", "2015-02-26", "2015-02-27", "2015-03-02", "2015-03-03", "2015-03-04", "2015-03-05", "2015-03-06", "2015-03-09", "2015-03-10", "2015-03-11", "2015-03-12", "2015-03-13", "2015-03-16", "2015-03-17", "2015-03-18", "2015-03-19", "2015-03-20", "2015-03-23", "2015-03-24", "2015-03-25", "2015-03-26", "2015-03-27", "2015-03-30", "2015-03-31", "2015-04-01", "2015-04-02", "2015-04-06", "2015-04-07", "2015-04-08", "2015-04-09", "2015-04-10", "2015-04-13", "2015-04-14", "2015-04-15", "2015-04-16", "2015-04-17", "2015-04-20", "2015-04-21", "2015-04-22", "2015-04-23", "2015-04-24", "2015-04-27", "2015-04-28", "2015-04-29", "2015-04-30", "2015-05-01", "2015-05-04", "2015-05-05", "2015-05-06", "2015-05-07", "2015-05-08", "2015-05-11", "2015-05-12", "2015-05-13", "2015-05-14", "2015-05-15", "2015-05-18", "2015-05-19", "2015-05-20", "2015-05-21", "2015-05-22", "2015-05-26", "2015-05-27", "2015-05-28", "2015-05-29", "2015-06-01", "2015-06-02", "2015-06-03", "2015-06-04", "2015-06-05", "2015-06-08", "2015-06-09", "2015-06-10", "2015-06-11", "2015-06-12", "2015-06-15", "2015-06-16", "2015-06-17", "2015-06-18", "2015-06-19", "2015-06-22", "2015-06-23", "2015-06-24", "2015-06-25", "2015-06-26", "2015-06-29", "2015-06-30", "2015-07-01", "2015-07-02", "2015-07-06", "2015-07-07", "2015-07-08", "2015-07-09", "2015-07-10", "2015-07-13", "2015-07-14", "2015-07-15", "2015-07-16", "2015-07-17", "2015-07-20", "2015-07-21", "2015-07-22", "2015-07-23", "2015-07-24", "2015-07-27", "2015-07-28", "2015-07-29", "2015-07-30", "2015-07-31", "2015-08-03", "2015-08-04", "2015-08-05", "2015-08-06", "2015-08-07", "2015-08-10", "2015-08-11", "2015-08-12", "2015-08-13", "2015-08-14", "2015-08-17", "2015-08-18", "2015-08-19", "2015-08-20", "2015-08-21", "2015-08-24", "2015-08-25", "2015-08-26", "2015-08-27", "2015-08-28", "2015-08-31", "2015-09-01", "2015-09-02", "2015-09-03", "2015-09-04", "2015-09-08", "2015-09-09", "2015-09-10", "2015-09-11", "2015-09-14", "2015-09-15", "2015-09-16", "2015-09-17", "2015-09-18", "2015-09-21", "2015-09-22", "2015-09-23", "2015-09-24", "2015-09-25", "2015-09-28", "2015-09-29", "2015-09-30", "2015-10-01", "2015-10-02", "2015-10-05", "2015-10-06", "2015-10-07", "2015-10-08", "2015-10-09", "2015-10-12", "2015-10-13", "2015-10-14", "2015-10-15", "2015-10-16", "2015-10-19", "2015-10-20", "2015-10-21", "2015-10-22", "2015-10-23", "2015-10-26", "2015-10-27", "2015-10-28", "2015-10-29", "2015-10-30", "2015-11-02", "2015-11-03", "2015-11-04", "2015-11-05", "2015-11-06", "2015-11-09", "2015-11-10", "2015-11-11", "2015-11-12", "2015-11-13", "2015-11-16", "2015-11-17", "2015-11-18", "2015-11-19", "2015-11-20", "2015-11-23", "2015-11-24", "2015-11-25", "2015-11-27", "2015-11-30", "2015-12-01", "2015-12-02", "2015-12-03", "2015-12-04", "2015-12-07", "2015-12-08", "2015-12-09", "2015-12-10", "2015-12-11", "2015-12-14", "2015-12-15", "2015-12-16", "2015-12-17", "2015-12-18", "2015-12-21", "2015-12-22", "2015-12-23", "2015-12-24", "2015-12-28", "2015-12-29", "2015-12-30", "2015-12-31", "2016-01-04", "2016-01-05", "2016-01-06", "2016-01-07", "2016-01-08", "2016-01-11", "2016-01-12", "2016-01-13", "2016-01-14", "2016-01-15", "2016-01-19", "2016-01-20", "2016-01-21", "2016-01-22", "2016-01-25", "2016-01-26", "2016-01-27", "2016-01-28", "2016-01-29", "2016-02-01", "2016-02-02", "2016-02-03", "2016-02-04", "2016-02-05", "2016-02-08", "2016-02-09", "2016-02-10", "2016-02-11", "2016-02-12", "2016-02-16", "2016-02-17", "2016-02-18", "2016-02-19", "2016-02-22", "2016-02-23", "2016-02-24", "2016-02-25", "2016-02-26", "2016-02-29", "2016-03-01", "2016-03-02", "2016-03-03", "2016-03-04", "2016-03-07", "2016-03-08", "2016-03-09", "2016-03-10", "2016-03-11", "2016-03-14", "2016-03-15", "2016-03-16", "2016-03-17", "2016-03-18", "2016-03-21", "2016-03-22", "2016-03-23", "2016-03-24", "2016-03-28", "2016-03-29", "2016-03-30", "2016-03-31", "2016-04-01", "2016-04-04", "2016-04-05", "2016-04-06", "2016-04-07", "2016-04-08", "2016-04-11", "2016-04-12", "2016-04-13", "2016-04-14", "2016-04-15", "2016-04-18", "2016-04-19", "2016-04-20", "2016-04-21", "2016-04-22", "2016-04-25", "2016-04-26", "2016-04-27", "2016-04-28", "2016-04-29", "2016-05-02", "2016-05-03", "2016-05-04", "2016-05-05", "2016-05-06", "2016-05-09", "2016-05-10", "2016-05-11", "2016-05-12", "2016-05-13", "2016-05-16", "2016-05-17", "2016-05-18", "2016-05-19", "2016-05-20", "2016-05-23", "2016-05-24", "2016-05-25", "2016-05-26", "2016-05-27", "2016-05-31", "2016-06-01", "2016-06-02", "2016-06-03", "2016-06-06", "2016-06-07", "2016-06-08", "2016-06-09", "2016-06-10", "2016-06-13", "2016-06-14", "2016-06-15", "2016-06-16", "2016-06-17", "2016-06-20", "2016-06-21", "2016-06-22", "2016-06-23", "2016-06-24", "2016-06-27", "2016-06-28", "2016-06-29", "2016-06-30", "2016-07-01", "2016-07-05", "2016-07-06", "2016-07-07", "2016-07-08", "2016-07-11", "2016-07-12", "2016-07-13", "2016-07-14", "2016-07-15", "2016-07-18", "2016-07-19", "2016-07-20", "2016-07-21", "2016-07-22", "2016-07-25", "2016-07-26", "2016-07-27", "2016-07-28", "2016-07-29", "2016-08-01", "2016-08-02", "2016-08-03", "2016-08-04", "2016-08-05", "2016-08-08", "2016-08-09", "2016-08-10", "2016-08-11", "2016-08-12", "2016-08-15", "2016-08-16", "2016-08-17", "2016-08-18", "2016-08-19", "2016-08-22", "2016-08-23", "2016-08-24", "2016-08-25", "2016-08-26", "2016-08-29", "2016-08-30", "2016-08-31", "2016-09-01", "2016-09-02", "2016-09-06", "2016-09-07", "2016-09-08", "2016-09-09", "2016-09-12", "2016-09-13", "2016-09-14", "2016-09-15", "2016-09-16", "2016-09-19", "2016-09-20", "2016-09-21", "2016-09-22", "2016-09-23", "2016-09-26", "2016-09-27", "2016-09-28", "2016-09-29", "2016-09-30", "2016-10-03", "2016-10-04", "2016-10-05", "2016-10-06", "2016-10-07", "2016-10-10", "2016-10-11", "2016-10-12", "2016-10-13", "2016-10-14", "2016-10-17", "2016-10-18", "2016-10-19", "2016-10-20", "2016-10-21", "2016-10-24", "2016-10-25", "2016-10-26", "2016-10-27", "2016-10-28", "2016-10-31", "2016-11-01", "2016-11-02", "2016-11-03", "2016-11-04", "2016-11-07", "2016-11-08", "2016-11-09", "2016-11-10", "2016-11-11", "2016-11-14", "2016-11-15", "2016-11-16", "2016-11-17", "2016-11-18", "2016-11-21", "2016-11-22", "2016-11-23", "2016-11-25", "2016-11-28", "2016-11-29", "2016-11-30", "2016-12-01", "2016-12-02", "2016-12-05", "2016-12-06", "2016-12-07", "2016-12-08", "2016-12-09", "2016-12-12", "2016-12-13", "2016-12-14", "2016-12-15", "2016-12-16", "2016-12-19", "2016-12-20", "2016-12-21", "2016-12-22", "2016-12-23", "2016-12-27", "2016-12-28", "2016-12-29", "2016-12-30", "2017-01-03", "2017-01-04", "2017-01-05", "2017-01-06", "2017-01-09", "2017-01-10", "2017-01-11", "2017-01-12", "2017-01-13", "2017-01-17", "2017-01-18", "2017-01-19", "2017-01-20", "2017-01-23", "2017-01-24", "2017-01-25", "2017-01-26", "2017-01-27", "2017-01-30", "2017-01-31", "2017-02-01", "2017-02-02", "2017-02-03", "2017-02-06", "2017-02-07", "2017-02-08", "2017-02-09", "2017-02-10", "2017-02-13", "2017-02-14", "2017-02-15", "2017-02-16", "2017-02-17", "2017-02-21", "2017-02-22", "2017-02-23", "2017-02-24", "2017-02-27", "2017-02-28", "2017-03-01", "2017-03-02", "2017-03-03", "2017-03-06", "2017-03-07", "2017-03-08", "2017-03-09", "2017-03-10", "2017-03-13", "2017-03-14", "2017-03-15", "2017-03-16", "2017-03-17", "2017-03-20", "2017-03-21", "2017-03-22", "2017-03-23", "2017-03-24", "2017-03-27", "2017-03-28", "2017-03-29", "2017-03-30", "2017-03-31", "2017-04-03", "2017-04-04", "2017-04-05", "2017-04-06", "2017-04-07", "2017-04-10", "2017-04-11", "2017-04-12", "2017-04-13", "2017-04-17", "2017-04-18", "2017-04-19", "2017-04-20", "2017-04-21", "2017-04-24", "2017-04-25", "2017-04-26", "2017-04-27", "2017-04-28", "2017-05-01", "2017-05-02", "2017-05-03", "2017-05-04", "2017-05-05", "2017-05-08", "2017-05-09", "2017-05-10", "2017-05-11", "2017-05-12", "2017-05-15", "2017-05-16", "2017-05-17", "2017-05-18", "2017-05-19", "2017-05-22", "2017-05-23", "2017-05-24", "2017-05-25", "2017-05-26", "2017-05-30", "2017-05-31", "2017-06-01", "2017-06-02", "2017-06-05", "2017-06-06", "2017-06-07", "2017-06-08", "2017-06-09", "2017-06-12", "2017-06-13", "2017-06-14", "2017-06-15", "2017-06-16", "2017-06-19", "2017-06-20", "2017-06-21", "2017-06-22", "2017-06-23", "2017-06-26", "2017-06-27", "2017-06-28", "2017-06-29", "2017-06-30"], "y": [53.10917319210857, 54.31224741988544, 54.61204261580394, 54.17338124688422, 53.86579916276005, 54.81320389445057, 54.60295791289733, 55.45406479377765, 55.35309481004406, 55.47379157723203, 55.83133952734264, 55.846264396403505, 56.03418796510047, 55.1506357166965, 55.327138516025144, 54.377138154932744, 57.170035391368344, 56.90917463647821, 57.23233049701374, 58.11484449365696, 58.83253602328005, 58.730008661905316, 59.2680826369175, 60.02912117755218, 60.9259111359058, 60.38082896150852, 60.345787964582975, 60.22638901209596, 59.36939000574175, 61.05595359903942, 63.95747005195509, 65.12408607737322, 65.04700842283833, 65.62443763138795, 66.33120053144529, 65.45983111492357, 65.62835683416091, 65.70674088962014, 65.45329911030197, 65.70804729054446, 63.82944276137168, 64.13069881451997, 64.23573344883532, 63.64994327437006, 63.82813636044736, 65.14903833502774, 64.70211857881773, 65.08750685149226, 66.126095586327, 64.61981532058553, 61.101677631390636, 61.75226529170222, 60.734578971656596, 58.803718405511006, 59.48304688615764, 60.70583815132154, 61.701315655653715, 61.062485603661024, 64.09725495085738, 63.89606920851203, 62.90712370880146, 63.51982574230775, 63.06650462156856, 62.2826640669763, 63.74713950313949, 63.95616365103077, 63.1527270825737, 63.10308384744953, 63.71970508372877, 62.83004605426657, 63.567901296322745, 63.96635357824047, 64.38100523161978, 64.80271144999041, 65.147601294011, 65.46557927899059, 65.90792663196548, 66.48143663774215, 68.11077987055458, 67.91553825241489, 68.58082292312507, 69.48877156552777, 68.71120173537224, 69.22304961752099, 67.4988616776029, 68.57246195720941, 68.28583759441352, 67.9367672674351, 68.81466868857844, 68.64470592832434, 68.45148923161734, 67.34400794611464, 68.40418343394518, 68.20549908372212, 68.3319106875016, 68.4139074034667, 69.40286138480192, 68.98643896029337, 68.15044039143146, 68.27146439047607, 67.67357166989737, 68.47987271022065, 68.3043156388595, 68.82205131338262, 70.09142355091893, 71.74187026970324, 73.07037475432978, 72.43437458562627, 74.4175387480381, 74.24382134658644, 74.62502723282792, 73.5894244787882, 74.43173048733973, 74.31609409303, 73.76550717012347, 73.65775507542577, 72.85487056493436, 73.25828389508307, 72.92845736131329, 72.37392828860072, 71.54476277940256, 72.14396954991659, 74.91267276367337, 74.59467267932162, 74.09927585369927, 73.59862282833556, 72.86669701435241, 73.72082947232198, 72.68404407334043, 71.087473401905, 71.47511813282965, 70.96362419549942, 71.41335778586878, 70.5012757257508, 70.0309772538934, 70.39759718585265, 71.79837441692275, 73.23988719598835, 72.83121766609828, 71.04673785390953, 72.15053979959329, 72.47116798381572, 73.08482930361849, 71.75632481899196, 72.33844894034661, 66.55662922486023, 65.801050512041, 65.67385047830028, 65.78133976301092, 65.90354640699735, 66.85754666005259, 67.35688563548096, 67.74715846627629, 68.6949392436332, 69.92560019721661, 70.8469435749262, 70.84165609499674, 71.96656744999079, 71.90840517076668, 72.17277916724002, 71.03332724243992, 70.21112411340782, 69.43122082381146, 69.7352509197558, 69.00954429943647, 68.38694353774177, 69.7511133595442, 69.56208595206577, 69.76301018938551, 70.22302094324913, 70.37107038127421, 70.15824931411316, 70.1172713446598, 70.18072110381338, 70.86412788469698, 70.93286512378005, 70.14503061428947, 69.35719610479893, 69.62817945118411, 70.244170862967, 70.22566468321386, 69.88726596772797, 70.43848575037491, 71.27390757923067, 72.04059216900335, 71.3518979081903, 71.04522407228124, 70.96591187333921, 70.95004943355082, 71.59908759489285, 71.71805589330587, 71.22103277993598, 70.2996894022264, 69.19592796695021, 69.19196235700309, 70.10140890487139, 69.19724983693257, 68.68568615375665, 68.95931324010654, 68.4675643879663, 68.60637395481464, 69.3902428543581, 70.21376785337256, 70.28369477543976, 69.36512732469313, 75.0518119888347, 75.60303177148164, 78.5309737824239, 78.29832466552736, 78.00222578947721, 78.18596571702619, 78.33137141508655, 79.43909846030984, 78.57327362185963, 78.29832466552736, 78.15952831737886, 77.83419039401828, 78.80289319953012, 78.9265149640757, 78.9411368932155, 78.26985741907009, 79.42498982111438, 80.3661103512034, 80.38206154662863, 80.59474415229845, 80.72235371570036, 81.63423038750979, 83.16288661576172, 82.94754547752102, 84.45892124406228, 84.14255586812841, 83.56432503396353, 84.74604276171655, 85.71374861751431, 86.05005298772974, 85.81344358892204, 87.18657566177792, 87.69834318167095, 87.3354534857468, 85.87458983805213, 84.93479857424855, 85.79084606206962, 85.67918769409295, 85.77223633407354, 85.47448068613575, 84.59051860632049, 84.51607969433606, 84.00431217444302, 84.07875108642745, 84.58121374232246, 85.58613905411241, 86.47010113392767, 87.01908810981291, 86.98186865382071, 87.49363617371374, 89.29691881653686, 88.72187822145702, 88.75909767744926, 88.4287750055183, 88.60091498948229, 89.74541326124313, 88.69396362946286, 88.19150097356787, 86.61888590925655, 87.86583073363596, 87.40896191133145, 88.13567178957955, 90.4339731970992, 90.28509537313032, 90.88153715540571, 92.13676330874331, 91.5412520128678, 91.32724014091251, 88.95449982140842, 89.44765761330534, 88.94519495741038, 88.50786634950177, 88.35898852553288, 88.34968366153483, 88.59281361233921, 89.76170760659109, 89.74300530268307, 90.93060160084299, 91.17373155164742, 91.62258684544013, 92.72602277601385, 94.00713059371395, 94.04453520153002, 94.05388635348405, 94.74587159808115, 94.95159694106951, 94.34283694886312, 95.50331490635638, 95.61552872980455, 95.84930752865496, 96.59739968497615, 92.52029743302558, 91.75350297279631, 92.5483508888876, 91.97793061969269, 91.63193799739412, 94.44663473555269, 94.84873426957529, 95.06381076451768, 95.03575730865565, 94.31571860819643, 94.98900154888555, 95.18537573991988, 94.40923012773659, 94.50274164727678, 95.98022365601116, 95.1479711321038, 91.51972417394596, 94.21285593670228, 93.61438221164534, 94.21285593670228, 92.7447250799219, 93.41800802061104, 93.1561757658986, 93.1561757658986, 92.34262554589928, 94.25961169647238, 94.46533703946068, 94.19415363279428, 93.33384765302489, 92.34262554589928, 91.21113615946345, 90.01418870934951, 91.33270113486564, 93.2870918932548, 95.82125407279293, 96.30751397440169, 98.02812593394049, 98.39282086014704, 98.28995818865288, 99.81419595715737, 100.37526507439829, 100.03862360405373, 100.99244110336326, 102.30160237692543, 101.55351022060415, 101.79664017140855, 102.086525881983, 102.37766500823341, 102.20861648331379, 103.02568435375841, 104.48137998501022, 105.95585878569756, 107.23311430731206, 107.05467419767471, 108.44462873590228, 107.693301958482, 109.23352185219362, 109.38378720767768, 111.4076737143536, 110.44503628078384, 111.75985814126936, 111.69411704824509, 108.06896534719215, 107.65573561961098, 108.876641632919, 108.4634119053378, 108.00322425416788, 105.56141222755191, 107.17676479900557, 105.138790915253, 104.82886861956713, 103.05385910791166, 101.64042560788971, 100.25047106966215, 102.75332839694352, 105.79620184549576, 104.97913397505116, 106.0685578023106, 105.69289441360044, 105.19514042355951, 107.05467419767471, 106.97954151993272, 105.67411124416495, 103.66431211456565, 102.67819571920151, 99.78558762613336, 99.79497921085111, 101.19432533379644, 105.08244140694643, 105.19514042355951, 102.60306304145948, 103.5140467590816, 103.11960020093592, 100.32090795504531, 99.54140642347177, 102.10530905141852, 102.88481058299207, 105.56141222755191, 106.10612414118162, 106.21882315779465, 102.4997556095642, 108.29436338041825, 111.66594229409183, 110.03180655320268, 111.4123695067125, 111.43115267614799, 112.28578688546358, 113.08407158647265, 112.13180451708513, 112.87664707630907, 115.04517604620136, 117.74169467832836, 119.23137979677614, 119.81593977996452, 120.52306879188593, 121.35748102595319, 121.10762877507428, 122.09289519835148, 125.39754478073088, 124.6149886742045, 121.42819392714532, 122.96030678630841, 121.11705716189994, 121.71104553191392, 121.96561197620562, 121.19248425650486, 119.18423786264805, 119.36337721233481, 119.87251010091822, 117.39284436578043, 115.25260055636498, 117.33627404482678, 116.52543277782353, 117.80769338610772, 119.77822623266205, 121.12648554872551, 120.20721783322772, 118.7033901345415, 119.93850880869756, 119.44823269376538, 116.32743665448551, 117.13827792148876, 116.20486762575248, 119.14652431534556, 117.31741727117551, 117.14770630831435, 118.15654369865558, 120.0705062242562, 118.8071023896233, 118.42053852977293, 119.32566366503237, 119.83479655361576, 119.59908688297527, 119.08052560756624, 119.53308817519594, 118.9579565788332, 117.61912564959532, 120.30621589489668, 119.65565720392898, 121.26791135110982, 122.25789196779978, 122.83302356416254, 125.06755124183422, 123.09701839527989, 121.28676812476105, 117.99626112262008, 121.57904811635521, 121.34333844571476, 118.60910626628531, 117.86426370706141, 118.59024949263409, 120.82458598315468, 119.59380740786793, 119.16303490651752, 119.30031405529951, 122.08376714094813, 121.9133516459084, 123.2577405512217, 123.1441302211952, 123.134662693693, 124.3938438514864, 125.48260951424012, 122.71809148359593, 125.01396690288091, 124.76307742407243, 123.34294829874152, 123.58437025004778, 123.03998741867096, 123.19146785870623, 122.47193576853859, 121.79974131588196, 120.99500147819441, 120.63523543311058, 122.01749444843271, 121.7429361508687, 120.39854724555543, 120.16185905800027, 120.80565092815027, 120.52162510308409, 121.07074169821207, 119.85889817792969, 120.81511845565252, 120.26600186052454, 121.2884948307628, 120.71097565312824, 120.00091109046276, 117.899119984973, 118.74646369642043, 119.85889817792969, 119.70741773789436, 119.29084652779731, 118.99735317522892, 116.0434845945406, 113.67660271898909, 116.71567904719723, 118.96895059272232, 118.92161295521127, 120.0671837829782, 121.66719593085104, 122.71809148359593, 125.03763572163643, 123.7879220913452, 118.55237938262523, 118.495574217612, 117.87071740246635, 116.23283514458471, 116.8103543222193, 116.44112074963327, 115.85413404449648, 114.84110860176042, 112.1333957361295, 108.53573528529114, 109.2552673754588, 109.49195556301396, 109.86285682827562, 113.85717814647816, 107.9322681911444, 109.59656874039543, 109.51097614071968, 110.28130953780159, 111.42254420014518, 110.79486513585621, 109.3778320967796, 107.13340392750388, 100.58081490788116, 98.07009865072528, 98.65973655960278, 104.31835842705635, 107.3901817265312, 107.74206241408714, 107.2380171048854, 102.44483152304231, 106.83858497306512, 104.96505806905107, 103.91892629523613, 106.81005410650654, 104.75583171428808, 107.05732161668098, 108.61700898855057, 109.6631407623655, 110.5856387810932, 110.70927253618044, 108.34121061181752, 107.89422703573294, 109.56803787383686, 107.84667559146864, 108.72162216593205, 109.3683218079267, 109.0925234311937, 106.93368786159377, 103.719210229326, 104.56562593723083, 104.21374524967487, 104.97456835790392, 105.35497991201844, 105.85902522122022, 105.35497991201844, 104.13766293885195, 106.62935861830215, 106.13482359795324, 106.31551908615766, 104.81289344740526, 106.38209110812772, 105.60224742219292, 106.25845735304048, 108.19855627902456, 108.1890459901717, 109.84383625056992, 113.24851965989492, 109.6346098958069, 108.94035880954789, 113.42921514809929, 114.62751154356009, 113.64795179171516, 115.24568031899621, 116.56761046954416, 116.02552400493096, 115.49294782917065, 115.6266644409477, 115.15865629972794, 111.5292054086359, 110.89882709597256, 110.52633082030785, 107.29802976454704, 109.05067249748228, 108.58743994954024, 112.02586710952221, 113.44899390629247, 113.94565560717876, 112.46522169107544, 113.54450577184751, 112.73265491462958, 112.52252881040846, 112.99053695162821, 112.07362304229972, 111.06119726741615, 110.02966911942156, 113.68777357018013, 112.97143457851723, 112.92367864573968, 110.4308189547528, 110.95613421530558, 108.10032943520949, 107.43174637632411, 105.53106025177854, 106.3429111089965, 104.08883108189724, 101.27123104802315, 102.51288530023886, 102.4173734346838, 103.73543717934356, 103.18146835912424, 102.02577478590807, 103.85960260456513, 102.50333411368335, 100.53578968324926, 100.6217503622488, 98.1002371115954, 96.1804486139388, 92.12119432784904, 92.60830484217982, 94.10784113139415, 95.47366080883141, 93.01900586406654, 95.05340860038919, 92.7706750136234, 92.32176924551466, 92.44593467073624, 91.97792652951648, 96.86813404593521, 94.97699910794516, 95.50231436849792, 89.22718480153091, 89.8671143007498, 92.97124993128902, 92.10209195473804, 90.23961057641449, 92.025682462294, 92.76112382706788, 90.28365281802198, 91.23431029823729, 91.21510509661677, 90.52371783827834, 89.97636959209382, 90.2548450155912, 92.79953423030891, 94.22071915022673, 92.4346353995192, 92.22337818169359, 93.02999664975503, 90.92702707230907, 92.28099378655511, 92.914765440032, 93.0588044521858, 92.84754723436019, 96.53494594549831, 96.74620316332391, 97.46639822409307, 98.91639094644171, 97.82169445407257, 97.01507598601108, 97.10149939330336, 97.14951239735466, 98.19619588567251, 98.44586350673912, 100.42399927365177, 101.75876078627728, 101.59551657250292, 101.71074778222601, 101.70114518141571, 102.47895584704644, 101.91240239924136, 101.47068276196958, 101.00975792307732, 103.40080552483096, 105.206094477159, 104.65874623097444, 105.61900631199998, 106.70410020355885, 105.44615949741535, 106.55045859059477, 104.22662919451294, 104.34186040423599, 104.6875540334052, 106.05112334846147, 107.58753947810236, 107.64515508296387, 105.48456990065641, 103.20875350862585, 102.66140526244128, 102.87266248026691, 101.75876078627728, 101.48028536277988, 100.90412931416456, 100.20313945501587, 93.93264112591906, 91.06146348365269, 90.01477999533483, 89.91875398723228, 91.39755451201162, 90.44689703179633, 90.0819982010066, 89.5796103946518, 89.64723952243034, 90.25590167243713, 89.3767230113162, 87.28022005018167, 87.45412352161215, 90.70032165498178, 90.32353080021566, 91.3572903248304, 91.00948338196936, 91.99493638674228, 93.16395416691408, 94.58416585026329, 96.24591013282154, 97.00915314632212, 96.95118532251196, 96.47778142806222, 95.12519887249157, 94.41026237883275, 94.60348845819999, 95.28944103995373, 95.67589319868816, 95.58894146297293, 96.27489404472662, 95.48266711932095, 94.043132828035, 94.15906847565536, 93.84990674866778, 94.2460202113706, 92.10121073039429, 91.87900073912192, 92.66156636055923, 92.31375941769821, 92.84513113595811, 90.23657906450045, 88.9226417248032, 90.4201438398993, 91.2027094613366, 92.36206593754, 92.6422437526225, 91.77272639546995, 92.2944368097615, 92.69055027246435, 93.40548676612312, 93.69532588517401, 94.12042325978192, 93.58905154152201, 95.44402190344748, 95.43436059947912, 96.44879751615713, 96.4874427320306, 96.57439446774583, 96.06234535742266, 95.31842495185879, 94.043132828035, 93.39582546215479, 99.46312435428604, 100.80604560588837, 100.68044865429964, 102.45812858447823, 100.94130386144545, 102.20693468130085, 102.83491943924436, 104.39876396835727, 105.26324945339485, 105.69063553588532, 104.90385661130057, 104.83586337090435, 105.07869637231941, 106.34142797967763, 106.24429477911163, 106.088881658206, 105.95289517741355, 106.22486813899842, 105.39923593418726, 105.72948881611171, 104.93299657147035, 104.48618384886669, 103.87424468530077, 103.75768484462156, 102.96119259998018, 103.05832580054621, 103.67026496411215, 104.64159696977232, 104.61245700960251, 105.25353613333824, 102.49495323726327, 100.17346974373545, 102.41724667681049, 104.85529001101757, 108.56577827263949, 112.2568398941482, 111.62547409046907, 110.32388920288444, 110.3141758828278, 110.29474924271463, 111.33407448877102, 109.47883035796005, 109.64395679892228, 109.84793652011093, 110.6832820449787, 108.96402439496016, 109.80908323988452, 109.2942772768846, 109.76051663960152, 109.80908323988452, 110.62500212463907, 110.79012856560131, 112.72307925686508, 112.96591225828014, 113.97609754416678, 113.62641802212907, 114.2577838258082, 114.18007726535538, 114.10237070490255, 113.7624045029215, 113.7041245825819, 113.2573118599782, 114.2772104659214, 114.86000966931749, 112.2762665342614, 111.1980880079786, 110.45987568367686, 110.28503592265804, 108.29380531105465, 108.39093851162063, 107.23505342488501, 106.26844409327585, 107.8013498009793, 108.43599229142977, 108.26024514022808, 105.24325237793276, 105.86813113776093, 103.21239640849123, 104.57931869561534, 107.39127311484205, 107.3522181923528, 107.45961922919822, 109.09016224312485, 109.15850835748104, 108.60197571200912, 109.14874462685871, 108.9339425531678, 108.82654151632237, 107.90875083782473, 106.90308658372628, 107.30339953924124, 106.53206482007832, 107.3522181923528, 108.4067010995628, 109.47094773739514, 111.25771044127876, 110.62306795082829, 112.46841303844582, 112.46841303844582, 113.08352806765166, 113.22998402698641, 113.88415397868148, 114.18682962797324, 114.29423066481873, 113.54242340690048, 113.7669892112137, 114.489505277265, 114.00131874614927, 113.97202755428232, 113.08352806765166, 113.40573117818806, 113.27880268009797, 113.85486278681455, 115.1241477677155, 116.17863067492549, 116.29579544239328, 116.92067420222143, 116.43248767110569, 116.22744932803707, 117.16476746777931, 117.155003737157, 116.94996539408838, 117.16476746777931, 117.24287731275784, 117.13547627591237, 119.00034882477448, 119.05893120850841, 119.06869493913072, 118.75625555921663, 118.48287110179182, 125.70803176230488, 125.49322968861395, 126.03023487284128, 127.21164627814136, 128.42234887530844, 128.9202991370465, 129.8478535461664, 129.55368079232372, 130.70095453231022, 132.39735074613642, 132.8778329107462, 132.7160378961327, 133.08375383843608, 134.0447181676555, 134.4467542645739, 133.87802027381136, 134.00549513380986, 134.27025061226828, 134.32908516303684, 137.07469753223532, 136.26081957993722, 137.0648917737739, 136.6334384014713, 136.80994205377692, 136.3000426137829, 135.98625834301737, 136.4373232322428, 136.49615778301134, 136.2902368553215, 137.7316833491507, 137.95721579376342, 137.2708127014638, 138.712259195293, 137.12372632454245, 138.6730361614473, 138.18274823837615, 137.9081870014563, 138.14352520453042, 141.00680667526606, 141.3205909460316, 141.13428153526456, 140.86952605680608, 140.9087490906518, 141.95796524602414, 141.22253336141736, 140.86952605680608, 140.55574178604058, 140.38904389219636, 138.8789570891372, 139.0456549829814, 138.31022309837468, 139.07507225836568, 138.457309475296, 137.947410035302, 139.67322352451248, 139.5065256306683, 140.84991453988326, 141.72262704294994, 140.88913757372896, 140.9970009168046, 140.85972029834468, 143.73280752754172, 144.64474306445405, 144.20348393369002, 143.6837787352346, 146.06657804136043, 150.03791021823682, 150.99887454745632, 150.28305417977242, 151.57741429668027, 153.694279777277, 153.30044433902643, 153.07398896203242, 147.9344364928627, 150.18914437684708, 150.70113044657282, 151.61679784050534, 151.42972600733634, 150.97681525334818, 151.49864720903014, 151.2426541741673, 151.3017294899049, 150.4057538678849, 150.819281078048, 153.05429719011983, 151.55772252476774, 152.06970859449345, 152.97553010246975, 152.60138643613172, 146.68400897641718, 143.17887357598732, 144.33084223287017, 142.92288054112444, 142.0662884629295, 140.07741949976423, 144.08469508396357, 142.77519225178048, 143.62193844401918, 143.38563718106883, 144.025619768226, 143.5727090142379, 141.51491884937872, 143.58255490019414, 141.4656894195974, 141.8004495421104], "line": {"color": "black"}}], {"title": "AAPL Stock"}, {"showLink": false, "linkText": "Export to plot.ly", "displayModeBar": false})});</script>


## The Alpha Research Process

In this project you will code and evaluate a "breakout" signal. It is important to understand where these steps fit in the alpha research workflow. The signal-to-noise ratio in trading signals is very low and, as such, it is very easy to fall into the trap of _overfitting_ to noise. It is therefore inadvisable to jump right into signal coding. To help mitigate overfitting, it is best to start with a general observation and hypothesis; i.e., you should be able to answer the following question _before_ you touch any data:

> What feature of markets or investor behaviour would lead to a persistent anomaly that my signal will try to use?

Ideally the assumptions behind the hypothesis will be testable _before_ you actually code and evaluate the signal itself. The workflow therefore is as follows:

![image](images/alpha_steps.png)

In this project, we assume that the first three steps area done ("observe & research", "form hypothesis", "validate hypothesis"). The hypothesis you'll be using for this project is the following:
- In the absence of news or significant investor trading interest, stocks oscillate in a range.
- Traders seek to capitalize on this range-bound behaviour periodically by selling/shorting at the top of the range and buying/covering at the bottom of the range. This behaviour reinforces the existence of the range.
- When stocks break out of the range, due to, e.g., a significant news release or from market pressure from a large investor:
    - the liquidity traders who have been providing liquidity at the bounds of the range seek to cover their positions to mitigate losses, thus magnifying the move out of the range, _and_
    - the move out of the range attracts other investor interest; these investors, due to the behavioural bias of _herding_ (e.g., [Herd Behavior](https://www.investopedia.com/university/behavioral_finance/behavioral8.asp)) build positions which favor continuation of the trend.


Using this hypothesis, let start coding..
## Compute the Highs and Lows in a Window
You'll use the price highs and lows as an indicator for the breakout strategy. In this section, implement `get_high_lows_lookback` to get the maximum high price and minimum low price over a window of days. The variable `lookback_days` contains the number of days to look in the past. Make sure this doesn't include the current day.


```python
def get_high_lows_lookback(high, low, lookback_days):
    """
    Get the highs and lows in a lookback window.
    
    Parameters
    ----------
    high : DataFrame
        High price for each ticker and date
    low : DataFrame
        Low price for each ticker and date
    lookback_days : int
        The number of days to look back
    
    Returns
    -------
    lookback_high : DataFrame
        Lookback high price for each ticker and date
    lookback_low : DataFrame
        Lookback low price for each ticker and date
    """
    #TODO: Implement function
    month = list(high.index)
    lookback_high = high.rolling(lookback_days).max().shift(1)
    lookback_low = low.rolling(lookback_days).min().shift(1)
    return lookback_high, lookback_low

project_tests.test_get_high_lows_lookback(get_high_lows_lookback)
```

    Tests Passed


### View Data
Let's use your implementation of `get_high_lows_lookback` to get the highs and lows for the past 50 days and compare it to it their respective stock.  Just like last time, we'll use Apple's stock as the example to look at.


```python
lookback_days = 50
lookback_high, lookback_low = get_high_lows_lookback(high, low, lookback_days)
project_helper.plot_high_low(
    close[apple_ticker],
    lookback_high[apple_ticker],
    lookback_low[apple_ticker],
    'High and Low of {} Stock'.format(apple_ticker))
```


<div id="a9a3da1e-3349-446e-937e-2716d79d5b18" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("a9a3da1e-3349-446e-937e-2716d79d5b18", [{"type": "scatter", "name": "Index", "x": ["2013-07-01", "2013-07-02", "2013-07-03", "2013-07-05", "2013-07-08", "2013-07-09", "2013-07-10", "2013-07-11", "2013-07-12", "2013-07-15", "2013-07-16", "2013-07-17", "2013-07-18", "2013-07-19", "2013-07-22", "2013-07-23", "2013-07-24", "2013-07-25", "2013-07-26", "2013-07-29", "2013-07-30", "2013-07-31", "2013-08-01", "2013-08-02", "2013-08-05", "2013-08-06", "2013-08-07", "2013-08-08", "2013-08-09", "2013-08-12", "2013-08-13", "2013-08-14", "2013-08-15", "2013-08-16", "2013-08-19", "2013-08-20", "2013-08-21", "2013-08-22", "2013-08-23", "2013-08-26", "2013-08-27", "2013-08-28", "2013-08-29", "2013-08-30", "2013-09-03", "2013-09-04", "2013-09-05", "2013-09-06", "2013-09-09", "2013-09-10", "2013-09-11", "2013-09-12", "2013-09-13", "2013-09-16", "2013-09-17", "2013-09-18", "2013-09-19", "2013-09-20", "2013-09-23", "2013-09-24", "2013-09-25", "2013-09-26", "2013-09-27", "2013-09-30", "2013-10-01", "2013-10-02", "2013-10-03", "2013-10-04", "2013-10-07", "2013-10-08", "2013-10-09", "2013-10-10", "2013-10-11", "2013-10-14", "2013-10-15", "2013-10-16", "2013-10-17", "2013-10-18", "2013-10-21", "2013-10-22", "2013-10-23", "2013-10-24", "2013-10-25", "2013-10-28", "2013-10-29", "2013-10-30", "2013-10-31", "2013-11-01", "2013-11-04", "2013-11-05", "2013-11-06", "2013-11-07", "2013-11-08", "2013-11-11", "2013-11-12", "2013-11-13", "2013-11-14", "2013-11-15", "2013-11-18", "2013-11-19", "2013-11-20", "2013-11-21", "2013-11-22", "2013-11-25", "2013-11-26", "2013-11-27", "2013-11-29", "2013-12-02", "2013-12-03", "2013-12-04", "2013-12-05", "2013-12-06", "2013-12-09", "2013-12-10", "2013-12-11", "2013-12-12", "2013-12-13", "2013-12-16", "2013-12-17", "2013-12-18", "2013-12-19", "2013-12-20", "2013-12-23", "2013-12-24", "2013-12-26", "2013-12-27", "2013-12-30", "2013-12-31", "2014-01-02", "2014-01-03", "2014-01-06", "2014-01-07", "2014-01-08", "2014-01-09", "2014-01-10", "2014-01-13", "2014-01-14", "2014-01-15", "2014-01-16", "2014-01-17", "2014-01-21", "2014-01-22", "2014-01-23", "2014-01-24", "2014-01-27", "2014-01-28", "2014-01-29", "2014-01-30", "2014-01-31", "2014-02-03", "2014-02-04", "2014-02-05", "2014-02-06", "2014-02-07", "2014-02-10", "2014-02-11", "2014-02-12", "2014-02-13", "2014-02-14", "2014-02-18", "2014-02-19", "2014-02-20", "2014-02-21", "2014-02-24", "2014-02-25", "2014-02-26", "2014-02-27", "2014-02-28", "2014-03-03", "2014-03-04", "2014-03-05", "2014-03-06", "2014-03-07", "2014-03-10", "2014-03-11", "2014-03-12", "2014-03-13", "2014-03-14", "2014-03-17", "2014-03-18", "2014-03-19", "2014-03-20", "2014-03-21", "2014-03-24", "2014-03-25", "2014-03-26", "2014-03-27", "2014-03-28", "2014-03-31", "2014-04-01", "2014-04-02", "2014-04-03", "2014-04-04", "2014-04-07", "2014-04-08", "2014-04-09", "2014-04-10", "2014-04-11", "2014-04-14", "2014-04-15", "2014-04-16", "2014-04-17", "2014-04-21", "2014-04-22", "2014-04-23", "2014-04-24", "2014-04-25", "2014-04-28", "2014-04-29", "2014-04-30", "2014-05-01", "2014-05-02", "2014-05-05", "2014-05-06", "2014-05-07", "2014-05-08", "2014-05-09", "2014-05-12", "2014-05-13", "2014-05-14", "2014-05-15", "2014-05-16", "2014-05-19", "2014-05-20", "2014-05-21", "2014-05-22", "2014-05-23", "2014-05-27", "2014-05-28", "2014-05-29", "2014-05-30", "2014-06-02", "2014-06-03", "2014-06-04", "2014-06-05", "2014-06-06", "2014-06-09", "2014-06-10", "2014-06-11", "2014-06-12", "2014-06-13", "2014-06-16", "2014-06-17", "2014-06-18", "2014-06-19", "2014-06-20", "2014-06-23", "2014-06-24", "2014-06-25", "2014-06-26", "2014-06-27", "2014-06-30", "2014-07-01", "2014-07-02", "2014-07-03", "2014-07-07", "2014-07-08", "2014-07-09", "2014-07-10", "2014-07-11", "2014-07-14", "2014-07-15", "2014-07-16", "2014-07-17", "2014-07-18", "2014-07-21", "2014-07-22", "2014-07-23", "2014-07-24", "2014-07-25", "2014-07-28", "2014-07-29", "2014-07-30", "2014-07-31", "2014-08-01", "2014-08-04", "2014-08-05", "2014-08-06", "2014-08-07", "2014-08-08", "2014-08-11", "2014-08-12", "2014-08-13", "2014-08-14", "2014-08-15", "2014-08-18", "2014-08-19", "2014-08-20", "2014-08-21", "2014-08-22", "2014-08-25", "2014-08-26", "2014-08-27", "2014-08-28", "2014-08-29", "2014-09-02", "2014-09-03", "2014-09-04", "2014-09-05", "2014-09-08", "2014-09-09", "2014-09-10", "2014-09-11", "2014-09-12", "2014-09-15", "2014-09-16", "2014-09-17", "2014-09-18", "2014-09-19", "2014-09-22", "2014-09-23", "2014-09-24", "2014-09-25", "2014-09-26", "2014-09-29", "2014-09-30", "2014-10-01", "2014-10-02", "2014-10-03", "2014-10-06", "2014-10-07", "2014-10-08", "2014-10-09", "2014-10-10", "2014-10-13", "2014-10-14", "2014-10-15", "2014-10-16", "2014-10-17", "2014-10-20", "2014-10-21", "2014-10-22", "2014-10-23", "2014-10-24", "2014-10-27", "2014-10-28", "2014-10-29", "2014-10-30", "2014-10-31", "2014-11-03", "2014-11-04", "2014-11-05", "2014-11-06", "2014-11-07", "2014-11-10", "2014-11-11", "2014-11-12", "2014-11-13", "2014-11-14", "2014-11-17", "2014-11-18", "2014-11-19", "2014-11-20", "2014-11-21", "2014-11-24", "2014-11-25", "2014-11-26", "2014-11-28", "2014-12-01", "2014-12-02", "2014-12-03", "2014-12-04", "2014-12-05", "2014-12-08", "2014-12-09", "2014-12-10", "2014-12-11", "2014-12-12", "2014-12-15", "2014-12-16", "2014-12-17", "2014-12-18", "2014-12-19", "2014-12-22", "2014-12-23", "2014-12-24", "2014-12-26", "2014-12-29", "2014-12-30", "2014-12-31", "2015-01-02", "2015-01-05", "2015-01-06", "2015-01-07", "2015-01-08", "2015-01-09", "2015-01-12", "2015-01-13", "2015-01-14", "2015-01-15", "2015-01-16", "2015-01-20", "2015-01-21", "2015-01-22", "2015-01-23", "2015-01-26", "2015-01-27", "2015-01-28", "2015-01-29", "2015-01-30", "2015-02-02", "2015-02-03", "2015-02-04", "2015-02-05", "2015-02-06", "2015-02-09", "2015-02-10", "2015-02-11", "2015-02-12", "2015-02-13", "2015-02-17", "2015-02-18", "2015-02-19", "2015-02-20", "2015-02-23", "2015-02-24", "2015-02-25", "2015-02-26", "2015-02-27", "2015-03-02", "2015-03-03", "2015-03-04", "2015-03-05", "2015-03-06", "2015-03-09", "2015-03-10", "2015-03-11", "2015-03-12", "2015-03-13", "2015-03-16", "2015-03-17", "2015-03-18", "2015-03-19", "2015-03-20", "2015-03-23", "2015-03-24", "2015-03-25", "2015-03-26", "2015-03-27", "2015-03-30", "2015-03-31", "2015-04-01", "2015-04-02", "2015-04-06", "2015-04-07", "2015-04-08", "2015-04-09", "2015-04-10", "2015-04-13", "2015-04-14", "2015-04-15", "2015-04-16", "2015-04-17", "2015-04-20", "2015-04-21", "2015-04-22", "2015-04-23", "2015-04-24", "2015-04-27", "2015-04-28", "2015-04-29", "2015-04-30", "2015-05-01", "2015-05-04", "2015-05-05", "2015-05-06", "2015-05-07", "2015-05-08", "2015-05-11", "2015-05-12", "2015-05-13", "2015-05-14", "2015-05-15", "2015-05-18", "2015-05-19", "2015-05-20", "2015-05-21", "2015-05-22", "2015-05-26", "2015-05-27", "2015-05-28", "2015-05-29", "2015-06-01", "2015-06-02", "2015-06-03", "2015-06-04", "2015-06-05", "2015-06-08", "2015-06-09", "2015-06-10", "2015-06-11", "2015-06-12", "2015-06-15", "2015-06-16", "2015-06-17", "2015-06-18", "2015-06-19", "2015-06-22", "2015-06-23", "2015-06-24", "2015-06-25", "2015-06-26", "2015-06-29", "2015-06-30", "2015-07-01", "2015-07-02", "2015-07-06", "2015-07-07", "2015-07-08", "2015-07-09", "2015-07-10", "2015-07-13", "2015-07-14", "2015-07-15", "2015-07-16", "2015-07-17", "2015-07-20", "2015-07-21", "2015-07-22", "2015-07-23", "2015-07-24", "2015-07-27", "2015-07-28", "2015-07-29", "2015-07-30", "2015-07-31", "2015-08-03", "2015-08-04", "2015-08-05", "2015-08-06", "2015-08-07", "2015-08-10", "2015-08-11", "2015-08-12", "2015-08-13", "2015-08-14", "2015-08-17", "2015-08-18", "2015-08-19", "2015-08-20", "2015-08-21", "2015-08-24", "2015-08-25", "2015-08-26", "2015-08-27", "2015-08-28", "2015-08-31", "2015-09-01", "2015-09-02", "2015-09-03", "2015-09-04", "2015-09-08", "2015-09-09", "2015-09-10", "2015-09-11", "2015-09-14", "2015-09-15", "2015-09-16", "2015-09-17", "2015-09-18", "2015-09-21", "2015-09-22", "2015-09-23", "2015-09-24", "2015-09-25", "2015-09-28", "2015-09-29", "2015-09-30", "2015-10-01", "2015-10-02", "2015-10-05", "2015-10-06", "2015-10-07", "2015-10-08", "2015-10-09", "2015-10-12", "2015-10-13", "2015-10-14", "2015-10-15", "2015-10-16", "2015-10-19", "2015-10-20", "2015-10-21", "2015-10-22", "2015-10-23", "2015-10-26", "2015-10-27", "2015-10-28", "2015-10-29", "2015-10-30", "2015-11-02", "2015-11-03", "2015-11-04", "2015-11-05", "2015-11-06", "2015-11-09", "2015-11-10", "2015-11-11", "2015-11-12", "2015-11-13", "2015-11-16", "2015-11-17", "2015-11-18", "2015-11-19", "2015-11-20", "2015-11-23", "2015-11-24", "2015-11-25", "2015-11-27", "2015-11-30", "2015-12-01", "2015-12-02", "2015-12-03", "2015-12-04", "2015-12-07", "2015-12-08", "2015-12-09", "2015-12-10", "2015-12-11", "2015-12-14", "2015-12-15", "2015-12-16", "2015-12-17", "2015-12-18", "2015-12-21", "2015-12-22", "2015-12-23", "2015-12-24", "2015-12-28", "2015-12-29", "2015-12-30", "2015-12-31", "2016-01-04", "2016-01-05", "2016-01-06", "2016-01-07", "2016-01-08", "2016-01-11", "2016-01-12", "2016-01-13", "2016-01-14", "2016-01-15", "2016-01-19", "2016-01-20", "2016-01-21", "2016-01-22", "2016-01-25", "2016-01-26", "2016-01-27", "2016-01-28", "2016-01-29", "2016-02-01", "2016-02-02", "2016-02-03", "2016-02-04", "2016-02-05", "2016-02-08", "2016-02-09", "2016-02-10", "2016-02-11", "2016-02-12", "2016-02-16", "2016-02-17", "2016-02-18", "2016-02-19", "2016-02-22", "2016-02-23", "2016-02-24", "2016-02-25", "2016-02-26", "2016-02-29", "2016-03-01", "2016-03-02", "2016-03-03", "2016-03-04", "2016-03-07", "2016-03-08", "2016-03-09", "2016-03-10", "2016-03-11", "2016-03-14", "2016-03-15", "2016-03-16", "2016-03-17", "2016-03-18", "2016-03-21", "2016-03-22", "2016-03-23", "2016-03-24", "2016-03-28", "2016-03-29", "2016-03-30", "2016-03-31", "2016-04-01", "2016-04-04", "2016-04-05", "2016-04-06", "2016-04-07", "2016-04-08", "2016-04-11", "2016-04-12", "2016-04-13", "2016-04-14", "2016-04-15", "2016-04-18", "2016-04-19", "2016-04-20", "2016-04-21", "2016-04-22", "2016-04-25", "2016-04-26", "2016-04-27", "2016-04-28", "2016-04-29", "2016-05-02", "2016-05-03", "2016-05-04", "2016-05-05", "2016-05-06", "2016-05-09", "2016-05-10", "2016-05-11", "2016-05-12", "2016-05-13", "2016-05-16", "2016-05-17", "2016-05-18", "2016-05-19", "2016-05-20", "2016-05-23", "2016-05-24", "2016-05-25", "2016-05-26", "2016-05-27", "2016-05-31", "2016-06-01", "2016-06-02", "2016-06-03", "2016-06-06", "2016-06-07", "2016-06-08", "2016-06-09", "2016-06-10", "2016-06-13", "2016-06-14", "2016-06-15", "2016-06-16", "2016-06-17", "2016-06-20", "2016-06-21", "2016-06-22", "2016-06-23", "2016-06-24", "2016-06-27", "2016-06-28", "2016-06-29", "2016-06-30", "2016-07-01", "2016-07-05", "2016-07-06", "2016-07-07", "2016-07-08", "2016-07-11", "2016-07-12", "2016-07-13", "2016-07-14", "2016-07-15", "2016-07-18", "2016-07-19", "2016-07-20", "2016-07-21", "2016-07-22", "2016-07-25", "2016-07-26", "2016-07-27", "2016-07-28", "2016-07-29", "2016-08-01", "2016-08-02", "2016-08-03", "2016-08-04", "2016-08-05", "2016-08-08", "2016-08-09", "2016-08-10", "2016-08-11", "2016-08-12", "2016-08-15", "2016-08-16", "2016-08-17", "2016-08-18", "2016-08-19", "2016-08-22", "2016-08-23", "2016-08-24", "2016-08-25", "2016-08-26", "2016-08-29", "2016-08-30", "2016-08-31", "2016-09-01", "2016-09-02", "2016-09-06", "2016-09-07", "2016-09-08", "2016-09-09", "2016-09-12", "2016-09-13", "2016-09-14", "2016-09-15", "2016-09-16", "2016-09-19", "2016-09-20", "2016-09-21", "2016-09-22", "2016-09-23", "2016-09-26", "2016-09-27", "2016-09-28", "2016-09-29", "2016-09-30", "2016-10-03", "2016-10-04", "2016-10-05", "2016-10-06", "2016-10-07", "2016-10-10", "2016-10-11", "2016-10-12", "2016-10-13", "2016-10-14", "2016-10-17", "2016-10-18", "2016-10-19", "2016-10-20", "2016-10-21", "2016-10-24", "2016-10-25", "2016-10-26", "2016-10-27", "2016-10-28", "2016-10-31", "2016-11-01", "2016-11-02", "2016-11-03", "2016-11-04", "2016-11-07", "2016-11-08", "2016-11-09", "2016-11-10", "2016-11-11", "2016-11-14", "2016-11-15", "2016-11-16", "2016-11-17", "2016-11-18", "2016-11-21", "2016-11-22", "2016-11-23", "2016-11-25", "2016-11-28", "2016-11-29", "2016-11-30", "2016-12-01", "2016-12-02", "2016-12-05", "2016-12-06", "2016-12-07", "2016-12-08", "2016-12-09", "2016-12-12", "2016-12-13", "2016-12-14", "2016-12-15", "2016-12-16", "2016-12-19", "2016-12-20", "2016-12-21", "2016-12-22", "2016-12-23", "2016-12-27", "2016-12-28", "2016-12-29", "2016-12-30", "2017-01-03", "2017-01-04", "2017-01-05", "2017-01-06", "2017-01-09", "2017-01-10", "2017-01-11", "2017-01-12", "2017-01-13", "2017-01-17", "2017-01-18", "2017-01-19", "2017-01-20", "2017-01-23", "2017-01-24", "2017-01-25", "2017-01-26", "2017-01-27", "2017-01-30", "2017-01-31", "2017-02-01", "2017-02-02", "2017-02-03", "2017-02-06", "2017-02-07", "2017-02-08", "2017-02-09", "2017-02-10", "2017-02-13", "2017-02-14", "2017-02-15", "2017-02-16", "2017-02-17", "2017-02-21", "2017-02-22", "2017-02-23", "2017-02-24", "2017-02-27", "2017-02-28", "2017-03-01", "2017-03-02", "2017-03-03", "2017-03-06", "2017-03-07", "2017-03-08", "2017-03-09", "2017-03-10", "2017-03-13", "2017-03-14", "2017-03-15", "2017-03-16", "2017-03-17", "2017-03-20", "2017-03-21", "2017-03-22", "2017-03-23", "2017-03-24", "2017-03-27", "2017-03-28", "2017-03-29", "2017-03-30", "2017-03-31", "2017-04-03", "2017-04-04", "2017-04-05", "2017-04-06", "2017-04-07", "2017-04-10", "2017-04-11", "2017-04-12", "2017-04-13", "2017-04-17", "2017-04-18", "2017-04-19", "2017-04-20", "2017-04-21", "2017-04-24", "2017-04-25", "2017-04-26", "2017-04-27", "2017-04-28", "2017-05-01", "2017-05-02", "2017-05-03", "2017-05-04", "2017-05-05", "2017-05-08", "2017-05-09", "2017-05-10", "2017-05-11", "2017-05-12", "2017-05-15", "2017-05-16", "2017-05-17", "2017-05-18", "2017-05-19", "2017-05-22", "2017-05-23", "2017-05-24", "2017-05-25", "2017-05-26", "2017-05-30", "2017-05-31", "2017-06-01", "2017-06-02", "2017-06-05", "2017-06-06", "2017-06-07", "2017-06-08", "2017-06-09", "2017-06-12", "2017-06-13", "2017-06-14", "2017-06-15", "2017-06-16", "2017-06-19", "2017-06-20", "2017-06-21", "2017-06-22", "2017-06-23", "2017-06-26", "2017-06-27", "2017-06-28", "2017-06-29", "2017-06-30"], "y": [53.10917319210857, 54.31224741988544, 54.61204261580394, 54.17338124688422, 53.86579916276005, 54.81320389445057, 54.60295791289733, 55.45406479377765, 55.35309481004406, 55.47379157723203, 55.83133952734264, 55.846264396403505, 56.03418796510047, 55.1506357166965, 55.327138516025144, 54.377138154932744, 57.170035391368344, 56.90917463647821, 57.23233049701374, 58.11484449365696, 58.83253602328005, 58.730008661905316, 59.2680826369175, 60.02912117755218, 60.9259111359058, 60.38082896150852, 60.345787964582975, 60.22638901209596, 59.36939000574175, 61.05595359903942, 63.95747005195509, 65.12408607737322, 65.04700842283833, 65.62443763138795, 66.33120053144529, 65.45983111492357, 65.62835683416091, 65.70674088962014, 65.45329911030197, 65.70804729054446, 63.82944276137168, 64.13069881451997, 64.23573344883532, 63.64994327437006, 63.82813636044736, 65.14903833502774, 64.70211857881773, 65.08750685149226, 66.126095586327, 64.61981532058553, 61.101677631390636, 61.75226529170222, 60.734578971656596, 58.803718405511006, 59.48304688615764, 60.70583815132154, 61.701315655653715, 61.062485603661024, 64.09725495085738, 63.89606920851203, 62.90712370880146, 63.51982574230775, 63.06650462156856, 62.2826640669763, 63.74713950313949, 63.95616365103077, 63.1527270825737, 63.10308384744953, 63.71970508372877, 62.83004605426657, 63.567901296322745, 63.96635357824047, 64.38100523161978, 64.80271144999041, 65.147601294011, 65.46557927899059, 65.90792663196548, 66.48143663774215, 68.11077987055458, 67.91553825241489, 68.58082292312507, 69.48877156552777, 68.71120173537224, 69.22304961752099, 67.4988616776029, 68.57246195720941, 68.28583759441352, 67.9367672674351, 68.81466868857844, 68.64470592832434, 68.45148923161734, 67.34400794611464, 68.40418343394518, 68.20549908372212, 68.3319106875016, 68.4139074034667, 69.40286138480192, 68.98643896029337, 68.15044039143146, 68.27146439047607, 67.67357166989737, 68.47987271022065, 68.3043156388595, 68.82205131338262, 70.09142355091893, 71.74187026970324, 73.07037475432978, 72.43437458562627, 74.4175387480381, 74.24382134658644, 74.62502723282792, 73.5894244787882, 74.43173048733973, 74.31609409303, 73.76550717012347, 73.65775507542577, 72.85487056493436, 73.25828389508307, 72.92845736131329, 72.37392828860072, 71.54476277940256, 72.14396954991659, 74.91267276367337, 74.59467267932162, 74.09927585369927, 73.59862282833556, 72.86669701435241, 73.72082947232198, 72.68404407334043, 71.087473401905, 71.47511813282965, 70.96362419549942, 71.41335778586878, 70.5012757257508, 70.0309772538934, 70.39759718585265, 71.79837441692275, 73.23988719598835, 72.83121766609828, 71.04673785390953, 72.15053979959329, 72.47116798381572, 73.08482930361849, 71.75632481899196, 72.33844894034661, 66.55662922486023, 65.801050512041, 65.67385047830028, 65.78133976301092, 65.90354640699735, 66.85754666005259, 67.35688563548096, 67.74715846627629, 68.6949392436332, 69.92560019721661, 70.8469435749262, 70.84165609499674, 71.96656744999079, 71.90840517076668, 72.17277916724002, 71.03332724243992, 70.21112411340782, 69.43122082381146, 69.7352509197558, 69.00954429943647, 68.38694353774177, 69.7511133595442, 69.56208595206577, 69.76301018938551, 70.22302094324913, 70.37107038127421, 70.15824931411316, 70.1172713446598, 70.18072110381338, 70.86412788469698, 70.93286512378005, 70.14503061428947, 69.35719610479893, 69.62817945118411, 70.244170862967, 70.22566468321386, 69.88726596772797, 70.43848575037491, 71.27390757923067, 72.04059216900335, 71.3518979081903, 71.04522407228124, 70.96591187333921, 70.95004943355082, 71.59908759489285, 71.71805589330587, 71.22103277993598, 70.2996894022264, 69.19592796695021, 69.19196235700309, 70.10140890487139, 69.19724983693257, 68.68568615375665, 68.95931324010654, 68.4675643879663, 68.60637395481464, 69.3902428543581, 70.21376785337256, 70.28369477543976, 69.36512732469313, 75.0518119888347, 75.60303177148164, 78.5309737824239, 78.29832466552736, 78.00222578947721, 78.18596571702619, 78.33137141508655, 79.43909846030984, 78.57327362185963, 78.29832466552736, 78.15952831737886, 77.83419039401828, 78.80289319953012, 78.9265149640757, 78.9411368932155, 78.26985741907009, 79.42498982111438, 80.3661103512034, 80.38206154662863, 80.59474415229845, 80.72235371570036, 81.63423038750979, 83.16288661576172, 82.94754547752102, 84.45892124406228, 84.14255586812841, 83.56432503396353, 84.74604276171655, 85.71374861751431, 86.05005298772974, 85.81344358892204, 87.18657566177792, 87.69834318167095, 87.3354534857468, 85.87458983805213, 84.93479857424855, 85.79084606206962, 85.67918769409295, 85.77223633407354, 85.47448068613575, 84.59051860632049, 84.51607969433606, 84.00431217444302, 84.07875108642745, 84.58121374232246, 85.58613905411241, 86.47010113392767, 87.01908810981291, 86.98186865382071, 87.49363617371374, 89.29691881653686, 88.72187822145702, 88.75909767744926, 88.4287750055183, 88.60091498948229, 89.74541326124313, 88.69396362946286, 88.19150097356787, 86.61888590925655, 87.86583073363596, 87.40896191133145, 88.13567178957955, 90.4339731970992, 90.28509537313032, 90.88153715540571, 92.13676330874331, 91.5412520128678, 91.32724014091251, 88.95449982140842, 89.44765761330534, 88.94519495741038, 88.50786634950177, 88.35898852553288, 88.34968366153483, 88.59281361233921, 89.76170760659109, 89.74300530268307, 90.93060160084299, 91.17373155164742, 91.62258684544013, 92.72602277601385, 94.00713059371395, 94.04453520153002, 94.05388635348405, 94.74587159808115, 94.95159694106951, 94.34283694886312, 95.50331490635638, 95.61552872980455, 95.84930752865496, 96.59739968497615, 92.52029743302558, 91.75350297279631, 92.5483508888876, 91.97793061969269, 91.63193799739412, 94.44663473555269, 94.84873426957529, 95.06381076451768, 95.03575730865565, 94.31571860819643, 94.98900154888555, 95.18537573991988, 94.40923012773659, 94.50274164727678, 95.98022365601116, 95.1479711321038, 91.51972417394596, 94.21285593670228, 93.61438221164534, 94.21285593670228, 92.7447250799219, 93.41800802061104, 93.1561757658986, 93.1561757658986, 92.34262554589928, 94.25961169647238, 94.46533703946068, 94.19415363279428, 93.33384765302489, 92.34262554589928, 91.21113615946345, 90.01418870934951, 91.33270113486564, 93.2870918932548, 95.82125407279293, 96.30751397440169, 98.02812593394049, 98.39282086014704, 98.28995818865288, 99.81419595715737, 100.37526507439829, 100.03862360405373, 100.99244110336326, 102.30160237692543, 101.55351022060415, 101.79664017140855, 102.086525881983, 102.37766500823341, 102.20861648331379, 103.02568435375841, 104.48137998501022, 105.95585878569756, 107.23311430731206, 107.05467419767471, 108.44462873590228, 107.693301958482, 109.23352185219362, 109.38378720767768, 111.4076737143536, 110.44503628078384, 111.75985814126936, 111.69411704824509, 108.06896534719215, 107.65573561961098, 108.876641632919, 108.4634119053378, 108.00322425416788, 105.56141222755191, 107.17676479900557, 105.138790915253, 104.82886861956713, 103.05385910791166, 101.64042560788971, 100.25047106966215, 102.75332839694352, 105.79620184549576, 104.97913397505116, 106.0685578023106, 105.69289441360044, 105.19514042355951, 107.05467419767471, 106.97954151993272, 105.67411124416495, 103.66431211456565, 102.67819571920151, 99.78558762613336, 99.79497921085111, 101.19432533379644, 105.08244140694643, 105.19514042355951, 102.60306304145948, 103.5140467590816, 103.11960020093592, 100.32090795504531, 99.54140642347177, 102.10530905141852, 102.88481058299207, 105.56141222755191, 106.10612414118162, 106.21882315779465, 102.4997556095642, 108.29436338041825, 111.66594229409183, 110.03180655320268, 111.4123695067125, 111.43115267614799, 112.28578688546358, 113.08407158647265, 112.13180451708513, 112.87664707630907, 115.04517604620136, 117.74169467832836, 119.23137979677614, 119.81593977996452, 120.52306879188593, 121.35748102595319, 121.10762877507428, 122.09289519835148, 125.39754478073088, 124.6149886742045, 121.42819392714532, 122.96030678630841, 121.11705716189994, 121.71104553191392, 121.96561197620562, 121.19248425650486, 119.18423786264805, 119.36337721233481, 119.87251010091822, 117.39284436578043, 115.25260055636498, 117.33627404482678, 116.52543277782353, 117.80769338610772, 119.77822623266205, 121.12648554872551, 120.20721783322772, 118.7033901345415, 119.93850880869756, 119.44823269376538, 116.32743665448551, 117.13827792148876, 116.20486762575248, 119.14652431534556, 117.31741727117551, 117.14770630831435, 118.15654369865558, 120.0705062242562, 118.8071023896233, 118.42053852977293, 119.32566366503237, 119.83479655361576, 119.59908688297527, 119.08052560756624, 119.53308817519594, 118.9579565788332, 117.61912564959532, 120.30621589489668, 119.65565720392898, 121.26791135110982, 122.25789196779978, 122.83302356416254, 125.06755124183422, 123.09701839527989, 121.28676812476105, 117.99626112262008, 121.57904811635521, 121.34333844571476, 118.60910626628531, 117.86426370706141, 118.59024949263409, 120.82458598315468, 119.59380740786793, 119.16303490651752, 119.30031405529951, 122.08376714094813, 121.9133516459084, 123.2577405512217, 123.1441302211952, 123.134662693693, 124.3938438514864, 125.48260951424012, 122.71809148359593, 125.01396690288091, 124.76307742407243, 123.34294829874152, 123.58437025004778, 123.03998741867096, 123.19146785870623, 122.47193576853859, 121.79974131588196, 120.99500147819441, 120.63523543311058, 122.01749444843271, 121.7429361508687, 120.39854724555543, 120.16185905800027, 120.80565092815027, 120.52162510308409, 121.07074169821207, 119.85889817792969, 120.81511845565252, 120.26600186052454, 121.2884948307628, 120.71097565312824, 120.00091109046276, 117.899119984973, 118.74646369642043, 119.85889817792969, 119.70741773789436, 119.29084652779731, 118.99735317522892, 116.0434845945406, 113.67660271898909, 116.71567904719723, 118.96895059272232, 118.92161295521127, 120.0671837829782, 121.66719593085104, 122.71809148359593, 125.03763572163643, 123.7879220913452, 118.55237938262523, 118.495574217612, 117.87071740246635, 116.23283514458471, 116.8103543222193, 116.44112074963327, 115.85413404449648, 114.84110860176042, 112.1333957361295, 108.53573528529114, 109.2552673754588, 109.49195556301396, 109.86285682827562, 113.85717814647816, 107.9322681911444, 109.59656874039543, 109.51097614071968, 110.28130953780159, 111.42254420014518, 110.79486513585621, 109.3778320967796, 107.13340392750388, 100.58081490788116, 98.07009865072528, 98.65973655960278, 104.31835842705635, 107.3901817265312, 107.74206241408714, 107.2380171048854, 102.44483152304231, 106.83858497306512, 104.96505806905107, 103.91892629523613, 106.81005410650654, 104.75583171428808, 107.05732161668098, 108.61700898855057, 109.6631407623655, 110.5856387810932, 110.70927253618044, 108.34121061181752, 107.89422703573294, 109.56803787383686, 107.84667559146864, 108.72162216593205, 109.3683218079267, 109.0925234311937, 106.93368786159377, 103.719210229326, 104.56562593723083, 104.21374524967487, 104.97456835790392, 105.35497991201844, 105.85902522122022, 105.35497991201844, 104.13766293885195, 106.62935861830215, 106.13482359795324, 106.31551908615766, 104.81289344740526, 106.38209110812772, 105.60224742219292, 106.25845735304048, 108.19855627902456, 108.1890459901717, 109.84383625056992, 113.24851965989492, 109.6346098958069, 108.94035880954789, 113.42921514809929, 114.62751154356009, 113.64795179171516, 115.24568031899621, 116.56761046954416, 116.02552400493096, 115.49294782917065, 115.6266644409477, 115.15865629972794, 111.5292054086359, 110.89882709597256, 110.52633082030785, 107.29802976454704, 109.05067249748228, 108.58743994954024, 112.02586710952221, 113.44899390629247, 113.94565560717876, 112.46522169107544, 113.54450577184751, 112.73265491462958, 112.52252881040846, 112.99053695162821, 112.07362304229972, 111.06119726741615, 110.02966911942156, 113.68777357018013, 112.97143457851723, 112.92367864573968, 110.4308189547528, 110.95613421530558, 108.10032943520949, 107.43174637632411, 105.53106025177854, 106.3429111089965, 104.08883108189724, 101.27123104802315, 102.51288530023886, 102.4173734346838, 103.73543717934356, 103.18146835912424, 102.02577478590807, 103.85960260456513, 102.50333411368335, 100.53578968324926, 100.6217503622488, 98.1002371115954, 96.1804486139388, 92.12119432784904, 92.60830484217982, 94.10784113139415, 95.47366080883141, 93.01900586406654, 95.05340860038919, 92.7706750136234, 92.32176924551466, 92.44593467073624, 91.97792652951648, 96.86813404593521, 94.97699910794516, 95.50231436849792, 89.22718480153091, 89.8671143007498, 92.97124993128902, 92.10209195473804, 90.23961057641449, 92.025682462294, 92.76112382706788, 90.28365281802198, 91.23431029823729, 91.21510509661677, 90.52371783827834, 89.97636959209382, 90.2548450155912, 92.79953423030891, 94.22071915022673, 92.4346353995192, 92.22337818169359, 93.02999664975503, 90.92702707230907, 92.28099378655511, 92.914765440032, 93.0588044521858, 92.84754723436019, 96.53494594549831, 96.74620316332391, 97.46639822409307, 98.91639094644171, 97.82169445407257, 97.01507598601108, 97.10149939330336, 97.14951239735466, 98.19619588567251, 98.44586350673912, 100.42399927365177, 101.75876078627728, 101.59551657250292, 101.71074778222601, 101.70114518141571, 102.47895584704644, 101.91240239924136, 101.47068276196958, 101.00975792307732, 103.40080552483096, 105.206094477159, 104.65874623097444, 105.61900631199998, 106.70410020355885, 105.44615949741535, 106.55045859059477, 104.22662919451294, 104.34186040423599, 104.6875540334052, 106.05112334846147, 107.58753947810236, 107.64515508296387, 105.48456990065641, 103.20875350862585, 102.66140526244128, 102.87266248026691, 101.75876078627728, 101.48028536277988, 100.90412931416456, 100.20313945501587, 93.93264112591906, 91.06146348365269, 90.01477999533483, 89.91875398723228, 91.39755451201162, 90.44689703179633, 90.0819982010066, 89.5796103946518, 89.64723952243034, 90.25590167243713, 89.3767230113162, 87.28022005018167, 87.45412352161215, 90.70032165498178, 90.32353080021566, 91.3572903248304, 91.00948338196936, 91.99493638674228, 93.16395416691408, 94.58416585026329, 96.24591013282154, 97.00915314632212, 96.95118532251196, 96.47778142806222, 95.12519887249157, 94.41026237883275, 94.60348845819999, 95.28944103995373, 95.67589319868816, 95.58894146297293, 96.27489404472662, 95.48266711932095, 94.043132828035, 94.15906847565536, 93.84990674866778, 94.2460202113706, 92.10121073039429, 91.87900073912192, 92.66156636055923, 92.31375941769821, 92.84513113595811, 90.23657906450045, 88.9226417248032, 90.4201438398993, 91.2027094613366, 92.36206593754, 92.6422437526225, 91.77272639546995, 92.2944368097615, 92.69055027246435, 93.40548676612312, 93.69532588517401, 94.12042325978192, 93.58905154152201, 95.44402190344748, 95.43436059947912, 96.44879751615713, 96.4874427320306, 96.57439446774583, 96.06234535742266, 95.31842495185879, 94.043132828035, 93.39582546215479, 99.46312435428604, 100.80604560588837, 100.68044865429964, 102.45812858447823, 100.94130386144545, 102.20693468130085, 102.83491943924436, 104.39876396835727, 105.26324945339485, 105.69063553588532, 104.90385661130057, 104.83586337090435, 105.07869637231941, 106.34142797967763, 106.24429477911163, 106.088881658206, 105.95289517741355, 106.22486813899842, 105.39923593418726, 105.72948881611171, 104.93299657147035, 104.48618384886669, 103.87424468530077, 103.75768484462156, 102.96119259998018, 103.05832580054621, 103.67026496411215, 104.64159696977232, 104.61245700960251, 105.25353613333824, 102.49495323726327, 100.17346974373545, 102.41724667681049, 104.85529001101757, 108.56577827263949, 112.2568398941482, 111.62547409046907, 110.32388920288444, 110.3141758828278, 110.29474924271463, 111.33407448877102, 109.47883035796005, 109.64395679892228, 109.84793652011093, 110.6832820449787, 108.96402439496016, 109.80908323988452, 109.2942772768846, 109.76051663960152, 109.80908323988452, 110.62500212463907, 110.79012856560131, 112.72307925686508, 112.96591225828014, 113.97609754416678, 113.62641802212907, 114.2577838258082, 114.18007726535538, 114.10237070490255, 113.7624045029215, 113.7041245825819, 113.2573118599782, 114.2772104659214, 114.86000966931749, 112.2762665342614, 111.1980880079786, 110.45987568367686, 110.28503592265804, 108.29380531105465, 108.39093851162063, 107.23505342488501, 106.26844409327585, 107.8013498009793, 108.43599229142977, 108.26024514022808, 105.24325237793276, 105.86813113776093, 103.21239640849123, 104.57931869561534, 107.39127311484205, 107.3522181923528, 107.45961922919822, 109.09016224312485, 109.15850835748104, 108.60197571200912, 109.14874462685871, 108.9339425531678, 108.82654151632237, 107.90875083782473, 106.90308658372628, 107.30339953924124, 106.53206482007832, 107.3522181923528, 108.4067010995628, 109.47094773739514, 111.25771044127876, 110.62306795082829, 112.46841303844582, 112.46841303844582, 113.08352806765166, 113.22998402698641, 113.88415397868148, 114.18682962797324, 114.29423066481873, 113.54242340690048, 113.7669892112137, 114.489505277265, 114.00131874614927, 113.97202755428232, 113.08352806765166, 113.40573117818806, 113.27880268009797, 113.85486278681455, 115.1241477677155, 116.17863067492549, 116.29579544239328, 116.92067420222143, 116.43248767110569, 116.22744932803707, 117.16476746777931, 117.155003737157, 116.94996539408838, 117.16476746777931, 117.24287731275784, 117.13547627591237, 119.00034882477448, 119.05893120850841, 119.06869493913072, 118.75625555921663, 118.48287110179182, 125.70803176230488, 125.49322968861395, 126.03023487284128, 127.21164627814136, 128.42234887530844, 128.9202991370465, 129.8478535461664, 129.55368079232372, 130.70095453231022, 132.39735074613642, 132.8778329107462, 132.7160378961327, 133.08375383843608, 134.0447181676555, 134.4467542645739, 133.87802027381136, 134.00549513380986, 134.27025061226828, 134.32908516303684, 137.07469753223532, 136.26081957993722, 137.0648917737739, 136.6334384014713, 136.80994205377692, 136.3000426137829, 135.98625834301737, 136.4373232322428, 136.49615778301134, 136.2902368553215, 137.7316833491507, 137.95721579376342, 137.2708127014638, 138.712259195293, 137.12372632454245, 138.6730361614473, 138.18274823837615, 137.9081870014563, 138.14352520453042, 141.00680667526606, 141.3205909460316, 141.13428153526456, 140.86952605680608, 140.9087490906518, 141.95796524602414, 141.22253336141736, 140.86952605680608, 140.55574178604058, 140.38904389219636, 138.8789570891372, 139.0456549829814, 138.31022309837468, 139.07507225836568, 138.457309475296, 137.947410035302, 139.67322352451248, 139.5065256306683, 140.84991453988326, 141.72262704294994, 140.88913757372896, 140.9970009168046, 140.85972029834468, 143.73280752754172, 144.64474306445405, 144.20348393369002, 143.6837787352346, 146.06657804136043, 150.03791021823682, 150.99887454745632, 150.28305417977242, 151.57741429668027, 153.694279777277, 153.30044433902643, 153.07398896203242, 147.9344364928627, 150.18914437684708, 150.70113044657282, 151.61679784050534, 151.42972600733634, 150.97681525334818, 151.49864720903014, 151.2426541741673, 151.3017294899049, 150.4057538678849, 150.819281078048, 153.05429719011983, 151.55772252476774, 152.06970859449345, 152.97553010246975, 152.60138643613172, 146.68400897641718, 143.17887357598732, 144.33084223287017, 142.92288054112444, 142.0662884629295, 140.07741949976423, 144.08469508396357, 142.77519225178048, 143.62193844401918, 143.38563718106883, 144.025619768226, 143.5727090142379, 141.51491884937872, 143.58255490019414, 141.4656894195974, 141.8004495421104], "line": {"color": "black"}}, {"type": "scatter", "x": ["2013-07-01", "2013-07-02", "2013-07-03", "2013-07-05", "2013-07-08", "2013-07-09", "2013-07-10", "2013-07-11", "2013-07-12", "2013-07-15", "2013-07-16", "2013-07-17", "2013-07-18", "2013-07-19", "2013-07-22", "2013-07-23", "2013-07-24", "2013-07-25", "2013-07-26", "2013-07-29", "2013-07-30", "2013-07-31", "2013-08-01", "2013-08-02", "2013-08-05", "2013-08-06", "2013-08-07", "2013-08-08", "2013-08-09", "2013-08-12", "2013-08-13", "2013-08-14", "2013-08-15", "2013-08-16", "2013-08-19", "2013-08-20", "2013-08-21", "2013-08-22", "2013-08-23", "2013-08-26", "2013-08-27", "2013-08-28", "2013-08-29", "2013-08-30", "2013-09-03", "2013-09-04", "2013-09-05", "2013-09-06", "2013-09-09", "2013-09-10", "2013-09-11", "2013-09-12", "2013-09-13", "2013-09-16", "2013-09-17", "2013-09-18", "2013-09-19", "2013-09-20", "2013-09-23", "2013-09-24", "2013-09-25", "2013-09-26", "2013-09-27", "2013-09-30", "2013-10-01", "2013-10-02", "2013-10-03", "2013-10-04", "2013-10-07", "2013-10-08", "2013-10-09", "2013-10-10", "2013-10-11", "2013-10-14", "2013-10-15", "2013-10-16", "2013-10-17", "2013-10-18", "2013-10-21", "2013-10-22", "2013-10-23", "2013-10-24", "2013-10-25", "2013-10-28", "2013-10-29", "2013-10-30", "2013-10-31", "2013-11-01", "2013-11-04", "2013-11-05", "2013-11-06", "2013-11-07", "2013-11-08", "2013-11-11", "2013-11-12", "2013-11-13", "2013-11-14", "2013-11-15", "2013-11-18", "2013-11-19", "2013-11-20", "2013-11-21", "2013-11-22", "2013-11-25", "2013-11-26", "2013-11-27", "2013-11-29", "2013-12-02", "2013-12-03", "2013-12-04", "2013-12-05", "2013-12-06", "2013-12-09", "2013-12-10", "2013-12-11", "2013-12-12", "2013-12-13", "2013-12-16", "2013-12-17", "2013-12-18", "2013-12-19", "2013-12-20", "2013-12-23", "2013-12-24", "2013-12-26", "2013-12-27", "2013-12-30", "2013-12-31", "2014-01-02", "2014-01-03", "2014-01-06", "2014-01-07", "2014-01-08", "2014-01-09", "2014-01-10", "2014-01-13", "2014-01-14", "2014-01-15", "2014-01-16", "2014-01-17", "2014-01-21", "2014-01-22", "2014-01-23", "2014-01-24", "2014-01-27", "2014-01-28", "2014-01-29", "2014-01-30", "2014-01-31", "2014-02-03", "2014-02-04", "2014-02-05", "2014-02-06", "2014-02-07", "2014-02-10", "2014-02-11", "2014-02-12", "2014-02-13", "2014-02-14", "2014-02-18", "2014-02-19", "2014-02-20", "2014-02-21", "2014-02-24", "2014-02-25", "2014-02-26", "2014-02-27", "2014-02-28", "2014-03-03", "2014-03-04", "2014-03-05", "2014-03-06", "2014-03-07", "2014-03-10", "2014-03-11", "2014-03-12", "2014-03-13", "2014-03-14", "2014-03-17", "2014-03-18", "2014-03-19", "2014-03-20", "2014-03-21", "2014-03-24", "2014-03-25", "2014-03-26", "2014-03-27", "2014-03-28", "2014-03-31", "2014-04-01", "2014-04-02", "2014-04-03", "2014-04-04", "2014-04-07", "2014-04-08", "2014-04-09", "2014-04-10", "2014-04-11", "2014-04-14", "2014-04-15", "2014-04-16", "2014-04-17", "2014-04-21", "2014-04-22", "2014-04-23", "2014-04-24", "2014-04-25", "2014-04-28", "2014-04-29", "2014-04-30", "2014-05-01", "2014-05-02", "2014-05-05", "2014-05-06", "2014-05-07", "2014-05-08", "2014-05-09", "2014-05-12", "2014-05-13", "2014-05-14", "2014-05-15", "2014-05-16", "2014-05-19", "2014-05-20", "2014-05-21", "2014-05-22", "2014-05-23", "2014-05-27", "2014-05-28", "2014-05-29", "2014-05-30", "2014-06-02", "2014-06-03", "2014-06-04", "2014-06-05", "2014-06-06", "2014-06-09", "2014-06-10", "2014-06-11", "2014-06-12", "2014-06-13", "2014-06-16", "2014-06-17", "2014-06-18", "2014-06-19", "2014-06-20", "2014-06-23", "2014-06-24", "2014-06-25", "2014-06-26", "2014-06-27", "2014-06-30", "2014-07-01", "2014-07-02", "2014-07-03", "2014-07-07", "2014-07-08", "2014-07-09", "2014-07-10", "2014-07-11", "2014-07-14", "2014-07-15", "2014-07-16", "2014-07-17", "2014-07-18", "2014-07-21", "2014-07-22", "2014-07-23", "2014-07-24", "2014-07-25", "2014-07-28", "2014-07-29", "2014-07-30", "2014-07-31", "2014-08-01", "2014-08-04", "2014-08-05", "2014-08-06", "2014-08-07", "2014-08-08", "2014-08-11", "2014-08-12", "2014-08-13", "2014-08-14", "2014-08-15", "2014-08-18", "2014-08-19", "2014-08-20", "2014-08-21", "2014-08-22", "2014-08-25", "2014-08-26", "2014-08-27", "2014-08-28", "2014-08-29", "2014-09-02", "2014-09-03", "2014-09-04", "2014-09-05", "2014-09-08", "2014-09-09", "2014-09-10", "2014-09-11", "2014-09-12", "2014-09-15", "2014-09-16", "2014-09-17", "2014-09-18", "2014-09-19", "2014-09-22", "2014-09-23", "2014-09-24", "2014-09-25", "2014-09-26", "2014-09-29", "2014-09-30", "2014-10-01", "2014-10-02", "2014-10-03", "2014-10-06", "2014-10-07", "2014-10-08", "2014-10-09", "2014-10-10", "2014-10-13", "2014-10-14", "2014-10-15", "2014-10-16", "2014-10-17", "2014-10-20", "2014-10-21", "2014-10-22", "2014-10-23", "2014-10-24", "2014-10-27", "2014-10-28", "2014-10-29", "2014-10-30", "2014-10-31", "2014-11-03", "2014-11-04", "2014-11-05", "2014-11-06", "2014-11-07", "2014-11-10", "2014-11-11", "2014-11-12", "2014-11-13", "2014-11-14", "2014-11-17", "2014-11-18", "2014-11-19", "2014-11-20", "2014-11-21", "2014-11-24", "2014-11-25", "2014-11-26", "2014-11-28", "2014-12-01", "2014-12-02", "2014-12-03", "2014-12-04", "2014-12-05", "2014-12-08", "2014-12-09", "2014-12-10", "2014-12-11", "2014-12-12", "2014-12-15", "2014-12-16", "2014-12-17", "2014-12-18", "2014-12-19", "2014-12-22", "2014-12-23", "2014-12-24", "2014-12-26", "2014-12-29", "2014-12-30", "2014-12-31", "2015-01-02", "2015-01-05", "2015-01-06", "2015-01-07", "2015-01-08", "2015-01-09", "2015-01-12", "2015-01-13", "2015-01-14", "2015-01-15", "2015-01-16", "2015-01-20", "2015-01-21", "2015-01-22", "2015-01-23", "2015-01-26", "2015-01-27", "2015-01-28", "2015-01-29", "2015-01-30", "2015-02-02", "2015-02-03", "2015-02-04", "2015-02-05", "2015-02-06", "2015-02-09", "2015-02-10", "2015-02-11", "2015-02-12", "2015-02-13", "2015-02-17", "2015-02-18", "2015-02-19", "2015-02-20", "2015-02-23", "2015-02-24", "2015-02-25", "2015-02-26", "2015-02-27", "2015-03-02", "2015-03-03", "2015-03-04", "2015-03-05", "2015-03-06", "2015-03-09", "2015-03-10", "2015-03-11", "2015-03-12", "2015-03-13", "2015-03-16", "2015-03-17", "2015-03-18", "2015-03-19", "2015-03-20", "2015-03-23", "2015-03-24", "2015-03-25", "2015-03-26", "2015-03-27", "2015-03-30", "2015-03-31", "2015-04-01", "2015-04-02", "2015-04-06", "2015-04-07", "2015-04-08", "2015-04-09", "2015-04-10", "2015-04-13", "2015-04-14", "2015-04-15", "2015-04-16", "2015-04-17", "2015-04-20", "2015-04-21", "2015-04-22", "2015-04-23", "2015-04-24", "2015-04-27", "2015-04-28", "2015-04-29", "2015-04-30", "2015-05-01", "2015-05-04", "2015-05-05", "2015-05-06", "2015-05-07", "2015-05-08", "2015-05-11", "2015-05-12", "2015-05-13", "2015-05-14", "2015-05-15", "2015-05-18", "2015-05-19", "2015-05-20", "2015-05-21", "2015-05-22", "2015-05-26", "2015-05-27", "2015-05-28", "2015-05-29", "2015-06-01", "2015-06-02", "2015-06-03", "2015-06-04", "2015-06-05", "2015-06-08", "2015-06-09", "2015-06-10", "2015-06-11", "2015-06-12", "2015-06-15", "2015-06-16", "2015-06-17", "2015-06-18", "2015-06-19", "2015-06-22", "2015-06-23", "2015-06-24", "2015-06-25", "2015-06-26", "2015-06-29", "2015-06-30", "2015-07-01", "2015-07-02", "2015-07-06", "2015-07-07", "2015-07-08", "2015-07-09", "2015-07-10", "2015-07-13", "2015-07-14", "2015-07-15", "2015-07-16", "2015-07-17", "2015-07-20", "2015-07-21", "2015-07-22", "2015-07-23", "2015-07-24", "2015-07-27", "2015-07-28", "2015-07-29", "2015-07-30", "2015-07-31", "2015-08-03", "2015-08-04", "2015-08-05", "2015-08-06", "2015-08-07", "2015-08-10", "2015-08-11", "2015-08-12", "2015-08-13", "2015-08-14", "2015-08-17", "2015-08-18", "2015-08-19", "2015-08-20", "2015-08-21", "2015-08-24", "2015-08-25", "2015-08-26", "2015-08-27", "2015-08-28", "2015-08-31", "2015-09-01", "2015-09-02", "2015-09-03", "2015-09-04", "2015-09-08", "2015-09-09", "2015-09-10", "2015-09-11", "2015-09-14", "2015-09-15", "2015-09-16", "2015-09-17", "2015-09-18", "2015-09-21", "2015-09-22", "2015-09-23", "2015-09-24", "2015-09-25", "2015-09-28", "2015-09-29", "2015-09-30", "2015-10-01", "2015-10-02", "2015-10-05", "2015-10-06", "2015-10-07", "2015-10-08", "2015-10-09", "2015-10-12", "2015-10-13", "2015-10-14", "2015-10-15", "2015-10-16", "2015-10-19", "2015-10-20", "2015-10-21", "2015-10-22", "2015-10-23", "2015-10-26", "2015-10-27", "2015-10-28", "2015-10-29", "2015-10-30", "2015-11-02", "2015-11-03", "2015-11-04", "2015-11-05", "2015-11-06", "2015-11-09", "2015-11-10", "2015-11-11", "2015-11-12", "2015-11-13", "2015-11-16", "2015-11-17", "2015-11-18", "2015-11-19", "2015-11-20", "2015-11-23", "2015-11-24", "2015-11-25", "2015-11-27", "2015-11-30", "2015-12-01", "2015-12-02", "2015-12-03", "2015-12-04", "2015-12-07", "2015-12-08", "2015-12-09", "2015-12-10", "2015-12-11", "2015-12-14", "2015-12-15", "2015-12-16", "2015-12-17", "2015-12-18", "2015-12-21", "2015-12-22", "2015-12-23", "2015-12-24", "2015-12-28", "2015-12-29", "2015-12-30", "2015-12-31", "2016-01-04", "2016-01-05", "2016-01-06", "2016-01-07", "2016-01-08", "2016-01-11", "2016-01-12", "2016-01-13", "2016-01-14", "2016-01-15", "2016-01-19", "2016-01-20", "2016-01-21", "2016-01-22", "2016-01-25", "2016-01-26", "2016-01-27", "2016-01-28", "2016-01-29", "2016-02-01", "2016-02-02", "2016-02-03", "2016-02-04", "2016-02-05", "2016-02-08", "2016-02-09", "2016-02-10", "2016-02-11", "2016-02-12", "2016-02-16", "2016-02-17", "2016-02-18", "2016-02-19", "2016-02-22", "2016-02-23", "2016-02-24", "2016-02-25", "2016-02-26", "2016-02-29", "2016-03-01", "2016-03-02", "2016-03-03", "2016-03-04", "2016-03-07", "2016-03-08", "2016-03-09", "2016-03-10", "2016-03-11", "2016-03-14", "2016-03-15", "2016-03-16", "2016-03-17", "2016-03-18", "2016-03-21", "2016-03-22", "2016-03-23", "2016-03-24", "2016-03-28", "2016-03-29", "2016-03-30", "2016-03-31", "2016-04-01", "2016-04-04", "2016-04-05", "2016-04-06", "2016-04-07", "2016-04-08", "2016-04-11", "2016-04-12", "2016-04-13", "2016-04-14", "2016-04-15", "2016-04-18", "2016-04-19", "2016-04-20", "2016-04-21", "2016-04-22", "2016-04-25", "2016-04-26", "2016-04-27", "2016-04-28", "2016-04-29", "2016-05-02", "2016-05-03", "2016-05-04", "2016-05-05", "2016-05-06", "2016-05-09", "2016-05-10", "2016-05-11", "2016-05-12", "2016-05-13", "2016-05-16", "2016-05-17", "2016-05-18", "2016-05-19", "2016-05-20", "2016-05-23", "2016-05-24", "2016-05-25", "2016-05-26", "2016-05-27", "2016-05-31", "2016-06-01", "2016-06-02", "2016-06-03", "2016-06-06", "2016-06-07", "2016-06-08", "2016-06-09", "2016-06-10", "2016-06-13", "2016-06-14", "2016-06-15", "2016-06-16", "2016-06-17", "2016-06-20", "2016-06-21", "2016-06-22", "2016-06-23", "2016-06-24", "2016-06-27", "2016-06-28", "2016-06-29", "2016-06-30", "2016-07-01", "2016-07-05", "2016-07-06", "2016-07-07", "2016-07-08", "2016-07-11", "2016-07-12", "2016-07-13", "2016-07-14", "2016-07-15", "2016-07-18", "2016-07-19", "2016-07-20", "2016-07-21", "2016-07-22", "2016-07-25", "2016-07-26", "2016-07-27", "2016-07-28", "2016-07-29", "2016-08-01", "2016-08-02", "2016-08-03", "2016-08-04", "2016-08-05", "2016-08-08", "2016-08-09", "2016-08-10", "2016-08-11", "2016-08-12", "2016-08-15", "2016-08-16", "2016-08-17", "2016-08-18", "2016-08-19", "2016-08-22", "2016-08-23", "2016-08-24", "2016-08-25", "2016-08-26", "2016-08-29", "2016-08-30", "2016-08-31", "2016-09-01", "2016-09-02", "2016-09-06", "2016-09-07", "2016-09-08", "2016-09-09", "2016-09-12", "2016-09-13", "2016-09-14", "2016-09-15", "2016-09-16", "2016-09-19", "2016-09-20", "2016-09-21", "2016-09-22", "2016-09-23", "2016-09-26", "2016-09-27", "2016-09-28", "2016-09-29", "2016-09-30", "2016-10-03", "2016-10-04", "2016-10-05", "2016-10-06", "2016-10-07", "2016-10-10", "2016-10-11", "2016-10-12", "2016-10-13", "2016-10-14", "2016-10-17", "2016-10-18", "2016-10-19", "2016-10-20", "2016-10-21", "2016-10-24", "2016-10-25", "2016-10-26", "2016-10-27", "2016-10-28", "2016-10-31", "2016-11-01", "2016-11-02", "2016-11-03", "2016-11-04", "2016-11-07", "2016-11-08", "2016-11-09", "2016-11-10", "2016-11-11", "2016-11-14", "2016-11-15", "2016-11-16", "2016-11-17", "2016-11-18", "2016-11-21", "2016-11-22", "2016-11-23", "2016-11-25", "2016-11-28", "2016-11-29", "2016-11-30", "2016-12-01", "2016-12-02", "2016-12-05", "2016-12-06", "2016-12-07", "2016-12-08", "2016-12-09", "2016-12-12", "2016-12-13", "2016-12-14", "2016-12-15", "2016-12-16", "2016-12-19", "2016-12-20", "2016-12-21", "2016-12-22", "2016-12-23", "2016-12-27", "2016-12-28", "2016-12-29", "2016-12-30", "2017-01-03", "2017-01-04", "2017-01-05", "2017-01-06", "2017-01-09", "2017-01-10", "2017-01-11", "2017-01-12", "2017-01-13", "2017-01-17", "2017-01-18", "2017-01-19", "2017-01-20", "2017-01-23", "2017-01-24", "2017-01-25", "2017-01-26", "2017-01-27", "2017-01-30", "2017-01-31", "2017-02-01", "2017-02-02", "2017-02-03", "2017-02-06", "2017-02-07", "2017-02-08", "2017-02-09", "2017-02-10", "2017-02-13", "2017-02-14", "2017-02-15", "2017-02-16", "2017-02-17", "2017-02-21", "2017-02-22", "2017-02-23", "2017-02-24", "2017-02-27", "2017-02-28", "2017-03-01", "2017-03-02", "2017-03-03", "2017-03-06", "2017-03-07", "2017-03-08", "2017-03-09", "2017-03-10", "2017-03-13", "2017-03-14", "2017-03-15", "2017-03-16", "2017-03-17", "2017-03-20", "2017-03-21", "2017-03-22", "2017-03-23", "2017-03-24", "2017-03-27", "2017-03-28", "2017-03-29", "2017-03-30", "2017-03-31", "2017-04-03", "2017-04-04", "2017-04-05", "2017-04-06", "2017-04-07", "2017-04-10", "2017-04-11", "2017-04-12", "2017-04-13", "2017-04-17", "2017-04-18", "2017-04-19", "2017-04-20", "2017-04-21", "2017-04-24", "2017-04-25", "2017-04-26", "2017-04-27", "2017-04-28", "2017-05-01", "2017-05-02", "2017-05-03", "2017-05-04", "2017-05-05", "2017-05-08", "2017-05-09", "2017-05-10", "2017-05-11", "2017-05-12", "2017-05-15", "2017-05-16", "2017-05-17", "2017-05-18", "2017-05-19", "2017-05-22", "2017-05-23", "2017-05-24", "2017-05-25", "2017-05-26", "2017-05-30", "2017-05-31", "2017-06-01", "2017-06-02", "2017-06-05", "2017-06-06", "2017-06-07", "2017-06-08", "2017-06-09", "2017-06-12", "2017-06-13", "2017-06-14", "2017-06-15", "2017-06-16", "2017-06-19", "2017-06-20", "2017-06-21", "2017-06-22", "2017-06-23", "2017-06-26", "2017-06-27", "2017-06-28", "2017-06-29", "2017-06-30"], "y": [null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 67.11504108603755, 68.49460046211992, 69.03670458967594, 69.03670458967594, 69.56193001728971, 69.66121648753807, 69.66121648753807, 70.44766984397894, 70.44766984397894, 70.44766984397894, 70.44766984397894, 70.44766984397894, 70.44766984397894, 70.44766984397894, 70.44766984397894, 70.44766984397894, 70.44766984397894, 70.44766984397894, 70.44766984397894, 70.44766984397894, 70.44766984397894, 70.44766984397894, 70.44766984397894, 70.44766984397894, 70.44766984397894, 70.44766984397894, 70.44766984397894, 70.4514732332015, 71.74712646944458, 73.36735003971611, 74.15576686041943, 74.42516023766305, 74.79440826949299, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.57571608004613, 75.14788770209884, 75.14788770209884, 75.14788770209884, 75.14788770209884, 75.14788770209884, 75.14788770209884, 75.14788770209884, 75.14788770209884, 75.14788770209884, 75.14788770209884, 75.14788770209884, 75.14788770209884, 75.14788770209884, 74.83514381748844, 74.1662924004015, 73.75499477064076, 73.75499477064076, 73.6130773776243, 73.6130773776243, 73.6130773776243, 73.6130773776243, 73.6130773776243, 73.6130773776243, 73.6130773776243, 73.6130773776243, 73.6130773776243, 73.6130773776243, 73.23068884644097, 73.23068884644097, 73.23068884644097, 73.23068884644097, 73.1268789015493, 73.01124250723956, 72.90349041254186, 72.86015155807074, 72.86015155807074, 72.86015155807074, 72.86015155807074, 72.86015155807074, 72.86015155807074, 72.86015155807074, 72.86015155807074, 72.86015155807074, 72.86015155807074, 72.86015155807074, 75.34658899490249, 75.60964112139347, 78.75040419949677, 78.78080720909121, 79.23685235300772, 79.23685235300772, 79.23685235300772, 79.4443859402393, 79.89513038552653, 79.89513038552653, 79.89513038552653, 79.89513038552653, 79.89513038552653, 79.89513038552653, 79.89513038552653, 79.89513038552653, 79.89513038552653, 80.730329313413, 80.730329313413, 80.730329313413, 81.06530441734297, 81.71389331599599, 83.19345974032677, 83.72117845564505, 84.6569819205923, 85.62734630896092, 85.62734630896092, 85.62734630896092, 86.12183336714328, 86.31855148472505, 86.56979610533539, 87.3540632137429, 88.44273230151535, 88.44273230151535, 88.44273230151535, 88.44273230151535, 88.44273230151535, 88.44273230151535, 88.44273230151535, 88.44273230151535, 88.44273230151535, 88.44273230151535, 88.44273230151535, 88.44273230151535, 88.44273230151535, 88.44273230151535, 88.44273230151535, 88.44273230151535, 88.44273230151535, 88.44273230151535, 89.31738951733256, 90.07108350117504, 90.07108350117504, 90.07108350117504, 90.07108350117504, 90.15482727715755, 90.15482727715755, 90.35022942111671, 90.35022942111671, 90.35022942111671, 90.35022942111671, 90.35022942111671, 91.07600881296499, 91.07600881296499, 91.07600881296499, 92.34147031670055, 92.52756759666164, 92.52756759666164, 92.52756759666164, 92.52756759666164, 92.52756759666164, 92.52756759666164, 92.52756759666164, 92.52756759666164, 92.52756759666164, 92.52756759666164, 92.52756759666164, 92.52756759666164, 92.52756759666164, 92.52756759666164, 92.9223969670482, 94.14739787302419, 94.53079510313879, 94.53079510313879, 94.88613887739142, 95.54071951417244, 95.54071951417244, 95.91476559233305, 96.11113978336736, 96.22335360681556, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.0088503709528, 97.35484299325138, 98.23478639212419, 98.64530196290545, 98.64530196290545, 99.81419595715737, 100.40331853026032, 100.40331853026032, 101.02984571117932, 103.14320605278674, 103.14320605278674, 103.14320605278674, 103.14320605278674, 103.14320605278674, 103.14320605278674, 103.14320605278674, 104.6504285099298, 106.54752862291605, 107.24250589202984, 110.1445055698157, 110.1445055698157, 110.1445055698157, 110.1445055698157, 110.41686152663056, 111.54385169276102, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.4642269951009, 112.69901661304472, 112.69901661304472, 112.69901661304472, 113.1779874336502, 113.3574948044156, 113.37635157806685, 113.37635157806685, 115.16774507493444, 117.77940822563083, 120.19307525298927, 120.19307525298927, 121.5130494085759, 121.5130494085759, 121.6544752109602, 122.09760939176428, 125.39754478073088, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 125.963247990268, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 126.84951635187618, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.889713196835, 125.84237555932394, 120.32280702553776, 120.32280702553776, 119.04469081273994, 117.31213327983622, 117.31213327983622, 116.92396465224577, 116.1121241689316, 116.1121241689316, 116.0434845945406, 114.11395594550548, 114.11395594550548, 114.11395594550548, 114.11395594550548, 114.11395594550548, 112.39259366313722, 111.88854835393549, 111.88854835393549, 113.38927193491728, 113.38927193491728, 113.38927193491728, 113.45774601465791, 114.7796761652059, 115.28372147440763, 115.41686551834772, 117.44255704400759, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.75639657615207, 117.18350784949509, 116.34300343261059, 116.34300343261059, 114.5378291736201, 114.5378291736201, 114.5378291736201, 114.5378291736201, 114.5378291736201, 114.5378291736201, 114.5378291736201, 114.5378291736201, 114.5378291736201, 114.48052205428705, 114.48052205428705, 114.48052205428705, 114.48052205428705, 114.48052205428705, 114.48052205428705, 114.48052205428705, 114.48052205428705, 114.48052205428705, 114.48052205428705, 113.27707254829338, 112.4079145717424, 111.6915755800795, 110.21114166397615, 107.73738434610027, 107.73738434610027, 107.21206908554748, 107.21206908554748, 104.60459515589451, 104.518634476895, 104.518634476895, 104.518634476895, 104.518634476895, 104.518634476895, 104.518634476895, 103.82139785834309, 102.2263497035737, 101.09930969002407, 102.08524921382595, 102.23889082679004, 102.26769862922082, 103.37199772240021, 103.37199772240021, 103.37199772240021, 103.37199772240021, 103.37199772240021, 103.50643413374378, 106.03191814684095, 106.03191814684095, 106.03191814684095, 107.7315784902562, 107.7315784902562, 107.7315784902562, 107.7315784902562, 107.7315784902562, 107.7315784902562, 107.7315784902562, 107.87561750241, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.9236305064613, 107.837207099169, 104.6203358277334, 103.79451215805143, 103.79451215805143, 102.6806104640618, 102.24849342760031, 101.4514775603491, 101.11538653199017, 98.43902613363967, 98.43902613363967, 98.43902613363967, 98.43902613363967, 98.43902613363967, 98.43902613363967, 98.43902613363967, 98.43902613363967, 98.43902613363967, 98.43902613363967, 98.43902613363967, 98.43902613363967, 98.43902613363967, 98.43902613363967, 100.81570690985671, 100.91231994954036, 101.00893298922395, 102.55474162416188, 102.55474162416188, 102.55474162416188, 102.96119259998018, 104.5638904093195, 105.26324945339485, 105.81690869662113, 105.81690869662113, 105.81690869662113, 105.81690869662113, 106.39970790001726, 107.06992698392281, 107.06992698392281, 107.06992698392281, 107.06992698392281, 107.06992698392281, 107.06992698392281, 107.06992698392281, 107.06992698392281, 107.06992698392281, 107.06992698392281, 107.06992698392281, 107.06992698392281, 107.06992698392281, 107.06992698392281, 107.06992698392281, 107.06992698392281, 107.06992698392281, 107.06992698392281, 107.06992698392281, 107.06992698392281, 109.78965659977129, 112.41225301505385, 112.8007858173179, 112.84935241760091, 112.84935241760091, 112.84935241760091, 112.84935241760091, 112.84935241760091, 112.84935241760091, 112.84935241760091, 112.84935241760091, 112.84935241760091, 112.84935241760091, 112.84935241760091, 112.84935241760091, 112.84935241760091, 112.84935241760091, 112.84935241760091, 113.40301166082723, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 115.28739575180799, 114.96685618994013, 114.96685618994013, 114.96685618994013, 115.01674673087, 115.22822913614937, 115.22822913614937, 115.22822913614937, 115.22822913614937, 115.22822913614937, 115.22822913614937, 115.36824103327335, 116.60823482230735, 116.60823482230735, 117.09642135342312, 117.09642135342312, 117.09642135342312, 117.39909700271488, 117.65295399889506, 117.65295399889506, 117.65295399889506, 117.9556296481868, 117.9556296481868, 119.21515089846544, 119.54711773962416, 119.54711773962416, 119.54711773962416, 119.54711773962416, 127.40692089058771, 127.40692089058771, 127.40692089058771, 127.41668462121001, 128.9691177901581, 129.09604628824815, 129.87236794231995, 130.35775298616042, 131.22065973076565, 132.4659910553664, 133.62307055381436, 133.62307055381436, 133.62307055381436, 134.09374695996266, 134.45656002303534, 134.80956732764656, 134.80956732764656, 134.80956732764656, 134.80956732764656, 137.42770483684657, 137.55380689066047, 137.55380689066047, 137.55380689066047, 137.55380689066047, 137.55380689066047, 137.55380689066047, 137.55380689066047, 137.55380689066047, 137.55380689066047, 138.01614840211658, 138.2808058229904, 138.2808058229904, 138.7514822291387, 140.02623082912373, 140.02623082912373, 140.02623082912373, 140.02623082912373, 140.02623082912373, 141.24214487834018, 141.68340400910432, 141.69320976756566, 141.69320976756566, 141.69320976756566, 142.07563434756116, 142.63456257986232, 142.63456257986232, 142.63456257986232, 142.63456257986232, 142.63456257986232, 142.63456257986232, 142.63456257986232, 142.63456257986232, 142.63456257986232, 142.63456257986232, 142.63456257986232, 142.63456257986232, 142.63456257986232, 142.63456257986232, 142.63456257986232, 142.63456257986232, 142.63456257986232, 144.3407645521499, 145.2134770552166, 145.2134770552166, 145.2134770552166, 146.08618955828325, 150.71450755207502, 151.87158705052298, 151.87158705052298, 151.87158705052298, 154.00934812787742, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146, 154.23580350487146], "name": "Column lookback_high", "line": {"color": "#2D3ECF"}}, {"type": "scatter", "x": ["2013-07-01", "2013-07-02", "2013-07-03", "2013-07-05", "2013-07-08", "2013-07-09", "2013-07-10", "2013-07-11", "2013-07-12", "2013-07-15", "2013-07-16", "2013-07-17", "2013-07-18", "2013-07-19", "2013-07-22", "2013-07-23", "2013-07-24", "2013-07-25", "2013-07-26", "2013-07-29", "2013-07-30", "2013-07-31", "2013-08-01", "2013-08-02", "2013-08-05", "2013-08-06", "2013-08-07", "2013-08-08", "2013-08-09", "2013-08-12", "2013-08-13", "2013-08-14", "2013-08-15", "2013-08-16", "2013-08-19", "2013-08-20", "2013-08-21", "2013-08-22", "2013-08-23", "2013-08-26", "2013-08-27", "2013-08-28", "2013-08-29", "2013-08-30", "2013-09-03", "2013-09-04", "2013-09-05", "2013-09-06", "2013-09-09", "2013-09-10", "2013-09-11", "2013-09-12", "2013-09-13", "2013-09-16", "2013-09-17", "2013-09-18", "2013-09-19", "2013-09-20", "2013-09-23", "2013-09-24", "2013-09-25", "2013-09-26", "2013-09-27", "2013-09-30", "2013-10-01", "2013-10-02", "2013-10-03", "2013-10-04", "2013-10-07", "2013-10-08", "2013-10-09", "2013-10-10", "2013-10-11", "2013-10-14", "2013-10-15", "2013-10-16", "2013-10-17", "2013-10-18", "2013-10-21", "2013-10-22", "2013-10-23", "2013-10-24", "2013-10-25", "2013-10-28", "2013-10-29", "2013-10-30", "2013-10-31", "2013-11-01", "2013-11-04", "2013-11-05", "2013-11-06", "2013-11-07", "2013-11-08", "2013-11-11", "2013-11-12", "2013-11-13", "2013-11-14", "2013-11-15", "2013-11-18", "2013-11-19", "2013-11-20", "2013-11-21", "2013-11-22", "2013-11-25", "2013-11-26", "2013-11-27", "2013-11-29", "2013-12-02", "2013-12-03", "2013-12-04", "2013-12-05", "2013-12-06", "2013-12-09", "2013-12-10", "2013-12-11", "2013-12-12", "2013-12-13", "2013-12-16", "2013-12-17", "2013-12-18", "2013-12-19", "2013-12-20", "2013-12-23", "2013-12-24", "2013-12-26", "2013-12-27", "2013-12-30", "2013-12-31", "2014-01-02", "2014-01-03", "2014-01-06", "2014-01-07", "2014-01-08", "2014-01-09", "2014-01-10", "2014-01-13", "2014-01-14", "2014-01-15", "2014-01-16", "2014-01-17", "2014-01-21", "2014-01-22", "2014-01-23", "2014-01-24", "2014-01-27", "2014-01-28", "2014-01-29", "2014-01-30", "2014-01-31", "2014-02-03", "2014-02-04", "2014-02-05", "2014-02-06", "2014-02-07", "2014-02-10", "2014-02-11", "2014-02-12", "2014-02-13", "2014-02-14", "2014-02-18", "2014-02-19", "2014-02-20", "2014-02-21", "2014-02-24", "2014-02-25", "2014-02-26", "2014-02-27", "2014-02-28", "2014-03-03", "2014-03-04", "2014-03-05", "2014-03-06", "2014-03-07", "2014-03-10", "2014-03-11", "2014-03-12", "2014-03-13", "2014-03-14", "2014-03-17", "2014-03-18", "2014-03-19", "2014-03-20", "2014-03-21", "2014-03-24", "2014-03-25", "2014-03-26", "2014-03-27", "2014-03-28", "2014-03-31", "2014-04-01", "2014-04-02", "2014-04-03", "2014-04-04", "2014-04-07", "2014-04-08", "2014-04-09", "2014-04-10", "2014-04-11", "2014-04-14", "2014-04-15", "2014-04-16", "2014-04-17", "2014-04-21", "2014-04-22", "2014-04-23", "2014-04-24", "2014-04-25", "2014-04-28", "2014-04-29", "2014-04-30", "2014-05-01", "2014-05-02", "2014-05-05", "2014-05-06", "2014-05-07", "2014-05-08", "2014-05-09", "2014-05-12", "2014-05-13", "2014-05-14", "2014-05-15", "2014-05-16", "2014-05-19", "2014-05-20", "2014-05-21", "2014-05-22", "2014-05-23", "2014-05-27", "2014-05-28", "2014-05-29", "2014-05-30", "2014-06-02", "2014-06-03", "2014-06-04", "2014-06-05", "2014-06-06", "2014-06-09", "2014-06-10", "2014-06-11", "2014-06-12", "2014-06-13", "2014-06-16", "2014-06-17", "2014-06-18", "2014-06-19", "2014-06-20", "2014-06-23", "2014-06-24", "2014-06-25", "2014-06-26", "2014-06-27", "2014-06-30", "2014-07-01", "2014-07-02", "2014-07-03", "2014-07-07", "2014-07-08", "2014-07-09", "2014-07-10", "2014-07-11", "2014-07-14", "2014-07-15", "2014-07-16", "2014-07-17", "2014-07-18", "2014-07-21", "2014-07-22", "2014-07-23", "2014-07-24", "2014-07-25", "2014-07-28", "2014-07-29", "2014-07-30", "2014-07-31", "2014-08-01", "2014-08-04", "2014-08-05", "2014-08-06", "2014-08-07", "2014-08-08", "2014-08-11", "2014-08-12", "2014-08-13", "2014-08-14", "2014-08-15", "2014-08-18", "2014-08-19", "2014-08-20", "2014-08-21", "2014-08-22", "2014-08-25", "2014-08-26", "2014-08-27", "2014-08-28", "2014-08-29", "2014-09-02", "2014-09-03", "2014-09-04", "2014-09-05", "2014-09-08", "2014-09-09", "2014-09-10", "2014-09-11", "2014-09-12", "2014-09-15", "2014-09-16", "2014-09-17", "2014-09-18", "2014-09-19", "2014-09-22", "2014-09-23", "2014-09-24", "2014-09-25", "2014-09-26", "2014-09-29", "2014-09-30", "2014-10-01", "2014-10-02", "2014-10-03", "2014-10-06", "2014-10-07", "2014-10-08", "2014-10-09", "2014-10-10", "2014-10-13", "2014-10-14", "2014-10-15", "2014-10-16", "2014-10-17", "2014-10-20", "2014-10-21", "2014-10-22", "2014-10-23", "2014-10-24", "2014-10-27", "2014-10-28", "2014-10-29", "2014-10-30", "2014-10-31", "2014-11-03", "2014-11-04", "2014-11-05", "2014-11-06", "2014-11-07", "2014-11-10", "2014-11-11", "2014-11-12", "2014-11-13", "2014-11-14", "2014-11-17", "2014-11-18", "2014-11-19", "2014-11-20", "2014-11-21", "2014-11-24", "2014-11-25", "2014-11-26", "2014-11-28", "2014-12-01", "2014-12-02", "2014-12-03", "2014-12-04", "2014-12-05", "2014-12-08", "2014-12-09", "2014-12-10", "2014-12-11", "2014-12-12", "2014-12-15", "2014-12-16", "2014-12-17", "2014-12-18", "2014-12-19", "2014-12-22", "2014-12-23", "2014-12-24", "2014-12-26", "2014-12-29", "2014-12-30", "2014-12-31", "2015-01-02", "2015-01-05", "2015-01-06", "2015-01-07", "2015-01-08", "2015-01-09", "2015-01-12", "2015-01-13", "2015-01-14", "2015-01-15", "2015-01-16", "2015-01-20", "2015-01-21", "2015-01-22", "2015-01-23", "2015-01-26", "2015-01-27", "2015-01-28", "2015-01-29", "2015-01-30", "2015-02-02", "2015-02-03", "2015-02-04", "2015-02-05", "2015-02-06", "2015-02-09", "2015-02-10", "2015-02-11", "2015-02-12", "2015-02-13", "2015-02-17", "2015-02-18", "2015-02-19", "2015-02-20", "2015-02-23", "2015-02-24", "2015-02-25", "2015-02-26", "2015-02-27", "2015-03-02", "2015-03-03", "2015-03-04", "2015-03-05", "2015-03-06", "2015-03-09", "2015-03-10", "2015-03-11", "2015-03-12", "2015-03-13", "2015-03-16", "2015-03-17", "2015-03-18", "2015-03-19", "2015-03-20", "2015-03-23", "2015-03-24", "2015-03-25", "2015-03-26", "2015-03-27", "2015-03-30", "2015-03-31", "2015-04-01", "2015-04-02", "2015-04-06", "2015-04-07", "2015-04-08", "2015-04-09", "2015-04-10", "2015-04-13", "2015-04-14", "2015-04-15", "2015-04-16", "2015-04-17", "2015-04-20", "2015-04-21", "2015-04-22", "2015-04-23", "2015-04-24", "2015-04-27", "2015-04-28", "2015-04-29", "2015-04-30", "2015-05-01", "2015-05-04", "2015-05-05", "2015-05-06", "2015-05-07", "2015-05-08", "2015-05-11", "2015-05-12", "2015-05-13", "2015-05-14", "2015-05-15", "2015-05-18", "2015-05-19", "2015-05-20", "2015-05-21", "2015-05-22", "2015-05-26", "2015-05-27", "2015-05-28", "2015-05-29", "2015-06-01", "2015-06-02", "2015-06-03", "2015-06-04", "2015-06-05", "2015-06-08", "2015-06-09", "2015-06-10", "2015-06-11", "2015-06-12", "2015-06-15", "2015-06-16", "2015-06-17", "2015-06-18", "2015-06-19", "2015-06-22", "2015-06-23", "2015-06-24", "2015-06-25", "2015-06-26", "2015-06-29", "2015-06-30", "2015-07-01", "2015-07-02", "2015-07-06", "2015-07-07", "2015-07-08", "2015-07-09", "2015-07-10", "2015-07-13", "2015-07-14", "2015-07-15", "2015-07-16", "2015-07-17", "2015-07-20", "2015-07-21", "2015-07-22", "2015-07-23", "2015-07-24", "2015-07-27", "2015-07-28", "2015-07-29", "2015-07-30", "2015-07-31", "2015-08-03", "2015-08-04", "2015-08-05", "2015-08-06", "2015-08-07", "2015-08-10", "2015-08-11", "2015-08-12", "2015-08-13", "2015-08-14", "2015-08-17", "2015-08-18", "2015-08-19", "2015-08-20", "2015-08-21", "2015-08-24", "2015-08-25", "2015-08-26", "2015-08-27", "2015-08-28", "2015-08-31", "2015-09-01", "2015-09-02", "2015-09-03", "2015-09-04", "2015-09-08", "2015-09-09", "2015-09-10", "2015-09-11", "2015-09-14", "2015-09-15", "2015-09-16", "2015-09-17", "2015-09-18", "2015-09-21", "2015-09-22", "2015-09-23", "2015-09-24", "2015-09-25", "2015-09-28", "2015-09-29", "2015-09-30", "2015-10-01", "2015-10-02", "2015-10-05", "2015-10-06", "2015-10-07", "2015-10-08", "2015-10-09", "2015-10-12", "2015-10-13", "2015-10-14", "2015-10-15", "2015-10-16", "2015-10-19", "2015-10-20", "2015-10-21", "2015-10-22", "2015-10-23", "2015-10-26", "2015-10-27", "2015-10-28", "2015-10-29", "2015-10-30", "2015-11-02", "2015-11-03", "2015-11-04", "2015-11-05", "2015-11-06", "2015-11-09", "2015-11-10", "2015-11-11", "2015-11-12", "2015-11-13", "2015-11-16", "2015-11-17", "2015-11-18", "2015-11-19", "2015-11-20", "2015-11-23", "2015-11-24", "2015-11-25", "2015-11-27", "2015-11-30", "2015-12-01", "2015-12-02", "2015-12-03", "2015-12-04", "2015-12-07", "2015-12-08", "2015-12-09", "2015-12-10", "2015-12-11", "2015-12-14", "2015-12-15", "2015-12-16", "2015-12-17", "2015-12-18", "2015-12-21", "2015-12-22", "2015-12-23", "2015-12-24", "2015-12-28", "2015-12-29", "2015-12-30", "2015-12-31", "2016-01-04", "2016-01-05", "2016-01-06", "2016-01-07", "2016-01-08", "2016-01-11", "2016-01-12", "2016-01-13", "2016-01-14", "2016-01-15", "2016-01-19", "2016-01-20", "2016-01-21", "2016-01-22", "2016-01-25", "2016-01-26", "2016-01-27", "2016-01-28", "2016-01-29", "2016-02-01", "2016-02-02", "2016-02-03", "2016-02-04", "2016-02-05", "2016-02-08", "2016-02-09", "2016-02-10", "2016-02-11", "2016-02-12", "2016-02-16", "2016-02-17", "2016-02-18", "2016-02-19", "2016-02-22", "2016-02-23", "2016-02-24", "2016-02-25", "2016-02-26", "2016-02-29", "2016-03-01", "2016-03-02", "2016-03-03", "2016-03-04", "2016-03-07", "2016-03-08", "2016-03-09", "2016-03-10", "2016-03-11", "2016-03-14", "2016-03-15", "2016-03-16", "2016-03-17", "2016-03-18", "2016-03-21", "2016-03-22", "2016-03-23", "2016-03-24", "2016-03-28", "2016-03-29", "2016-03-30", "2016-03-31", "2016-04-01", "2016-04-04", "2016-04-05", "2016-04-06", "2016-04-07", "2016-04-08", "2016-04-11", "2016-04-12", "2016-04-13", "2016-04-14", "2016-04-15", "2016-04-18", "2016-04-19", "2016-04-20", "2016-04-21", "2016-04-22", "2016-04-25", "2016-04-26", "2016-04-27", "2016-04-28", "2016-04-29", "2016-05-02", "2016-05-03", "2016-05-04", "2016-05-05", "2016-05-06", "2016-05-09", "2016-05-10", "2016-05-11", "2016-05-12", "2016-05-13", "2016-05-16", "2016-05-17", "2016-05-18", "2016-05-19", "2016-05-20", "2016-05-23", "2016-05-24", "2016-05-25", "2016-05-26", "2016-05-27", "2016-05-31", "2016-06-01", "2016-06-02", "2016-06-03", "2016-06-06", "2016-06-07", "2016-06-08", "2016-06-09", "2016-06-10", "2016-06-13", "2016-06-14", "2016-06-15", "2016-06-16", "2016-06-17", "2016-06-20", "2016-06-21", "2016-06-22", "2016-06-23", "2016-06-24", "2016-06-27", "2016-06-28", "2016-06-29", "2016-06-30", "2016-07-01", "2016-07-05", "2016-07-06", "2016-07-07", "2016-07-08", "2016-07-11", "2016-07-12", "2016-07-13", "2016-07-14", "2016-07-15", "2016-07-18", "2016-07-19", "2016-07-20", "2016-07-21", "2016-07-22", "2016-07-25", "2016-07-26", "2016-07-27", "2016-07-28", "2016-07-29", "2016-08-01", "2016-08-02", "2016-08-03", "2016-08-04", "2016-08-05", "2016-08-08", "2016-08-09", "2016-08-10", "2016-08-11", "2016-08-12", "2016-08-15", "2016-08-16", "2016-08-17", "2016-08-18", "2016-08-19", "2016-08-22", "2016-08-23", "2016-08-24", "2016-08-25", "2016-08-26", "2016-08-29", "2016-08-30", "2016-08-31", "2016-09-01", "2016-09-02", "2016-09-06", "2016-09-07", "2016-09-08", "2016-09-09", "2016-09-12", "2016-09-13", "2016-09-14", "2016-09-15", "2016-09-16", "2016-09-19", "2016-09-20", "2016-09-21", "2016-09-22", "2016-09-23", "2016-09-26", "2016-09-27", "2016-09-28", "2016-09-29", "2016-09-30", "2016-10-03", "2016-10-04", "2016-10-05", "2016-10-06", "2016-10-07", "2016-10-10", "2016-10-11", "2016-10-12", "2016-10-13", "2016-10-14", "2016-10-17", "2016-10-18", "2016-10-19", "2016-10-20", "2016-10-21", "2016-10-24", "2016-10-25", "2016-10-26", "2016-10-27", "2016-10-28", "2016-10-31", "2016-11-01", "2016-11-02", "2016-11-03", "2016-11-04", "2016-11-07", "2016-11-08", "2016-11-09", "2016-11-10", "2016-11-11", "2016-11-14", "2016-11-15", "2016-11-16", "2016-11-17", "2016-11-18", "2016-11-21", "2016-11-22", "2016-11-23", "2016-11-25", "2016-11-28", "2016-11-29", "2016-11-30", "2016-12-01", "2016-12-02", "2016-12-05", "2016-12-06", "2016-12-07", "2016-12-08", "2016-12-09", "2016-12-12", "2016-12-13", "2016-12-14", "2016-12-15", "2016-12-16", "2016-12-19", "2016-12-20", "2016-12-21", "2016-12-22", "2016-12-23", "2016-12-27", "2016-12-28", "2016-12-29", "2016-12-30", "2017-01-03", "2017-01-04", "2017-01-05", "2017-01-06", "2017-01-09", "2017-01-10", "2017-01-11", "2017-01-12", "2017-01-13", "2017-01-17", "2017-01-18", "2017-01-19", "2017-01-20", "2017-01-23", "2017-01-24", "2017-01-25", "2017-01-26", "2017-01-27", "2017-01-30", "2017-01-31", "2017-02-01", "2017-02-02", "2017-02-03", "2017-02-06", "2017-02-07", "2017-02-08", "2017-02-09", "2017-02-10", "2017-02-13", "2017-02-14", "2017-02-15", "2017-02-16", "2017-02-17", "2017-02-21", "2017-02-22", "2017-02-23", "2017-02-24", "2017-02-27", "2017-02-28", "2017-03-01", "2017-03-02", "2017-03-03", "2017-03-06", "2017-03-07", "2017-03-08", "2017-03-09", "2017-03-10", "2017-03-13", "2017-03-14", "2017-03-15", "2017-03-16", "2017-03-17", "2017-03-20", "2017-03-21", "2017-03-22", "2017-03-23", "2017-03-24", "2017-03-27", "2017-03-28", "2017-03-29", "2017-03-30", "2017-03-31", "2017-04-03", "2017-04-04", "2017-04-05", "2017-04-06", "2017-04-07", "2017-04-10", "2017-04-11", "2017-04-12", "2017-04-13", "2017-04-17", "2017-04-18", "2017-04-19", "2017-04-20", "2017-04-21", "2017-04-24", "2017-04-25", "2017-04-26", "2017-04-27", "2017-04-28", "2017-05-01", "2017-05-02", "2017-05-03", "2017-05-04", "2017-05-05", "2017-05-08", "2017-05-09", "2017-05-10", "2017-05-11", "2017-05-12", "2017-05-15", "2017-05-16", "2017-05-17", "2017-05-18", "2017-05-19", "2017-05-22", "2017-05-23", "2017-05-24", "2017-05-25", "2017-05-26", "2017-05-30", "2017-05-31", "2017-06-01", "2017-06-02", "2017-06-05", "2017-06-06", "2017-06-07", "2017-06-08", "2017-06-09", "2017-06-12", "2017-06-13", "2017-06-14", "2017-06-15", "2017-06-16", "2017-06-19", "2017-06-20", "2017-06-21", "2017-06-22", "2017-06-23", "2017-06-26", "2017-06-27", "2017-06-28", "2017-06-29", "2017-06-30"], "y": [null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, 52.07092143135186, 53.14161855963223, 53.259719697418305, 53.259719697418305, 53.259719697418305, 53.259719697418305, 54.28109986706274, 54.340799343306244, 54.340799343306244, 54.340799343306244, 54.340799343306244, 54.340799343306244, 54.340799343306244, 54.340799343306244, 54.340799343306244, 54.340799343306244, 56.3692837208847, 56.3692837208847, 56.3692837208847, 57.12980313563901, 58.30172981059317, 58.32768610461209, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.42486213745809, 58.46144136333906, 60.18066497974474, 60.87828307333184, 60.87828307333184, 61.97709689077775, 61.97709689077775, 61.97709689077775, 61.97709689077775, 61.97709689077775, 61.97709689077775, 62.48254340839732, 62.48254340839732, 62.48254340839732, 62.48254340839732, 62.48254340839732, 62.48254340839732, 62.48254340839732, 63.381347244329774, 63.381347244329774, 63.92872923162003, 64.73477860192574, 65.21945334484862, 65.27824138644304, 66.06600114380825, 66.3690861582506, 66.3690861582506, 67.21955315998318, 67.21955315998318, 67.21955315998318, 67.21955315998318, 67.21955315998318, 67.32929058683887, 67.32929058683887, 67.32929058683887, 67.32929058683887, 67.32929058683887, 67.32929058683887, 67.32929058683887, 67.35688563548096, 67.49880302849743, 67.49880302849743, 67.49880302849743, 65.97450510350558, 65.52115787581403, 65.26886028822916, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 64.85493455859776, 65.61051327141699, 66.06517454904389, 66.5240276459645, 67.12587957456392, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.591177808357, 67.96201521321018, 68.63148948447962, 69.26069959608617, 69.32547122522213, 69.32547122522213, 74.12121552124856, 74.54817952555301, 75.683665840406, 77.14131034273453, 77.14131034273453, 77.14131034273453, 77.14131034273453, 77.14131034273453, 77.14131034273453, 77.14131034273453, 77.14131034273453, 77.14131034273453, 77.81524834945081, 77.81524834945081, 77.81524834945081, 77.81524834945081, 77.81524834945081, 79.40106302797652, 79.85301356502492, 80.02980598098794, 80.30097630321703, 80.61601241286546, 81.83362033032525, 82.74682626842011, 82.74682626842011, 82.74682626842011, 82.74682626842011, 83.41810574256553, 83.41810574256553, 83.41810574256553, 83.41810574256553, 83.41810574256553, 83.41810574256553, 83.41810574256553, 83.41810574256553, 83.41810574256553, 83.41810574256553, 83.41810574256553, 83.41810574256553, 83.41810574256553, 83.41810574256553, 83.41810574256553, 83.41810574256553, 83.41810574256553, 83.55767870253635, 84.46025051034772, 85.68849255809101, 86.13512602999765, 86.13512602999765, 86.13512602999765, 86.13512602999765, 86.13512602999765, 86.13512602999765, 86.13512602999765, 86.13512602999765, 86.13512602999765, 86.13512602999765, 86.13512602999765, 86.13512602999765, 86.55384490991017, 87.20518538977403, 87.22754542705302, 87.22754542705302, 87.22754542705302, 87.22754542705302, 87.22754542705302, 87.22754542705302, 87.22754542705302, 87.22754542705302, 87.22754542705302, 87.22754542705302, 87.22754542705302, 87.22754542705302, 87.22754542705302, 87.22754542705302, 88.68211711350006, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.00426429831589, 89.21934079325823, 90.52850206682035, 91.84701449233648, 94.69911583831109, 95.94281904819508, 96.90598769945863, 97.74759137532, 97.90656095853828, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.26415090185725, 98.79947123076923, 98.79947123076923, 98.79947123076923, 98.79947123076923, 98.79947123076923, 98.79947123076923, 98.79947123076923, 98.79947123076923, 100.02037724407721, 101.68268773911959, 102.39644817766892, 102.39644817766892, 102.39644817766892, 102.39644817766892, 108.29436338041825, 108.52915299836208, 109.01751540368528, 109.01751540368528, 110.4544278655016, 111.11089963727258, 111.6603851758042, 111.6603851758042, 111.6603851758042, 113.29149609663624, 114.67746896000223, 114.67746896000223, 114.67746896000223, 114.67746896000223, 114.67746896000223, 114.67746896000223, 114.67746896000223, 114.67746896000223, 114.67746896000223, 114.67746896000223, 114.67746896000223, 114.67746896000223, 114.67746896000223, 114.67746896000223, 114.67746896000223, 114.67746896000223, 114.67746896000223, 114.67746896000223, 114.67746896000223, 114.67746896000223, 114.67746896000223, 115.573165708436, 115.59202248208729, 115.59202248208729, 115.59202248208729, 115.59202248208729, 115.59202248208729, 115.59202248208729, 115.59202248208729, 115.59202248208729, 115.59202248208729, 115.88430247368143, 116.06344182336821, 116.06344182336821, 116.06344182336821, 116.30857988083427, 116.30857988083427, 116.30857988083427, 116.30857988083427, 116.30857988083427, 116.30857988083427, 116.30857988083427, 116.30857988083427, 116.30857988083427, 116.30857988083427, 116.30857988083427, 116.30857988083427, 116.30857988083427, 116.30857988083427, 116.30857988083427, 116.30857988083427, 116.30857988083427, 116.015082012034, 112.87186288130155, 112.87186288130155, 112.87186288130155, 112.87186288130155, 112.87186288130155, 112.87186288130155, 112.87186288130155, 112.87186288130155, 112.87186288130155, 112.87186288130155, 112.87186288130155, 112.87186288130155, 112.87186288130155, 112.87186288130155, 112.87186288130155, 112.87186288130155, 112.87186288130155, 111.2623832059265, 107.21974896248449, 106.13098329973076, 106.13098329973076, 106.13098329973076, 106.13098329973076, 106.13098329973076, 104.26129669393923, 104.26129669393923, 104.26129669393923, 104.26129669393923, 104.26129669393923, 104.26129669393923, 104.26129669393923, 100.47144658607321, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 87.4946574463414, 98.43148962713407, 99.90558439932785, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.05490968007494, 102.28315661254364, 102.91083567683262, 102.91083567683262, 102.91083567683262, 102.91083567683262, 101.06110494380205, 100.83187646646992, 100.83187646646992, 100.83187646646992, 100.83187646646992, 100.83187646646992, 100.83187646646992, 100.83187646646992, 100.115537474807, 97.42210286615452, 97.42210286615452, 95.38770012983187, 92.10209195473804, 92.10209195473804, 92.10209195473804, 92.10209195473804, 92.10209195473804, 91.44306008240817, 91.08011499329895, 91.08011499329895, 89.22718480153091, 89.22718480153091, 89.22718480153091, 89.22718480153091, 89.22718480153091, 89.15077530908688, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.24341258631388, 88.91048090215546, 88.91048090215546, 88.91048090215546, 88.91048090215546, 88.91048090215546, 88.91048090215546, 88.91048090215546, 88.91048090215546, 88.91048090215546, 88.91048090215546, 89.31379013618619, 89.61147076130409, 89.61147076130409, 89.61147076130409, 88.83366009567341, 88.7280314867606, 88.7280314867606, 88.7280314867606, 88.7280314867606, 88.7280314867606, 88.7280314867606, 88.7280314867606, 88.7280314867606, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.4396866049342, 86.95173571525736, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 88.40093131051167, 89.01925476448679, 90.45878905577273, 91.10609642165298, 91.17372554943151, 91.17372554943151, 91.17372554943151, 92.38138854547677, 92.79682461611631, 93.15429286294571, 93.15429286294571, 93.15429286294571, 93.15429286294571, 93.15429286294571, 93.15429286294571, 93.15429286294571, 93.15429286294571, 93.15429286294571, 93.15429286294571, 93.15429286294571, 93.15429286294571, 99.2698982749188, 99.33752740269735, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 99.59067054033932, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 101.62090831705393, 103.65108082535187, 104.08136843387727, 105.69238398655924, 105.69238398655924, 105.69238398655924, 105.69238398655924, 105.69238398655924, 105.69238398655924, 105.69238398655924, 105.69238398655924, 105.69238398655924, 105.69238398655924, 105.69238398655924, 105.69238398655924, 106.58088347318993, 106.58088347318993, 107.98686068280323, 109.65645861921914, 109.8322057704208, 111.06243582883243, 112.04857262168629, 112.04857262168629, 112.04857262168629, 112.04857262168629, 112.04857262168629, 112.04857262168629, 112.04857262168629, 112.04857262168629, 112.04857262168629, 112.04857262168629, 112.04857262168629, 112.04857262168629, 112.04857262168629, 113.01518195329544, 113.07376433702936, 113.71817055810213, 115.15343895958245, 115.41705968638493, 115.41705968638493, 115.41705968638493, 115.42682341700724, 115.42682341700724, 116.54965243857347, 116.54965243857347, 116.67658093666357, 116.67658093666357, 116.67658093666357, 117.43815192520412, 117.77011876636284, 117.77011876636284, 117.77011876636284, 117.77011876636284, 124.00914263402208, 124.76094989194031, 125.1319716555883, 125.8544877216396, 127.36786596809841, 128.11967322601666, 128.57310494618142, 129.48504048309377, 130.17144357539334, 130.66173149846458, 132.00512040767953, 132.22065097866158, 132.47579681382783, 132.65230046613345, 132.65230046613345, 132.65230046613345, 132.65230046613345, 133.63287631227578, 134.0447181676555, 134.38791971380536, 134.38791971380536, 134.38791971380536, 134.38791971380536, 134.38791971380536, 134.38791971380536, 134.38791971380536, 135.92742379224882, 135.92742379224882, 135.92742379224882, 135.92742379224882, 135.92742379224882, 135.92742379224882, 135.92742379224882, 135.92742379224882, 135.92742379224882, 135.92742379224882, 135.92742379224882, 135.92742379224882, 137.33945301069377, 137.33945301069377, 137.33945301069377, 137.33945301069377, 137.33945301069377, 137.33945301069377, 137.33945301069377, 137.33945301069377, 137.33945301069377, 137.33945301069377, 137.33945301069377, 137.72187759068925, 137.72187759068925, 137.72187759068925, 137.72187759068925, 137.72187759068925, 138.4180864414503], "name": "Column lookback_low", "line": {"color": "#B6B2CF"}}], {"title": "High and Low of AAPL Stock"}, {"showLink": false, "linkText": "Export to plot.ly", "displayModeBar": false})});</script>


## Compute Long and Short Signals
Using the generated indicator of highs and lows, create long and short signals using a breakout strategy. Implement `get_long_short` to generate the following signals:

| Signal | Condition |
|----|------|
| -1 | Low > Close Price |
| 1  | High < Close Price |
| 0  | Otherwise |

In this chart, **Close Price** is the `close` parameter. **Low** and **High** are the values generated from `get_high_lows_lookback`, the `lookback_high` and `lookback_low` parameters.


```python
def get_long_short(close, lookback_high, lookback_low):
    """
    Generate the signals long, short, and do nothing.
    
    Parameters
    ----------
    close : DataFrame
        Close price for each ticker and date
    lookback_high : DataFrame
        Lookback high price for each ticker and date
    lookback_low : DataFrame
        Lookback low price for each ticker and date
    
    Returns
    -------
    long_short : DataFrame
        The long, short, and do nothing signals for each ticker and date
    """
    long_short = pd.DataFrame(0,columns=close.columns,index=close.index)
    long_short[(lookback_high<close)] = 1
    long_short[(lookback_low>close)] = -1
    #TODO: Implement function
    
    return long_short

project_tests.test_get_long_short(get_long_short)
```

    Tests Passed


### View Data
Let's compare the signals you generated against the close prices. This chart will show a lot of signals. Too many in fact. We'll talk about filtering the redundant signals in the next problem. 


```python
signal = get_long_short(close, lookback_high, lookback_low)
project_helper.plot_signal(
    close[apple_ticker],
    signal[apple_ticker],
    'Long and Short of {} Stock'.format(apple_ticker))
```


<div id="75a6edcf-12c4-404f-8d24-7b2d149b4fae" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("75a6edcf-12c4-404f-8d24-7b2d149b4fae", [{"type": "scatter", "name": "Index", "x": ["2013-07-01", "2013-07-02", "2013-07-03", "2013-07-05", "2013-07-08", "2013-07-09", "2013-07-10", "2013-07-11", "2013-07-12", "2013-07-15", "2013-07-16", "2013-07-17", "2013-07-18", "2013-07-19", "2013-07-22", "2013-07-23", "2013-07-24", "2013-07-25", "2013-07-26", "2013-07-29", "2013-07-30", "2013-07-31", "2013-08-01", "2013-08-02", "2013-08-05", "2013-08-06", "2013-08-07", "2013-08-08", "2013-08-09", "2013-08-12", "2013-08-13", "2013-08-14", "2013-08-15", "2013-08-16", "2013-08-19", "2013-08-20", "2013-08-21", "2013-08-22", "2013-08-23", "2013-08-26", "2013-08-27", "2013-08-28", "2013-08-29", "2013-08-30", "2013-09-03", "2013-09-04", "2013-09-05", "2013-09-06", "2013-09-09", "2013-09-10", "2013-09-11", "2013-09-12", "2013-09-13", "2013-09-16", "2013-09-17", "2013-09-18", "2013-09-19", "2013-09-20", "2013-09-23", "2013-09-24", "2013-09-25", "2013-09-26", "2013-09-27", "2013-09-30", "2013-10-01", "2013-10-02", "2013-10-03", "2013-10-04", "2013-10-07", "2013-10-08", "2013-10-09", "2013-10-10", "2013-10-11", "2013-10-14", "2013-10-15", "2013-10-16", "2013-10-17", "2013-10-18", "2013-10-21", "2013-10-22", "2013-10-23", "2013-10-24", "2013-10-25", "2013-10-28", "2013-10-29", "2013-10-30", "2013-10-31", "2013-11-01", "2013-11-04", "2013-11-05", "2013-11-06", "2013-11-07", "2013-11-08", "2013-11-11", "2013-11-12", "2013-11-13", "2013-11-14", "2013-11-15", "2013-11-18", "2013-11-19", "2013-11-20", "2013-11-21", "2013-11-22", "2013-11-25", "2013-11-26", "2013-11-27", "2013-11-29", "2013-12-02", "2013-12-03", "2013-12-04", "2013-12-05", "2013-12-06", "2013-12-09", "2013-12-10", "2013-12-11", "2013-12-12", "2013-12-13", "2013-12-16", "2013-12-17", "2013-12-18", "2013-12-19", "2013-12-20", "2013-12-23", "2013-12-24", "2013-12-26", "2013-12-27", "2013-12-30", "2013-12-31", "2014-01-02", "2014-01-03", "2014-01-06", "2014-01-07", "2014-01-08", "2014-01-09", "2014-01-10", "2014-01-13", "2014-01-14", "2014-01-15", "2014-01-16", "2014-01-17", "2014-01-21", "2014-01-22", "2014-01-23", "2014-01-24", "2014-01-27", "2014-01-28", "2014-01-29", "2014-01-30", "2014-01-31", "2014-02-03", "2014-02-04", "2014-02-05", "2014-02-06", "2014-02-07", "2014-02-10", "2014-02-11", "2014-02-12", "2014-02-13", "2014-02-14", "2014-02-18", "2014-02-19", "2014-02-20", "2014-02-21", "2014-02-24", "2014-02-25", "2014-02-26", "2014-02-27", "2014-02-28", "2014-03-03", "2014-03-04", "2014-03-05", "2014-03-06", "2014-03-07", "2014-03-10", "2014-03-11", "2014-03-12", "2014-03-13", "2014-03-14", "2014-03-17", "2014-03-18", "2014-03-19", "2014-03-20", "2014-03-21", "2014-03-24", "2014-03-25", "2014-03-26", "2014-03-27", "2014-03-28", "2014-03-31", "2014-04-01", "2014-04-02", "2014-04-03", "2014-04-04", "2014-04-07", "2014-04-08", "2014-04-09", "2014-04-10", "2014-04-11", "2014-04-14", "2014-04-15", "2014-04-16", "2014-04-17", "2014-04-21", "2014-04-22", "2014-04-23", "2014-04-24", "2014-04-25", "2014-04-28", "2014-04-29", "2014-04-30", "2014-05-01", "2014-05-02", "2014-05-05", "2014-05-06", "2014-05-07", "2014-05-08", "2014-05-09", "2014-05-12", "2014-05-13", "2014-05-14", "2014-05-15", "2014-05-16", "2014-05-19", "2014-05-20", "2014-05-21", "2014-05-22", "2014-05-23", "2014-05-27", "2014-05-28", "2014-05-29", "2014-05-30", "2014-06-02", "2014-06-03", "2014-06-04", "2014-06-05", "2014-06-06", "2014-06-09", "2014-06-10", "2014-06-11", "2014-06-12", "2014-06-13", "2014-06-16", "2014-06-17", "2014-06-18", "2014-06-19", "2014-06-20", "2014-06-23", "2014-06-24", "2014-06-25", "2014-06-26", "2014-06-27", "2014-06-30", "2014-07-01", "2014-07-02", "2014-07-03", "2014-07-07", "2014-07-08", "2014-07-09", "2014-07-10", "2014-07-11", "2014-07-14", "2014-07-15", "2014-07-16", "2014-07-17", "2014-07-18", "2014-07-21", "2014-07-22", "2014-07-23", "2014-07-24", "2014-07-25", "2014-07-28", "2014-07-29", "2014-07-30", "2014-07-31", "2014-08-01", "2014-08-04", "2014-08-05", "2014-08-06", "2014-08-07", "2014-08-08", "2014-08-11", "2014-08-12", "2014-08-13", "2014-08-14", "2014-08-15", "2014-08-18", "2014-08-19", "2014-08-20", "2014-08-21", "2014-08-22", "2014-08-25", "2014-08-26", "2014-08-27", "2014-08-28", "2014-08-29", "2014-09-02", "2014-09-03", "2014-09-04", "2014-09-05", "2014-09-08", "2014-09-09", "2014-09-10", "2014-09-11", "2014-09-12", "2014-09-15", "2014-09-16", "2014-09-17", "2014-09-18", "2014-09-19", "2014-09-22", "2014-09-23", "2014-09-24", "2014-09-25", "2014-09-26", "2014-09-29", "2014-09-30", "2014-10-01", "2014-10-02", "2014-10-03", "2014-10-06", "2014-10-07", "2014-10-08", "2014-10-09", "2014-10-10", "2014-10-13", "2014-10-14", "2014-10-15", "2014-10-16", "2014-10-17", "2014-10-20", "2014-10-21", "2014-10-22", "2014-10-23", "2014-10-24", "2014-10-27", "2014-10-28", "2014-10-29", "2014-10-30", "2014-10-31", "2014-11-03", "2014-11-04", "2014-11-05", "2014-11-06", "2014-11-07", "2014-11-10", "2014-11-11", "2014-11-12", "2014-11-13", "2014-11-14", "2014-11-17", "2014-11-18", "2014-11-19", "2014-11-20", "2014-11-21", "2014-11-24", "2014-11-25", "2014-11-26", "2014-11-28", "2014-12-01", "2014-12-02", "2014-12-03", "2014-12-04", "2014-12-05", "2014-12-08", "2014-12-09", "2014-12-10", "2014-12-11", "2014-12-12", "2014-12-15", "2014-12-16", "2014-12-17", "2014-12-18", "2014-12-19", "2014-12-22", "2014-12-23", "2014-12-24", "2014-12-26", "2014-12-29", "2014-12-30", "2014-12-31", "2015-01-02", "2015-01-05", "2015-01-06", "2015-01-07", "2015-01-08", "2015-01-09", "2015-01-12", "2015-01-13", "2015-01-14", "2015-01-15", "2015-01-16", "2015-01-20", "2015-01-21", "2015-01-22", "2015-01-23", "2015-01-26", "2015-01-27", "2015-01-28", "2015-01-29", "2015-01-30", "2015-02-02", "2015-02-03", "2015-02-04", "2015-02-05", "2015-02-06", "2015-02-09", "2015-02-10", "2015-02-11", "2015-02-12", "2015-02-13", "2015-02-17", "2015-02-18", "2015-02-19", "2015-02-20", "2015-02-23", "2015-02-24", "2015-02-25", "2015-02-26", "2015-02-27", "2015-03-02", "2015-03-03", "2015-03-04", "2015-03-05", "2015-03-06", "2015-03-09", "2015-03-10", "2015-03-11", "2015-03-12", "2015-03-13", "2015-03-16", "2015-03-17", "2015-03-18", "2015-03-19", "2015-03-20", "2015-03-23", "2015-03-24", "2015-03-25", "2015-03-26", "2015-03-27", "2015-03-30", "2015-03-31", "2015-04-01", "2015-04-02", "2015-04-06", "2015-04-07", "2015-04-08", "2015-04-09", "2015-04-10", "2015-04-13", "2015-04-14", "2015-04-15", "2015-04-16", "2015-04-17", "2015-04-20", "2015-04-21", "2015-04-22", "2015-04-23", "2015-04-24", "2015-04-27", "2015-04-28", "2015-04-29", "2015-04-30", "2015-05-01", "2015-05-04", "2015-05-05", "2015-05-06", "2015-05-07", "2015-05-08", "2015-05-11", "2015-05-12", "2015-05-13", "2015-05-14", "2015-05-15", "2015-05-18", "2015-05-19", "2015-05-20", "2015-05-21", "2015-05-22", "2015-05-26", "2015-05-27", "2015-05-28", "2015-05-29", "2015-06-01", "2015-06-02", "2015-06-03", "2015-06-04", "2015-06-05", "2015-06-08", "2015-06-09", "2015-06-10", "2015-06-11", "2015-06-12", "2015-06-15", "2015-06-16", "2015-06-17", "2015-06-18", "2015-06-19", "2015-06-22", "2015-06-23", "2015-06-24", "2015-06-25", "2015-06-26", "2015-06-29", "2015-06-30", "2015-07-01", "2015-07-02", "2015-07-06", "2015-07-07", "2015-07-08", "2015-07-09", "2015-07-10", "2015-07-13", "2015-07-14", "2015-07-15", "2015-07-16", "2015-07-17", "2015-07-20", "2015-07-21", "2015-07-22", "2015-07-23", "2015-07-24", "2015-07-27", "2015-07-28", "2015-07-29", "2015-07-30", "2015-07-31", "2015-08-03", "2015-08-04", "2015-08-05", "2015-08-06", "2015-08-07", "2015-08-10", "2015-08-11", "2015-08-12", "2015-08-13", "2015-08-14", "2015-08-17", "2015-08-18", "2015-08-19", "2015-08-20", "2015-08-21", "2015-08-24", "2015-08-25", "2015-08-26", "2015-08-27", "2015-08-28", "2015-08-31", "2015-09-01", "2015-09-02", "2015-09-03", "2015-09-04", "2015-09-08", "2015-09-09", "2015-09-10", "2015-09-11", "2015-09-14", "2015-09-15", "2015-09-16", "2015-09-17", "2015-09-18", "2015-09-21", "2015-09-22", "2015-09-23", "2015-09-24", "2015-09-25", "2015-09-28", "2015-09-29", "2015-09-30", "2015-10-01", "2015-10-02", "2015-10-05", "2015-10-06", "2015-10-07", "2015-10-08", "2015-10-09", "2015-10-12", "2015-10-13", "2015-10-14", "2015-10-15", "2015-10-16", "2015-10-19", "2015-10-20", "2015-10-21", "2015-10-22", "2015-10-23", "2015-10-26", "2015-10-27", "2015-10-28", "2015-10-29", "2015-10-30", "2015-11-02", "2015-11-03", "2015-11-04", "2015-11-05", "2015-11-06", "2015-11-09", "2015-11-10", "2015-11-11", "2015-11-12", "2015-11-13", "2015-11-16", "2015-11-17", "2015-11-18", "2015-11-19", "2015-11-20", "2015-11-23", "2015-11-24", "2015-11-25", "2015-11-27", "2015-11-30", "2015-12-01", "2015-12-02", "2015-12-03", "2015-12-04", "2015-12-07", "2015-12-08", "2015-12-09", "2015-12-10", "2015-12-11", "2015-12-14", "2015-12-15", "2015-12-16", "2015-12-17", "2015-12-18", "2015-12-21", "2015-12-22", "2015-12-23", "2015-12-24", "2015-12-28", "2015-12-29", "2015-12-30", "2015-12-31", "2016-01-04", "2016-01-05", "2016-01-06", "2016-01-07", "2016-01-08", "2016-01-11", "2016-01-12", "2016-01-13", "2016-01-14", "2016-01-15", "2016-01-19", "2016-01-20", "2016-01-21", "2016-01-22", "2016-01-25", "2016-01-26", "2016-01-27", "2016-01-28", "2016-01-29", "2016-02-01", "2016-02-02", "2016-02-03", "2016-02-04", "2016-02-05", "2016-02-08", "2016-02-09", "2016-02-10", "2016-02-11", "2016-02-12", "2016-02-16", "2016-02-17", "2016-02-18", "2016-02-19", "2016-02-22", "2016-02-23", "2016-02-24", "2016-02-25", "2016-02-26", "2016-02-29", "2016-03-01", "2016-03-02", "2016-03-03", "2016-03-04", "2016-03-07", "2016-03-08", "2016-03-09", "2016-03-10", "2016-03-11", "2016-03-14", "2016-03-15", "2016-03-16", "2016-03-17", "2016-03-18", "2016-03-21", "2016-03-22", "2016-03-23", "2016-03-24", "2016-03-28", "2016-03-29", "2016-03-30", "2016-03-31", "2016-04-01", "2016-04-04", "2016-04-05", "2016-04-06", "2016-04-07", "2016-04-08", "2016-04-11", "2016-04-12", "2016-04-13", "2016-04-14", "2016-04-15", "2016-04-18", "2016-04-19", "2016-04-20", "2016-04-21", "2016-04-22", "2016-04-25", "2016-04-26", "2016-04-27", "2016-04-28", "2016-04-29", "2016-05-02", "2016-05-03", "2016-05-04", "2016-05-05", "2016-05-06", "2016-05-09", "2016-05-10", "2016-05-11", "2016-05-12", "2016-05-13", "2016-05-16", "2016-05-17", "2016-05-18", "2016-05-19", "2016-05-20", "2016-05-23", "2016-05-24", "2016-05-25", "2016-05-26", "2016-05-27", "2016-05-31", "2016-06-01", "2016-06-02", "2016-06-03", "2016-06-06", "2016-06-07", "2016-06-08", "2016-06-09", "2016-06-10", "2016-06-13", "2016-06-14", "2016-06-15", "2016-06-16", "2016-06-17", "2016-06-20", "2016-06-21", "2016-06-22", "2016-06-23", "2016-06-24", "2016-06-27", "2016-06-28", "2016-06-29", "2016-06-30", "2016-07-01", "2016-07-05", "2016-07-06", "2016-07-07", "2016-07-08", "2016-07-11", "2016-07-12", "2016-07-13", "2016-07-14", "2016-07-15", "2016-07-18", "2016-07-19", "2016-07-20", "2016-07-21", "2016-07-22", "2016-07-25", "2016-07-26", "2016-07-27", "2016-07-28", "2016-07-29", "2016-08-01", "2016-08-02", "2016-08-03", "2016-08-04", "2016-08-05", "2016-08-08", "2016-08-09", "2016-08-10", "2016-08-11", "2016-08-12", "2016-08-15", "2016-08-16", "2016-08-17", "2016-08-18", "2016-08-19", "2016-08-22", "2016-08-23", "2016-08-24", "2016-08-25", "2016-08-26", "2016-08-29", "2016-08-30", "2016-08-31", "2016-09-01", "2016-09-02", "2016-09-06", "2016-09-07", "2016-09-08", "2016-09-09", "2016-09-12", "2016-09-13", "2016-09-14", "2016-09-15", "2016-09-16", "2016-09-19", "2016-09-20", "2016-09-21", "2016-09-22", "2016-09-23", "2016-09-26", "2016-09-27", "2016-09-28", "2016-09-29", "2016-09-30", "2016-10-03", "2016-10-04", "2016-10-05", "2016-10-06", "2016-10-07", "2016-10-10", "2016-10-11", "2016-10-12", "2016-10-13", "2016-10-14", "2016-10-17", "2016-10-18", "2016-10-19", "2016-10-20", "2016-10-21", "2016-10-24", "2016-10-25", "2016-10-26", "2016-10-27", "2016-10-28", "2016-10-31", "2016-11-01", "2016-11-02", "2016-11-03", "2016-11-04", "2016-11-07", "2016-11-08", "2016-11-09", "2016-11-10", "2016-11-11", "2016-11-14", "2016-11-15", "2016-11-16", "2016-11-17", "2016-11-18", "2016-11-21", "2016-11-22", "2016-11-23", "2016-11-25", "2016-11-28", "2016-11-29", "2016-11-30", "2016-12-01", "2016-12-02", "2016-12-05", "2016-12-06", "2016-12-07", "2016-12-08", "2016-12-09", "2016-12-12", "2016-12-13", "2016-12-14", "2016-12-15", "2016-12-16", "2016-12-19", "2016-12-20", "2016-12-21", "2016-12-22", "2016-12-23", "2016-12-27", "2016-12-28", "2016-12-29", "2016-12-30", "2017-01-03", "2017-01-04", "2017-01-05", "2017-01-06", "2017-01-09", "2017-01-10", "2017-01-11", "2017-01-12", "2017-01-13", "2017-01-17", "2017-01-18", "2017-01-19", "2017-01-20", "2017-01-23", "2017-01-24", "2017-01-25", "2017-01-26", "2017-01-27", "2017-01-30", "2017-01-31", "2017-02-01", "2017-02-02", "2017-02-03", "2017-02-06", "2017-02-07", "2017-02-08", "2017-02-09", "2017-02-10", "2017-02-13", "2017-02-14", "2017-02-15", "2017-02-16", "2017-02-17", "2017-02-21", "2017-02-22", "2017-02-23", "2017-02-24", "2017-02-27", "2017-02-28", "2017-03-01", "2017-03-02", "2017-03-03", "2017-03-06", "2017-03-07", "2017-03-08", "2017-03-09", "2017-03-10", "2017-03-13", "2017-03-14", "2017-03-15", "2017-03-16", "2017-03-17", "2017-03-20", "2017-03-21", "2017-03-22", "2017-03-23", "2017-03-24", "2017-03-27", "2017-03-28", "2017-03-29", "2017-03-30", "2017-03-31", "2017-04-03", "2017-04-04", "2017-04-05", "2017-04-06", "2017-04-07", "2017-04-10", "2017-04-11", "2017-04-12", "2017-04-13", "2017-04-17", "2017-04-18", "2017-04-19", "2017-04-20", "2017-04-21", "2017-04-24", "2017-04-25", "2017-04-26", "2017-04-27", "2017-04-28", "2017-05-01", "2017-05-02", "2017-05-03", "2017-05-04", "2017-05-05", "2017-05-08", "2017-05-09", "2017-05-10", "2017-05-11", "2017-05-12", "2017-05-15", "2017-05-16", "2017-05-17", "2017-05-18", "2017-05-19", "2017-05-22", "2017-05-23", "2017-05-24", "2017-05-25", "2017-05-26", "2017-05-30", "2017-05-31", "2017-06-01", "2017-06-02", "2017-06-05", "2017-06-06", "2017-06-07", "2017-06-08", "2017-06-09", "2017-06-12", "2017-06-13", "2017-06-14", "2017-06-15", "2017-06-16", "2017-06-19", "2017-06-20", "2017-06-21", "2017-06-22", "2017-06-23", "2017-06-26", "2017-06-27", "2017-06-28", "2017-06-29", "2017-06-30"], "y": [53.10917319210857, 54.31224741988544, 54.61204261580394, 54.17338124688422, 53.86579916276005, 54.81320389445057, 54.60295791289733, 55.45406479377765, 55.35309481004406, 55.47379157723203, 55.83133952734264, 55.846264396403505, 56.03418796510047, 55.1506357166965, 55.327138516025144, 54.377138154932744, 57.170035391368344, 56.90917463647821, 57.23233049701374, 58.11484449365696, 58.83253602328005, 58.730008661905316, 59.2680826369175, 60.02912117755218, 60.9259111359058, 60.38082896150852, 60.345787964582975, 60.22638901209596, 59.36939000574175, 61.05595359903942, 63.95747005195509, 65.12408607737322, 65.04700842283833, 65.62443763138795, 66.33120053144529, 65.45983111492357, 65.62835683416091, 65.70674088962014, 65.45329911030197, 65.70804729054446, 63.82944276137168, 64.13069881451997, 64.23573344883532, 63.64994327437006, 63.82813636044736, 65.14903833502774, 64.70211857881773, 65.08750685149226, 66.126095586327, 64.61981532058553, 61.101677631390636, 61.75226529170222, 60.734578971656596, 58.803718405511006, 59.48304688615764, 60.70583815132154, 61.701315655653715, 61.062485603661024, 64.09725495085738, 63.89606920851203, 62.90712370880146, 63.51982574230775, 63.06650462156856, 62.2826640669763, 63.74713950313949, 63.95616365103077, 63.1527270825737, 63.10308384744953, 63.71970508372877, 62.83004605426657, 63.567901296322745, 63.96635357824047, 64.38100523161978, 64.80271144999041, 65.147601294011, 65.46557927899059, 65.90792663196548, 66.48143663774215, 68.11077987055458, 67.91553825241489, 68.58082292312507, 69.48877156552777, 68.71120173537224, 69.22304961752099, 67.4988616776029, 68.57246195720941, 68.28583759441352, 67.9367672674351, 68.81466868857844, 68.64470592832434, 68.45148923161734, 67.34400794611464, 68.40418343394518, 68.20549908372212, 68.3319106875016, 68.4139074034667, 69.40286138480192, 68.98643896029337, 68.15044039143146, 68.27146439047607, 67.67357166989737, 68.47987271022065, 68.3043156388595, 68.82205131338262, 70.09142355091893, 71.74187026970324, 73.07037475432978, 72.43437458562627, 74.4175387480381, 74.24382134658644, 74.62502723282792, 73.5894244787882, 74.43173048733973, 74.31609409303, 73.76550717012347, 73.65775507542577, 72.85487056493436, 73.25828389508307, 72.92845736131329, 72.37392828860072, 71.54476277940256, 72.14396954991659, 74.91267276367337, 74.59467267932162, 74.09927585369927, 73.59862282833556, 72.86669701435241, 73.72082947232198, 72.68404407334043, 71.087473401905, 71.47511813282965, 70.96362419549942, 71.41335778586878, 70.5012757257508, 70.0309772538934, 70.39759718585265, 71.79837441692275, 73.23988719598835, 72.83121766609828, 71.04673785390953, 72.15053979959329, 72.47116798381572, 73.08482930361849, 71.75632481899196, 72.33844894034661, 66.55662922486023, 65.801050512041, 65.67385047830028, 65.78133976301092, 65.90354640699735, 66.85754666005259, 67.35688563548096, 67.74715846627629, 68.6949392436332, 69.92560019721661, 70.8469435749262, 70.84165609499674, 71.96656744999079, 71.90840517076668, 72.17277916724002, 71.03332724243992, 70.21112411340782, 69.43122082381146, 69.7352509197558, 69.00954429943647, 68.38694353774177, 69.7511133595442, 69.56208595206577, 69.76301018938551, 70.22302094324913, 70.37107038127421, 70.15824931411316, 70.1172713446598, 70.18072110381338, 70.86412788469698, 70.93286512378005, 70.14503061428947, 69.35719610479893, 69.62817945118411, 70.244170862967, 70.22566468321386, 69.88726596772797, 70.43848575037491, 71.27390757923067, 72.04059216900335, 71.3518979081903, 71.04522407228124, 70.96591187333921, 70.95004943355082, 71.59908759489285, 71.71805589330587, 71.22103277993598, 70.2996894022264, 69.19592796695021, 69.19196235700309, 70.10140890487139, 69.19724983693257, 68.68568615375665, 68.95931324010654, 68.4675643879663, 68.60637395481464, 69.3902428543581, 70.21376785337256, 70.28369477543976, 69.36512732469313, 75.0518119888347, 75.60303177148164, 78.5309737824239, 78.29832466552736, 78.00222578947721, 78.18596571702619, 78.33137141508655, 79.43909846030984, 78.57327362185963, 78.29832466552736, 78.15952831737886, 77.83419039401828, 78.80289319953012, 78.9265149640757, 78.9411368932155, 78.26985741907009, 79.42498982111438, 80.3661103512034, 80.38206154662863, 80.59474415229845, 80.72235371570036, 81.63423038750979, 83.16288661576172, 82.94754547752102, 84.45892124406228, 84.14255586812841, 83.56432503396353, 84.74604276171655, 85.71374861751431, 86.05005298772974, 85.81344358892204, 87.18657566177792, 87.69834318167095, 87.3354534857468, 85.87458983805213, 84.93479857424855, 85.79084606206962, 85.67918769409295, 85.77223633407354, 85.47448068613575, 84.59051860632049, 84.51607969433606, 84.00431217444302, 84.07875108642745, 84.58121374232246, 85.58613905411241, 86.47010113392767, 87.01908810981291, 86.98186865382071, 87.49363617371374, 89.29691881653686, 88.72187822145702, 88.75909767744926, 88.4287750055183, 88.60091498948229, 89.74541326124313, 88.69396362946286, 88.19150097356787, 86.61888590925655, 87.86583073363596, 87.40896191133145, 88.13567178957955, 90.4339731970992, 90.28509537313032, 90.88153715540571, 92.13676330874331, 91.5412520128678, 91.32724014091251, 88.95449982140842, 89.44765761330534, 88.94519495741038, 88.50786634950177, 88.35898852553288, 88.34968366153483, 88.59281361233921, 89.76170760659109, 89.74300530268307, 90.93060160084299, 91.17373155164742, 91.62258684544013, 92.72602277601385, 94.00713059371395, 94.04453520153002, 94.05388635348405, 94.74587159808115, 94.95159694106951, 94.34283694886312, 95.50331490635638, 95.61552872980455, 95.84930752865496, 96.59739968497615, 92.52029743302558, 91.75350297279631, 92.5483508888876, 91.97793061969269, 91.63193799739412, 94.44663473555269, 94.84873426957529, 95.06381076451768, 95.03575730865565, 94.31571860819643, 94.98900154888555, 95.18537573991988, 94.40923012773659, 94.50274164727678, 95.98022365601116, 95.1479711321038, 91.51972417394596, 94.21285593670228, 93.61438221164534, 94.21285593670228, 92.7447250799219, 93.41800802061104, 93.1561757658986, 93.1561757658986, 92.34262554589928, 94.25961169647238, 94.46533703946068, 94.19415363279428, 93.33384765302489, 92.34262554589928, 91.21113615946345, 90.01418870934951, 91.33270113486564, 93.2870918932548, 95.82125407279293, 96.30751397440169, 98.02812593394049, 98.39282086014704, 98.28995818865288, 99.81419595715737, 100.37526507439829, 100.03862360405373, 100.99244110336326, 102.30160237692543, 101.55351022060415, 101.79664017140855, 102.086525881983, 102.37766500823341, 102.20861648331379, 103.02568435375841, 104.48137998501022, 105.95585878569756, 107.23311430731206, 107.05467419767471, 108.44462873590228, 107.693301958482, 109.23352185219362, 109.38378720767768, 111.4076737143536, 110.44503628078384, 111.75985814126936, 111.69411704824509, 108.06896534719215, 107.65573561961098, 108.876641632919, 108.4634119053378, 108.00322425416788, 105.56141222755191, 107.17676479900557, 105.138790915253, 104.82886861956713, 103.05385910791166, 101.64042560788971, 100.25047106966215, 102.75332839694352, 105.79620184549576, 104.97913397505116, 106.0685578023106, 105.69289441360044, 105.19514042355951, 107.05467419767471, 106.97954151993272, 105.67411124416495, 103.66431211456565, 102.67819571920151, 99.78558762613336, 99.79497921085111, 101.19432533379644, 105.08244140694643, 105.19514042355951, 102.60306304145948, 103.5140467590816, 103.11960020093592, 100.32090795504531, 99.54140642347177, 102.10530905141852, 102.88481058299207, 105.56141222755191, 106.10612414118162, 106.21882315779465, 102.4997556095642, 108.29436338041825, 111.66594229409183, 110.03180655320268, 111.4123695067125, 111.43115267614799, 112.28578688546358, 113.08407158647265, 112.13180451708513, 112.87664707630907, 115.04517604620136, 117.74169467832836, 119.23137979677614, 119.81593977996452, 120.52306879188593, 121.35748102595319, 121.10762877507428, 122.09289519835148, 125.39754478073088, 124.6149886742045, 121.42819392714532, 122.96030678630841, 121.11705716189994, 121.71104553191392, 121.96561197620562, 121.19248425650486, 119.18423786264805, 119.36337721233481, 119.87251010091822, 117.39284436578043, 115.25260055636498, 117.33627404482678, 116.52543277782353, 117.80769338610772, 119.77822623266205, 121.12648554872551, 120.20721783322772, 118.7033901345415, 119.93850880869756, 119.44823269376538, 116.32743665448551, 117.13827792148876, 116.20486762575248, 119.14652431534556, 117.31741727117551, 117.14770630831435, 118.15654369865558, 120.0705062242562, 118.8071023896233, 118.42053852977293, 119.32566366503237, 119.83479655361576, 119.59908688297527, 119.08052560756624, 119.53308817519594, 118.9579565788332, 117.61912564959532, 120.30621589489668, 119.65565720392898, 121.26791135110982, 122.25789196779978, 122.83302356416254, 125.06755124183422, 123.09701839527989, 121.28676812476105, 117.99626112262008, 121.57904811635521, 121.34333844571476, 118.60910626628531, 117.86426370706141, 118.59024949263409, 120.82458598315468, 119.59380740786793, 119.16303490651752, 119.30031405529951, 122.08376714094813, 121.9133516459084, 123.2577405512217, 123.1441302211952, 123.134662693693, 124.3938438514864, 125.48260951424012, 122.71809148359593, 125.01396690288091, 124.76307742407243, 123.34294829874152, 123.58437025004778, 123.03998741867096, 123.19146785870623, 122.47193576853859, 121.79974131588196, 120.99500147819441, 120.63523543311058, 122.01749444843271, 121.7429361508687, 120.39854724555543, 120.16185905800027, 120.80565092815027, 120.52162510308409, 121.07074169821207, 119.85889817792969, 120.81511845565252, 120.26600186052454, 121.2884948307628, 120.71097565312824, 120.00091109046276, 117.899119984973, 118.74646369642043, 119.85889817792969, 119.70741773789436, 119.29084652779731, 118.99735317522892, 116.0434845945406, 113.67660271898909, 116.71567904719723, 118.96895059272232, 118.92161295521127, 120.0671837829782, 121.66719593085104, 122.71809148359593, 125.03763572163643, 123.7879220913452, 118.55237938262523, 118.495574217612, 117.87071740246635, 116.23283514458471, 116.8103543222193, 116.44112074963327, 115.85413404449648, 114.84110860176042, 112.1333957361295, 108.53573528529114, 109.2552673754588, 109.49195556301396, 109.86285682827562, 113.85717814647816, 107.9322681911444, 109.59656874039543, 109.51097614071968, 110.28130953780159, 111.42254420014518, 110.79486513585621, 109.3778320967796, 107.13340392750388, 100.58081490788116, 98.07009865072528, 98.65973655960278, 104.31835842705635, 107.3901817265312, 107.74206241408714, 107.2380171048854, 102.44483152304231, 106.83858497306512, 104.96505806905107, 103.91892629523613, 106.81005410650654, 104.75583171428808, 107.05732161668098, 108.61700898855057, 109.6631407623655, 110.5856387810932, 110.70927253618044, 108.34121061181752, 107.89422703573294, 109.56803787383686, 107.84667559146864, 108.72162216593205, 109.3683218079267, 109.0925234311937, 106.93368786159377, 103.719210229326, 104.56562593723083, 104.21374524967487, 104.97456835790392, 105.35497991201844, 105.85902522122022, 105.35497991201844, 104.13766293885195, 106.62935861830215, 106.13482359795324, 106.31551908615766, 104.81289344740526, 106.38209110812772, 105.60224742219292, 106.25845735304048, 108.19855627902456, 108.1890459901717, 109.84383625056992, 113.24851965989492, 109.6346098958069, 108.94035880954789, 113.42921514809929, 114.62751154356009, 113.64795179171516, 115.24568031899621, 116.56761046954416, 116.02552400493096, 115.49294782917065, 115.6266644409477, 115.15865629972794, 111.5292054086359, 110.89882709597256, 110.52633082030785, 107.29802976454704, 109.05067249748228, 108.58743994954024, 112.02586710952221, 113.44899390629247, 113.94565560717876, 112.46522169107544, 113.54450577184751, 112.73265491462958, 112.52252881040846, 112.99053695162821, 112.07362304229972, 111.06119726741615, 110.02966911942156, 113.68777357018013, 112.97143457851723, 112.92367864573968, 110.4308189547528, 110.95613421530558, 108.10032943520949, 107.43174637632411, 105.53106025177854, 106.3429111089965, 104.08883108189724, 101.27123104802315, 102.51288530023886, 102.4173734346838, 103.73543717934356, 103.18146835912424, 102.02577478590807, 103.85960260456513, 102.50333411368335, 100.53578968324926, 100.6217503622488, 98.1002371115954, 96.1804486139388, 92.12119432784904, 92.60830484217982, 94.10784113139415, 95.47366080883141, 93.01900586406654, 95.05340860038919, 92.7706750136234, 92.32176924551466, 92.44593467073624, 91.97792652951648, 96.86813404593521, 94.97699910794516, 95.50231436849792, 89.22718480153091, 89.8671143007498, 92.97124993128902, 92.10209195473804, 90.23961057641449, 92.025682462294, 92.76112382706788, 90.28365281802198, 91.23431029823729, 91.21510509661677, 90.52371783827834, 89.97636959209382, 90.2548450155912, 92.79953423030891, 94.22071915022673, 92.4346353995192, 92.22337818169359, 93.02999664975503, 90.92702707230907, 92.28099378655511, 92.914765440032, 93.0588044521858, 92.84754723436019, 96.53494594549831, 96.74620316332391, 97.46639822409307, 98.91639094644171, 97.82169445407257, 97.01507598601108, 97.10149939330336, 97.14951239735466, 98.19619588567251, 98.44586350673912, 100.42399927365177, 101.75876078627728, 101.59551657250292, 101.71074778222601, 101.70114518141571, 102.47895584704644, 101.91240239924136, 101.47068276196958, 101.00975792307732, 103.40080552483096, 105.206094477159, 104.65874623097444, 105.61900631199998, 106.70410020355885, 105.44615949741535, 106.55045859059477, 104.22662919451294, 104.34186040423599, 104.6875540334052, 106.05112334846147, 107.58753947810236, 107.64515508296387, 105.48456990065641, 103.20875350862585, 102.66140526244128, 102.87266248026691, 101.75876078627728, 101.48028536277988, 100.90412931416456, 100.20313945501587, 93.93264112591906, 91.06146348365269, 90.01477999533483, 89.91875398723228, 91.39755451201162, 90.44689703179633, 90.0819982010066, 89.5796103946518, 89.64723952243034, 90.25590167243713, 89.3767230113162, 87.28022005018167, 87.45412352161215, 90.70032165498178, 90.32353080021566, 91.3572903248304, 91.00948338196936, 91.99493638674228, 93.16395416691408, 94.58416585026329, 96.24591013282154, 97.00915314632212, 96.95118532251196, 96.47778142806222, 95.12519887249157, 94.41026237883275, 94.60348845819999, 95.28944103995373, 95.67589319868816, 95.58894146297293, 96.27489404472662, 95.48266711932095, 94.043132828035, 94.15906847565536, 93.84990674866778, 94.2460202113706, 92.10121073039429, 91.87900073912192, 92.66156636055923, 92.31375941769821, 92.84513113595811, 90.23657906450045, 88.9226417248032, 90.4201438398993, 91.2027094613366, 92.36206593754, 92.6422437526225, 91.77272639546995, 92.2944368097615, 92.69055027246435, 93.40548676612312, 93.69532588517401, 94.12042325978192, 93.58905154152201, 95.44402190344748, 95.43436059947912, 96.44879751615713, 96.4874427320306, 96.57439446774583, 96.06234535742266, 95.31842495185879, 94.043132828035, 93.39582546215479, 99.46312435428604, 100.80604560588837, 100.68044865429964, 102.45812858447823, 100.94130386144545, 102.20693468130085, 102.83491943924436, 104.39876396835727, 105.26324945339485, 105.69063553588532, 104.90385661130057, 104.83586337090435, 105.07869637231941, 106.34142797967763, 106.24429477911163, 106.088881658206, 105.95289517741355, 106.22486813899842, 105.39923593418726, 105.72948881611171, 104.93299657147035, 104.48618384886669, 103.87424468530077, 103.75768484462156, 102.96119259998018, 103.05832580054621, 103.67026496411215, 104.64159696977232, 104.61245700960251, 105.25353613333824, 102.49495323726327, 100.17346974373545, 102.41724667681049, 104.85529001101757, 108.56577827263949, 112.2568398941482, 111.62547409046907, 110.32388920288444, 110.3141758828278, 110.29474924271463, 111.33407448877102, 109.47883035796005, 109.64395679892228, 109.84793652011093, 110.6832820449787, 108.96402439496016, 109.80908323988452, 109.2942772768846, 109.76051663960152, 109.80908323988452, 110.62500212463907, 110.79012856560131, 112.72307925686508, 112.96591225828014, 113.97609754416678, 113.62641802212907, 114.2577838258082, 114.18007726535538, 114.10237070490255, 113.7624045029215, 113.7041245825819, 113.2573118599782, 114.2772104659214, 114.86000966931749, 112.2762665342614, 111.1980880079786, 110.45987568367686, 110.28503592265804, 108.29380531105465, 108.39093851162063, 107.23505342488501, 106.26844409327585, 107.8013498009793, 108.43599229142977, 108.26024514022808, 105.24325237793276, 105.86813113776093, 103.21239640849123, 104.57931869561534, 107.39127311484205, 107.3522181923528, 107.45961922919822, 109.09016224312485, 109.15850835748104, 108.60197571200912, 109.14874462685871, 108.9339425531678, 108.82654151632237, 107.90875083782473, 106.90308658372628, 107.30339953924124, 106.53206482007832, 107.3522181923528, 108.4067010995628, 109.47094773739514, 111.25771044127876, 110.62306795082829, 112.46841303844582, 112.46841303844582, 113.08352806765166, 113.22998402698641, 113.88415397868148, 114.18682962797324, 114.29423066481873, 113.54242340690048, 113.7669892112137, 114.489505277265, 114.00131874614927, 113.97202755428232, 113.08352806765166, 113.40573117818806, 113.27880268009797, 113.85486278681455, 115.1241477677155, 116.17863067492549, 116.29579544239328, 116.92067420222143, 116.43248767110569, 116.22744932803707, 117.16476746777931, 117.155003737157, 116.94996539408838, 117.16476746777931, 117.24287731275784, 117.13547627591237, 119.00034882477448, 119.05893120850841, 119.06869493913072, 118.75625555921663, 118.48287110179182, 125.70803176230488, 125.49322968861395, 126.03023487284128, 127.21164627814136, 128.42234887530844, 128.9202991370465, 129.8478535461664, 129.55368079232372, 130.70095453231022, 132.39735074613642, 132.8778329107462, 132.7160378961327, 133.08375383843608, 134.0447181676555, 134.4467542645739, 133.87802027381136, 134.00549513380986, 134.27025061226828, 134.32908516303684, 137.07469753223532, 136.26081957993722, 137.0648917737739, 136.6334384014713, 136.80994205377692, 136.3000426137829, 135.98625834301737, 136.4373232322428, 136.49615778301134, 136.2902368553215, 137.7316833491507, 137.95721579376342, 137.2708127014638, 138.712259195293, 137.12372632454245, 138.6730361614473, 138.18274823837615, 137.9081870014563, 138.14352520453042, 141.00680667526606, 141.3205909460316, 141.13428153526456, 140.86952605680608, 140.9087490906518, 141.95796524602414, 141.22253336141736, 140.86952605680608, 140.55574178604058, 140.38904389219636, 138.8789570891372, 139.0456549829814, 138.31022309837468, 139.07507225836568, 138.457309475296, 137.947410035302, 139.67322352451248, 139.5065256306683, 140.84991453988326, 141.72262704294994, 140.88913757372896, 140.9970009168046, 140.85972029834468, 143.73280752754172, 144.64474306445405, 144.20348393369002, 143.6837787352346, 146.06657804136043, 150.03791021823682, 150.99887454745632, 150.28305417977242, 151.57741429668027, 153.694279777277, 153.30044433902643, 153.07398896203242, 147.9344364928627, 150.18914437684708, 150.70113044657282, 151.61679784050534, 151.42972600733634, 150.97681525334818, 151.49864720903014, 151.2426541741673, 151.3017294899049, 150.4057538678849, 150.819281078048, 153.05429719011983, 151.55772252476774, 152.06970859449345, 152.97553010246975, 152.60138643613172, 146.68400897641718, 143.17887357598732, 144.33084223287017, 142.92288054112444, 142.0662884629295, 140.07741949976423, 144.08469508396357, 142.77519225178048, 143.62193844401918, 143.38563718106883, 144.025619768226, 143.5727090142379, 141.51491884937872, 143.58255490019414, 141.4656894195974, 141.8004495421104], "line": {"color": "black"}}], {"title": "Long and Short of AAPL Stock", "annotations": [{"x": "2013-10-21", "y": 68.11077987055458, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2013-10-24", "y": 69.48877156552777, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2013-11-27", "y": 71.74187026970324, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2013-11-29", "y": 73.07037475432978, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2013-12-03", "y": 74.4175387480381, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-04-24", "y": 75.0518119888347, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-04-25", "y": 75.60303177148164, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-04-28", "y": 78.5309737824239, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-05-05", "y": 79.43909846030984, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-05-19", "y": 80.3661103512034, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-05-23", "y": 81.63423038750979, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-05-27", "y": 83.16288661576172, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-05-29", "y": 84.45892124406228, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-06-04", "y": 85.71374861751431, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-06-09", "y": 87.18657566177792, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-06-10", "y": 87.69834318167095, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-07-07", "y": 89.29691881653686, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-07-23", "y": 90.4339731970992, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-07-28", "y": 92.13676330874331, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-08-18", "y": 92.72602277601385, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-08-19", "y": 94.00713059371395, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-08-22", "y": 94.74587159808115, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-08-25", "y": 94.95159694106951, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-09-02", "y": 96.59739968497615, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-10-23", "y": 98.02812593394049, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-10-24", "y": 98.39282086014704, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-10-28", "y": 99.81419595715737, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-10-29", "y": 100.37526507439829, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-10-31", "y": 100.99244110336326, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-11-03", "y": 102.30160237692543, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-11-12", "y": 104.48137998501022, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-11-13", "y": 105.95585878569756, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-11-14", "y": 107.23311430731206, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-11-24", "y": 111.4076737143536, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2015-02-10", "y": 115.04517604620136, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2015-02-11", "y": 117.74169467832836, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2015-02-12", "y": 119.23137979677614, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2015-02-17", "y": 120.52306879188593, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2015-02-20", "y": 122.09289519835148, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2015-02-23", "y": 125.39754478073088, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2015-10-23", "y": 113.24851965989492, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2015-10-28", "y": 113.42921514809929, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2015-10-29", "y": 114.62751154356009, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2015-11-03", "y": 116.56761046954416, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-03-16", "y": 101.75876078627728, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-03-29", "y": 103.40080552483096, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-03-30", "y": 105.206094477159, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-04-04", "y": 106.70410020355885, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-07-27", "y": 99.46312435428604, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-08-01", "y": 102.45812858447823, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-08-04", "y": 102.83491943924436, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-08-05", "y": 104.39876396835727, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-08-08", "y": 105.26324945339485, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-08-09", "y": 105.69063553588532, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-08-15", "y": 106.34142797967763, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-09-14", "y": 108.56577827263949, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-09-15", "y": 112.2568398941482, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-01-09", "y": 116.17863067492549, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-01-11", "y": 116.92067420222143, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-01-17", "y": 117.16476746777931, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-01-25", "y": 119.00034882477448, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-02-01", "y": 125.70803176230488, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-02-07", "y": 128.42234887530844, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-02-09", "y": 129.8478535461664, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-02-13", "y": 130.70095453231022, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-02-14", "y": 132.39735074613642, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-02-15", "y": 132.8778329107462, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-02-21", "y": 134.0447181676555, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-02-22", "y": 134.4467542645739, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-03-01", "y": 137.07469753223532, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-03-15", "y": 137.7316833491507, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-03-20", "y": 138.712259195293, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-03-28", "y": 141.00680667526606, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-03-29", "y": 141.3205909460316, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-04-04", "y": 141.95796524602414, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-05-01", "y": 143.73280752754172, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-05-02", "y": 144.64474306445405, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-05-05", "y": 146.06657804136043, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-05-08", "y": 150.03791021823682, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-05-09", "y": 150.99887454745632, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-05-12", "y": 153.694279777277, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-01-28", "y": 66.55662922486023, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2014-01-29", "y": 65.801050512041, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2015-07-08", "y": 116.0434845945406, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2015-07-09", "y": 113.67660271898909, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2015-08-03", "y": 112.1333957361295, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2015-08-04", "y": 108.53573528529114, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2015-08-21", "y": 100.58081490788116, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2015-08-24", "y": 98.07009865072528, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2015-12-18", "y": 101.27123104802315, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2015-12-31", "y": 100.53578968324926, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2016-01-06", "y": 96.1804486139388, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2016-01-07", "y": 92.12119432784904, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2016-05-12", "y": 87.28022005018167, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}]}, {"showLink": false, "linkText": "Export to plot.ly", "displayModeBar": false})});</script>


## Filter Signals
That was a lot of repeated signals! If we're already shorting a stock, having an additional signal to short a stock isn't helpful for this strategy. This also applies to additional long signals when the last signal was long.

Implement `filter_signals` to filter out repeated long or short signals within the `lookahead_days`. If the previous signal was the same, change the signal to `0` (do nothing signal). For example, say you have a single stock time series that is

`[1, 0, 1, 0, 1, 0, -1, -1]`

Running `filter_signals` with a lookahead of 3 days should turn those signals into

`[1, 0, 0, 0, 1, 0, -1, 0]`

To help you implement the function, we have provided you with the `clear_signals` function. This will remove all signals within a window after the last signal. For example, say you're using a windows size of 3 with `clear_signals`. It would turn the Series of long signals

`[0, 1, 0, 0, 1, 1, 0, 1, 0]`

into

`[0, 1, 0, 0, 0, 1, 0, 0, 0]`

`clear_signals` only takes a Series of the same type of signals, where `1` is the signal and `0` is no signal. It can't take a mix of long and short signals. Using this function, implement `filter_signals`. 

For implementing `filter_signals`, we don't reccommend you try to find a vectorized solution. Instead, you should use the [`iterrows`](https://pandas.pydata.org/pandas-docs/version/0.21/generated/pandas.DataFrame.iterrows.html) over each column.


```python
def clear_signals(signals, window_size):
    """
    Clear out signals in a Series of just long or short signals.
    
    Remove the number of signals down to 1 within the window size time period.
    
    Parameters
    ----------
    signals : Pandas Series
        The long, short, or do nothing signals
    window_size : int
        The number of days to have a single signal       
    
    Returns
    -------
    signals : Pandas Series
        Signals with the signals removed from the window size
    """
    # Start with buffer of window size
    # This handles the edge case of calculating past_signal in the beginning
    clean_signals = [0]*window_size
    
    for signal_i, current_signal in enumerate(signals):
        # Check if there was a signal in the past window_size of days
        has_past_signal = bool(sum(clean_signals[signal_i:signal_i+window_size]))
        # Use the current signal if there's no past signal, else 0/False
        clean_signals.append(not has_past_signal and current_signal)
        
    # Remove buffer
    clean_signals = clean_signals[window_size:]

    # Return the signals as a Series of Ints
    return pd.Series(np.array(clean_signals).astype(np.int), signals.index)


def filter_signals(signal, lookahead_days):
    """
    Filter out signals in a DataFrame.
    
    Parameters
    ----------
    signal : DataFrame
        The long, short, and do nothing signals for each ticker and date
    lookahead_days : int
        The number of days to look ahead
    
    Returns
    -------
    filtered_signal : DataFrame
        The filtered long, short, and do nothing signals for each ticker and date
    """
    #TODO: Implement function
    long_signal_only = signal.copy()
    short_signal_only = signal.copy()
    long_signal_only[long_signal_only==-1] = 0
    short_signal_only[short_signal_only==1] = 0
    month = list(signal.columns)
    for c in signal:
        long_signal_only[c] = clear_signals(long_signal_only[c], lookahead_days)
        short_signal_only[c] = clear_signals(short_signal_only[c], lookahead_days)
    return long_signal_only + short_signal_only

project_tests.test_filter_signals(filter_signals)
```

    Tests Passed


### View Data
Let's view the same chart as before, but with the redundant signals removed.


```python
signal_5 = filter_signals(signal, 5)
signal_10 = filter_signals(signal, 10)
signal_20 = filter_signals(signal, 20)
for signal_data, signal_days in [(signal_5, 5), (signal_10, 10), (signal_20, 20)]:
    project_helper.plot_signal(
        close[apple_ticker],
        signal_data[apple_ticker],
        'Long and Short of {} Stock with {} day signal window'.format(apple_ticker, signal_days))
```


<div id="3ec9df91-5c82-41f3-90a5-7d1d0f4d8616" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("3ec9df91-5c82-41f3-90a5-7d1d0f4d8616", [{"type": "scatter", "name": "Index", "x": ["2013-07-01", "2013-07-02", "2013-07-03", "2013-07-05", "2013-07-08", "2013-07-09", "2013-07-10", "2013-07-11", "2013-07-12", "2013-07-15", "2013-07-16", "2013-07-17", "2013-07-18", "2013-07-19", "2013-07-22", "2013-07-23", "2013-07-24", "2013-07-25", "2013-07-26", "2013-07-29", "2013-07-30", "2013-07-31", "2013-08-01", "2013-08-02", "2013-08-05", "2013-08-06", "2013-08-07", "2013-08-08", "2013-08-09", "2013-08-12", "2013-08-13", "2013-08-14", "2013-08-15", "2013-08-16", "2013-08-19", "2013-08-20", "2013-08-21", "2013-08-22", "2013-08-23", "2013-08-26", "2013-08-27", "2013-08-28", "2013-08-29", "2013-08-30", "2013-09-03", "2013-09-04", "2013-09-05", "2013-09-06", "2013-09-09", "2013-09-10", "2013-09-11", "2013-09-12", "2013-09-13", "2013-09-16", "2013-09-17", "2013-09-18", "2013-09-19", "2013-09-20", "2013-09-23", "2013-09-24", "2013-09-25", "2013-09-26", "2013-09-27", "2013-09-30", "2013-10-01", "2013-10-02", "2013-10-03", "2013-10-04", "2013-10-07", "2013-10-08", "2013-10-09", "2013-10-10", "2013-10-11", "2013-10-14", "2013-10-15", "2013-10-16", "2013-10-17", "2013-10-18", "2013-10-21", "2013-10-22", "2013-10-23", "2013-10-24", "2013-10-25", "2013-10-28", "2013-10-29", "2013-10-30", "2013-10-31", "2013-11-01", "2013-11-04", "2013-11-05", "2013-11-06", "2013-11-07", "2013-11-08", "2013-11-11", "2013-11-12", "2013-11-13", "2013-11-14", "2013-11-15", "2013-11-18", "2013-11-19", "2013-11-20", "2013-11-21", "2013-11-22", "2013-11-25", "2013-11-26", "2013-11-27", "2013-11-29", "2013-12-02", "2013-12-03", "2013-12-04", "2013-12-05", "2013-12-06", "2013-12-09", "2013-12-10", "2013-12-11", "2013-12-12", "2013-12-13", "2013-12-16", "2013-12-17", "2013-12-18", "2013-12-19", "2013-12-20", "2013-12-23", "2013-12-24", "2013-12-26", "2013-12-27", "2013-12-30", "2013-12-31", "2014-01-02", "2014-01-03", "2014-01-06", "2014-01-07", "2014-01-08", "2014-01-09", "2014-01-10", "2014-01-13", "2014-01-14", "2014-01-15", "2014-01-16", "2014-01-17", "2014-01-21", "2014-01-22", "2014-01-23", "2014-01-24", "2014-01-27", "2014-01-28", "2014-01-29", "2014-01-30", "2014-01-31", "2014-02-03", "2014-02-04", "2014-02-05", "2014-02-06", "2014-02-07", "2014-02-10", "2014-02-11", "2014-02-12", "2014-02-13", "2014-02-14", "2014-02-18", "2014-02-19", "2014-02-20", "2014-02-21", "2014-02-24", "2014-02-25", "2014-02-26", "2014-02-27", "2014-02-28", "2014-03-03", "2014-03-04", "2014-03-05", "2014-03-06", "2014-03-07", "2014-03-10", "2014-03-11", "2014-03-12", "2014-03-13", "2014-03-14", "2014-03-17", "2014-03-18", "2014-03-19", "2014-03-20", "2014-03-21", "2014-03-24", "2014-03-25", "2014-03-26", "2014-03-27", "2014-03-28", "2014-03-31", "2014-04-01", "2014-04-02", "2014-04-03", "2014-04-04", "2014-04-07", "2014-04-08", "2014-04-09", "2014-04-10", "2014-04-11", "2014-04-14", "2014-04-15", "2014-04-16", "2014-04-17", "2014-04-21", "2014-04-22", "2014-04-23", "2014-04-24", "2014-04-25", "2014-04-28", "2014-04-29", "2014-04-30", "2014-05-01", "2014-05-02", "2014-05-05", "2014-05-06", "2014-05-07", "2014-05-08", "2014-05-09", "2014-05-12", "2014-05-13", "2014-05-14", "2014-05-15", "2014-05-16", "2014-05-19", "2014-05-20", "2014-05-21", "2014-05-22", "2014-05-23", "2014-05-27", "2014-05-28", "2014-05-29", "2014-05-30", "2014-06-02", "2014-06-03", "2014-06-04", "2014-06-05", "2014-06-06", "2014-06-09", "2014-06-10", "2014-06-11", "2014-06-12", "2014-06-13", "2014-06-16", "2014-06-17", "2014-06-18", "2014-06-19", "2014-06-20", "2014-06-23", "2014-06-24", "2014-06-25", "2014-06-26", "2014-06-27", "2014-06-30", "2014-07-01", "2014-07-02", "2014-07-03", "2014-07-07", "2014-07-08", "2014-07-09", "2014-07-10", "2014-07-11", "2014-07-14", "2014-07-15", "2014-07-16", "2014-07-17", "2014-07-18", "2014-07-21", "2014-07-22", "2014-07-23", "2014-07-24", "2014-07-25", "2014-07-28", "2014-07-29", "2014-07-30", "2014-07-31", "2014-08-01", "2014-08-04", "2014-08-05", "2014-08-06", "2014-08-07", "2014-08-08", "2014-08-11", "2014-08-12", "2014-08-13", "2014-08-14", "2014-08-15", "2014-08-18", "2014-08-19", "2014-08-20", "2014-08-21", "2014-08-22", "2014-08-25", "2014-08-26", "2014-08-27", "2014-08-28", "2014-08-29", "2014-09-02", "2014-09-03", "2014-09-04", "2014-09-05", "2014-09-08", "2014-09-09", "2014-09-10", "2014-09-11", "2014-09-12", "2014-09-15", "2014-09-16", "2014-09-17", "2014-09-18", "2014-09-19", "2014-09-22", "2014-09-23", "2014-09-24", "2014-09-25", "2014-09-26", "2014-09-29", "2014-09-30", "2014-10-01", "2014-10-02", "2014-10-03", "2014-10-06", "2014-10-07", "2014-10-08", "2014-10-09", "2014-10-10", "2014-10-13", "2014-10-14", "2014-10-15", "2014-10-16", "2014-10-17", "2014-10-20", "2014-10-21", "2014-10-22", "2014-10-23", "2014-10-24", "2014-10-27", "2014-10-28", "2014-10-29", "2014-10-30", "2014-10-31", "2014-11-03", "2014-11-04", "2014-11-05", "2014-11-06", "2014-11-07", "2014-11-10", "2014-11-11", "2014-11-12", "2014-11-13", "2014-11-14", "2014-11-17", "2014-11-18", "2014-11-19", "2014-11-20", "2014-11-21", "2014-11-24", "2014-11-25", "2014-11-26", "2014-11-28", "2014-12-01", "2014-12-02", "2014-12-03", "2014-12-04", "2014-12-05", "2014-12-08", "2014-12-09", "2014-12-10", "2014-12-11", "2014-12-12", "2014-12-15", "2014-12-16", "2014-12-17", "2014-12-18", "2014-12-19", "2014-12-22", "2014-12-23", "2014-12-24", "2014-12-26", "2014-12-29", "2014-12-30", "2014-12-31", "2015-01-02", "2015-01-05", "2015-01-06", "2015-01-07", "2015-01-08", "2015-01-09", "2015-01-12", "2015-01-13", "2015-01-14", "2015-01-15", "2015-01-16", "2015-01-20", "2015-01-21", "2015-01-22", "2015-01-23", "2015-01-26", "2015-01-27", "2015-01-28", "2015-01-29", "2015-01-30", "2015-02-02", "2015-02-03", "2015-02-04", "2015-02-05", "2015-02-06", "2015-02-09", "2015-02-10", "2015-02-11", "2015-02-12", "2015-02-13", "2015-02-17", "2015-02-18", "2015-02-19", "2015-02-20", "2015-02-23", "2015-02-24", "2015-02-25", "2015-02-26", "2015-02-27", "2015-03-02", "2015-03-03", "2015-03-04", "2015-03-05", "2015-03-06", "2015-03-09", "2015-03-10", "2015-03-11", "2015-03-12", "2015-03-13", "2015-03-16", "2015-03-17", "2015-03-18", "2015-03-19", "2015-03-20", "2015-03-23", "2015-03-24", "2015-03-25", "2015-03-26", "2015-03-27", "2015-03-30", "2015-03-31", "2015-04-01", "2015-04-02", "2015-04-06", "2015-04-07", "2015-04-08", "2015-04-09", "2015-04-10", "2015-04-13", "2015-04-14", "2015-04-15", "2015-04-16", "2015-04-17", "2015-04-20", "2015-04-21", "2015-04-22", "2015-04-23", "2015-04-24", "2015-04-27", "2015-04-28", "2015-04-29", "2015-04-30", "2015-05-01", "2015-05-04", "2015-05-05", "2015-05-06", "2015-05-07", "2015-05-08", "2015-05-11", "2015-05-12", "2015-05-13", "2015-05-14", "2015-05-15", "2015-05-18", "2015-05-19", "2015-05-20", "2015-05-21", "2015-05-22", "2015-05-26", "2015-05-27", "2015-05-28", "2015-05-29", "2015-06-01", "2015-06-02", "2015-06-03", "2015-06-04", "2015-06-05", "2015-06-08", "2015-06-09", "2015-06-10", "2015-06-11", "2015-06-12", "2015-06-15", "2015-06-16", "2015-06-17", "2015-06-18", "2015-06-19", "2015-06-22", "2015-06-23", "2015-06-24", "2015-06-25", "2015-06-26", "2015-06-29", "2015-06-30", "2015-07-01", "2015-07-02", "2015-07-06", "2015-07-07", "2015-07-08", "2015-07-09", "2015-07-10", "2015-07-13", "2015-07-14", "2015-07-15", "2015-07-16", "2015-07-17", "2015-07-20", "2015-07-21", "2015-07-22", "2015-07-23", "2015-07-24", "2015-07-27", "2015-07-28", "2015-07-29", "2015-07-30", "2015-07-31", "2015-08-03", "2015-08-04", "2015-08-05", "2015-08-06", "2015-08-07", "2015-08-10", "2015-08-11", "2015-08-12", "2015-08-13", "2015-08-14", "2015-08-17", "2015-08-18", "2015-08-19", "2015-08-20", "2015-08-21", "2015-08-24", "2015-08-25", "2015-08-26", "2015-08-27", "2015-08-28", "2015-08-31", "2015-09-01", "2015-09-02", "2015-09-03", "2015-09-04", "2015-09-08", "2015-09-09", "2015-09-10", "2015-09-11", "2015-09-14", "2015-09-15", "2015-09-16", "2015-09-17", "2015-09-18", "2015-09-21", "2015-09-22", "2015-09-23", "2015-09-24", "2015-09-25", "2015-09-28", "2015-09-29", "2015-09-30", "2015-10-01", "2015-10-02", "2015-10-05", "2015-10-06", "2015-10-07", "2015-10-08", "2015-10-09", "2015-10-12", "2015-10-13", "2015-10-14", "2015-10-15", "2015-10-16", "2015-10-19", "2015-10-20", "2015-10-21", "2015-10-22", "2015-10-23", "2015-10-26", "2015-10-27", "2015-10-28", "2015-10-29", "2015-10-30", "2015-11-02", "2015-11-03", "2015-11-04", "2015-11-05", "2015-11-06", "2015-11-09", "2015-11-10", "2015-11-11", "2015-11-12", "2015-11-13", "2015-11-16", "2015-11-17", "2015-11-18", "2015-11-19", "2015-11-20", "2015-11-23", "2015-11-24", "2015-11-25", "2015-11-27", "2015-11-30", "2015-12-01", "2015-12-02", "2015-12-03", "2015-12-04", "2015-12-07", "2015-12-08", "2015-12-09", "2015-12-10", "2015-12-11", "2015-12-14", "2015-12-15", "2015-12-16", "2015-12-17", "2015-12-18", "2015-12-21", "2015-12-22", "2015-12-23", "2015-12-24", "2015-12-28", "2015-12-29", "2015-12-30", "2015-12-31", "2016-01-04", "2016-01-05", "2016-01-06", "2016-01-07", "2016-01-08", "2016-01-11", "2016-01-12", "2016-01-13", "2016-01-14", "2016-01-15", "2016-01-19", "2016-01-20", "2016-01-21", "2016-01-22", "2016-01-25", "2016-01-26", "2016-01-27", "2016-01-28", "2016-01-29", "2016-02-01", "2016-02-02", "2016-02-03", "2016-02-04", "2016-02-05", "2016-02-08", "2016-02-09", "2016-02-10", "2016-02-11", "2016-02-12", "2016-02-16", "2016-02-17", "2016-02-18", "2016-02-19", "2016-02-22", "2016-02-23", "2016-02-24", "2016-02-25", "2016-02-26", "2016-02-29", "2016-03-01", "2016-03-02", "2016-03-03", "2016-03-04", "2016-03-07", "2016-03-08", "2016-03-09", "2016-03-10", "2016-03-11", "2016-03-14", "2016-03-15", "2016-03-16", "2016-03-17", "2016-03-18", "2016-03-21", "2016-03-22", "2016-03-23", "2016-03-24", "2016-03-28", "2016-03-29", "2016-03-30", "2016-03-31", "2016-04-01", "2016-04-04", "2016-04-05", "2016-04-06", "2016-04-07", "2016-04-08", "2016-04-11", "2016-04-12", "2016-04-13", "2016-04-14", "2016-04-15", "2016-04-18", "2016-04-19", "2016-04-20", "2016-04-21", "2016-04-22", "2016-04-25", "2016-04-26", "2016-04-27", "2016-04-28", "2016-04-29", "2016-05-02", "2016-05-03", "2016-05-04", "2016-05-05", "2016-05-06", "2016-05-09", "2016-05-10", "2016-05-11", "2016-05-12", "2016-05-13", "2016-05-16", "2016-05-17", "2016-05-18", "2016-05-19", "2016-05-20", "2016-05-23", "2016-05-24", "2016-05-25", "2016-05-26", "2016-05-27", "2016-05-31", "2016-06-01", "2016-06-02", "2016-06-03", "2016-06-06", "2016-06-07", "2016-06-08", "2016-06-09", "2016-06-10", "2016-06-13", "2016-06-14", "2016-06-15", "2016-06-16", "2016-06-17", "2016-06-20", "2016-06-21", "2016-06-22", "2016-06-23", "2016-06-24", "2016-06-27", "2016-06-28", "2016-06-29", "2016-06-30", "2016-07-01", "2016-07-05", "2016-07-06", "2016-07-07", "2016-07-08", "2016-07-11", "2016-07-12", "2016-07-13", "2016-07-14", "2016-07-15", "2016-07-18", "2016-07-19", "2016-07-20", "2016-07-21", "2016-07-22", "2016-07-25", "2016-07-26", "2016-07-27", "2016-07-28", "2016-07-29", "2016-08-01", "2016-08-02", "2016-08-03", "2016-08-04", "2016-08-05", "2016-08-08", "2016-08-09", "2016-08-10", "2016-08-11", "2016-08-12", "2016-08-15", "2016-08-16", "2016-08-17", "2016-08-18", "2016-08-19", "2016-08-22", "2016-08-23", "2016-08-24", "2016-08-25", "2016-08-26", "2016-08-29", "2016-08-30", "2016-08-31", "2016-09-01", "2016-09-02", "2016-09-06", "2016-09-07", "2016-09-08", "2016-09-09", "2016-09-12", "2016-09-13", "2016-09-14", "2016-09-15", "2016-09-16", "2016-09-19", "2016-09-20", "2016-09-21", "2016-09-22", "2016-09-23", "2016-09-26", "2016-09-27", "2016-09-28", "2016-09-29", "2016-09-30", "2016-10-03", "2016-10-04", "2016-10-05", "2016-10-06", "2016-10-07", "2016-10-10", "2016-10-11", "2016-10-12", "2016-10-13", "2016-10-14", "2016-10-17", "2016-10-18", "2016-10-19", "2016-10-20", "2016-10-21", "2016-10-24", "2016-10-25", "2016-10-26", "2016-10-27", "2016-10-28", "2016-10-31", "2016-11-01", "2016-11-02", "2016-11-03", "2016-11-04", "2016-11-07", "2016-11-08", "2016-11-09", "2016-11-10", "2016-11-11", "2016-11-14", "2016-11-15", "2016-11-16", "2016-11-17", "2016-11-18", "2016-11-21", "2016-11-22", "2016-11-23", "2016-11-25", "2016-11-28", "2016-11-29", "2016-11-30", "2016-12-01", "2016-12-02", "2016-12-05", "2016-12-06", "2016-12-07", "2016-12-08", "2016-12-09", "2016-12-12", "2016-12-13", "2016-12-14", "2016-12-15", "2016-12-16", "2016-12-19", "2016-12-20", "2016-12-21", "2016-12-22", "2016-12-23", "2016-12-27", "2016-12-28", "2016-12-29", "2016-12-30", "2017-01-03", "2017-01-04", "2017-01-05", "2017-01-06", "2017-01-09", "2017-01-10", "2017-01-11", "2017-01-12", "2017-01-13", "2017-01-17", "2017-01-18", "2017-01-19", "2017-01-20", "2017-01-23", "2017-01-24", "2017-01-25", "2017-01-26", "2017-01-27", "2017-01-30", "2017-01-31", "2017-02-01", "2017-02-02", "2017-02-03", "2017-02-06", "2017-02-07", "2017-02-08", "2017-02-09", "2017-02-10", "2017-02-13", "2017-02-14", "2017-02-15", "2017-02-16", "2017-02-17", "2017-02-21", "2017-02-22", "2017-02-23", "2017-02-24", "2017-02-27", "2017-02-28", "2017-03-01", "2017-03-02", "2017-03-03", "2017-03-06", "2017-03-07", "2017-03-08", "2017-03-09", "2017-03-10", "2017-03-13", "2017-03-14", "2017-03-15", "2017-03-16", "2017-03-17", "2017-03-20", "2017-03-21", "2017-03-22", "2017-03-23", "2017-03-24", "2017-03-27", "2017-03-28", "2017-03-29", "2017-03-30", "2017-03-31", "2017-04-03", "2017-04-04", "2017-04-05", "2017-04-06", "2017-04-07", "2017-04-10", "2017-04-11", "2017-04-12", "2017-04-13", "2017-04-17", "2017-04-18", "2017-04-19", "2017-04-20", "2017-04-21", "2017-04-24", "2017-04-25", "2017-04-26", "2017-04-27", "2017-04-28", "2017-05-01", "2017-05-02", "2017-05-03", "2017-05-04", "2017-05-05", "2017-05-08", "2017-05-09", "2017-05-10", "2017-05-11", "2017-05-12", "2017-05-15", "2017-05-16", "2017-05-17", "2017-05-18", "2017-05-19", "2017-05-22", "2017-05-23", "2017-05-24", "2017-05-25", "2017-05-26", "2017-05-30", "2017-05-31", "2017-06-01", "2017-06-02", "2017-06-05", "2017-06-06", "2017-06-07", "2017-06-08", "2017-06-09", "2017-06-12", "2017-06-13", "2017-06-14", "2017-06-15", "2017-06-16", "2017-06-19", "2017-06-20", "2017-06-21", "2017-06-22", "2017-06-23", "2017-06-26", "2017-06-27", "2017-06-28", "2017-06-29", "2017-06-30"], "y": [53.10917319210857, 54.31224741988544, 54.61204261580394, 54.17338124688422, 53.86579916276005, 54.81320389445057, 54.60295791289733, 55.45406479377765, 55.35309481004406, 55.47379157723203, 55.83133952734264, 55.846264396403505, 56.03418796510047, 55.1506357166965, 55.327138516025144, 54.377138154932744, 57.170035391368344, 56.90917463647821, 57.23233049701374, 58.11484449365696, 58.83253602328005, 58.730008661905316, 59.2680826369175, 60.02912117755218, 60.9259111359058, 60.38082896150852, 60.345787964582975, 60.22638901209596, 59.36939000574175, 61.05595359903942, 63.95747005195509, 65.12408607737322, 65.04700842283833, 65.62443763138795, 66.33120053144529, 65.45983111492357, 65.62835683416091, 65.70674088962014, 65.45329911030197, 65.70804729054446, 63.82944276137168, 64.13069881451997, 64.23573344883532, 63.64994327437006, 63.82813636044736, 65.14903833502774, 64.70211857881773, 65.08750685149226, 66.126095586327, 64.61981532058553, 61.101677631390636, 61.75226529170222, 60.734578971656596, 58.803718405511006, 59.48304688615764, 60.70583815132154, 61.701315655653715, 61.062485603661024, 64.09725495085738, 63.89606920851203, 62.90712370880146, 63.51982574230775, 63.06650462156856, 62.2826640669763, 63.74713950313949, 63.95616365103077, 63.1527270825737, 63.10308384744953, 63.71970508372877, 62.83004605426657, 63.567901296322745, 63.96635357824047, 64.38100523161978, 64.80271144999041, 65.147601294011, 65.46557927899059, 65.90792663196548, 66.48143663774215, 68.11077987055458, 67.91553825241489, 68.58082292312507, 69.48877156552777, 68.71120173537224, 69.22304961752099, 67.4988616776029, 68.57246195720941, 68.28583759441352, 67.9367672674351, 68.81466868857844, 68.64470592832434, 68.45148923161734, 67.34400794611464, 68.40418343394518, 68.20549908372212, 68.3319106875016, 68.4139074034667, 69.40286138480192, 68.98643896029337, 68.15044039143146, 68.27146439047607, 67.67357166989737, 68.47987271022065, 68.3043156388595, 68.82205131338262, 70.09142355091893, 71.74187026970324, 73.07037475432978, 72.43437458562627, 74.4175387480381, 74.24382134658644, 74.62502723282792, 73.5894244787882, 74.43173048733973, 74.31609409303, 73.76550717012347, 73.65775507542577, 72.85487056493436, 73.25828389508307, 72.92845736131329, 72.37392828860072, 71.54476277940256, 72.14396954991659, 74.91267276367337, 74.59467267932162, 74.09927585369927, 73.59862282833556, 72.86669701435241, 73.72082947232198, 72.68404407334043, 71.087473401905, 71.47511813282965, 70.96362419549942, 71.41335778586878, 70.5012757257508, 70.0309772538934, 70.39759718585265, 71.79837441692275, 73.23988719598835, 72.83121766609828, 71.04673785390953, 72.15053979959329, 72.47116798381572, 73.08482930361849, 71.75632481899196, 72.33844894034661, 66.55662922486023, 65.801050512041, 65.67385047830028, 65.78133976301092, 65.90354640699735, 66.85754666005259, 67.35688563548096, 67.74715846627629, 68.6949392436332, 69.92560019721661, 70.8469435749262, 70.84165609499674, 71.96656744999079, 71.90840517076668, 72.17277916724002, 71.03332724243992, 70.21112411340782, 69.43122082381146, 69.7352509197558, 69.00954429943647, 68.38694353774177, 69.7511133595442, 69.56208595206577, 69.76301018938551, 70.22302094324913, 70.37107038127421, 70.15824931411316, 70.1172713446598, 70.18072110381338, 70.86412788469698, 70.93286512378005, 70.14503061428947, 69.35719610479893, 69.62817945118411, 70.244170862967, 70.22566468321386, 69.88726596772797, 70.43848575037491, 71.27390757923067, 72.04059216900335, 71.3518979081903, 71.04522407228124, 70.96591187333921, 70.95004943355082, 71.59908759489285, 71.71805589330587, 71.22103277993598, 70.2996894022264, 69.19592796695021, 69.19196235700309, 70.10140890487139, 69.19724983693257, 68.68568615375665, 68.95931324010654, 68.4675643879663, 68.60637395481464, 69.3902428543581, 70.21376785337256, 70.28369477543976, 69.36512732469313, 75.0518119888347, 75.60303177148164, 78.5309737824239, 78.29832466552736, 78.00222578947721, 78.18596571702619, 78.33137141508655, 79.43909846030984, 78.57327362185963, 78.29832466552736, 78.15952831737886, 77.83419039401828, 78.80289319953012, 78.9265149640757, 78.9411368932155, 78.26985741907009, 79.42498982111438, 80.3661103512034, 80.38206154662863, 80.59474415229845, 80.72235371570036, 81.63423038750979, 83.16288661576172, 82.94754547752102, 84.45892124406228, 84.14255586812841, 83.56432503396353, 84.74604276171655, 85.71374861751431, 86.05005298772974, 85.81344358892204, 87.18657566177792, 87.69834318167095, 87.3354534857468, 85.87458983805213, 84.93479857424855, 85.79084606206962, 85.67918769409295, 85.77223633407354, 85.47448068613575, 84.59051860632049, 84.51607969433606, 84.00431217444302, 84.07875108642745, 84.58121374232246, 85.58613905411241, 86.47010113392767, 87.01908810981291, 86.98186865382071, 87.49363617371374, 89.29691881653686, 88.72187822145702, 88.75909767744926, 88.4287750055183, 88.60091498948229, 89.74541326124313, 88.69396362946286, 88.19150097356787, 86.61888590925655, 87.86583073363596, 87.40896191133145, 88.13567178957955, 90.4339731970992, 90.28509537313032, 90.88153715540571, 92.13676330874331, 91.5412520128678, 91.32724014091251, 88.95449982140842, 89.44765761330534, 88.94519495741038, 88.50786634950177, 88.35898852553288, 88.34968366153483, 88.59281361233921, 89.76170760659109, 89.74300530268307, 90.93060160084299, 91.17373155164742, 91.62258684544013, 92.72602277601385, 94.00713059371395, 94.04453520153002, 94.05388635348405, 94.74587159808115, 94.95159694106951, 94.34283694886312, 95.50331490635638, 95.61552872980455, 95.84930752865496, 96.59739968497615, 92.52029743302558, 91.75350297279631, 92.5483508888876, 91.97793061969269, 91.63193799739412, 94.44663473555269, 94.84873426957529, 95.06381076451768, 95.03575730865565, 94.31571860819643, 94.98900154888555, 95.18537573991988, 94.40923012773659, 94.50274164727678, 95.98022365601116, 95.1479711321038, 91.51972417394596, 94.21285593670228, 93.61438221164534, 94.21285593670228, 92.7447250799219, 93.41800802061104, 93.1561757658986, 93.1561757658986, 92.34262554589928, 94.25961169647238, 94.46533703946068, 94.19415363279428, 93.33384765302489, 92.34262554589928, 91.21113615946345, 90.01418870934951, 91.33270113486564, 93.2870918932548, 95.82125407279293, 96.30751397440169, 98.02812593394049, 98.39282086014704, 98.28995818865288, 99.81419595715737, 100.37526507439829, 100.03862360405373, 100.99244110336326, 102.30160237692543, 101.55351022060415, 101.79664017140855, 102.086525881983, 102.37766500823341, 102.20861648331379, 103.02568435375841, 104.48137998501022, 105.95585878569756, 107.23311430731206, 107.05467419767471, 108.44462873590228, 107.693301958482, 109.23352185219362, 109.38378720767768, 111.4076737143536, 110.44503628078384, 111.75985814126936, 111.69411704824509, 108.06896534719215, 107.65573561961098, 108.876641632919, 108.4634119053378, 108.00322425416788, 105.56141222755191, 107.17676479900557, 105.138790915253, 104.82886861956713, 103.05385910791166, 101.64042560788971, 100.25047106966215, 102.75332839694352, 105.79620184549576, 104.97913397505116, 106.0685578023106, 105.69289441360044, 105.19514042355951, 107.05467419767471, 106.97954151993272, 105.67411124416495, 103.66431211456565, 102.67819571920151, 99.78558762613336, 99.79497921085111, 101.19432533379644, 105.08244140694643, 105.19514042355951, 102.60306304145948, 103.5140467590816, 103.11960020093592, 100.32090795504531, 99.54140642347177, 102.10530905141852, 102.88481058299207, 105.56141222755191, 106.10612414118162, 106.21882315779465, 102.4997556095642, 108.29436338041825, 111.66594229409183, 110.03180655320268, 111.4123695067125, 111.43115267614799, 112.28578688546358, 113.08407158647265, 112.13180451708513, 112.87664707630907, 115.04517604620136, 117.74169467832836, 119.23137979677614, 119.81593977996452, 120.52306879188593, 121.35748102595319, 121.10762877507428, 122.09289519835148, 125.39754478073088, 124.6149886742045, 121.42819392714532, 122.96030678630841, 121.11705716189994, 121.71104553191392, 121.96561197620562, 121.19248425650486, 119.18423786264805, 119.36337721233481, 119.87251010091822, 117.39284436578043, 115.25260055636498, 117.33627404482678, 116.52543277782353, 117.80769338610772, 119.77822623266205, 121.12648554872551, 120.20721783322772, 118.7033901345415, 119.93850880869756, 119.44823269376538, 116.32743665448551, 117.13827792148876, 116.20486762575248, 119.14652431534556, 117.31741727117551, 117.14770630831435, 118.15654369865558, 120.0705062242562, 118.8071023896233, 118.42053852977293, 119.32566366503237, 119.83479655361576, 119.59908688297527, 119.08052560756624, 119.53308817519594, 118.9579565788332, 117.61912564959532, 120.30621589489668, 119.65565720392898, 121.26791135110982, 122.25789196779978, 122.83302356416254, 125.06755124183422, 123.09701839527989, 121.28676812476105, 117.99626112262008, 121.57904811635521, 121.34333844571476, 118.60910626628531, 117.86426370706141, 118.59024949263409, 120.82458598315468, 119.59380740786793, 119.16303490651752, 119.30031405529951, 122.08376714094813, 121.9133516459084, 123.2577405512217, 123.1441302211952, 123.134662693693, 124.3938438514864, 125.48260951424012, 122.71809148359593, 125.01396690288091, 124.76307742407243, 123.34294829874152, 123.58437025004778, 123.03998741867096, 123.19146785870623, 122.47193576853859, 121.79974131588196, 120.99500147819441, 120.63523543311058, 122.01749444843271, 121.7429361508687, 120.39854724555543, 120.16185905800027, 120.80565092815027, 120.52162510308409, 121.07074169821207, 119.85889817792969, 120.81511845565252, 120.26600186052454, 121.2884948307628, 120.71097565312824, 120.00091109046276, 117.899119984973, 118.74646369642043, 119.85889817792969, 119.70741773789436, 119.29084652779731, 118.99735317522892, 116.0434845945406, 113.67660271898909, 116.71567904719723, 118.96895059272232, 118.92161295521127, 120.0671837829782, 121.66719593085104, 122.71809148359593, 125.03763572163643, 123.7879220913452, 118.55237938262523, 118.495574217612, 117.87071740246635, 116.23283514458471, 116.8103543222193, 116.44112074963327, 115.85413404449648, 114.84110860176042, 112.1333957361295, 108.53573528529114, 109.2552673754588, 109.49195556301396, 109.86285682827562, 113.85717814647816, 107.9322681911444, 109.59656874039543, 109.51097614071968, 110.28130953780159, 111.42254420014518, 110.79486513585621, 109.3778320967796, 107.13340392750388, 100.58081490788116, 98.07009865072528, 98.65973655960278, 104.31835842705635, 107.3901817265312, 107.74206241408714, 107.2380171048854, 102.44483152304231, 106.83858497306512, 104.96505806905107, 103.91892629523613, 106.81005410650654, 104.75583171428808, 107.05732161668098, 108.61700898855057, 109.6631407623655, 110.5856387810932, 110.70927253618044, 108.34121061181752, 107.89422703573294, 109.56803787383686, 107.84667559146864, 108.72162216593205, 109.3683218079267, 109.0925234311937, 106.93368786159377, 103.719210229326, 104.56562593723083, 104.21374524967487, 104.97456835790392, 105.35497991201844, 105.85902522122022, 105.35497991201844, 104.13766293885195, 106.62935861830215, 106.13482359795324, 106.31551908615766, 104.81289344740526, 106.38209110812772, 105.60224742219292, 106.25845735304048, 108.19855627902456, 108.1890459901717, 109.84383625056992, 113.24851965989492, 109.6346098958069, 108.94035880954789, 113.42921514809929, 114.62751154356009, 113.64795179171516, 115.24568031899621, 116.56761046954416, 116.02552400493096, 115.49294782917065, 115.6266644409477, 115.15865629972794, 111.5292054086359, 110.89882709597256, 110.52633082030785, 107.29802976454704, 109.05067249748228, 108.58743994954024, 112.02586710952221, 113.44899390629247, 113.94565560717876, 112.46522169107544, 113.54450577184751, 112.73265491462958, 112.52252881040846, 112.99053695162821, 112.07362304229972, 111.06119726741615, 110.02966911942156, 113.68777357018013, 112.97143457851723, 112.92367864573968, 110.4308189547528, 110.95613421530558, 108.10032943520949, 107.43174637632411, 105.53106025177854, 106.3429111089965, 104.08883108189724, 101.27123104802315, 102.51288530023886, 102.4173734346838, 103.73543717934356, 103.18146835912424, 102.02577478590807, 103.85960260456513, 102.50333411368335, 100.53578968324926, 100.6217503622488, 98.1002371115954, 96.1804486139388, 92.12119432784904, 92.60830484217982, 94.10784113139415, 95.47366080883141, 93.01900586406654, 95.05340860038919, 92.7706750136234, 92.32176924551466, 92.44593467073624, 91.97792652951648, 96.86813404593521, 94.97699910794516, 95.50231436849792, 89.22718480153091, 89.8671143007498, 92.97124993128902, 92.10209195473804, 90.23961057641449, 92.025682462294, 92.76112382706788, 90.28365281802198, 91.23431029823729, 91.21510509661677, 90.52371783827834, 89.97636959209382, 90.2548450155912, 92.79953423030891, 94.22071915022673, 92.4346353995192, 92.22337818169359, 93.02999664975503, 90.92702707230907, 92.28099378655511, 92.914765440032, 93.0588044521858, 92.84754723436019, 96.53494594549831, 96.74620316332391, 97.46639822409307, 98.91639094644171, 97.82169445407257, 97.01507598601108, 97.10149939330336, 97.14951239735466, 98.19619588567251, 98.44586350673912, 100.42399927365177, 101.75876078627728, 101.59551657250292, 101.71074778222601, 101.70114518141571, 102.47895584704644, 101.91240239924136, 101.47068276196958, 101.00975792307732, 103.40080552483096, 105.206094477159, 104.65874623097444, 105.61900631199998, 106.70410020355885, 105.44615949741535, 106.55045859059477, 104.22662919451294, 104.34186040423599, 104.6875540334052, 106.05112334846147, 107.58753947810236, 107.64515508296387, 105.48456990065641, 103.20875350862585, 102.66140526244128, 102.87266248026691, 101.75876078627728, 101.48028536277988, 100.90412931416456, 100.20313945501587, 93.93264112591906, 91.06146348365269, 90.01477999533483, 89.91875398723228, 91.39755451201162, 90.44689703179633, 90.0819982010066, 89.5796103946518, 89.64723952243034, 90.25590167243713, 89.3767230113162, 87.28022005018167, 87.45412352161215, 90.70032165498178, 90.32353080021566, 91.3572903248304, 91.00948338196936, 91.99493638674228, 93.16395416691408, 94.58416585026329, 96.24591013282154, 97.00915314632212, 96.95118532251196, 96.47778142806222, 95.12519887249157, 94.41026237883275, 94.60348845819999, 95.28944103995373, 95.67589319868816, 95.58894146297293, 96.27489404472662, 95.48266711932095, 94.043132828035, 94.15906847565536, 93.84990674866778, 94.2460202113706, 92.10121073039429, 91.87900073912192, 92.66156636055923, 92.31375941769821, 92.84513113595811, 90.23657906450045, 88.9226417248032, 90.4201438398993, 91.2027094613366, 92.36206593754, 92.6422437526225, 91.77272639546995, 92.2944368097615, 92.69055027246435, 93.40548676612312, 93.69532588517401, 94.12042325978192, 93.58905154152201, 95.44402190344748, 95.43436059947912, 96.44879751615713, 96.4874427320306, 96.57439446774583, 96.06234535742266, 95.31842495185879, 94.043132828035, 93.39582546215479, 99.46312435428604, 100.80604560588837, 100.68044865429964, 102.45812858447823, 100.94130386144545, 102.20693468130085, 102.83491943924436, 104.39876396835727, 105.26324945339485, 105.69063553588532, 104.90385661130057, 104.83586337090435, 105.07869637231941, 106.34142797967763, 106.24429477911163, 106.088881658206, 105.95289517741355, 106.22486813899842, 105.39923593418726, 105.72948881611171, 104.93299657147035, 104.48618384886669, 103.87424468530077, 103.75768484462156, 102.96119259998018, 103.05832580054621, 103.67026496411215, 104.64159696977232, 104.61245700960251, 105.25353613333824, 102.49495323726327, 100.17346974373545, 102.41724667681049, 104.85529001101757, 108.56577827263949, 112.2568398941482, 111.62547409046907, 110.32388920288444, 110.3141758828278, 110.29474924271463, 111.33407448877102, 109.47883035796005, 109.64395679892228, 109.84793652011093, 110.6832820449787, 108.96402439496016, 109.80908323988452, 109.2942772768846, 109.76051663960152, 109.80908323988452, 110.62500212463907, 110.79012856560131, 112.72307925686508, 112.96591225828014, 113.97609754416678, 113.62641802212907, 114.2577838258082, 114.18007726535538, 114.10237070490255, 113.7624045029215, 113.7041245825819, 113.2573118599782, 114.2772104659214, 114.86000966931749, 112.2762665342614, 111.1980880079786, 110.45987568367686, 110.28503592265804, 108.29380531105465, 108.39093851162063, 107.23505342488501, 106.26844409327585, 107.8013498009793, 108.43599229142977, 108.26024514022808, 105.24325237793276, 105.86813113776093, 103.21239640849123, 104.57931869561534, 107.39127311484205, 107.3522181923528, 107.45961922919822, 109.09016224312485, 109.15850835748104, 108.60197571200912, 109.14874462685871, 108.9339425531678, 108.82654151632237, 107.90875083782473, 106.90308658372628, 107.30339953924124, 106.53206482007832, 107.3522181923528, 108.4067010995628, 109.47094773739514, 111.25771044127876, 110.62306795082829, 112.46841303844582, 112.46841303844582, 113.08352806765166, 113.22998402698641, 113.88415397868148, 114.18682962797324, 114.29423066481873, 113.54242340690048, 113.7669892112137, 114.489505277265, 114.00131874614927, 113.97202755428232, 113.08352806765166, 113.40573117818806, 113.27880268009797, 113.85486278681455, 115.1241477677155, 116.17863067492549, 116.29579544239328, 116.92067420222143, 116.43248767110569, 116.22744932803707, 117.16476746777931, 117.155003737157, 116.94996539408838, 117.16476746777931, 117.24287731275784, 117.13547627591237, 119.00034882477448, 119.05893120850841, 119.06869493913072, 118.75625555921663, 118.48287110179182, 125.70803176230488, 125.49322968861395, 126.03023487284128, 127.21164627814136, 128.42234887530844, 128.9202991370465, 129.8478535461664, 129.55368079232372, 130.70095453231022, 132.39735074613642, 132.8778329107462, 132.7160378961327, 133.08375383843608, 134.0447181676555, 134.4467542645739, 133.87802027381136, 134.00549513380986, 134.27025061226828, 134.32908516303684, 137.07469753223532, 136.26081957993722, 137.0648917737739, 136.6334384014713, 136.80994205377692, 136.3000426137829, 135.98625834301737, 136.4373232322428, 136.49615778301134, 136.2902368553215, 137.7316833491507, 137.95721579376342, 137.2708127014638, 138.712259195293, 137.12372632454245, 138.6730361614473, 138.18274823837615, 137.9081870014563, 138.14352520453042, 141.00680667526606, 141.3205909460316, 141.13428153526456, 140.86952605680608, 140.9087490906518, 141.95796524602414, 141.22253336141736, 140.86952605680608, 140.55574178604058, 140.38904389219636, 138.8789570891372, 139.0456549829814, 138.31022309837468, 139.07507225836568, 138.457309475296, 137.947410035302, 139.67322352451248, 139.5065256306683, 140.84991453988326, 141.72262704294994, 140.88913757372896, 140.9970009168046, 140.85972029834468, 143.73280752754172, 144.64474306445405, 144.20348393369002, 143.6837787352346, 146.06657804136043, 150.03791021823682, 150.99887454745632, 150.28305417977242, 151.57741429668027, 153.694279777277, 153.30044433902643, 153.07398896203242, 147.9344364928627, 150.18914437684708, 150.70113044657282, 151.61679784050534, 151.42972600733634, 150.97681525334818, 151.49864720903014, 151.2426541741673, 151.3017294899049, 150.4057538678849, 150.819281078048, 153.05429719011983, 151.55772252476774, 152.06970859449345, 152.97553010246975, 152.60138643613172, 146.68400897641718, 143.17887357598732, 144.33084223287017, 142.92288054112444, 142.0662884629295, 140.07741949976423, 144.08469508396357, 142.77519225178048, 143.62193844401918, 143.38563718106883, 144.025619768226, 143.5727090142379, 141.51491884937872, 143.58255490019414, 141.4656894195974, 141.8004495421104], "line": {"color": "black"}}], {"title": "Long and Short of AAPL Stock with 5 day signal window", "annotations": [{"x": "2013-10-21", "y": 68.11077987055458, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2013-11-27", "y": 71.74187026970324, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-04-24", "y": 75.0518119888347, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-05-05", "y": 79.43909846030984, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-05-19", "y": 80.3661103512034, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-05-29", "y": 84.45892124406228, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-06-09", "y": 87.18657566177792, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-07-07", "y": 89.29691881653686, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-07-23", "y": 90.4339731970992, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-08-18", "y": 92.72602277601385, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-09-02", "y": 96.59739968497615, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-10-23", "y": 98.02812593394049, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-10-31", "y": 100.99244110336326, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-11-12", "y": 104.48137998501022, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-11-24", "y": 111.4076737143536, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2015-02-10", "y": 115.04517604620136, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2015-02-20", "y": 122.09289519835148, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2015-10-23", "y": 113.24851965989492, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2015-11-03", "y": 116.56761046954416, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-03-16", "y": 101.75876078627728, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-03-29", "y": 103.40080552483096, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-07-27", "y": 99.46312435428604, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-08-04", "y": 102.83491943924436, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-08-15", "y": 106.34142797967763, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-09-14", "y": 108.56577827263949, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-01-09", "y": 116.17863067492549, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-01-25", "y": 119.00034882477448, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-02-07", "y": 128.42234887530844, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-02-15", "y": 132.8778329107462, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-03-01", "y": 137.07469753223532, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-03-15", "y": 137.7316833491507, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-03-28", "y": 141.00680667526606, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-05-01", "y": 143.73280752754172, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-05-09", "y": 150.99887454745632, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-01-28", "y": 66.55662922486023, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2015-07-08", "y": 116.0434845945406, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2015-08-03", "y": 112.1333957361295, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2015-08-21", "y": 100.58081490788116, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2015-12-18", "y": 101.27123104802315, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2015-12-31", "y": 100.53578968324926, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2016-05-12", "y": 87.28022005018167, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}]}, {"showLink": false, "linkText": "Export to plot.ly", "displayModeBar": false})});</script>



<div id="8743471b-25fb-4d15-b51b-6a11603609ed" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("8743471b-25fb-4d15-b51b-6a11603609ed", [{"type": "scatter", "name": "Index", "x": ["2013-07-01", "2013-07-02", "2013-07-03", "2013-07-05", "2013-07-08", "2013-07-09", "2013-07-10", "2013-07-11", "2013-07-12", "2013-07-15", "2013-07-16", "2013-07-17", "2013-07-18", "2013-07-19", "2013-07-22", "2013-07-23", "2013-07-24", "2013-07-25", "2013-07-26", "2013-07-29", "2013-07-30", "2013-07-31", "2013-08-01", "2013-08-02", "2013-08-05", "2013-08-06", "2013-08-07", "2013-08-08", "2013-08-09", "2013-08-12", "2013-08-13", "2013-08-14", "2013-08-15", "2013-08-16", "2013-08-19", "2013-08-20", "2013-08-21", "2013-08-22", "2013-08-23", "2013-08-26", "2013-08-27", "2013-08-28", "2013-08-29", "2013-08-30", "2013-09-03", "2013-09-04", "2013-09-05", "2013-09-06", "2013-09-09", "2013-09-10", "2013-09-11", "2013-09-12", "2013-09-13", "2013-09-16", "2013-09-17", "2013-09-18", "2013-09-19", "2013-09-20", "2013-09-23", "2013-09-24", "2013-09-25", "2013-09-26", "2013-09-27", "2013-09-30", "2013-10-01", "2013-10-02", "2013-10-03", "2013-10-04", "2013-10-07", "2013-10-08", "2013-10-09", "2013-10-10", "2013-10-11", "2013-10-14", "2013-10-15", "2013-10-16", "2013-10-17", "2013-10-18", "2013-10-21", "2013-10-22", "2013-10-23", "2013-10-24", "2013-10-25", "2013-10-28", "2013-10-29", "2013-10-30", "2013-10-31", "2013-11-01", "2013-11-04", "2013-11-05", "2013-11-06", "2013-11-07", "2013-11-08", "2013-11-11", "2013-11-12", "2013-11-13", "2013-11-14", "2013-11-15", "2013-11-18", "2013-11-19", "2013-11-20", "2013-11-21", "2013-11-22", "2013-11-25", "2013-11-26", "2013-11-27", "2013-11-29", "2013-12-02", "2013-12-03", "2013-12-04", "2013-12-05", "2013-12-06", "2013-12-09", "2013-12-10", "2013-12-11", "2013-12-12", "2013-12-13", "2013-12-16", "2013-12-17", "2013-12-18", "2013-12-19", "2013-12-20", "2013-12-23", "2013-12-24", "2013-12-26", "2013-12-27", "2013-12-30", "2013-12-31", "2014-01-02", "2014-01-03", "2014-01-06", "2014-01-07", "2014-01-08", "2014-01-09", "2014-01-10", "2014-01-13", "2014-01-14", "2014-01-15", "2014-01-16", "2014-01-17", "2014-01-21", "2014-01-22", "2014-01-23", "2014-01-24", "2014-01-27", "2014-01-28", "2014-01-29", "2014-01-30", "2014-01-31", "2014-02-03", "2014-02-04", "2014-02-05", "2014-02-06", "2014-02-07", "2014-02-10", "2014-02-11", "2014-02-12", "2014-02-13", "2014-02-14", "2014-02-18", "2014-02-19", "2014-02-20", "2014-02-21", "2014-02-24", "2014-02-25", "2014-02-26", "2014-02-27", "2014-02-28", "2014-03-03", "2014-03-04", "2014-03-05", "2014-03-06", "2014-03-07", "2014-03-10", "2014-03-11", "2014-03-12", "2014-03-13", "2014-03-14", "2014-03-17", "2014-03-18", "2014-03-19", "2014-03-20", "2014-03-21", "2014-03-24", "2014-03-25", "2014-03-26", "2014-03-27", "2014-03-28", "2014-03-31", "2014-04-01", "2014-04-02", "2014-04-03", "2014-04-04", "2014-04-07", "2014-04-08", "2014-04-09", "2014-04-10", "2014-04-11", "2014-04-14", "2014-04-15", "2014-04-16", "2014-04-17", "2014-04-21", "2014-04-22", "2014-04-23", "2014-04-24", "2014-04-25", "2014-04-28", "2014-04-29", "2014-04-30", "2014-05-01", "2014-05-02", "2014-05-05", "2014-05-06", "2014-05-07", "2014-05-08", "2014-05-09", "2014-05-12", "2014-05-13", "2014-05-14", "2014-05-15", "2014-05-16", "2014-05-19", "2014-05-20", "2014-05-21", "2014-05-22", "2014-05-23", "2014-05-27", "2014-05-28", "2014-05-29", "2014-05-30", "2014-06-02", "2014-06-03", "2014-06-04", "2014-06-05", "2014-06-06", "2014-06-09", "2014-06-10", "2014-06-11", "2014-06-12", "2014-06-13", "2014-06-16", "2014-06-17", "2014-06-18", "2014-06-19", "2014-06-20", "2014-06-23", "2014-06-24", "2014-06-25", "2014-06-26", "2014-06-27", "2014-06-30", "2014-07-01", "2014-07-02", "2014-07-03", "2014-07-07", "2014-07-08", "2014-07-09", "2014-07-10", "2014-07-11", "2014-07-14", "2014-07-15", "2014-07-16", "2014-07-17", "2014-07-18", "2014-07-21", "2014-07-22", "2014-07-23", "2014-07-24", "2014-07-25", "2014-07-28", "2014-07-29", "2014-07-30", "2014-07-31", "2014-08-01", "2014-08-04", "2014-08-05", "2014-08-06", "2014-08-07", "2014-08-08", "2014-08-11", "2014-08-12", "2014-08-13", "2014-08-14", "2014-08-15", "2014-08-18", "2014-08-19", "2014-08-20", "2014-08-21", "2014-08-22", "2014-08-25", "2014-08-26", "2014-08-27", "2014-08-28", "2014-08-29", "2014-09-02", "2014-09-03", "2014-09-04", "2014-09-05", "2014-09-08", "2014-09-09", "2014-09-10", "2014-09-11", "2014-09-12", "2014-09-15", "2014-09-16", "2014-09-17", "2014-09-18", "2014-09-19", "2014-09-22", "2014-09-23", "2014-09-24", "2014-09-25", "2014-09-26", "2014-09-29", "2014-09-30", "2014-10-01", "2014-10-02", "2014-10-03", "2014-10-06", "2014-10-07", "2014-10-08", "2014-10-09", "2014-10-10", "2014-10-13", "2014-10-14", "2014-10-15", "2014-10-16", "2014-10-17", "2014-10-20", "2014-10-21", "2014-10-22", "2014-10-23", "2014-10-24", "2014-10-27", "2014-10-28", "2014-10-29", "2014-10-30", "2014-10-31", "2014-11-03", "2014-11-04", "2014-11-05", "2014-11-06", "2014-11-07", "2014-11-10", "2014-11-11", "2014-11-12", "2014-11-13", "2014-11-14", "2014-11-17", "2014-11-18", "2014-11-19", "2014-11-20", "2014-11-21", "2014-11-24", "2014-11-25", "2014-11-26", "2014-11-28", "2014-12-01", "2014-12-02", "2014-12-03", "2014-12-04", "2014-12-05", "2014-12-08", "2014-12-09", "2014-12-10", "2014-12-11", "2014-12-12", "2014-12-15", "2014-12-16", "2014-12-17", "2014-12-18", "2014-12-19", "2014-12-22", "2014-12-23", "2014-12-24", "2014-12-26", "2014-12-29", "2014-12-30", "2014-12-31", "2015-01-02", "2015-01-05", "2015-01-06", "2015-01-07", "2015-01-08", "2015-01-09", "2015-01-12", "2015-01-13", "2015-01-14", "2015-01-15", "2015-01-16", "2015-01-20", "2015-01-21", "2015-01-22", "2015-01-23", "2015-01-26", "2015-01-27", "2015-01-28", "2015-01-29", "2015-01-30", "2015-02-02", "2015-02-03", "2015-02-04", "2015-02-05", "2015-02-06", "2015-02-09", "2015-02-10", "2015-02-11", "2015-02-12", "2015-02-13", "2015-02-17", "2015-02-18", "2015-02-19", "2015-02-20", "2015-02-23", "2015-02-24", "2015-02-25", "2015-02-26", "2015-02-27", "2015-03-02", "2015-03-03", "2015-03-04", "2015-03-05", "2015-03-06", "2015-03-09", "2015-03-10", "2015-03-11", "2015-03-12", "2015-03-13", "2015-03-16", "2015-03-17", "2015-03-18", "2015-03-19", "2015-03-20", "2015-03-23", "2015-03-24", "2015-03-25", "2015-03-26", "2015-03-27", "2015-03-30", "2015-03-31", "2015-04-01", "2015-04-02", "2015-04-06", "2015-04-07", "2015-04-08", "2015-04-09", "2015-04-10", "2015-04-13", "2015-04-14", "2015-04-15", "2015-04-16", "2015-04-17", "2015-04-20", "2015-04-21", "2015-04-22", "2015-04-23", "2015-04-24", "2015-04-27", "2015-04-28", "2015-04-29", "2015-04-30", "2015-05-01", "2015-05-04", "2015-05-05", "2015-05-06", "2015-05-07", "2015-05-08", "2015-05-11", "2015-05-12", "2015-05-13", "2015-05-14", "2015-05-15", "2015-05-18", "2015-05-19", "2015-05-20", "2015-05-21", "2015-05-22", "2015-05-26", "2015-05-27", "2015-05-28", "2015-05-29", "2015-06-01", "2015-06-02", "2015-06-03", "2015-06-04", "2015-06-05", "2015-06-08", "2015-06-09", "2015-06-10", "2015-06-11", "2015-06-12", "2015-06-15", "2015-06-16", "2015-06-17", "2015-06-18", "2015-06-19", "2015-06-22", "2015-06-23", "2015-06-24", "2015-06-25", "2015-06-26", "2015-06-29", "2015-06-30", "2015-07-01", "2015-07-02", "2015-07-06", "2015-07-07", "2015-07-08", "2015-07-09", "2015-07-10", "2015-07-13", "2015-07-14", "2015-07-15", "2015-07-16", "2015-07-17", "2015-07-20", "2015-07-21", "2015-07-22", "2015-07-23", "2015-07-24", "2015-07-27", "2015-07-28", "2015-07-29", "2015-07-30", "2015-07-31", "2015-08-03", "2015-08-04", "2015-08-05", "2015-08-06", "2015-08-07", "2015-08-10", "2015-08-11", "2015-08-12", "2015-08-13", "2015-08-14", "2015-08-17", "2015-08-18", "2015-08-19", "2015-08-20", "2015-08-21", "2015-08-24", "2015-08-25", "2015-08-26", "2015-08-27", "2015-08-28", "2015-08-31", "2015-09-01", "2015-09-02", "2015-09-03", "2015-09-04", "2015-09-08", "2015-09-09", "2015-09-10", "2015-09-11", "2015-09-14", "2015-09-15", "2015-09-16", "2015-09-17", "2015-09-18", "2015-09-21", "2015-09-22", "2015-09-23", "2015-09-24", "2015-09-25", "2015-09-28", "2015-09-29", "2015-09-30", "2015-10-01", "2015-10-02", "2015-10-05", "2015-10-06", "2015-10-07", "2015-10-08", "2015-10-09", "2015-10-12", "2015-10-13", "2015-10-14", "2015-10-15", "2015-10-16", "2015-10-19", "2015-10-20", "2015-10-21", "2015-10-22", "2015-10-23", "2015-10-26", "2015-10-27", "2015-10-28", "2015-10-29", "2015-10-30", "2015-11-02", "2015-11-03", "2015-11-04", "2015-11-05", "2015-11-06", "2015-11-09", "2015-11-10", "2015-11-11", "2015-11-12", "2015-11-13", "2015-11-16", "2015-11-17", "2015-11-18", "2015-11-19", "2015-11-20", "2015-11-23", "2015-11-24", "2015-11-25", "2015-11-27", "2015-11-30", "2015-12-01", "2015-12-02", "2015-12-03", "2015-12-04", "2015-12-07", "2015-12-08", "2015-12-09", "2015-12-10", "2015-12-11", "2015-12-14", "2015-12-15", "2015-12-16", "2015-12-17", "2015-12-18", "2015-12-21", "2015-12-22", "2015-12-23", "2015-12-24", "2015-12-28", "2015-12-29", "2015-12-30", "2015-12-31", "2016-01-04", "2016-01-05", "2016-01-06", "2016-01-07", "2016-01-08", "2016-01-11", "2016-01-12", "2016-01-13", "2016-01-14", "2016-01-15", "2016-01-19", "2016-01-20", "2016-01-21", "2016-01-22", "2016-01-25", "2016-01-26", "2016-01-27", "2016-01-28", "2016-01-29", "2016-02-01", "2016-02-02", "2016-02-03", "2016-02-04", "2016-02-05", "2016-02-08", "2016-02-09", "2016-02-10", "2016-02-11", "2016-02-12", "2016-02-16", "2016-02-17", "2016-02-18", "2016-02-19", "2016-02-22", "2016-02-23", "2016-02-24", "2016-02-25", "2016-02-26", "2016-02-29", "2016-03-01", "2016-03-02", "2016-03-03", "2016-03-04", "2016-03-07", "2016-03-08", "2016-03-09", "2016-03-10", "2016-03-11", "2016-03-14", "2016-03-15", "2016-03-16", "2016-03-17", "2016-03-18", "2016-03-21", "2016-03-22", "2016-03-23", "2016-03-24", "2016-03-28", "2016-03-29", "2016-03-30", "2016-03-31", "2016-04-01", "2016-04-04", "2016-04-05", "2016-04-06", "2016-04-07", "2016-04-08", "2016-04-11", "2016-04-12", "2016-04-13", "2016-04-14", "2016-04-15", "2016-04-18", "2016-04-19", "2016-04-20", "2016-04-21", "2016-04-22", "2016-04-25", "2016-04-26", "2016-04-27", "2016-04-28", "2016-04-29", "2016-05-02", "2016-05-03", "2016-05-04", "2016-05-05", "2016-05-06", "2016-05-09", "2016-05-10", "2016-05-11", "2016-05-12", "2016-05-13", "2016-05-16", "2016-05-17", "2016-05-18", "2016-05-19", "2016-05-20", "2016-05-23", "2016-05-24", "2016-05-25", "2016-05-26", "2016-05-27", "2016-05-31", "2016-06-01", "2016-06-02", "2016-06-03", "2016-06-06", "2016-06-07", "2016-06-08", "2016-06-09", "2016-06-10", "2016-06-13", "2016-06-14", "2016-06-15", "2016-06-16", "2016-06-17", "2016-06-20", "2016-06-21", "2016-06-22", "2016-06-23", "2016-06-24", "2016-06-27", "2016-06-28", "2016-06-29", "2016-06-30", "2016-07-01", "2016-07-05", "2016-07-06", "2016-07-07", "2016-07-08", "2016-07-11", "2016-07-12", "2016-07-13", "2016-07-14", "2016-07-15", "2016-07-18", "2016-07-19", "2016-07-20", "2016-07-21", "2016-07-22", "2016-07-25", "2016-07-26", "2016-07-27", "2016-07-28", "2016-07-29", "2016-08-01", "2016-08-02", "2016-08-03", "2016-08-04", "2016-08-05", "2016-08-08", "2016-08-09", "2016-08-10", "2016-08-11", "2016-08-12", "2016-08-15", "2016-08-16", "2016-08-17", "2016-08-18", "2016-08-19", "2016-08-22", "2016-08-23", "2016-08-24", "2016-08-25", "2016-08-26", "2016-08-29", "2016-08-30", "2016-08-31", "2016-09-01", "2016-09-02", "2016-09-06", "2016-09-07", "2016-09-08", "2016-09-09", "2016-09-12", "2016-09-13", "2016-09-14", "2016-09-15", "2016-09-16", "2016-09-19", "2016-09-20", "2016-09-21", "2016-09-22", "2016-09-23", "2016-09-26", "2016-09-27", "2016-09-28", "2016-09-29", "2016-09-30", "2016-10-03", "2016-10-04", "2016-10-05", "2016-10-06", "2016-10-07", "2016-10-10", "2016-10-11", "2016-10-12", "2016-10-13", "2016-10-14", "2016-10-17", "2016-10-18", "2016-10-19", "2016-10-20", "2016-10-21", "2016-10-24", "2016-10-25", "2016-10-26", "2016-10-27", "2016-10-28", "2016-10-31", "2016-11-01", "2016-11-02", "2016-11-03", "2016-11-04", "2016-11-07", "2016-11-08", "2016-11-09", "2016-11-10", "2016-11-11", "2016-11-14", "2016-11-15", "2016-11-16", "2016-11-17", "2016-11-18", "2016-11-21", "2016-11-22", "2016-11-23", "2016-11-25", "2016-11-28", "2016-11-29", "2016-11-30", "2016-12-01", "2016-12-02", "2016-12-05", "2016-12-06", "2016-12-07", "2016-12-08", "2016-12-09", "2016-12-12", "2016-12-13", "2016-12-14", "2016-12-15", "2016-12-16", "2016-12-19", "2016-12-20", "2016-12-21", "2016-12-22", "2016-12-23", "2016-12-27", "2016-12-28", "2016-12-29", "2016-12-30", "2017-01-03", "2017-01-04", "2017-01-05", "2017-01-06", "2017-01-09", "2017-01-10", "2017-01-11", "2017-01-12", "2017-01-13", "2017-01-17", "2017-01-18", "2017-01-19", "2017-01-20", "2017-01-23", "2017-01-24", "2017-01-25", "2017-01-26", "2017-01-27", "2017-01-30", "2017-01-31", "2017-02-01", "2017-02-02", "2017-02-03", "2017-02-06", "2017-02-07", "2017-02-08", "2017-02-09", "2017-02-10", "2017-02-13", "2017-02-14", "2017-02-15", "2017-02-16", "2017-02-17", "2017-02-21", "2017-02-22", "2017-02-23", "2017-02-24", "2017-02-27", "2017-02-28", "2017-03-01", "2017-03-02", "2017-03-03", "2017-03-06", "2017-03-07", "2017-03-08", "2017-03-09", "2017-03-10", "2017-03-13", "2017-03-14", "2017-03-15", "2017-03-16", "2017-03-17", "2017-03-20", "2017-03-21", "2017-03-22", "2017-03-23", "2017-03-24", "2017-03-27", "2017-03-28", "2017-03-29", "2017-03-30", "2017-03-31", "2017-04-03", "2017-04-04", "2017-04-05", "2017-04-06", "2017-04-07", "2017-04-10", "2017-04-11", "2017-04-12", "2017-04-13", "2017-04-17", "2017-04-18", "2017-04-19", "2017-04-20", "2017-04-21", "2017-04-24", "2017-04-25", "2017-04-26", "2017-04-27", "2017-04-28", "2017-05-01", "2017-05-02", "2017-05-03", "2017-05-04", "2017-05-05", "2017-05-08", "2017-05-09", "2017-05-10", "2017-05-11", "2017-05-12", "2017-05-15", "2017-05-16", "2017-05-17", "2017-05-18", "2017-05-19", "2017-05-22", "2017-05-23", "2017-05-24", "2017-05-25", "2017-05-26", "2017-05-30", "2017-05-31", "2017-06-01", "2017-06-02", "2017-06-05", "2017-06-06", "2017-06-07", "2017-06-08", "2017-06-09", "2017-06-12", "2017-06-13", "2017-06-14", "2017-06-15", "2017-06-16", "2017-06-19", "2017-06-20", "2017-06-21", "2017-06-22", "2017-06-23", "2017-06-26", "2017-06-27", "2017-06-28", "2017-06-29", "2017-06-30"], "y": [53.10917319210857, 54.31224741988544, 54.61204261580394, 54.17338124688422, 53.86579916276005, 54.81320389445057, 54.60295791289733, 55.45406479377765, 55.35309481004406, 55.47379157723203, 55.83133952734264, 55.846264396403505, 56.03418796510047, 55.1506357166965, 55.327138516025144, 54.377138154932744, 57.170035391368344, 56.90917463647821, 57.23233049701374, 58.11484449365696, 58.83253602328005, 58.730008661905316, 59.2680826369175, 60.02912117755218, 60.9259111359058, 60.38082896150852, 60.345787964582975, 60.22638901209596, 59.36939000574175, 61.05595359903942, 63.95747005195509, 65.12408607737322, 65.04700842283833, 65.62443763138795, 66.33120053144529, 65.45983111492357, 65.62835683416091, 65.70674088962014, 65.45329911030197, 65.70804729054446, 63.82944276137168, 64.13069881451997, 64.23573344883532, 63.64994327437006, 63.82813636044736, 65.14903833502774, 64.70211857881773, 65.08750685149226, 66.126095586327, 64.61981532058553, 61.101677631390636, 61.75226529170222, 60.734578971656596, 58.803718405511006, 59.48304688615764, 60.70583815132154, 61.701315655653715, 61.062485603661024, 64.09725495085738, 63.89606920851203, 62.90712370880146, 63.51982574230775, 63.06650462156856, 62.2826640669763, 63.74713950313949, 63.95616365103077, 63.1527270825737, 63.10308384744953, 63.71970508372877, 62.83004605426657, 63.567901296322745, 63.96635357824047, 64.38100523161978, 64.80271144999041, 65.147601294011, 65.46557927899059, 65.90792663196548, 66.48143663774215, 68.11077987055458, 67.91553825241489, 68.58082292312507, 69.48877156552777, 68.71120173537224, 69.22304961752099, 67.4988616776029, 68.57246195720941, 68.28583759441352, 67.9367672674351, 68.81466868857844, 68.64470592832434, 68.45148923161734, 67.34400794611464, 68.40418343394518, 68.20549908372212, 68.3319106875016, 68.4139074034667, 69.40286138480192, 68.98643896029337, 68.15044039143146, 68.27146439047607, 67.67357166989737, 68.47987271022065, 68.3043156388595, 68.82205131338262, 70.09142355091893, 71.74187026970324, 73.07037475432978, 72.43437458562627, 74.4175387480381, 74.24382134658644, 74.62502723282792, 73.5894244787882, 74.43173048733973, 74.31609409303, 73.76550717012347, 73.65775507542577, 72.85487056493436, 73.25828389508307, 72.92845736131329, 72.37392828860072, 71.54476277940256, 72.14396954991659, 74.91267276367337, 74.59467267932162, 74.09927585369927, 73.59862282833556, 72.86669701435241, 73.72082947232198, 72.68404407334043, 71.087473401905, 71.47511813282965, 70.96362419549942, 71.41335778586878, 70.5012757257508, 70.0309772538934, 70.39759718585265, 71.79837441692275, 73.23988719598835, 72.83121766609828, 71.04673785390953, 72.15053979959329, 72.47116798381572, 73.08482930361849, 71.75632481899196, 72.33844894034661, 66.55662922486023, 65.801050512041, 65.67385047830028, 65.78133976301092, 65.90354640699735, 66.85754666005259, 67.35688563548096, 67.74715846627629, 68.6949392436332, 69.92560019721661, 70.8469435749262, 70.84165609499674, 71.96656744999079, 71.90840517076668, 72.17277916724002, 71.03332724243992, 70.21112411340782, 69.43122082381146, 69.7352509197558, 69.00954429943647, 68.38694353774177, 69.7511133595442, 69.56208595206577, 69.76301018938551, 70.22302094324913, 70.37107038127421, 70.15824931411316, 70.1172713446598, 70.18072110381338, 70.86412788469698, 70.93286512378005, 70.14503061428947, 69.35719610479893, 69.62817945118411, 70.244170862967, 70.22566468321386, 69.88726596772797, 70.43848575037491, 71.27390757923067, 72.04059216900335, 71.3518979081903, 71.04522407228124, 70.96591187333921, 70.95004943355082, 71.59908759489285, 71.71805589330587, 71.22103277993598, 70.2996894022264, 69.19592796695021, 69.19196235700309, 70.10140890487139, 69.19724983693257, 68.68568615375665, 68.95931324010654, 68.4675643879663, 68.60637395481464, 69.3902428543581, 70.21376785337256, 70.28369477543976, 69.36512732469313, 75.0518119888347, 75.60303177148164, 78.5309737824239, 78.29832466552736, 78.00222578947721, 78.18596571702619, 78.33137141508655, 79.43909846030984, 78.57327362185963, 78.29832466552736, 78.15952831737886, 77.83419039401828, 78.80289319953012, 78.9265149640757, 78.9411368932155, 78.26985741907009, 79.42498982111438, 80.3661103512034, 80.38206154662863, 80.59474415229845, 80.72235371570036, 81.63423038750979, 83.16288661576172, 82.94754547752102, 84.45892124406228, 84.14255586812841, 83.56432503396353, 84.74604276171655, 85.71374861751431, 86.05005298772974, 85.81344358892204, 87.18657566177792, 87.69834318167095, 87.3354534857468, 85.87458983805213, 84.93479857424855, 85.79084606206962, 85.67918769409295, 85.77223633407354, 85.47448068613575, 84.59051860632049, 84.51607969433606, 84.00431217444302, 84.07875108642745, 84.58121374232246, 85.58613905411241, 86.47010113392767, 87.01908810981291, 86.98186865382071, 87.49363617371374, 89.29691881653686, 88.72187822145702, 88.75909767744926, 88.4287750055183, 88.60091498948229, 89.74541326124313, 88.69396362946286, 88.19150097356787, 86.61888590925655, 87.86583073363596, 87.40896191133145, 88.13567178957955, 90.4339731970992, 90.28509537313032, 90.88153715540571, 92.13676330874331, 91.5412520128678, 91.32724014091251, 88.95449982140842, 89.44765761330534, 88.94519495741038, 88.50786634950177, 88.35898852553288, 88.34968366153483, 88.59281361233921, 89.76170760659109, 89.74300530268307, 90.93060160084299, 91.17373155164742, 91.62258684544013, 92.72602277601385, 94.00713059371395, 94.04453520153002, 94.05388635348405, 94.74587159808115, 94.95159694106951, 94.34283694886312, 95.50331490635638, 95.61552872980455, 95.84930752865496, 96.59739968497615, 92.52029743302558, 91.75350297279631, 92.5483508888876, 91.97793061969269, 91.63193799739412, 94.44663473555269, 94.84873426957529, 95.06381076451768, 95.03575730865565, 94.31571860819643, 94.98900154888555, 95.18537573991988, 94.40923012773659, 94.50274164727678, 95.98022365601116, 95.1479711321038, 91.51972417394596, 94.21285593670228, 93.61438221164534, 94.21285593670228, 92.7447250799219, 93.41800802061104, 93.1561757658986, 93.1561757658986, 92.34262554589928, 94.25961169647238, 94.46533703946068, 94.19415363279428, 93.33384765302489, 92.34262554589928, 91.21113615946345, 90.01418870934951, 91.33270113486564, 93.2870918932548, 95.82125407279293, 96.30751397440169, 98.02812593394049, 98.39282086014704, 98.28995818865288, 99.81419595715737, 100.37526507439829, 100.03862360405373, 100.99244110336326, 102.30160237692543, 101.55351022060415, 101.79664017140855, 102.086525881983, 102.37766500823341, 102.20861648331379, 103.02568435375841, 104.48137998501022, 105.95585878569756, 107.23311430731206, 107.05467419767471, 108.44462873590228, 107.693301958482, 109.23352185219362, 109.38378720767768, 111.4076737143536, 110.44503628078384, 111.75985814126936, 111.69411704824509, 108.06896534719215, 107.65573561961098, 108.876641632919, 108.4634119053378, 108.00322425416788, 105.56141222755191, 107.17676479900557, 105.138790915253, 104.82886861956713, 103.05385910791166, 101.64042560788971, 100.25047106966215, 102.75332839694352, 105.79620184549576, 104.97913397505116, 106.0685578023106, 105.69289441360044, 105.19514042355951, 107.05467419767471, 106.97954151993272, 105.67411124416495, 103.66431211456565, 102.67819571920151, 99.78558762613336, 99.79497921085111, 101.19432533379644, 105.08244140694643, 105.19514042355951, 102.60306304145948, 103.5140467590816, 103.11960020093592, 100.32090795504531, 99.54140642347177, 102.10530905141852, 102.88481058299207, 105.56141222755191, 106.10612414118162, 106.21882315779465, 102.4997556095642, 108.29436338041825, 111.66594229409183, 110.03180655320268, 111.4123695067125, 111.43115267614799, 112.28578688546358, 113.08407158647265, 112.13180451708513, 112.87664707630907, 115.04517604620136, 117.74169467832836, 119.23137979677614, 119.81593977996452, 120.52306879188593, 121.35748102595319, 121.10762877507428, 122.09289519835148, 125.39754478073088, 124.6149886742045, 121.42819392714532, 122.96030678630841, 121.11705716189994, 121.71104553191392, 121.96561197620562, 121.19248425650486, 119.18423786264805, 119.36337721233481, 119.87251010091822, 117.39284436578043, 115.25260055636498, 117.33627404482678, 116.52543277782353, 117.80769338610772, 119.77822623266205, 121.12648554872551, 120.20721783322772, 118.7033901345415, 119.93850880869756, 119.44823269376538, 116.32743665448551, 117.13827792148876, 116.20486762575248, 119.14652431534556, 117.31741727117551, 117.14770630831435, 118.15654369865558, 120.0705062242562, 118.8071023896233, 118.42053852977293, 119.32566366503237, 119.83479655361576, 119.59908688297527, 119.08052560756624, 119.53308817519594, 118.9579565788332, 117.61912564959532, 120.30621589489668, 119.65565720392898, 121.26791135110982, 122.25789196779978, 122.83302356416254, 125.06755124183422, 123.09701839527989, 121.28676812476105, 117.99626112262008, 121.57904811635521, 121.34333844571476, 118.60910626628531, 117.86426370706141, 118.59024949263409, 120.82458598315468, 119.59380740786793, 119.16303490651752, 119.30031405529951, 122.08376714094813, 121.9133516459084, 123.2577405512217, 123.1441302211952, 123.134662693693, 124.3938438514864, 125.48260951424012, 122.71809148359593, 125.01396690288091, 124.76307742407243, 123.34294829874152, 123.58437025004778, 123.03998741867096, 123.19146785870623, 122.47193576853859, 121.79974131588196, 120.99500147819441, 120.63523543311058, 122.01749444843271, 121.7429361508687, 120.39854724555543, 120.16185905800027, 120.80565092815027, 120.52162510308409, 121.07074169821207, 119.85889817792969, 120.81511845565252, 120.26600186052454, 121.2884948307628, 120.71097565312824, 120.00091109046276, 117.899119984973, 118.74646369642043, 119.85889817792969, 119.70741773789436, 119.29084652779731, 118.99735317522892, 116.0434845945406, 113.67660271898909, 116.71567904719723, 118.96895059272232, 118.92161295521127, 120.0671837829782, 121.66719593085104, 122.71809148359593, 125.03763572163643, 123.7879220913452, 118.55237938262523, 118.495574217612, 117.87071740246635, 116.23283514458471, 116.8103543222193, 116.44112074963327, 115.85413404449648, 114.84110860176042, 112.1333957361295, 108.53573528529114, 109.2552673754588, 109.49195556301396, 109.86285682827562, 113.85717814647816, 107.9322681911444, 109.59656874039543, 109.51097614071968, 110.28130953780159, 111.42254420014518, 110.79486513585621, 109.3778320967796, 107.13340392750388, 100.58081490788116, 98.07009865072528, 98.65973655960278, 104.31835842705635, 107.3901817265312, 107.74206241408714, 107.2380171048854, 102.44483152304231, 106.83858497306512, 104.96505806905107, 103.91892629523613, 106.81005410650654, 104.75583171428808, 107.05732161668098, 108.61700898855057, 109.6631407623655, 110.5856387810932, 110.70927253618044, 108.34121061181752, 107.89422703573294, 109.56803787383686, 107.84667559146864, 108.72162216593205, 109.3683218079267, 109.0925234311937, 106.93368786159377, 103.719210229326, 104.56562593723083, 104.21374524967487, 104.97456835790392, 105.35497991201844, 105.85902522122022, 105.35497991201844, 104.13766293885195, 106.62935861830215, 106.13482359795324, 106.31551908615766, 104.81289344740526, 106.38209110812772, 105.60224742219292, 106.25845735304048, 108.19855627902456, 108.1890459901717, 109.84383625056992, 113.24851965989492, 109.6346098958069, 108.94035880954789, 113.42921514809929, 114.62751154356009, 113.64795179171516, 115.24568031899621, 116.56761046954416, 116.02552400493096, 115.49294782917065, 115.6266644409477, 115.15865629972794, 111.5292054086359, 110.89882709597256, 110.52633082030785, 107.29802976454704, 109.05067249748228, 108.58743994954024, 112.02586710952221, 113.44899390629247, 113.94565560717876, 112.46522169107544, 113.54450577184751, 112.73265491462958, 112.52252881040846, 112.99053695162821, 112.07362304229972, 111.06119726741615, 110.02966911942156, 113.68777357018013, 112.97143457851723, 112.92367864573968, 110.4308189547528, 110.95613421530558, 108.10032943520949, 107.43174637632411, 105.53106025177854, 106.3429111089965, 104.08883108189724, 101.27123104802315, 102.51288530023886, 102.4173734346838, 103.73543717934356, 103.18146835912424, 102.02577478590807, 103.85960260456513, 102.50333411368335, 100.53578968324926, 100.6217503622488, 98.1002371115954, 96.1804486139388, 92.12119432784904, 92.60830484217982, 94.10784113139415, 95.47366080883141, 93.01900586406654, 95.05340860038919, 92.7706750136234, 92.32176924551466, 92.44593467073624, 91.97792652951648, 96.86813404593521, 94.97699910794516, 95.50231436849792, 89.22718480153091, 89.8671143007498, 92.97124993128902, 92.10209195473804, 90.23961057641449, 92.025682462294, 92.76112382706788, 90.28365281802198, 91.23431029823729, 91.21510509661677, 90.52371783827834, 89.97636959209382, 90.2548450155912, 92.79953423030891, 94.22071915022673, 92.4346353995192, 92.22337818169359, 93.02999664975503, 90.92702707230907, 92.28099378655511, 92.914765440032, 93.0588044521858, 92.84754723436019, 96.53494594549831, 96.74620316332391, 97.46639822409307, 98.91639094644171, 97.82169445407257, 97.01507598601108, 97.10149939330336, 97.14951239735466, 98.19619588567251, 98.44586350673912, 100.42399927365177, 101.75876078627728, 101.59551657250292, 101.71074778222601, 101.70114518141571, 102.47895584704644, 101.91240239924136, 101.47068276196958, 101.00975792307732, 103.40080552483096, 105.206094477159, 104.65874623097444, 105.61900631199998, 106.70410020355885, 105.44615949741535, 106.55045859059477, 104.22662919451294, 104.34186040423599, 104.6875540334052, 106.05112334846147, 107.58753947810236, 107.64515508296387, 105.48456990065641, 103.20875350862585, 102.66140526244128, 102.87266248026691, 101.75876078627728, 101.48028536277988, 100.90412931416456, 100.20313945501587, 93.93264112591906, 91.06146348365269, 90.01477999533483, 89.91875398723228, 91.39755451201162, 90.44689703179633, 90.0819982010066, 89.5796103946518, 89.64723952243034, 90.25590167243713, 89.3767230113162, 87.28022005018167, 87.45412352161215, 90.70032165498178, 90.32353080021566, 91.3572903248304, 91.00948338196936, 91.99493638674228, 93.16395416691408, 94.58416585026329, 96.24591013282154, 97.00915314632212, 96.95118532251196, 96.47778142806222, 95.12519887249157, 94.41026237883275, 94.60348845819999, 95.28944103995373, 95.67589319868816, 95.58894146297293, 96.27489404472662, 95.48266711932095, 94.043132828035, 94.15906847565536, 93.84990674866778, 94.2460202113706, 92.10121073039429, 91.87900073912192, 92.66156636055923, 92.31375941769821, 92.84513113595811, 90.23657906450045, 88.9226417248032, 90.4201438398993, 91.2027094613366, 92.36206593754, 92.6422437526225, 91.77272639546995, 92.2944368097615, 92.69055027246435, 93.40548676612312, 93.69532588517401, 94.12042325978192, 93.58905154152201, 95.44402190344748, 95.43436059947912, 96.44879751615713, 96.4874427320306, 96.57439446774583, 96.06234535742266, 95.31842495185879, 94.043132828035, 93.39582546215479, 99.46312435428604, 100.80604560588837, 100.68044865429964, 102.45812858447823, 100.94130386144545, 102.20693468130085, 102.83491943924436, 104.39876396835727, 105.26324945339485, 105.69063553588532, 104.90385661130057, 104.83586337090435, 105.07869637231941, 106.34142797967763, 106.24429477911163, 106.088881658206, 105.95289517741355, 106.22486813899842, 105.39923593418726, 105.72948881611171, 104.93299657147035, 104.48618384886669, 103.87424468530077, 103.75768484462156, 102.96119259998018, 103.05832580054621, 103.67026496411215, 104.64159696977232, 104.61245700960251, 105.25353613333824, 102.49495323726327, 100.17346974373545, 102.41724667681049, 104.85529001101757, 108.56577827263949, 112.2568398941482, 111.62547409046907, 110.32388920288444, 110.3141758828278, 110.29474924271463, 111.33407448877102, 109.47883035796005, 109.64395679892228, 109.84793652011093, 110.6832820449787, 108.96402439496016, 109.80908323988452, 109.2942772768846, 109.76051663960152, 109.80908323988452, 110.62500212463907, 110.79012856560131, 112.72307925686508, 112.96591225828014, 113.97609754416678, 113.62641802212907, 114.2577838258082, 114.18007726535538, 114.10237070490255, 113.7624045029215, 113.7041245825819, 113.2573118599782, 114.2772104659214, 114.86000966931749, 112.2762665342614, 111.1980880079786, 110.45987568367686, 110.28503592265804, 108.29380531105465, 108.39093851162063, 107.23505342488501, 106.26844409327585, 107.8013498009793, 108.43599229142977, 108.26024514022808, 105.24325237793276, 105.86813113776093, 103.21239640849123, 104.57931869561534, 107.39127311484205, 107.3522181923528, 107.45961922919822, 109.09016224312485, 109.15850835748104, 108.60197571200912, 109.14874462685871, 108.9339425531678, 108.82654151632237, 107.90875083782473, 106.90308658372628, 107.30339953924124, 106.53206482007832, 107.3522181923528, 108.4067010995628, 109.47094773739514, 111.25771044127876, 110.62306795082829, 112.46841303844582, 112.46841303844582, 113.08352806765166, 113.22998402698641, 113.88415397868148, 114.18682962797324, 114.29423066481873, 113.54242340690048, 113.7669892112137, 114.489505277265, 114.00131874614927, 113.97202755428232, 113.08352806765166, 113.40573117818806, 113.27880268009797, 113.85486278681455, 115.1241477677155, 116.17863067492549, 116.29579544239328, 116.92067420222143, 116.43248767110569, 116.22744932803707, 117.16476746777931, 117.155003737157, 116.94996539408838, 117.16476746777931, 117.24287731275784, 117.13547627591237, 119.00034882477448, 119.05893120850841, 119.06869493913072, 118.75625555921663, 118.48287110179182, 125.70803176230488, 125.49322968861395, 126.03023487284128, 127.21164627814136, 128.42234887530844, 128.9202991370465, 129.8478535461664, 129.55368079232372, 130.70095453231022, 132.39735074613642, 132.8778329107462, 132.7160378961327, 133.08375383843608, 134.0447181676555, 134.4467542645739, 133.87802027381136, 134.00549513380986, 134.27025061226828, 134.32908516303684, 137.07469753223532, 136.26081957993722, 137.0648917737739, 136.6334384014713, 136.80994205377692, 136.3000426137829, 135.98625834301737, 136.4373232322428, 136.49615778301134, 136.2902368553215, 137.7316833491507, 137.95721579376342, 137.2708127014638, 138.712259195293, 137.12372632454245, 138.6730361614473, 138.18274823837615, 137.9081870014563, 138.14352520453042, 141.00680667526606, 141.3205909460316, 141.13428153526456, 140.86952605680608, 140.9087490906518, 141.95796524602414, 141.22253336141736, 140.86952605680608, 140.55574178604058, 140.38904389219636, 138.8789570891372, 139.0456549829814, 138.31022309837468, 139.07507225836568, 138.457309475296, 137.947410035302, 139.67322352451248, 139.5065256306683, 140.84991453988326, 141.72262704294994, 140.88913757372896, 140.9970009168046, 140.85972029834468, 143.73280752754172, 144.64474306445405, 144.20348393369002, 143.6837787352346, 146.06657804136043, 150.03791021823682, 150.99887454745632, 150.28305417977242, 151.57741429668027, 153.694279777277, 153.30044433902643, 153.07398896203242, 147.9344364928627, 150.18914437684708, 150.70113044657282, 151.61679784050534, 151.42972600733634, 150.97681525334818, 151.49864720903014, 151.2426541741673, 151.3017294899049, 150.4057538678849, 150.819281078048, 153.05429719011983, 151.55772252476774, 152.06970859449345, 152.97553010246975, 152.60138643613172, 146.68400897641718, 143.17887357598732, 144.33084223287017, 142.92288054112444, 142.0662884629295, 140.07741949976423, 144.08469508396357, 142.77519225178048, 143.62193844401918, 143.38563718106883, 144.025619768226, 143.5727090142379, 141.51491884937872, 143.58255490019414, 141.4656894195974, 141.8004495421104], "line": {"color": "black"}}], {"title": "Long and Short of AAPL Stock with 10 day signal window", "annotations": [{"x": "2013-10-21", "y": 68.11077987055458, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2013-11-27", "y": 71.74187026970324, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-04-24", "y": 75.0518119888347, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-05-19", "y": 80.3661103512034, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-06-04", "y": 85.71374861751431, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-07-07", "y": 89.29691881653686, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-07-23", "y": 90.4339731970992, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-08-18", "y": 92.72602277601385, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-10-23", "y": 98.02812593394049, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-11-12", "y": 104.48137998501022, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2015-02-10", "y": 115.04517604620136, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2015-10-23", "y": 113.24851965989492, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-03-16", "y": 101.75876078627728, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-04-04", "y": 106.70410020355885, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-07-27", "y": 99.46312435428604, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-08-15", "y": 106.34142797967763, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2016-09-14", "y": 108.56577827263949, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-01-09", "y": 116.17863067492549, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-01-25", "y": 119.00034882477448, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-02-09", "y": 129.8478535461664, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-03-01", "y": 137.07469753223532, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-03-20", "y": 138.712259195293, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-04-04", "y": 141.95796524602414, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2017-05-01", "y": 143.73280752754172, "text": "Long", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 20}, {"x": "2014-01-28", "y": 66.55662922486023, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2015-07-08", "y": 116.0434845945406, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2015-08-03", "y": 112.1333957361295, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2015-08-21", "y": 100.58081490788116, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2015-12-18", "y": 101.27123104802315, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2016-01-06", "y": 96.1804486139388, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}, {"x": "2016-05-12", "y": 87.28022005018167, "text": "Short", "bgcolor": "#9dbdd5", "ayref": "y", "ax": 0, "ay": 160}]}, {"showLink": false, "linkText": "Export to plot.ly", "displayModeBar": false})});</script>


## Lookahead Close Prices
With the trading signal done, we can start working on evaluating how many days to short or long the stocks. In this problem, implement `get_lookahead_prices` to get the close price days ahead in time. You can get the number of days from the variable `lookahead_days`. We'll use the lookahead prices to calculate future returns in another problem.


```python
def get_lookahead_prices(close, lookahead_days):
    """
    Get the lookahead prices for `lookahead_days` number of days.
    
    Parameters
    ----------
    close : DataFrame
        Close price for each ticker and date
    lookahead_days : int
        The number of days to look ahead
    
    Returns
    -------
    lookahead_prices : DataFrame
        The lookahead prices for each ticker and date
    """
    #TODO: Implement function
    lookahead_prices = close.shift(-lookahead_days)
    return lookahead_prices

project_tests.test_get_lookahead_prices(get_lookahead_prices)
```

### View Data
Using the `get_lookahead_prices` function, let's generate lookahead closing prices for 5, 10, and 20 days.

Let's also chart a subsection of a few months of the Apple stock instead of years. This will allow you to view the differences between the 5, 10, and 20 day lookaheads. Otherwise, they will mesh together when looking at a chart that is zoomed out.


```python
lookahead_5 = get_lookahead_prices(close, 5)
lookahead_10 = get_lookahead_prices(close, 10)
lookahead_20 = get_lookahead_prices(close, 20)
project_helper.plot_lookahead_prices(
    close[apple_ticker].iloc[150:250],
    [
        (lookahead_5[apple_ticker].iloc[150:250], 5),
        (lookahead_10[apple_ticker].iloc[150:250], 10),
        (lookahead_20[apple_ticker].iloc[150:250], 20)],
    '5, 10, and 20 day Lookahead Prices for Slice of {} Stock'.format(apple_ticker))
```

## Lookahead Price Returns
Implement `get_return_lookahead` to generate the log price return between the closing price and the lookahead price.


```python
def get_return_lookahead(close, lookahead_prices):
    """
    Calculate the log returns from the lookahead days to the signal day.
    
    Parameters
    ----------
    close : DataFrame
        Close price for each ticker and date
    lookahead_prices : DataFrame
        The lookahead prices for each ticker and date
    
    Returns
    -------
    lookahead_returns : DataFrame
        The lookahead log returns for each ticker and date
    """
    #TODO: Implement function
    
    return np.log(lookahead_prices/close)

project_tests.test_get_return_lookahead(get_return_lookahead)
```

### View Data
Using the same lookahead prices and same subsection of the Apple stock from the previous problem, we'll view the lookahead returns.

In order to view price returns on the same chart as the stock, a second y-axis will be added. When viewing this chart, the axis for the price of the stock will be on the left side, like previous charts. The axis for price returns will be located on the right side.


```python
price_return_5 = get_return_lookahead(close, lookahead_5)
price_return_10 = get_return_lookahead(close, lookahead_10)
price_return_20 = get_return_lookahead(close, lookahead_20)
project_helper.plot_price_returns(
    close[apple_ticker].iloc[150:250],
    [
        (price_return_5[apple_ticker].iloc[150:250], 5),
        (price_return_10[apple_ticker].iloc[150:250], 10),
        (price_return_20[apple_ticker].iloc[150:250], 20)],
    '5, 10, and 20 day Lookahead Returns for Slice {} Stock'.format(apple_ticker))
```

## Compute the Signal Return
Using the price returns generate the signal returns.


```python
def get_signal_return(signal, lookahead_returns):
    """
    Compute the signal returns.
    
    Parameters
    ----------
    signal : DataFrame
        The long, short, and do nothing signals for each ticker and date
    lookahead_returns : DataFrame
        The lookahead log returns for each ticker and date
    
    Returns
    -------
    signal_return : DataFrame
        Signal returns for each ticker and date
    """
    #TODO: Implement function
    
    return signal*lookahead_returns

project_tests.test_get_signal_return(get_signal_return)
```

### View Data
Let's continue using the previous lookahead prices to view the signal returns. Just like before, the axis for the signal returns is on the right side of the chart.


```python
title_string = '{} day LookaheadSignal Returns for {} Stock'
signal_return_5 = get_signal_return(signal_5, price_return_5)
signal_return_10 = get_signal_return(signal_10, price_return_10)
signal_return_20 = get_signal_return(signal_20, price_return_20)
project_helper.plot_signal_returns(
    close[apple_ticker],
    [
        (signal_return_5[apple_ticker], signal_5[apple_ticker], 5),
        (signal_return_10[apple_ticker], signal_10[apple_ticker], 10),
        (signal_return_20[apple_ticker], signal_20[apple_ticker], 20)],
    [title_string.format(5, apple_ticker), title_string.format(10, apple_ticker), title_string.format(20, apple_ticker)])
```

## Test for Significance
### Histogram
Let's plot a histogram of the signal return values.


```python
project_helper.plot_signal_histograms(
    [signal_return_5, signal_return_10, signal_return_20],
    'Signal Return',
    ('5 Days', '10 Days', '20 Days'))
```

### Question: What do the histograms tell you about the signal returns?

*#TODO: Put Answer In this Cell*
Looks like the returns are normal in nature and probably falls under 2standard deviation but needs to check them through formula to be sure and looks like the graph has two peaks need to check for outliers also

## Outliers
You might have noticed the outliers in the 10 and 20 day histograms. To better visualize the outliers, let's compare the 5, 10, and 20 day signals returns to normal distributions with the same mean and deviation for each signal return distributions.


```python
project_helper.plot_signal_to_normal_histograms(
    [signal_return_5, signal_return_10, signal_return_20],
    'Signal Return',
    ('5 Days', '10 Days', '20 Days'))
```

## Kolmogorov-Smirnov Test
While you can see the outliers in the histogram, we need to find the stocks that are causing these outlying returns. We'll use the Kolmogorov-Smirnov Test or KS-Test. This test will be applied to teach ticker's signal returns where a long or short signal exits.


```python
# Filter out returns that don't have a long or short signal.
long_short_signal_returns_5 = signal_return_5[signal_5 != 0].stack()
long_short_signal_returns_10 = signal_return_10[signal_10 != 0].stack()
long_short_signal_returns_20 = signal_return_20[signal_20 != 0].stack()

# Get just ticker and signal return
long_short_signal_returns_5 = long_short_signal_returns_5.reset_index().iloc[:, [1,2]]
long_short_signal_returns_5.columns = ['ticker', 'signal_return']
long_short_signal_returns_10 = long_short_signal_returns_10.reset_index().iloc[:, [1,2]]
long_short_signal_returns_10.columns = ['ticker', 'signal_return']
long_short_signal_returns_20 = long_short_signal_returns_20.reset_index().iloc[:, [1,2]]
long_short_signal_returns_20.columns = ['ticker', 'signal_return']

# View some of the data
long_short_signal_returns_5.head(10)
```

This gives you the data to use in the KS-Test.

Now it's time to implement the function `calculate_kstest` to use Kolmogorov-Smirnov test (KS test) between a distribution of stock returns (the input dataframe in this case) and each stock's signal returns. Run KS test on a normal distribution against each stock's signal returns. Use [`scipy.stats.kstest`](https://docs.scipy.org/doc/scipy-0.14.0/reference/generated/scipy.stats.kstest.html#scipy-stats-kstest) perform the KS test. When calculating the standard deviation of the signal returns, make sure to set the delta degrees of freedom to 0.

For this function, we don't reccommend you try to find a vectorized solution. Instead, you should iterate over the [`groupby`](https://pandas.pydata.org/pandas-docs/version/0.21/generated/pandas.DataFrame.groupby.html) function.


```python
from scipy.stats import kstest


def calculate_kstest(long_short_signal_returns):
    """
    Calculate the KS-Test against the signal returns with a long or short signal.
    
    Parameters
    ----------
    long_short_signal_returns : DataFrame
        The signal returns which have a signal.
        This DataFrame contains two columns, "ticker" and "signal_return"
    
    Returns
    -------
    ks_values : Pandas Series
        KS static for all the tickers
    p_values : Pandas Series
        P value for all the tickers
    """
    #TODO: Implement function
    ticker_list = []
    ks_list = []
    p_list = []
    population_mean = long_short_signal_returns['signal_return'].mean()
    population_std = long_short_signal_returns['signal_return'].std(ddof = 0)
    
    grouped_returns = long_short_signal_returns.groupby(['ticker'])
    for name, group in grouped_returns:
        ks, p = kstest(group['signal_return'].values, 'norm', args = (population_mean, population_std))
        ticker_list.append(name)
        ks_list.append(ks)
        p_list.append(p)
    
    ks_values = pd.Series(ks_list, index=ticker_list)
    p_values = pd.Series(p_list, index=ticker_list)
    return ks_values, p_values

project_tests.test_calculate_kstest(calculate_kstest)
```

    Tests Passed


### View Data
Using the signal returns we created above, let's calculate the ks and p values.


```python
ks_values_5, p_values_5 = calculate_kstest(long_short_signal_returns_5)
ks_values_10, p_values_10 = calculate_kstest(long_short_signal_returns_10)
ks_values_20, p_values_20 = calculate_kstest(long_short_signal_returns_20)

print('ks_values_5')
print(ks_values_5.head(10))
print('p_values_5')
print(p_values_5.head(10))
```

## Find Outliers
With the ks and p values calculate, let's find which symbols are the outliers. Implement the `find_outliers` function to find the following outliers:
- Symbols that pass the null hypothesis with a p-value less than `pvalue_threshold` **AND** with a KS value above `ks_threshold`.

*Note: your function should return symbols that meet both requirements above.*


```python
def find_outliers(ks_values, p_values, ks_threshold, pvalue_threshold=0.05):
    """
    Find outlying symbols using KS values and P-values
    
    Parameters
    ----------
    ks_values : Pandas Series
        KS static for all the tickers
    p_values : Pandas Series
        P value for all the tickers
    ks_threshold : float
        The threshold for the KS statistic
    pvalue_threshold : float
        The threshold for the p-value
    
    Returns
    -------
    outliers : set of str
        Symbols that are outliers
    """
    #TODO: Implement function
    
    ks_index = ks_values[(ks_values > ks_threshold)].index
    p_index = p_values[(p_values < pvalue_threshold)].index
    
    return set(ks_index) & set(p_index)


project_tests.test_find_outliers(find_outliers)
```

    Tests Passed


### View Data
Using the `find_outliers` function you implemented, let's see what we found.


```python
ks_threshold = 0.8
outliers_5 = find_outliers(ks_values_5, p_values_5, ks_threshold)
outliers_10 = find_outliers(ks_values_10, p_values_10, ks_threshold)
outliers_20 = find_outliers(ks_values_20, p_values_20, ks_threshold)

outlier_tickers = outliers_5.union(outliers_10).union(outliers_20)
print('{} Outliers Found:\n{}'.format(len(outlier_tickers), ', '.join(list(outlier_tickers))))
```

### Show Significance without Outliers
Let's compare the 5, 10, and 20 day signals returns without outliers to normal distributions. Also, let's see how the P-Value has changed with the outliers removed.


```python
good_tickers = list(set(close.columns) - outlier_tickers)

project_helper.plot_signal_to_normal_histograms(
    [signal_return_5[good_tickers], signal_return_10[good_tickers], signal_return_20[good_tickers]],
    'Signal Return Without Outliers',
    ('5 Days', '10 Days', '20 Days'))
```

That's more like it! The returns are closer to a normal distribution. You have finished the research phase of a Breakout Strategy. You can now submit your project.
## Submission
Now that you're done with the project, it's time to submit it. Click the submit button in the bottom right. One of our reviewers will give you feedback on your project with a pass or not passed grade. You can continue to the next section while you wait for feedback.
