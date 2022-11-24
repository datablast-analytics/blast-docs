## Project Structure

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

`tasks` folder with the tasks you want to run on Blast-Scheduler. You can learn more about supported task types in [Tasks](project/tasks/tasks.md).
  - All the tasks you want to run must be inside the tasks folder.
  - tasks folder can contain folders/nested folders.
  
`pipeline.yml`: this file contains the pipeline-level configuration, such as the schedule. You can learn more about pipelines in [Pipeline](project/pipeline/pipeline.md).
