# Blast Data Platform
Blast is a data orchestration platform. It allows data pipelines to be built by SQL and non-SQL files without any additional configuration. 

It can run tasks on any schedule, against any data store.

```sql
-- @blast.name: core.orders
-- @blast.type: bq.sql

SELECT * FROM orders
WHERE status IN ['paid']
```

Head to the [Getting Started](project/project_structure.md) for more details.
