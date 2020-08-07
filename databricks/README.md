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

## Setup Mount Point for Blob Storage

Using an old driver called WASB 

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

To verify in Databricks Notebook

```python
%fs dbfs:/mnt/<mount-name>
```

## Setup Mount Point for ADLS Gen 2

Requiring the following items

- ``application-id``: An ID that uniquely identifies the application.
- ``directory-id``: An ID that uniquely identifies the Azure AD instance.
- ``storage-account-name``: The name of the storage account.
- ``service-credential``: A string that the application uses to prove its identity.

### Create Mount Point 

```python
configs = {"fs.azure.account.auth.type": "OAuth",
           "fs.azure.account.oauth.provider.type": "org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider",
           "fs.azure.account.oauth2.client.id": "<application-id>",
           "fs.azure.account.oauth2.client.secret": dbutils.secrets.get(scope="<scope-name>",key="<service-credential-key-name>"),
           "fs.azure.account.oauth2.client.endpoint": "https://login.microsoftonline.com/<directory-id>/oauth2/token"}

# Optionally, you can add <directory-name> to the source URI of your mount point.
dbutils.fs.mount(
  source = "abfss://<file-system-name>@<storage-account-name>.dfs.core.windows.net/",
  mount_point = "/mnt/<mount-name>",
  extra_configs = configs)
```

## Performance Tuning 

- Use Ganglia to see the metrics and gain insights

- Use Spark 3.0 if your application contians lots of joining logic
    - Adaptive Query Execution to speed up Spark SQL at runtime 
    - Ref: https://databricks.com/blog/2020/05/29/adaptive-query-execution-speeding-up-spark-sql-at-runtime.html
    - Simply enable it by setting ``spark.sql.adaptive.enabled`` to ``true``

## Common issues

### No output files written in storage 

Probably it is out of memory. Try adjust the hardware settings. 

### Clusters settings not apply to jobs 

Make sure the cluster is interactive or automated. Interactive one is for notebooks. If you create a job, you should be able to modify the cluster settings in the job creation page. 

### Spark conf is not supported via cluster settings for spark-submit task

Self-explanatory 

```
{"error_code":"INVALID_PARAMETER_VALUE","message":"Spark conf is not supported via cluster settings for spark-submit task. Please use spark-submit parameters to set spark conf."}
```

### Custom Dependencies cannot be found

Suppose your package is located in ``/dbfs/databricks/driver/jobs/``, add the following code in your entry point.

Python Example:

```python
import sys
sys.path.append("/dbfs/databricks/driver/jobs/")
```


## References:

- [Databricks File System (DBFS)](https://docs.databricks.com/data/databricks-file-system.html)
- [Create a Databricks-backed secret scope](https://docs.databricks.com/security/secrets/secret-scopes.html)
- [Azure Data Lake Storage Gen2](https://docs.microsoft.com/en-us/azure/databricks/data/data-sources/azure/azure-datalake-gen2)