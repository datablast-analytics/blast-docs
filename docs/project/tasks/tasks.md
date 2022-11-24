## Tasks

`tasks` directory consists of the tasks you want to run on Blast-Scheduler. The tasks directory can contain nested folders with  `.sql`, `.py`, `.sh` files or `.yml` files which run Blast-Scheduler custom operators.  For good convention, grouping similar tasks in the same folder is advised which helps to keep the project cleaner and more organized.

#### Task Parameters

- `name`: Name of the task.
- `run`: Path of the file to be run. 
- `type`: The type of task to be run.
- `depends`: The name(s) of the task(s) that this task is dependent on. If the task has multiple dependencies you can add all of them under this key.
- `connections`: Connection(s) needed for the task. If the task needs multiple connections you can add all of them under this key. If no specific connections is given, connections on pipeline.yml will be used by default.
- `parameters`: Any other parameters needed for the task. If the task needs multiple parameters you can add all of them under this key.
