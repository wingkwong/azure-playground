# Databricks

## Sample Cluster Setup

```json
{
    "num_workers": 5,
    "cluster_name": "Databricks-playground",
    "spark_version": "6.5.x-scala2.11",
    "spark_conf": {
        "spark.dynamicAllocation.enabled": "true",
        "spark.shuffle.compress": "true",
        "spark.shuffle.spill.compress": "true",
        "spark.executor.memory": "7849M",
        "spark.sql.shuffle.partitions": "1024",
        "spark.network.timeout": "600s",
        "spark.executor.instances": "0",
        "spark.driver.memory": "7849M",
        "spark.dynamicAllocation.executorIdleTimeout": "600s"
    },
    "node_type_id": "Standard_F8s",
    "driver_node_type_id": "Standard_F8s",
    "ssh_public_keys": [],
    "custom_tags": {},
    "cluster_log_conf": {
        "dbfs": {
            "destination": "dbfs:/cluster-logs"
        }
    },
    "spark_env_vars": {
        "PYSPARK_PYTHON": "/databricks/python3/bin/python3"
    },
    "autotermination_minutes": 0,
    "init_scripts": []
}
```

## Common commands

List the directory in DBFS

```
%fs ls 
```

Create a directory in DBFS

```
%fs mkdirs src
```

Copy files from src to dist in DBFS

```
%fs cp -r dbfs:/src dbfs:/dist
```

## Setup Mount Point

### Create Secret Scope

By default, scopes are created with MANAGE permission for the user who created the scope. If your account does not have the Premium plan (or, for customers who subscribed to Databricks before March 3, 2020, the Operational Security package), you must override that default and explicitly grant the MANAGE permission to “users” (all users) when you create the scope

```
databricks secrets create-scope --scope <scope-name> --initial-manage-principal users
```

To verify 

```
databricks secrets list-scopes
```

### Create Secret 
```
databricks secrets put --scope <scope-name> --key <key-name> --string-value <key>
```

The value of <key> can be retrieved from Storage Account -> Settings -> Access Keys

### Create Mount Point

```python
dbutils.fs.mount(
  source = "wasbs://<container-name>@<storage-account-name>.blob.core.windows.net",
  mount_point = "/mnt/<mount-name>",
  extra_configs = {"<conf-key>":dbutils.secrets.get(scope = "<scope-name>", key = "<key-name>")}
)
```

To verify in Databricks Notebook, 

```python
%fs dbfs:/mnt/<mount-name>
```

## References:

- [Databricks File System (DBFS)](https://docs.databricks.com/data/databricks-file-system.html)
- [Create a Databricks-backed secret scope](https://docs.databricks.com/security/secrets/secret-scopes.html)