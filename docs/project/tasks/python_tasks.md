## `Python Tasks`

You can create Python tasks in Blast-Scheduler.

#### 1.`Creating a Python task from comments`
To create a Python task from comments, you should define your task information on top of your `.py` file. 

```python
# @blast.name: my_python_task
# @blast.type: python
# @blast.depends: my_depend_task
# @blast.parameters.a_parameter: my_param
# @blast.connections.a_connection: my_connection

print("Hello World!")
```

#### 2.`Creating a Python task from YAML`
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
