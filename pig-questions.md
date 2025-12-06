## 1. What are the differences between Pig and MapReduce?

### MA: Pig does not support partitioning, while MapReduce does. Pig uses PigLatin, while MapReduce uses high level programming languages for writing queries. MapReduce is hard to use by non-programmers, while Pig Latin is simpler to learn and understand. Code performance is good in Pig, but even better in MapReduce, however in querying tables code performance is not important.

### VA: Pig uses less lines of code to run a query, than MapReduce. PigLatin is high level language that easily allows JOIN operations, while writing JOIN in Python or Java is a nightmare. On execution Pig operator is converted to MapReduce job. Pig works with all versions of Hadoop, while code written in MapReduce for one Hadoop version might not work on another Hadoop version.
