## Athena Query Sensor

Athena sensor is a sensor that checks if the data is available in Amazon Athena. The task type of the sensor is `athena.sensor.query` which checks the data with provided query in `parameters/query`.

``` yaml
name: aws.events_sensor
type: athena.sensor.query
parameters:
  region: "us-east-1"
  query: "SELECT COUNT(*) FROM raw_data WHERE processdate = {{ ds_nodash }} LIMIT 1;"
  database: "datablast_core_model"
  output_location: "s3://s3-output-loc/"
```
