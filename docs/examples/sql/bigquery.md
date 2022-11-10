# BigQuery Tasks

Query below is named `gcp.events` and it is a `Bigquery SQL task` that will run in Blast-Scheduler.

```sql
-- @blast.name: gcp.events
-- @blast.type: bq.sql

DECLARE end_dt DATE DEFAULT '{{ ds }}';
DECLARE start_dt DATE DEFAULT DATE_SUB(end_dt, INTERVAL 3 DAY);

CREATE TABLE IF NOT EXISTS my_schema.events_table
(
    user_id STRING,
    event_date DATE,
    event_name STRING,
    event_value INT64
)
PARTITION BY event_date
CLUSTER BY event_name
OPTIONS(REQUIRE_PARTITION_FILTER = True)
;

DELETE FROM my_schema.events_table WHERE dt BETWEEN start_dt AND end_dt;

INSERT INTO my_schema.events_table
SELECT
    user_id,
    event_date,
    event_name,
    event_value
FROM my_schema.raw_events_table
WHERE event_date BETWEEN start_dt AND end_dt
;
```

Below query is named `gcp.users`, it is another `Bigquery SQL Task`, but it depends `gcp.events`. Which means `gcp.events` must be successful for `gcp.users` to run.
```sql
-- @blast.name: gcp.users
-- @blast.type: bq.sql
-- @blast.depends: gcp.events

CREATE OR REPLACE TABLE my_schema.users
SELECT
    user_id,
    event_name,
    event_date,
    SUM(event_value) AS event_value
FROM my_schema.events_table
GROUP BY 1,2,3
;
```

This is created from a `.yml` file. This task will look for a SQL script named `totals.sql` in the project. You can speficy full path of where your script is located but it is advised to keep the scripts and task generator `.yml` file together under a folder to keep project organized.

```yaml
name: gcp.totals
type: bq.sql
run: totals.sql

depends:
  - gcp.users
```

This is how the `totals.sql` looks like:

```sql
CREATE OR REPLACE TABLE my_schema.total
SELECT
    SUM(event_value)
FROM my_schema.users
;
```

This is how the final pipeline looks like:

![Image](/assets/gcp_pipe.png "a title")
