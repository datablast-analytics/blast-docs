## `SQL Tasks`
Blast-Scheduler currently supports 3 SQL dialects for SQL tasks which are `BigQuery`, `Snowflake` and `Athena`. The corresponding task types are as follows:

```
bq.sql → BigQuery
sf.sql → Snowflake
athena.sql → AWS Athena
```

#### 1. `Creating a SQL task from comments`

To create a SQL task from comments, you need to define your task information on top of your `.sql` file. 

```
-- @blast.name: datablast-project.events
-- @blast.type: bq.sql
-- @blast.depends: core.model
-- @blast.depends: main.data
-- @blast.parameters.a_parameter: my_parameter
-- @blast.connections.a_connection: my_connection

SELECT * FROM MY_TABLE
```

#### 2. `Creating a SQL task from YAML`
By defining your task information in a `.yml` file you can create a SQL task. 

```
name: my_task
run: sql_file.sql
type: bq.sql

depends:
    - core.model
    - main.data

parameters:
    a_parameter: my_parameter

connections:
    gcp_conn: my_gcp_conn_id
    slack: my_slack_conn_id	
```
