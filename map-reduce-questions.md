## 1. What is distributed cache in MapReduce?

### MA: DistributedCache is a facility provided by the Map-Reduce framework to cache files (text, archives, jars etc.) needed by applications. For example if you will use a particular file a lot in Mapper or Reducer it is good idea to add it to DistributedCache firstly for better performance.

### VA: It is a mechanism allowing data from disk to be available for all DataNodes performing a map or reduce tasks for a given job. You should set it up in JobConf beforehand.

## 2. What are the roles of RecordReader, Partitioner and Combiner in MapReduce process?

### MA: RecoredReader - gets output from InputReader and transforms it into key-value pairs suitable to be processed my Mapper; Partitioner - gets output from Mapper or Combiner and decides how many Reducer or Reducer task will be needed for input set of key-value pairs, it gives an output to be shuffled and sorted; Combiner - is a optional prereducer, it uses ouput from Mapper and uses the same code as Reducer.

### VA: RecoredReader - communicates with InputReader and converts the data to key-value pairs suitable to be read by Mapper; Partitioner - decides how many reduce tasks will be needed to summarize data and appropriatetly partitions the keys; Combiner - is a minireducer, reduces intermediate key-value pairs from Mapper and passes output to Partitioner 

## 3. Why is MapReduce slower then other processing frameworks?

### MA: It has strict roles of classes to be fit into e.g. sometimes you have to unnnecesarily adjust a simpler problem to have mapping, partitioning, reducing classes and phases of processing flow. 

### VA: MapReduce is batch oriented processing, and no matter what processing do you do you have to provide mapping and reducing tasks, in indermediate phases data is read and written from HDFS, which can be unnecessary. 

## 4. Is it possible to change the number of mappers to be created for a particular MapReduce job?

### MA: No, The number of map tasks for a given job is driven by the number of input splits. For each input split a map task is spawned. So, we cannot directly change the number of mappers using a config other than changing the number of input splits.

### VA: By default it cannot be change as the number of mapper is equal tu number of input splits which are fully depend on the imput. However you can set a property in hdfs-site.xml to forcibly use more mappers.

## 5. Name data formats used for programming MapReduce.

### MA: Generally all typical Java data formats with Writable suffix.

### VA: IntWritable, LongWritable, FloatWritable, DoubleWritable, BooleanWritable, ArrayWritable, MapWritable, ObjectWritable

## 6. What is speculative execution in Hadoop?

### MA: In simple words, a speculative execution means that Hadoop in overall doesn't try to fix slow tasks as it is hard to detect the reason (misconfiguration, hardware issues, etc), instead, it just launches another parallel/backup task for each task that is performing slower than the expected, on faster nodes. So these backup tasks are called speculative tasks and it can be enabled/disabled as its benefits are per use case and up to the Hadoop Admin to consider it to be beneficial or not; speculative execution has an impact on the cluster throughput and resource usage. You can find this in MapReduce or Spark for example.

### VA: If a data node is executing a task slowly, the name node will create copy of that task in another node that processes the data faster. Any task that will finish first will complete, while the other will be killed afterwards.

## 7. How is identity mapper different from chain mapper

### MA: Identity mapper is a mapper that performs identity transformation. Chain mapper is a type of mapper which sequentionally performs some smaller mapper tasks before sending output to combiner / partitioner.

### VA: Identity mapper is a mapper that simply sends key-value pairs for further processing. If you do not specify mapper in driver class it will be used. Chain mapper is used to run more than one mapper in one map task.

## 8. What are major configuration parametrs required for MapReduce program?

### MA: Data formats used in processing, at least one of Mapper/Reducer logic, Partitioner logic, InputReader logic.

### VA: Input and output catalog, input and output format, classes that hold map and reduce functions, jar containing driver, mapper and reducer class (this is an answer to more of a "What do you need to specify to run a MapReduce job" and it looks like a mistranslation of a that question :? )

## 9. What are map-side join and reduce-side join?

### MA: Hadoop supports two kinds of joins to join two or more data sets based on some column. The Map side join and the reduce side join. Map side join is usually used when one data set is large and the other data set is small. Whereas the Reduce side join can join both the large data sets. The Map side join is faster as it does not have to wait for all mappers to complete as in case of reducer. Hence reduce side join is slower.

Map Side Join:

· Sorted by the same key.
· Equal number of partition.
· All the records of the same key should be in same partition.

Reduce Side Join:

· Much flexible to implement.
· There has to be custom WritableComparable with necessary function over ridden.
· We need a custom partitioner.
· Custom group comparator is required. 

### VA: 

Map Side Join:

· Join is done by mapper
· Each of the inputs must have the same number of partitions (strict rule)

Reduce Side Join:

· Join is done by reducer
· Does not have any partitioning constraints
· Values having identical keys are sent to the same reducer

## 10. What is the role of OutputCommiter in Mapreduce job?

### MA: The Map-Reduce framework relies on the OutputCommitter of the job to:

- Setup the job during initialization. For example, create the temporary output directory for the job during the initialization of the job.
- Cleanup the job after the job completion. For example, remove the temporary output directory after the job completion.
- Setup the task temporary output.
- Check whether a task needs a commit. This is to avoid the commit procedure if a task does not need commit.
- Commit of the task output.
- Discard the task commit.

The methods in this class can be called from several different processes and from several different contexts. It is important to know which process and which context each is called from. Each method should be marked accordingly in its documentation. It is also important to note that not all methods are guaranteed to be called once and only once. If a method is not guaranteed to have this property the output committer needs to handle this appropriately. Also note it will only be in rare situations where they may be called multiple times for the same task.

### VA: OutputCommiter describes the commit of task output of a MapReduce job.

## 11. 
