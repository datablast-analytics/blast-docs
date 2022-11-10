# Pipeline

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
- `start_date`: Start date of the pipeline.
- `default_connections`: Default connections to use for the tasks in the pipeline, if no task specific connection is specified.
- `notifications`: Specify the notification channels to be used. For more information see [Notifications](project/pipeline/notifications/notifications.md)
