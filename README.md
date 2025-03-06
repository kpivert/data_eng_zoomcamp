# data_eng_zoomcamp
Homework for January 2025 Cohort of Data Engineering Zoomcamp \

## Week 5

spark.version = 3.4.4

## Week 4

### Question 1

`select * from myproject.my_nyc_tripdata.ext_green_taxi`

### Question 2

Update the WHERE clause to pickup_datetime >= CURRENT_DATE - INTERVAL '{{ env_var("DAYS_BACK", var("days_back", "30")) }}' DAY

### Question 3

`dbt run --select +models/core/`

### Question 4

Setting a value for DBT_BIGQUERY_TARGET_DATASET env var is mandatory, or it'll fail to compile\
When using core, it materializes in the dataset defined in DBT_BIGQUERY_TARGET_DATASET\
When using staging, it materializes in the dataset defined in DBT_BIGQUERY_STAGING_DATASET, or defaults to DBT_BIGQUERY_TARGET_DATASET

### Question 5

green: {best: 2020/Q1, worst: 2020/Q2}, yellow: {best: 2020/Q1, worst: 2020/Q2}

### Question 6

green: {p97: 55.0, p95: 45.0, p90: 26.5}, yellow: {p97: 31.5, p95: 25.5, p90: 19.0}

## Week 3

### Question 1
```
create or replace external table `dezc-kestra.de_zoomcamp.module_3_hw_yellow_tripdata`
OPTIONS (
  format = 'PARQUET',
  uris = ['gs://kap-kestra-dezc-bucket/yellow_tripdata_2024-*.parquet']
);

-- Create a regular table from external table
CREATE OR REPLACE TABLE `dezc-kestra.de_zoomcamp.module_3_hw_yellow_tripdata_regular` AS
SELECT * FROM `dezc-kestra.de_zoomcamp.module_3_hw_yellow_tripdata`;

-- Question 1

select count(1) as num_rows
from `dezc-kestra.de_zoomcamp.module_3_hw_yellow_tripdata`;
```

**Answer: 20,332,093**

### Question 2

```
select count(distinct PULocationID) as `Unique PU Location IDs`
from `dezc-kestra.de_zoomcamp.module_3_hw_yellow_tripdata`;

select count(distinct PULocationID) as `Unique PU Location IDs`
from `dezc-kestra.de_zoomcamp.module_3_hw_yellow_tripdata_regular`;
```

**Answer: 0B and 155.12 MB**


### Question 3

```
select PULocationID 
from `dezc-kestra.de_zoomcamp.module_3_hw_yellow_tripdata_regular`;

select PULocationID, DOLocationID
from `dezc-kestra.de_zoomcamp.module_3_hw_yellow_tripdata_regular`;
```

**Answer: A. BigQuery is a columnar database...**

### Question 4

```
select count(1) as `0 Fares`
from `dezc-kestra.de_zoomcamp.module_3_hw_yellow_tripdata_regular`
where fare_amount = 0;
```

**Answer: 8,333 records** 

### Question 5

```
create or replace table `dezc-kestra.de_zoomcamp.module_3_hw_yellow_tripdata_partition_cluster`
partition by date(tpep_dropoff_datetime)
cluster by VendorID as 
select * from `dezc-kestra.de_zoomcamp.module_3_hw_yellow_tripdata_regular`;
```

**Answer: A. Partition on `tpep_dropoff_datetime` and cluster on `VendorID`

### Question 6

```
select distinct(VendorID) 
from `dezc-kestra.de_zoomcamp.module_3_hw_yellow_tripdata_regular`
where date(tpep_dropoff_datetime) between '2024-03-01' and '2024-03-15';

select distinct(VendorID)
from `dezc-kestra.de_zoomcamp.module_3_hw_yellow_tripdata_partition_cluster`
where date(tpep_dropoff_datetime) between '2024-03-01' and '2024-03-15';
```

**Answer: B. 310.24 MB and 26.48 MB**

### Question 7 

**C. GCP Bucket**

### Question 8

**Answer: False**

### Question 9

**0 MB, because it's only using metadata and not actually querying the data.**




