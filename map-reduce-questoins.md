## 1. What is distributed cache in MapReduce?

### MA: DistributedCache is a facility provided by the Map-Reduce framework to cache files (text, archives, jars etc.) needed by applications. For example if you will use a particular file a lot in Mapper or Reducer it is good idea to add it to DistributedCache firstly for better performance.
