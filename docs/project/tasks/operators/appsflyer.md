## Appsflyer Export to BigQuery
This operator exports aggregate data from Appsflyer to a table in BigQuery.

```yaml
name: appsflyer-geo-by-date-report
type: appsflyer.export.bq

connections:
    gcpConnectionId: gcp-connection-id
    appsflyer: appsflyer-token-id

appsflyer:
  apps:
    - app1_id # id specified in Appsflyer
    - app2_id
  report_type: geo_by_date_report
  refresh_days: 30
  reattribution: False # If not specified defaults to `False`
  events: 
    - level_completion_5
    - level_completion_10
    - ad_interstitial_completion
  
output:
  bigquery:
    project: my-project
    dataset: my_dataset
    table: my_report_table
```
For more information about aggregate data API Appsflyer provides, [click here.](https://support.appsflyer.com/hc/en-us/articles/207034346-Using-Pull-API-aggregate-data)

- `name`: Name of the task.
- `type`:For this operator it **MUST** be `appsflyer.export.bq`. 
- `connections`: Google Cloud and Appsflyer ids to be used by the operator. 
- `appsflyer`: These parameters are operator specific.
    - `apps`: App ID's of the app(s) that reports will generated.
    - `report_type`: Type of report that want to be produced. For more information about report types provided by Appsflyer, [click here.](https://support.appsflyer.com/hc/en-us/articles/360005437257-Aggregated-and-analytics-reporting-overview). Available report types for the operator are shown in the table below.

        | Report                  | Dimensions                                    | Event Support |
        |-------------------------|-----------------------------------------------|---------------|
        | daily_report            | Date, agency, media source, campaign          | No            |
        | partners_by_date_report | Date, agency, media source, campaign          | Yes           |
        | geo_by_date_report      | Date, country, agency, media source, campaign | Yes           |
        | installs_report         | This is a raw report.                         | No            |
    - `refresh_days`: How many days should be refreshed on every run. Data provided by Appsflyer services can be delayed. **Note**: Be careful of the rate limits of the API service provided by Appsflyer. For more information about rate limits, [click here.](https://support.appsflyer.com/hc/en-us/articles/207034366-Report-generation-quotas-rate-limitations-) 
    - `reattribution`: If set to True, retargeting report will be generated. For more information about retargeting reports, [click here.](https://support.appsflyer.com/hc/en-us/articles/360005437257-Aggregated-and-analytics-reporting-overview#retargeting)
    - `events`: Which event's metrics should be included to the report. Not all reports support event metrics.

- `output`: Where to export the data. Currently only supports `BigQuery` therefore `bigquery` key **MUST** be included. 
  -  `project`: Bigquery project of the output table.
  -  `dataset`: Schema/Dataset of the output table.
  -  `table`: Name of the output table.
