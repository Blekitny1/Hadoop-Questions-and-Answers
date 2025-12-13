## 1. What are key components of HBase?

### MA: ZooKeeper is monitoring the processes. HMaster is responsible for assigning regoins and load balancing. Then we have region servers, which are the machines in the hadoop cluster, they perform read and write operations. Each region servers has a HLog and MemStore, which store HFiles

### VA: Region server - containts HBase tables divided horizonatlly by regions - if a key is between start key and end key of a region it belongs there. Region server runs on every node and assigns data to the regions. HBsae architecture is similar to Hadoop 2.0 architecture, where Name Node and Secondary Name Node are HMaster and Secondery HMaster and Data Nodes are Region Servers. However HMaster cannot work without Zookeeper, which is a central monitoring unit and reads and saves metadata about regions and region servers. Before data is queried, HMaster asks Zookeeper for metadata and after that data can be queried. 

## 2. What are row keys and column families in HBase?

### MA: Row key is a primary key for HBase table - all entries in a table with the same row key are stored in the same region server. Column families are groups of columns which are defined when table is created, they contain specific fields (could be thought of as single columns for that family)

### VA: Row key is a primery key for a entry in HBse table, Column family is a set of columns with column qualifiers. Every entry in HBase table can have different number of cells however cells have to belong to column family

## 3. When and why do we have to disable HBase tables?

### MA: HBase is a strictly consistent NoSQL database in case of reads and writes. So achieving consistency is very important for HBase during DB operations. HBase demands disabling table in case of altering schema changes and dropping tables. HBase doesn't have a protocol to tell all the regions to update the schema changes online. So we need to disable the table before alter it.

### VA: You can only alter a table or change its settings if its is disabled. When its diabled very limited operations can be done on the table.

## 4. How can you import and export data with HBase?

### MA: For import lets create a target table first, which column families and whatever we need. After that we import with hbase Import "<target-table-name>" "<import-data-location">. For export we use hbase Export "<table-name>" "<target-directory>"

### VA: Hbase export: hbase org.apache.hadoop.hbase.mapreduce.Export "some_table" "/export/some_table" , Hbase import: hbase org.apache.hadoop.hbase.mapreduce.import "table_to_import" "target_import-_location"

## 5. How does bloom filter in HBase work?

### MA: Bloom filter is a fast data structure to quickly find out if an element belongs to a set, in exchange of possible wrong results it can provide. In HBase it is used to quickly find out if a cell exists in a table.

### VA: Bloom filters provide index structure for a table that reduces reads and provides a probability that a table contains a specific cell.

## 6. Does HBase use concept of namespaces?

## MA: Yes, you can create and use namespaces as in any other DB. You create a namespace with create_namespace command.

## VA: A namespace is logical group of tables and an equivalent of a database in RDBMS. You can create namespace with create_namespace 'my_namespace' command and list namespaces with list_namespaces command and list tables in a namespace with list_namespace_tables command.

