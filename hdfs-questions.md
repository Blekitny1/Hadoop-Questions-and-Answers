## 1. Why is HDFS fault tolerant?

### MA: Mainly because data is replicated across different nodes, so if one node fails the data will remain on another node and can be read from there. Additionally the metadata (editlog and fsimage files) 
is periodically saved on secondary name node, so if the name node crashes the state of the cluster can always be loaded from last saved state on secondary name node.

### VA: HDFS is fault tolerant as it replicates data across multiple data nodes. By default a block of data is replicated on 3 data nodes. There are two rules of replications: first states that two identical blocks (e. g. two replicas
of a data block) cannot be stored on the same node; second states that if the data nodes are divided into racks, that is impossible for all replicas of a block to be in one rack.

## 2. Explain the architecture of HDFS.

### MA: HDFS includes a name node, which is a master node and is responsible for saving metadata, secondary name node, which persists the state of the name node and saves and loads metadata with the name node, and data nodes on which
the data is stored. The name node recieves information from client about read, write and delete operations, and accordingly to the metadata sends instructions about these operations to data nodes, which perform the operations and return
the result to the name node

### VA: Name node in HDFS is a master process, which stores metadata in disk and in RAM. In disk it holds editlog, the log of all transactions performed on the cluster, and fsimage, that is the state of the file system. Metadata in RAM is 
responsible for running client requests. Data nodes hold actual data and send a block report to the name node every 10s. Data nodes store and retrieve data if asked by the name node. It reads and writes client requests and performs block
creation, deletion and replication according to the instructions from the name node.

## 3. What are the two metadata typs that the name node holds?

### MA: The first type is metadata on disk, which are editlog, the log of all transactions performed on the cluster, and fsimage, that is the state of the file system. The second type is metadata on RAM, which stores information 
about blocks, replicas, their sizes and locations

### VA: The first type is metadata on disk, that is editlog and fsimage, already described earlier. The second type is metadata in RAM, which stores information about files, how are files devided to blocks, how are they replicated and what
are the permissions of the files

## 4. What is the difference between high federation and high availability?

### MA: I have no idea, don't recall this from the video.

### VA: These are two features introduced in Hadoop 2.0 that are possible solution to the bottleneck of HDFS that was the uniqueness of a name node. Data federation:
- there is no limitation in number of name nodes and name nodes are not related to each other
- all name nodes share a pool of metadata in which each name node will have its dedicated pool
-  if one name node goes down it does not impact metadata on other name node

High availability: 
- that are exactly two name nodes, active name node and standby name node, both work all the time
- active name node is up and running, while standby node is idle and updates its metadata from active node from time to time
- if active name node fails, the standby name node will take over
- the name nodes must be on separate machines, that is two machines are required

## 5. If I have a file with size of 350MB, how it will be split into blocks and what will be the block sizes?

### MA: Following a rule, that a default block is 128MB and all blocks are supposed to have this size and only last blocks will be smaller, we have: 
350 // 128 = 2. 2 * 128 = 256, 350 - 256 = 94, so we will have 3 splits, 2 blocks of size 128MB and 1 block of size 94MB.

### VA: Each block by default is divided into blocks of size 128MB. The size of the last block is 128MB. So, that must be 3 splits total. The size of each split will be 128MB, 128MB and 94MB.

## 6. How does rack awareness work in HDFS?

### MA: It is related to data replication rule, that if data nodes are split into racks, that is impossible for all replicats of a data block to be all on nodes on one rack.

### VA: If data nodes are divided into racks, which is often the case HDFS rack awareness is about having knowledge of different data nodes and into which rack do they belong. When a cluster is rack aware, all replicas of the same block
cannot be placed on nodes, that are all on one rack.

## 7. How can you restart name node and all its daemons?

### MA: If you are using Cloudera, you can use Cloudera Manager UI for this operation.

### VA: If you are using Apache Hadoop you can start/stop name node with ./sbin /Hadoop-daemon.sh start/stop namenode. You can start/stop all the daemons with ./sbin start/stop-all.sh. If you are using vendor specific distribution however
you cannot run such scripts. Instead the restarts can be done by cloudera-scm server, which under the hood runs the aforementioned commands.

## 8. Which command check the status of the blocks and the filesystem health?

### MA: For blocks use hdfs fsck (path to file) -files -blocks

### MV: For block status use hdfs fsck <path> -files -blocks. For filesystem status use hdfs fsck / -files -blocks -locations > dfs-fsck.log
