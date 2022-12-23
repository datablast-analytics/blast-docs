## BigQuery Cost Tracker Operator
This operator provides daily notifications about the usage of projects on Google BigQuery. It sends daily reports to your Slack or Discord channels. It also sends alerts if costs are surpassed the thresholds specified. 

```yaml
name: cost-task
type: bq.cost_tracker

connections:
  gcpConnectionId: my-gcp-connection-id
  slack: slack-connection-id
  discord: discord-connection-id

parameters:
  report_time: 12 # UTC
  total_threshold: 150 # USD
  hourly_threshold: 20 # USD
  projects: project1, project2, project3 # You can specify multiple projects as comma seperated values.
```

- `name`: Name of the task.
- `type`: For this operator it **MUST** be `bq.cost_tracker`. 
- `connections`: Google Cloud, Slack and Discord connections to be used by the operator. 
- `parameters`: These parameters are operator speficic and 
  - `report_time`: What time the reports should be sent in UTC.
  - `total_threshold`: Total daily threshold for spendings.
  - `hourly_threshold`: Hourly threshold for spendings.
  - `projects`: Single or multiple comma seperated project names.
  - `user_list_length`: How many users to be shown on the report. Optional, Defaults to 5.
  - `project_list_length`: How many projects to be shown on the report. Optional, Defaults to 5.

Notifications received will look like this:
```
+-------+---------+-------+
| User  | Cost($) |     % |
+-------+---------+-------+
| user1 |    5.48 | 75.92 |
| user2 |    0.86 | 11.89 |
| user3 |    0.86 | 11.85 |
| user4 |    0.02 |  0.31 |
+-------+---------+-------+

+----------+---------+-------+
| Project  | Cost($) |     % |
+----------+---------+-------+
| project1 |    5.49 | 75.95 |
| project2 |    1.71 | 23.74 |
| project3 |    0.02 |  0.27 |
+----------+---------+-------+
```

_**Important Note**_: Service account used in _`gcpConnectionId` must have `BigQuery Resource Viewer` permission on every project speficied in `projects` parameter._
