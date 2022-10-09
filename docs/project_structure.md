# Project Structure

Running tasks on Blast-Scheduler requires a Git repository with the following structure:

```
pipeline.yml
tasks
  ├ folder1
  │   ├ subfolder1
  │   │  ┗ task.yml     --> assets can be nested in any subdirectory
  │   │ 
  │   └ python_task1.py  --> Python assets can be defined directly in the scripts.
  │
  ├ folder2
  │   ├ sql_task1.sql  --> SQL assets can also be defined directly in the SQL files.
  │   ├ sql_task2.yml  --> any other asset can also be defined as YAML files and refer to the actual query inside
  │   └ task2.sql       
  │   
  └ task.yml       --> tasks can also be defined just as YAML files as well, e.g. data ingestion tasks
```


- `tasks` folder with the tasks you want to run on Blast-Scheduler. 
  - All the tasks you want to run must be inside the tasks folder.
  - tasks folder can contain folders/nested folders.
- `pipeline.yml`: this file contains the pipeline-level configuration, such as the schedule.


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