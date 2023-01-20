## BigQuery Table Sensor

BigQuery sensor is a sensor that checks if the data is available in a Google BigQuery table. The task type of the sensor is `bigquery.sensor.table` which checks if the new data is available on a BigQuery table which its location is provided in `parameters`.

``` yaml
name: gcp.events_sensor
type: bq.sensor.table
parameters:
  project_id: datablast
  dataset_id: core_model
  table_id: events_{{ ds_nodash }}
```
