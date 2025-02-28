# 🚕Ingesting New York Taxi Data to Postgres
This project aims to manage and analyze New York Taxi data by storing it in PostgreSQL database. 

## 📍The main processes in this project include:
1. **Running PostgreSQL with Docker**, Setting up the database environtment using containers
2. **Downloading the Dataset**, Fetching New York Taxi data from reliable sources
3. **Data Transformation**, Using Jupyter Notebook to converting time formats and adjusting the data schema to fit PostgreSQL
4. **Connecting to PostgreSQL**, Using SQLAlchemy to interact with the database
5. **Uploading Data to PostgreSQL**, Storing data in the defines tables and verifying the upload results

## 🗃️Dataset
Data sources : (https://github.com/DataTalksClub/nyc-tlc-data/releases/download/yellow/yellow_tripdata_2021-01.csv.gz)

## ✅Step by Step
1. **Running PostgreSQL with Docker**
Run PostgreSQL using Docker with the following commnad in your terminal:
```
  docker run -it \
  -e POSTGRES_USER='root' \
  -e POSTGRES_PASSWORD='root' \
  -e POSTGRES_DB='ny_taxi' \
  -v $(pwd)/ny_taxi_postgres_data:/var/lib/postgresql/data \
  -p 5432:5432 \
  postgres:13
```
After executing the command, a folder named `ny_taxi_postgres_data` will be created
2. **Accesing the PostgreSQL Container**
Enter the PostgreSQL Container by run this command:
``` docker exec -it <container_id> bash ```
3. **Downloading teh Dataset**
Downloading data from the sources
4. Data Transformation with Jupyter Notebook
Create a Jupyter Notebook file `uploaded_data.ipynb` to transform data before uploading it to PostgreSQL
a. Displaying the DataFrame as an SQL query
```pyhton
import pandas as pd
print(pd.io.sql.get_schema(df, name='yellow_taxi_data'))
```
b. Converting data text to timestamp format
```pyhton
df.tpep_pickup_datetime = pd.to_datetime(df.tpep_pickup_datetime)
df.tpep_dropoff_datetime = pd.to_datetime(df.tpep_dropoff_datetime)
```
c. Use SQLAlchemy to create a connection to PostgreSQL
```pyhton
from sqlalchemy import create_engine
engine = create_engine('postgresql://root:root@localhost:5432/ny_taxi')
engine.connect()
```
d. Generating DDL Statement by create table schema in a format compatible with PostgreSQL
```pyhton
print(pd.io.sql.get_schema(df, name='yellow_taxi_data', con=engine))
```
now we get the data types that compatible with PostgreSQL 
5. **Verifying Table Structure in PostgreSQL**
Run this command to access the database and view the table structure:
```pgcli -h [localhost](http://localhost) -p 5432 -u root -d ny_taxi```
View the table structure:
```\d yellow_taxi_data;```
6. **Uploading Data to PostgreSQL**
Insert data into PostgreSQL:
```%time df.to_sql(name='yellow_taxi_data', con=engine, if_exists='append')```
After uploading the data, verify the number of records in the table:
```SELECT COUNT(1) FROM yellow_taxi_data;```
New Yotk taxi data is successfully ingested into PostgreSQL🎉
