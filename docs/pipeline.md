## `pipeline.yml`

`pipeline.yml` contains all the necessary information to build a data pipeline.

Here's an example `pipeline.yml` file for a pipeline called `marketing`:

```yaml
id: marketing 
schedule: "0 4 * * *"      # run it at 4am every day
start_date: "2022-09-01"   # start the pipeline at 2022-09-01, useful for triggering backfills

default_connections:       # define the default connections for tasks under this block
    gcp: "your-connection-id" 

notifications:             # define the preferred notifications under this section
    slack:
        - name: data-team
          connection: "slack-data-team"
          success: ":tada: Pipeline has finished successfully!"
          failure: ":red_circle: Pipeline has failed!"
        
        - name: marketing-team    
          connection: "slack-marketing-team"             # you can send notifications to different webhooks
          failure: ":red_circle: Pipeline has failed!"   # you don't have to define success or failure in every case
```

`pipeline.yml` consists of 5 arguments as can be seen from the above example.

- `id`: Name of the pipeline.
- `schedule`: Schedule information in the form of a cron job.
- `default_args`: Default arguments to use when creating the pipeline.
- `depends_on_past`: A boolean when set to true, keeps a task from getting triggered if the previous schedule for the task hasn’t succeeded.
- `start_date`: Start date of the pipeline.
- `retries`: How many retries should be made before marking a task as FAILED.
- `default_connections`: Connections to use when no connections are specified for the task.
- `notifications`: Specify the notification channels to be used. There can be multiple notification channels. For every notification channel you define there are four parameters to specify. The parameters are:
  - `name`: Name for the channel.
  - `connection`: Connection ID of the channel.
  - `success`: Message to be formatted with relevant information and sent to the specified channel when pipeline succeeds.
  - `failure`:  Message to be formatted with relevant information and sent to the specified channel when pipeline fails.
