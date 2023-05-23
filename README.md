```python
!pip show sqlalchemy
```

    Name: SQLAlchemy
    Version: 1.4.46
    Summary: Database Abstraction Library
    Home-page: https://www.sqlalchemy.org
    Author: Mike Bayer
    Author-email: mike_mp@zzzcomputing.com
    License: MIT
    Location: c:\users\hp\appdata\local\programs\python\python37\lib\site-packages
    Requires: greenlet, importlib-metadata
    Required-by: alembic, mlflow
    


```python
import zipfile
with zipfile.ZipFile('./archive_4.zip', 'r') as zip_ref:
    zip_ref.extractall('./')
```

## Save A CSV file to postgreSQL using SQLAlchemy

```python
import pandas as pd
from sqlalchemy import create_engine

# Load the CSV file into a Pandas DataFrame
df = pd.read_csv('path/to/csv/file.csv')

# Establish a connection to the PostgreSQL database using SQLAlchemy
engine = create_engine('postgresql://username:password@hostname/database_name')

# Save the DataFrame to the PostgreSQL database
df.to_sql('table_name', engine, if_exists='replace', index=False)
```
Make sure to replace `username`, `password`, `hostname`, and `database_name` with your database credentials.
Make sure to replace `table_nam` with the name of the table you want to create or replace in the database.

The `if_exists` parameter specifies what to do if the table already exists in the database. You can set it to `replace` to replace the table, `append` to append the data to the existing table, or `fail` to raise an error if the table already exists.

The index parameter specifies whether to include the DataFrame index as a column in the table. If you set it to False, the index will be excluded.


```python
header2015=['country', 'region', 'happiness_rank', 'happiness_score',
           'standard_error', 'economy', 'family',
           'life_expectancy', 'freedom', 'government_corruption',
           'generosity', 'dystopia_residual']

header2016=['country', 'region', 'happiness_rank', 'happiness_score',
           'lowerconfidenceinterval', 'upperconfidenceinterval',
           'economy', 'family', 'life_expectancy', 'freedom', 'government_corruption',
           'generosity', 'dystopia_residual']

header2017=['country', 'happiness_rank', 'happiness_score', 'lowerconfidenceinterval','upperconfidenceinterval', 
            'economy', 'family','life_expectancy', 'freedom', 'generosity',
            'government_corruption', 'dystopia_residual']

header2018=['overall_rank', 'country', 'happiness_score', 'economy','social_support', 'life_expectancy',
            'freedom', 'generosity','government_corruption']

header2019=['overall_rank', 'country', 'happiness_score', 'economy',
             'social_support', 'life_expectancy',
            'freedom', 'generosity','government_corruption']
```


```python
import pandas as pd
from sqlalchemy import create_engine

# Load the CSV file into a Pandas DataFrame
df = pd.read_csv('2015.csv',header=0, names=header2015)

# Establish a connection to the PostgreSQL database using SQLAlchemy
engine = create_engine('postgresql://postgres:password@localhost/datacamp')

# Save the DataFrame to the PostgreSQL database
df.to_sql('socialind2015', engine, if_exists='replace', index=False)
```


```python

# Load the CSV file into a Pandas DataFrame
df = pd.read_csv('2016.csv',header=0, names=header2016)

# Save the DataFrame to the PostgreSQL database
df.to_sql('socialind2016', engine, if_exists='replace', index=False)
```


```python
# Load the CSV file into a Pandas DataFrame
df = pd.read_csv('2017.csv',header=0, names=header2017)

# Save the DataFrame to the PostgreSQL database
df.to_sql('socialind2017', engine, if_exists='replace', index=False)
```


```python
# Load the CSV file into a Pandas DataFrame
df = pd.read_csv('2018.csv',header=0, names=header2018)

# Save the DataFrame to the PostgreSQL database
df.to_sql('socialind2018', engine, if_exists='replace', index=False)
```


```python
# Load the CSV file into a Pandas DataFrame
df = pd.read_csv('2019.csv',header=0, names=header2019)

# Save the DataFrame to the PostgreSQL database
df.to_sql('socialind2019', engine, if_exists='replace', index=False)
```

## Query postgreSQL using pandas and SQLAlchemy

To read data from a PostgreSQL database into Python, you can use the `read_sql_query` function from the Pandas library. This function allows you to execute a SQL query and return the results as a Pandas DataFrame.

