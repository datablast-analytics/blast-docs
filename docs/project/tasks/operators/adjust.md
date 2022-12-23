## Adjust Export to BigQuery
This operator exports data from Adjust Report Services to a table in BigQuery has the dimensions and metrics specified.

```yaml
name: adjust-export-task
type: adjust.export.bq

connections:
    gcpConnectionId: gcp-connection-id
    adjust: adjust-token-id

adjust:
  report_service: # this needs to be included for `Report Service API`.
    refresh_days: 5
    dimensions:
      - day
      - os_name
      - device_type
      - app
      - currency_code
      - network
    metrics:
      - clicks
      - impressions
      - installs
      - non_organic_installs
      - organic_installs
      - ad_impressions
      - ecpm
      - ad_revenue
    filters:
        os_name: ios, android # filtering platforms

output:
  bigquery:
    project: my-project
    dataset: my_dataset
    table: my_adjust_report_table
```
For more information about Adjust Report Service API, [click here.](https://help.adjust.com/vi/article/report-service-api)

- `name`: Name of the task.
- `type`:For this operator it **MUST** be `adjust.export.bq`. 
- `connections`: Google Cloud and Adjust ids to be used by the operator. 
- `adjust`: These parameters are operator specific. `report_service` key **MUST** be included.
  - `refresh_days`: How many days should be refreshed on every run. Data provided by Adjust services can be delayed.  
  - `dimensions`: Dimensions wanted on the report table. For more information about which dimensions are available [Adjust Dimensions](https://help.adjust.com/en/article/reports-endpoint#dimensions).
  - `metrics`: Metrics wanted on the report table. For more information about which metrics are available [Adjust Metrics](https://help.adjust.com/en/article/reports-endpoint#metrics).
  - `filters`: Filters to be used. For more information about which filter are available [Adjust Filters](https://help.adjust.com/en/article/reports-endpoint#filters).
- `output`: Where to export the data. Currently only supports `BigQuery` therefore `bigquery` key **MUST** be included. 
  -  `project`: Bigquery project of the output table.
  -  `dataset`: Schema/Dataset of the output table.
  -  `table`: Name of the output table.
