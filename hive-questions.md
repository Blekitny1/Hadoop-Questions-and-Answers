## 1. What are different components of hive architecture?

### MA: Hive UI, Hive Server, Hive Driver, CLI, Hive Metastore, YARN can be used as resource manager and HDFS can be used as storage

### VA: UI - calls execute interface to the driver, creates a session to the query and sends the query to compiler to provide execution plan. Metastore - stores metadata and sends it to compiler for query execution. Compiler - generates execution plan, which is a sequence of map, reduce, hdfs operation or metadata operation, Execution engine - communicates with metastore to create / drop tables
