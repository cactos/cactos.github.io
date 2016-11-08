---
title: "Build and run Spark Applications"
permalink: /docs/tutorials/build-and-run-spark-applications/
---
{% include base_path %}

{% include toc %}

# Set up Spark file structures

**1.** Download [Spark](http://d3kbcqa49mib13.cloudfront.net/spark-1.6.0-bin-hadoop2.6.tgz) and export the file as `$SPARK_HOME`.

**2.** Put the scala files inside `SPARK_HOME/src/main/scala/` (as it is available in [Github](https://github.com/cactos/Cactos-Prediction.git) under the folder `cactoscale-predictor`).

**3.** Put the build.sbt file inside `SPARK_HOME` (as it is available in [Github](https://github.com/cactos/Cactos-Prediction.git) under the `folder cactoscale_predictor`).This sbt file can be configured to set Spark application name, Spark version, HBase version and other important dependencies required for running a Spark application.

# Build Spark applications

**1.** Install [Scala Build Tool - SBT](http://www.scala-sbt.org/download.html) in the machine

**2.** Run the following command inside SPARK_HOME

```bash
 sbt package
```

this will generate scala class files and a jar file of the application as `SPARK_HOME/target/scala-VERSION/SPARK_PROJECT.jar`.

# Run Spark applications

**1.** Download [HBase](http://www.apache.org/dyn/closer.cgi/hbase/) and export the file as $HBASE_HOME

**2.** To run Spark application in a Standalone mode, i.e on a single machine using multiple cores, execute the following command inside SPARK_HOME:     

```bash
 ./bin/spark-submit --driver-class-path $HBASE_HOME/lib/hbase-client-1.1.1.jar:$HBASE_HOME/lib/zookeeper-3.4.6.jar:$HBASE_HOME/lib/protobuf-java-2.5.0.jar:$HBASE_HOME/lib/guava-12.0.1.jar:$HBASE_HOME/lib/hbase-common-1.1.1.jar:$HBASE_HOME/lib/hbase-protocol-1.1.1.jar:$HBASE_HOME/lib/htrace-core-3.1.0-incubating.jar --class APPLICATION_NAME --master local[1] target/scala-VERSION/SPARK_PROJECT.jar COMMANDLINE_ARGUMENTS
```

# Run the predictor tools for CACTOS 

## TOOL 1:

***APPLICATION_NAME:*** CACTOS_predictor_preprocessor - this preprocesses raw data:

*Input files:* workload_joblist.txt (D1), molpro-jobs-history.txt(D2) and data from HBase (D3 to be explained). Place D1 and D2 inside `$SPARK_HOME/CACTOS_predictor_raw_data`

Configure hosts file as below to access D3 (check access to HBase beforehand):

* IP1 monitoring01  
* IP2 monitoring02  
* IP3 monitoring03  
* IP4 monitoring04  
 
***Output:*** A file (D4) with the following fields: no. of cores, VM memory, MOLPRO memory, MOLPRO input file, type of hard disk and total execution time. File will be saved inside `$SPARK_HOME/CACTOS_predictor_input_data`

***COMMANDLINE_ARGUMENTS:*** NONE

## TOOL 2:

***APPLICATION_NAME:*** CACTOS_predictor_executor_1 - this predicts execution time:

***COMMANDLINE_ARGUMENTS:***
to build the model for specific first 3 arguments (core_numbers, input_file, disk_type):  
core_numbers input_file disk_type build (e.g: 1 lccsd-SP05 ssd build) or
core_numbers input_file disk_type build step_size (tuning step_size argument can improve model performance (default is 0.001)


### Example 1 (building model)

```bash
 ./bin/spark-submit --driver-class-path $HBASE_HOME/lib/hbase-client-1.1.1.jar:$HBASE_HOME/lib/zookeeper-3.4.6.jar:$HBASE_HOME/lib/protobuf-java-2.5.0.jar:$HBASE_HOME/lib/guava-12.0.1.jar:$HBASE_HOME/lib/hbase-common-1.1.1.jar:$HBASE_HOME/lib/hbase-protocol-1.1.1.jar:$HBASE_HOME/lib/htrace-core-3.1.0-incubating.jar --class CACTOS_predictor_preprocessor --master local[1] target/scala-VERSION/SPARK_PROJECT.jar 1 lccsd-SP05 ssd build 0.001
```

***Output:***

```yaml 
Training Mean Squared Error = 294.42249385793514  
Total analysis time >>>>> 5 seconds / 0 minutes
```

To predict the execution time for different VM and Molpro memory:  
core_numbers input_file disk_type VM_memory Molpro_memory

***Output:*** either of the following two:  
  *(a)* execution time (returned from database if query is already stored)  
  
  *(b)* execution time (predicted by learned model if query is not stored)  

### Example 2 (running predictor)

```bash
 ./bin/spark-submit --driver-class-path $HBASE_HOME/lib/hbase-client-1.1.1.jar:$HBASE_HOME/lib/zookeeper-3.4.6.jar:$HBASE_HOME/lib/protobuf-java-2.5.0.jar:$HBASE_HOME/lib/guava-12.0.1.jar:$HBASE_HOME/lib/hbase-common-1.1.1.jar:$HBASE_HOME/lib/hbase-protocol-1.1.1.jar:$HBASE_HOME/lib/htrace-core-3.1.0-incubating.jar --class CACTOS_predictor_executor_2 --master local[1] target/scala-VERSION/SPARK_PROJECT.jar 1 lccsd-SP05 ssd  16 8
```

***Output:***

```yaml 
Execution time for [1_lccsd-SP01_ssd_16_8 => core_numbers, input_file, disk_type, VM_memory,Molpro_memory]:   
 41.82418333333333 minutes (searched value from database) 
```

### Example 3 (running predictor)

```bash
 ./bin/spark-submit --driver-class-path $HBASE_HOME/lib/hbase-client-1.1.1.jar:$HBASE_HOME/lib/zookeeper-3.4.6.jar:$HBASE_HOME/lib/protobuf-java-2.5.0.jar:$HBASE_HOME/lib/guava-12.0.1.jar:$HBASE_HOME/lib/hbase-common-1.1.1.jar:$HBASE_HOME/lib/hbase-protocol-1.1.1.jar:$HBASE_HOME/lib/htrace-core-3.1.0-incubating.jar --class CACTOS_predictor_executor_1 --master local[1] target/scala-VERSION/SPARK_PROJECT.jar 1 lccsd-SP05 ssd  64 8
```

***Output:*** 
 
```yaml 
Execution time for [1_lccsd-SP01_ssd_64_8 => core_numbers, input_file, disk_type, VM_memory, Molpro_memory]:   
42.04205014590951 minutes (predicted value from learned model) 
```

## TOOL 3:

***APPLICATION_NAME:*** CACTOS_predictor_executor_2 - this predicts Molpro memory for minimum execution time:

***COMMANDLINE_ARGUMENTS:***
to build the model for specific first 3 arguments (core_numbers, input_file, disk_type):  
core_numbers input_file disk_type build or  
core_numbers input_file disk_type build step_size (tuning step_size argument can improve model performance (default is 0.001)

### Example 4 (building model)

```bash
 ./bin/spark-submit --driver-class-path $HBASE_HOME/lib/hbase-client-1.1.1.jar:$HBASE_HOME/lib/zookeeper-3.4.6.jar:$HBASE_HOME/lib/protobuf-java-2.5.0.jar:$HBASE_HOME/lib/guava-12.0.1.jar:$HBASE_HOME/lib/hbase-common-1.1.1.jar:$HBASE_HOME/lib/hbase-protocol-1.1.1.jar:$HBASE_HOME/lib/htrace-core-3.1.0-incubating.jar --class CACTOS_predictor_executor_2 --master local[1] target/scala-VERSION/SPARK_PROJECT.jar 1 lccsd-SP05 ssd build 0.001
```

***Output:***

```yaml 
Training Mean Squared Error = 14.418161033440537  
Total analysis time >>>>> 5 seconds / 0 minutes
```

To predict Molpro memory (with minimum execution time) for different VM memory :  
core_numbers input_file disk_type VM_memory or  
core_numbers input_file disk_type VM_memory Expected_execution_time (if query is not stored in database)

***Output:*** either of the following two:  
  *(a)* Molpro memory (returned from database if query is already stored)  
  
  *(b)* Molpro memory (predicted by learned model if query is not stored)  

### Example 5 (running predictor)

```bash
./bin/spark-submit --driver-class-path $HBASE_HOME/lib/hbase-client-1.1.1.jar:$HBASE_HOME/lib/zookeeper-3.4.6.jar:$HBASE_HOME/lib/protobuf-java-2.5.0.jar:$HBASE_HOME/lib/guava-12.0.1.jar:$HBASE_HOME/lib/hbase-common-1.1.1.jar:$HBASE_HOME/lib/hbase-protocol-1.1.1.jar:$HBASE_HOME/lib/htrace-core-3.1.0-incubating.jar --class CACTOS_predictor_executor_2 --master local[1] target/scala-VERSION/SPARK_PROJECT.jar 1 lccsd-SP05 ssd 16
```

***Output:***

```yaml
Molpro memory for minimum execution time with 1_lccsd-SP01_ssd_16 => core_numbers, input_file, disk_type, VM_memory]:  
 8 GB (searched value from database)
```

### Example 6 (running predictor) 

```bash
 ./bin/spark-submit --driver-class-path $HBASE_HOME/lib/hbase-client-1.1.1.jar:$HBASE_HOME/lib/zookeeper-3.4.6.jar:$HBASE_HOME/lib/protobuf-java-2.5.0.jar:$HBASE_HOME/lib/guava-12.0.1.jar:$HBASE_HOME/lib/hbase-common-1.1.1.jar:$HBASE_HOME/lib/hbase-protocol-1.1.1.jar:$HBASE_HOME/lib/htrace-core-3.1.0-incubating.jar --class CACTOS_predictor_executor_2 --master local[1] target/scala-VERSION/SPARK_PROJECT.jar 1 lccsd-SP05 ssd 64 30
```

***Output:***

```yaml
Molpro memory for minimum execution time with 1_lccsd-SP01_ssd_16 => core_numbers, input_file, disk_type, VM_memory]:  
 9.816018593737946 GB (predicted value form learned model)
```