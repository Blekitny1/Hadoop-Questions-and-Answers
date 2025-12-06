## 1. What benefits did YARN bring that helped to solve issues from Hadoop V1?

### MA: Can run 10,000 data nodes and 1,000,000 concurrent tasks instead of 4000 nodes and 40000 concurrent tasks; allowed dynamic allocation of resources; is multitenant; eliminated single point of failure <-> job tracker

### VA: Container concept, resource allocation, change architecture with application masters, node managers, backward compatibility with Hadoop V1.

## 2. How does yarn allocate resources to an application.

### MA: It resource manager negotiactes with a node manager a container within a node, which is an amount or RAM and CPU, that is used to run an application on that node. 

### VA: A lengthy and detailed description is provided, with the general idea being as I have written above.

## 3. Which of the following occupied a place of job tracker from Hadoop V1?

### MA: c) Resource Manager

### VA: c) Resource Manager - this is the master process in Hadoop V2

## 4. What yarn commands are used to check status of an application or kill an application?

### MA: yarn application -status <applicationId> and yarn application -kill <applicationId>

### VA: yarn application -status applicationId and yarn application -kill applicationId, you can do it from UI too

## 5. Can we have more than one resource manager in yarn cluster?

### MA: The ResourceManager high availability (HA) feature adds redundancy in the form of an active-standby ResourceManager pair to remove this single point of failure. Furthermore, upon failover from the active ResourceManager to the standby, the applications can resume from the last state saved to the state store.

### VA: Yes, there can be more than one resource manager in case of High Availability cluster. If resource manager fails a standby resource manager takes over.

## 6. What type of schedulers you have in yarn?

### MA: FIFO, FAIR, capacity scheduler

### VA: FIFO, Capacity scheduler, that assigned small and potentially quick jobs first and long lenghty job later (can be good or bad), FAIR scheduler - that dynamically balances resources for active jobs - its a good default.

## 7. What happens if resource manager fails in a High Availability cluster?

### MA: Look question 5 :P

### VA: After standby resource manager will take over it will tell aplication masters to abort, then it will recover its running state of containers from node managers

## 8. In a cluster of 10 datanodes, each with 16GB RAM and 10 CPU cores, what is total processing capacity of the cluster?

### MA: The total capacity could be 160GB RAM and 100 CPU cores, however around 30% of each nodes capacity is reserved for machine own processes and communication processes. That is, one can estimate a cluster capacity with 70%*10*(16GB RAM, 10 CPU cores) =  102GB RAM and 70 CPU cores

### VA: Every node has its own processes and linux file system running and requires some RAM and cores. For that reason around 20%-30% of each node cannot be used for calculations. So, instead of 16 GB RAM and 10 cores one should assume 11-12GB RAM and 7-8 CPU cores, thus 110-120GB RAM and 70-80 cores would be the capacity.

## 9. What happens if requested amount of CPU cores and RAM is more than maximum container size?

### MA: yarn will create a container with maximum size, thus the processed job might fail or take a lot of time to process

### VA: The application will fail
