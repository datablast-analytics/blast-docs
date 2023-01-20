# Athena

Query below is named `aws.events` and it is a `Athena SQL task` that will run in Blast-Scheduler. 

```sql
-- @blast.name: aws.events
-- @blast.type: athena.sql
-- @blast.parameters.database: datablast_core_model
-- @blast.parameters.s3_file_path: s3://path/to/s3/dt={{ ds }}/
-- @blast.depends: aws.sensor

CREATE TABLE IF NOT EXISTS aws.events
(
    dt date,
    app string,
    platform string,
    player_id string
)
PARTITIONED BY (dt date)
STORED AS ORC
LOCATION 's3://path/to/s3'
;

MSCK REPAIR TABLE aws.events;

INSERT INTO aws.events
SELECT
    dt,
    app,
    platform,
    player_id
FROM aws.raw_events_table
WHERE dt = {{ ds }} -- no dash date format
```