Here's an example:
```python
import pandas as pd
from sqlalchemy import create_engine

# Establish a connection to the PostgreSQL database using SQLAlchemy
engine = create_engine('postgresql://username:password@hostname/database_name')

# Execute a SQL query and store the results in a Pandas DataFrame
query = 'SELECT * FROM table_name'
df = pd.read_sql_query(query, engine)

# Display the results
print(df.head())
```
In this example, the `create_engine` function is used to create a connection to the PostgreSQL database. Replace `username`, `password`, `hostname`, and `database_name` with your database credentials.

The `read_sql_quer` function is then used to execute a SQL `query` and store the results in a Pandas DataFrame. Replace `table_name` with the name of the table you want to query.

Finally, the `head` function is used to display the first few rows of the DataFrame. You can modify the query to select specific columns or apply filters to the data, as needed.

Note that you can also use the `read_sql_table` function to read an entire table into a Pandas DataFrame, like this:
```python
df = pd.read_sql_table('table_name', engine)
```


```python
# Execute a SQL query and store the results in a Pandas DataFrame
query = '''
SELECT *
FROM socialind2015;
'''
df = pd.read_sql_query(query, engine)

# Display the results
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
      <th>country</th>
      <th>region</th>
      <th>happiness_rank</th>
      <th>happiness_score</th>
      <th>standard_error</th>
      <th>economy</th>
      <th>family</th>
      <th>life_expectancy</th>
      <th>freedom</th>
      <th>government_corruption</th>
      <th>generosity</th>
      <th>dystopia_residual</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Switzerland</td>
      <td>Western Europe</td>
      <td>1</td>
      <td>7.587</td>
      <td>0.03411</td>
      <td>1.39651</td>
      <td>1.34951</td>
      <td>0.94143</td>
      <td>0.66557</td>
      <td>0.41978</td>
      <td>0.29678</td>
      <td>2.51738</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Iceland</td>
      <td>Western Europe</td>
      <td>2</td>
      <td>7.561</td>
      <td>0.04884</td>
      <td>1.30232</td>
      <td>1.40223</td>
      <td>0.94784</td>
      <td>0.62877</td>
      <td>0.14145</td>
      <td>0.43630</td>
      <td>2.70201</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Denmark</td>
      <td>Western Europe</td>
      <td>3</td>
      <td>7.527</td>
      <td>0.03328</td>
      <td>1.32548</td>
      <td>1.36058</td>
      <td>0.87464</td>
      <td>0.64938</td>
      <td>0.48357</td>
      <td>0.34139</td>
      <td>2.49204</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Norway</td>
      <td>Western Europe</td>
      <td>4</td>
      <td>7.522</td>
      <td>0.03880</td>
      <td>1.45900</td>
      <td>1.33095</td>
      <td>0.88521</td>
      <td>0.66973</td>
      <td>0.36503</td>
      <td>0.34699</td>
      <td>2.46531</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Canada</td>
      <td>North America</td>
      <td>5</td>
      <td>7.427</td>
      <td>0.03553</td>
      <td>1.32629</td>
      <td>1.32261</td>
      <td>0.90563</td>
      <td>0.63297</td>
      <td>0.32957</td>
      <td>0.45811</td>
      <td>2.45176</td>
    </tr>
  </tbody>
</table>
</div>




```python
engine.dispose()
```

## Premier League Database


```python
import pandas as pd

df = pd.read_csv('./season-1819_csv.csv')
df = df.rename(columns={'Date':'date',
                        'HomeTeam':'home_team',
                        'AwayTeam':'away_team',
                        'FTHG':'fthg',
                        'FTAG':'ftag',
                        'FTR':'ftr',
                        'HTHG':'hthg',
                        'HTAG':'htag',
                        'HTR':'htr',
                        'Referee':'referee', 
                        'HS':'hs', 
                        'AS':'as', 
                        'HST':'hst', 
                        'AST':'ast', 
                        'HF':'hf', 
                        'AF':'af', 
                        'HC':'hc'             
           })
```


```python
# Establish a connection to the PostgreSQL database using SQLAlchemy
engine = create_engine('postgresql://postgres:postgres@localhost/premier_league')
```


```python
# Save the DataFrame to the PostgreSQL database
df.to_sql('premier', engine, if_exists='replace', index=False)
```


```python
engine.dispose()
```