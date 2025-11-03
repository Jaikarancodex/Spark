# Spark
# Hadoop Introduction:
## Overview of Hadoop and its role in distributed computing.
#### What is Hadoop?
Hadoop is an open-source framework that allows you to store and process massive amounts of data across multiple computers (nodes) working together — instead of relying on one big, powerful computer.
#### In simple terms:
Hadoop = A way to handle Big Data using many normal computers working together like one giant computer.
## Key Components:
Component	Role
* HDFS (Hadoop Distributed File System) -	Stores large files by splitting them into blocks and spreading them across nodes.
* MapReduce -	Processes the data in parallel (Map = divide work, Reduce = combine results).
* YARN	- Manages and schedules tasks across the cluster.

## Historical context and evolution. 
#### Before Hadoop:
* Companies stored data in relational databases (RDBMS).
* These worked fine for small or structured data.

###### //But when data became huge, unstructured, and real-time (videos, logs, social media, sensors), RDBMS couldn’t handle it.

## The Spark of Change: Google
In the early 2000s, Google faced the same problem — how to index and search the entire internet efficiently.
They published two famous research papers:
* Google File System (GFS) — explained how to store large data across clusters.
* MapReduce — explained how to process large datasets in parallel.
###### //These ideas inspired Doug Cutting and Mike Cafarella (Yahoo engineers at that time) to create Hadoop in 2005, named after Doug’s son’s toy elephant .

### Hadoop’s Evolution:
Year	Milestone
* 2005	Doug Cutting creates Hadoop based on Google’s GFS & MapReduce papers.
* 2006	Yahoo uses Hadoop for its search engine.
* 2008	Hadoop becomes a top-level Apache project.
* 2010s	Companies like Facebook, LinkedIn, and Twitter start using Hadoop.
* Later	Ecosystem grows — Hive, Pig, HBase, Spark, etc. join in.
  
#### Role in Distributed Computing:
* Hadoop became the foundation for big data processing — enabling:
* Scalability (add more nodes easily)
* Cost efficiency (runs on cheap hardware)
* Fault tolerance (no data loss if one node fails)

## Spark Introduction: 
### Overview of Apache Spark and its advantages.
Apache Spark is an open-source big data processing framework that’s built for speed, ease of use, and advanced analytics.

###### //Think of Spark as Hadoop 2.0 on steroids — it does the same kind of distributed data processing, but much faster and more flexible.

### Key Advantages of Spark
Feature	Explanation
* Speed	Runs up to 100x faster than Hadoop MapReduce (in-memory processing).
* In-Memory Processing	Data stays in RAM instead of being written to disk after each step.
* Ease of Use	Supports multiple languages (Python, Java, Scala, R, SQL).
* Rich APIs	Built-in libraries for streaming, SQL, ML, and graphs.
* Real-Time Processing	Unlike Hadoop (batch only), Spark handles streaming (live) data.
* Integration	Works with HDFS, Hive, Cassandra, HBase, and many other systems.
  
### Comparison with Hadoop MapReduce.
### Feature	                  Hadoop MapReduce	                             Apache Spark
* Processing           ----> Type	Batch (step-by-step, disk-based)	-----> Batch + Real-time (in-memory)
* Speed	Slower         –---> writes to disk after every operation   –--->	10–100x faster – keeps data in RAM
* Ease of Use	Complex  –--->Java programs	                          –--->Simple APIs (Python, Scala, Java, R)
* Data Storage         –--->	Always disk-based (HDFS)	            –--->Mostly in-memory, but can use HDFS too
* Machine Learning	   –--->External libraries needed	              –--->Built-in MLlib
* Best For             –--->Large-scale batch processing	          –--->Real-time analytics, ML, and iterative tasks

## Spark Architecture Overview: 
### Understanding the key components of the Spark architecture. 
When you run a Spark application, it’s not just one program running — it’s a cluster-based system with several parts working together.

#### Component	Role
* Driver Program	---->   Controls the Spark application, plans tasks.
* SparkContext	---->   Connects Driver to Cluster Manager.
* Cluster Manager	---->   Allocates resources to the application.
* Worker Node	---->   Executes the work assigned by the driver.
* Executor	---->   Runs tasks and stores data.
* Task	---->     The smallest execution unit.

### Interaction between components during the execution of Spark applications. 
### Step 1: SparkContext Initialization
* The Driver starts and creates a SparkContext.
* SparkContext contacts the Cluster Manager (e.g., YARN) to request resources.

### Step 2: Cluster Manager Allocates Executors
* The Cluster Manager launches Executors on available Worker Nodes.
* Executors register themselves with the Driver.

### Step 3: Job Creation
* When an action is called (like .count() or .collect()), Spark creates a DAG (Directed Acyclic Graph) of stages and tasks.
* This DAG shows how data will flow and what transformations will happen.

###### //Think of this as the Driver making a plan before sending tasks out.

### Step 4: Task Distribution
* The Driver sends tasks (small pieces of the job) to Executors.
* Each executor runs its assigned tasks in parallel.

### Step 5: Execution & Data Storage
* Executors process the data.
* Intermediate results can be stored in memory (that’s Spark’s superpower).
* If data is needed again, it’s reused from memory — no need to re-read from disk.

### Step 6: Collecting Results
* Executors send results back to the Driver.
* The Driver combines them and gives you the final output.
