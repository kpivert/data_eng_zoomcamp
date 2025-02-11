# data_eng_zoomcamp
Homework for January 2025 Cohort of Data Engineering Zoomcamp 

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


