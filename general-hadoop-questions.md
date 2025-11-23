# 1. What are different vendor specific distributions of Hadoop?

## QM: Cloudera, Microsoft, Amazon Web Services, Mapr

## QV: Cloudera, Hortonworks, Microsoft Azure, IBM InfoSphere, Amazon Web Services

# 2. What are different Hadoop configuration files?

## QM: core-site.xml, mapred-site.xml, hdfs-site.xml, yarn-site.xml

## QV: hadoop-env.sh, core-site.xml, hdfs-site.xml, mapred-site.xml, yarn-site.xml

# 3. What are hadoop operation modes?

## QM: 

- Local Mode: The simplest Hadoop mode, runs on a single JVM, no daemons, no configurations required. Instead of HDFS local file system is used

- Pseudo-Distributed Mode: runs on a single physical machine, but daemons run as separated processes on independent jvm and hdfs is fully functional

- Fully Distributed Mode: runs and multiple machines, fully scalable, generally a "full" Hadoop mode which uses all its capabilities.

## QV:

- Local Mode: Uses your file system and a uses a single java proces. It is also a default mode

- Pseudo-Distributed Mode: all services run on a single node, but they run independently

- Fully Distributed Mode: uses separate nodes to run master and slave daemons. Normally used in production environment

# 4. What are the differences between regular FS and HDFS?

## QM: 

FS is a single system maintained on one machine, whereas HDFS is a distributed system in which data is stored across many data nodes. Scaling ordinary FS is very costly and inefficient as it cannot be horizontally scalable, while HDFS scales linearly with number of nodes and adding extra node is cheap. FS is not fault tolerant and does not have any data replication mechanisms, which both are covered in HDFS. HDFS can be used to run Hadoop Map-Reduce tasks

## QV:

- FS: data is maintained in a single system vs HDFS: data is distributed and maintained on multiple system
- FS: If the machine crashes, data recovery is difficult due to low fault tolerance vs HDFS: It a datanode crashes, data can still be recovered from other nodes
- FS: Seek time is higher and it takes more time to process the data vs HDFS: time taken to read data is high, as it requires coordination with many machines, but with the number of data to be processed increasing it quickly outperforms regular FS.

