## 1. What are the differences between Sqoop and Flume?

### MA: I have no idea.

### VA: Sqoop is typically used for importing and exporting structured data between HDFS and RDBMS with usage of Sqoop connector. Flume is data ingesting tool typically used for streaming nonstructured data, is event driven.

## 2. What are default data formats to import data using Sqoop?

### MA: The default import type is delimited text file - it will write table data to text file with delimiters.

### VA: Delimited text file is the default format - it can be set up directly with --as-textfile argument though. It will write string representation of each record to output files and will delimit entries with a set delimiter.

## 3. What is the importance of eval tool?

### MA: Using eval tool, we can evaluate any type of SQL query. It can be used to firstly check with a query if we have correct credential to the database and to take a look at the data to be impoerted.

### VA: Sqoop eval tool allows users to execute custom queries on databases and provide a result to console

## 4. Explain how Sqoop imports and exports data with its architecture.

### MA: Sqoop import: Sqoop firstly gathers metadata from RDBMS and after that splits the input into map-only tasks, that are run on HDFS as any other map task, with their results saved on HDFS. Sqoop import: Sqoop firstly gathers metadata from RDBMS and after that splits the input into map-only tasks, that are run on HDFS as any other map task, with their results saved on RDBMS.

### VA: Additionally to MA Sqoop requires connector.jar files to respective RDBMS in lib directory that it needs to import or export data.

## 5. How to use Sqoop to update columns that are already exported?

### MA: In Sqoop export you have to use --update-key <column-name> parameter, it will allow you to overwrite existing entries

### VA: To update a column that is already exported use --update-key parameter.

## 6. Can Sqoop be used to convert data to new data formats?

### MA: Yes, as we can simply specify a data format when running import command

### VA: Yes, Sqoop can be used to convert data to different data formats. This depends on different arguments which we use to do an import. Some possible formats are AVRO, PARQUET, binary format

