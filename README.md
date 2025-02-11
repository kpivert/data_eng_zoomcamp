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

-- Question 1

select count(1) as num_rows
from `dezc-kestra.de_zoomcamp.module_3_hw_yellow_tripdata`;
```

**Answer: 20,332,093**
