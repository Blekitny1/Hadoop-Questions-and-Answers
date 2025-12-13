## 1. What are the differences between Pig and MapReduce?

### MA: Pig does not support partitioning, while MapReduce does. Pig uses PigLatin, while MapReduce uses high level programming languages for writing queries. MapReduce is hard to use by non-programmers, while Pig Latin is simpler to learn and understand. Code performance is good in Pig, but even better in MapReduce, however in querying tables code performance is not important.

### VA: Pig uses less lines of code to run a query, than MapReduce. PigLatin is high level language that easily allows JOIN operations, while writing JOIN in Python or Java is a nightmare. On execution Pig operator is converted to MapReduce job. Pig works with all versions of Hadoop, while code written in MapReduce for one Hadoop version might not work on another Hadoop version.

## 2. What are different ways of executing Pig script?

### MA: Straight from command line, use GUI accessable from Cloudera Manager

### VA: Create a .txt or .pig script file and execute it using pig command OR use Grunt Shell for pig commands OR use Pig as embedded script in another programming language

## 3. What are the major components of Pig execution environment?

### MA: Firstly we write a Pig script, then it is processed by parser, optimizer and compiler, after which the execution plan is performed

### VA: Pig scripts are written. Parser verifies the syntax of the script and transforms it into DAG. Optimizer optimizes the execution plan. Compiler compiles it into MapReduce jobs. Execution engine runs MapReduce job and saves the output.

## 4. Explain different complex data types in Pig.

### MA: Firstly, there are primitive Atoms, which correspond to single value of int, string, etc. They are stored as string The complex types are: Tuple, which is a sequence of fields and can be thought of as a row in RDBs; Bag is a collection of tuples and can be thought of as a table in RDBs. We have a Map, which is collection of key value pairs, where a key has to be chararray and value can be of any type.

### VA: Tuple is a sequence of fields with different data types and is denoted by ( ) e.g. (1, 23). Bag is a sequence of tuples and is denoted by { } e.g. {(12,3), (54, 3), (13, 5)}. Map is a sequence of key value pairs and is denoted by [ ] e.g. [qwe#rty, asd#4, zxc#0]

## 5. What are common operators in Pig?

### MA: LOAD - loads data to Pig, DUMP - flushes all command before, without dump no operations are actually executed most of sql keywords have their substitutes in Pig latin.

### VA: LOAD - loads data to Pig, DUMP - displays results of commands, DESCRIBE - view a schema of a relation, EXPLAIN - provides description of MapReduce execution plan, DUMP INTO saves the result into a file

## 6. What are keywords present in Pig which are not in SQL?

## MA: I have no idea

### VA: COGROUP - joins tables followed by GROUP operations, CROSS - performs a cartesian product on two tables, FOREACH - iterates through a relation performing a transformation

## 7. What is use of filters in Pig?

### MA: It does the same thing as WHERE in SQL, obviously you want to have an option to filter a relation by condition

### VA: FILTER operator is used to selected required tuples from a relation based on a condition. It also allows you to remove unwanted records from the file.
