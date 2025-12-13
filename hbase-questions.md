## 1. What are key components of HBase?

### MA: ZooKeeper is monitoring the processes. HMaster is responsible for assigning regoins and load balancing. Then we have region servers, which are the machines in the hadoop cluster, they perform read and write operations. Each region servers has a HLog and MemStore, which store HFiles

### VA: Region server - containts HBase tables divided horizonatlly by regions - if a key is between start key and end key of a region it belongs there. Region server runs on every node and assigns data to the regions. HBsae architecture is similar to Hadoop 2.0 architecture, where Name Node and Secondary Name Node are HMaster and Secondery HMaster and Data Nodes are Region Servers. However HMaster cannot work without Zookeeper, which is a central monitoring unit and reads and saves metadata about regions and region servers. Before data is queried, HMaster asks Zookeeper for metadata and after that data can be queried. 
