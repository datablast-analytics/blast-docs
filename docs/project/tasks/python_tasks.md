## Python Tasks

You can create Python tasks in Blast-Scheduler.

#### 1. Creating a Python task from comments
To create a Python task from comments, you should define your task information on top of your `.py` file. 

```python
# @blast.name: my_python_task
# @blast.type: python
# @blast.depends: my_depend_task
# @blast.parameters.a_parameter: my_param
# @blast.connections.a_connection: my_connection

print("Hello World!")
```

#### 2. Creating a Python task from YAML
By defining your task information in a `.yml` file you can create a Python task. 

```yaml
name: my_task
run: python_script.py
type: python

depends:
    - core.model
    - main.data

parameters:
    a_parameter:my_parameter

connections:
    gcp_conn: my_gcp_conn_id
    slack: my_slack_conn_id	
```

#### 3. Managing secrets in Python tasks
``` python
# @blast.secrets: my_secret:my_secret_in_env, another_secret:another_secret_var

first_secret = os.environ["my_secret_in_env"]
second_secret = os.environ["another_secret_var"]
```
You can use your environment variables for python tasks by using `blast.secrets` keyword in the form of:

```
name_on_scheduler:name_to_be_exported_on_script
``` 
