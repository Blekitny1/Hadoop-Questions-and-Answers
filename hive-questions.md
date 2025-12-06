## 1. What are different components of hive architecture?

### MA: Hive UI, Hive Server, Hive Driver, CLI, Hive Metastore, YARN can be used as resource manager and HDFS can be used as storage

### VA: UI - calls execute interface to the driver, creates a session to the query and sends the query to compiler to provide execution plan. Metastore - stores metadata and sends it to compiler for query execution. Compiler - generates execution plan, which is a sequence of map, reduce, hdfs operation or metadata operation, Execution engine - communicates with metastore to create / drop tables

## 2. What is the difference between external table and managed table in Hive?

### MA: If a managed table or partition is dropped, the data and metadata associated with that table or partition are deleted. Use managed tables when Hive should manage the lifecycle of the table, or when generating temporary tables. External table files can be accessed and managed by processes outside of Hive. External tables can access data stored in sources such as Azure Storage Volumes (ASV) or remote HDFS locations. Use external tables when files are already present or in remote locations, and the files should remain even if the table is dropped.

### VA: External tables in Hive refer to the data that exist outside the warehouse directory. If Hive deletes the metadata of a table it does not change the presence of the data in HDFS. Managed (internal) table has its data moved to warehouse directory by default. If managed table is dropped, the metadata is dropped as well as the data is deleted from the warehouse directory. By default a managed table is created, and if we want otherwise we should use EXTERNAL keyword

## 3. What is partition in Hive and why is it required for data to be partitioned in Hive?

### MA: A partition is a column or a set of columns in table. The entries with the same value in that column will be collected to the same partition. 

### VA: Partitioning is the process of grouping data based on a column of a partiton key. It is required as it allows to search only parts of the table if by the partition column we know, that we do not need to retrieve those records.

## 4. Why does hive not store metadata on HDFS? 

### MA: It stores metadata in metastore. HDFS is optimized for rare big queries and data operations, while metadata operations are very common, short. Using HDFS for storing metadata is simply bad idea performance wise.

### VA: HDFS read / write operations are time consuming. So, Hive stores metadata in metastore using rdbms, not hdfs. It allows to achieve low latency and query faster.

## 5. Write a query to insert a column c into hive table t in place of existing column e?

### MA: ALTER TABLE t ADD COLUMNS c BEFORE e

### VA: ALTER TABLE t ADD COLUMNS c INT BEFORE e

## 6. What are key differences between Hive and Pig?

### MA: Hive enables partitioning and there is no partitioning in Pig. Hive uses HiveQL which is very similar to SQL, while Pig uses Pig Latin for procedural language. In Hive code performance is worse then Pig and MapReduce, but the queries are very easy to write. In Pig code performance is better then in Hive, but is worse then MapReduce, however filling sql querying into MapReduce model was a nightmare.

### VA: Hive uses declarative HiveQL, while Pig uses procedural Pig Latin. Hive does not allow non-structured data, while Pig can process those. Hive does not support AVRO by default, while Pig does. Hive supports partitioning, while Pig does not.
