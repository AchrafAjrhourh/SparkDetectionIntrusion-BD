# Description
A project using Spark for Intrusion Detection with a 2 feature decision tree algorithm based on network traffic features, utilizing the UNSW-NB15 dataset and databricks.

# Abstract:
In this project we are interested in using Hive for Intrusion Detection using a simple 2 feature decision tree algorithm based on network traffic features. The project will be based on a research project that was done by Nour Moustafa and Jill Slay. During this project, I will use the UNSW-NB15 dataset which is free to use for academic purposes, and this is the case with my project.
Furthermore, my project will be based on two research papers that were published by the contributors of the main research project. As mentioned before, the goal behind this project is using Hive. So, the Hadoop environment will be a docker container that contains all the necessary tools.

# Description of the data set:
The UNSW-NB15 data set was created using an IXIA PerfectStorm tool in the Cyber Range Lab of the Australian Center for Cyber Security to generate a hybrid of the realistic modern normal activities and the synthetic contemporary attack behaviors from network traffic. A tcpdumb tool was used to capture 100 GB of raw network traffic. However, Tables 1, 2, 3, 4, and 5 provide a clear idea about the features of the data set and its description.

### Table 1. Flow features:
No. | Name | Description 
--- | --- | --- 
1 | Srcip | Source IP address
2 | Sport | Source port number
3 | Dstip | Destination IP address
4 | Dsport | Destination port number
5 | Proto | Protocol type (such as TC, UDP)

### Table 2. Basic features:
No. | Name | Description 
--- | --- | --- 
6 | state | Indicates to the state and its dependent protocol (such as ACC, CLO and CON)
7 | dur | Record total duration
7 | sbytes | Source to destination bytes
9 | dbytes | Destination to source bytes
10 | sttl | Source to destination time to live
11 | dttl | Destination to source time to live
12 | sloss | Source packets retransmitted or dropped
13 | dloss | Destination packets retransmitted or dropped
14 | service | Such as http, ftp, smtp, ssh, dns and ftp-data
15 | sload | Source bits per second
16 | dload | Destination bits per seconds
17 | spkts | Source to destination packet count
18 | dpkts | Destination to source packet count

### Table 3. Content features:
No. | Name | Description 
--- | --- | --- 
19 | swin | Source TCP window advertisement value
20 | dwin | Destination TCP window advertisement value
21 | stcpb | Source TCP base sequence number
22 | stcpb | Destination TCP base sequence number
23 | smeansz | Mean of the flow packet size transmitted by the src
24 | dmeansz | Mean of the flow packet size transmitted by the dst
25 | trans_depth | Represents the pipelined depth into the connection of http request/response transaction
26 | res_bdy_len | Actual uncombressed content size of the data transferred from the server's http service

### Table 4. Time features:
No. | Name | Description 
--- | --- | --- 
27 | sjit | Source jitter (mSec)
28 | djit | Destination jitter (mSec)
29 | stime | Record start time
30 | ltime | Record last time
31 | sintpkt | Source interpacket arrival time (mSec)
32 | dintpkt | Destination interpacket arrival time (mSec)
33 | tcprtt | TCP connection setup round-trip time, the sum of 'synack' and 'ackdat'
34 | synack | TCP connection setup time, the time between the SYN and the SYN_ACK packets
35 | ackdat | TCP connection setup time, the time between the SYN_ACK and the ACK packets

### Table 5. Additional generated features:

In total, there are 47 features with class label. The records were stored in CSV files.
No. | Name | Description 
--- | --- | --- 
36 | is_sm_ips_ports | If *srcip* (1) equals to *dstip* (3) and *sport* (2) equals to *dsport* (4), this variable assigns to 1 otherwise 0
37 | ct_state_ttl | No. for each *state* (6) according to specific range of values of *sttl* (10) and *dttl* (11)
38 | ct_flw_http_mthd | No. of flows that has methods such as Get and Post in http service
39 | is_ftp_cmd | If the ftp session is accessed by user and password then 1 else 0
40 | ct_ftp_cmd | No. of flows that has a command in ftp session
41 | ct_srv_src | No. of records that contain the same *service* (14) and *srcip* (1) in 100 records according to the *ltime* (26)
42 | ct_srv_dst | No. of records that contain the same *service* (14) and *dstip* (1) in 100 records according to the *ltime* (26)
43 | ct_dst_ltm | No. of records of the same *dstip* (3) in 100 records according to the *ltime* (26)
44 | ct_src_ltm | No. of records of the same *srcip* (1) in 100 records according to the *ltime* (26)
45 | ct_src_dport_ltm | No. of records of the same *srcip* (1) and the *dsport* (4) in 100 records according to the *ltime* (26)
46 | ct_dst_sport_ltm | No. of records of the same *dstip* (3) and the *sport* (2) in 100 records according to the *ltime* (26)
47 | ct_dst_src_ltm | No. of records of the same *srcip* (1) and the *dstip* (3) in 100 records according to the *ltime* (26)

# Overview of Hadoop architecture used:

I used the same architecture as the previous project. However, in this time I will add new containers to run spark successfully.

### Docker Container:

![alt text](https://github.com/AchrafAjrhourh/Hive-Detection-Intrusion/raw/master/Assets/Docker%20Container.png)

*Fig 1. Different Component of the Hadoop Architecture used in a Docker Container*

### Docker-Spark: spark-master and spark-worker:

![alt text](https://github.com/AchrafAjrhourh/Spark-Detection-Intrusion/raw/master/Assets/Docker%20Spark.png)

*Fig2: spark master and spark worker*

### NameNode Shell:

`hadoop fs -rm input train_set_schema.hql`

This Hadoop command is used to remove the **train_set_schema.hql** file from the **input** directory

`hadoop fs -ls input`

This Hadoop command is used to list the files and directories present in the **input** directory

`hadoop fs -put UNSW_NB15_training-set2.csv input/`

This Hadoop command is used to upload the **UNSW_NB15_training-set2.csv** file to the **input** directory

![alt text](https://github.com/AchrafAjrhourh/Hive-Detection-Intrusion/raw/master/Assets/Interaction%20with%20Namenode.png)

*Fig 3. Interaction with Namenode Using a Power Shell Window*

### Scala Console:

![alt text](https://github.com/AchrafAjrhourh/Spark-Detection-Intrusion/raw/master/Assets/Scala%20Console.png)

*Fig4: Scala Console with some code examples*

Since I faced some problems concerning the above architecture, I will switch to another one using Databricks. However, the main point behind this part is to give a general idea of how we can integrate spark with our local Hadoop Architecture.

# Overview of Databricks architecture used:
### What is Databricks:

The Databricks Lakehouse Platform makes it easy to build and execute data pipelines, collaborate on data science and analytics projects and build and deploy machine learning models.

![alt text](https://github.com/AchrafAjrhourh/Spark-Detection-Intrusion/raw/master/Assets/Databricks.png)

*Fig5: Overview of Databricks Solutions

### How to use Databricks:

To make the use of Databricks, especially for academic projects, I recommend you using Databricks Community Edition. The Databricks Community Edition is the **free version of the Databricks’ cloud-based big data platform**. Its users can access a micro-cluster as well as a cluster manager and notebook environment. All users can share their notebooks and host them free of charge with Databricks.

### Clusters Manager:

![alt text](https://github.com/AchrafAjrhourh/Spark-Detection-Intrusion/raw/master/Assets/Cluster%20Manager.png)

*Fig 6: The clusters managers of Databricks*

### Databricks Notebooks:

![alt text](https://github.com/AchrafAjrhourh/Spark-Detection-Intrusion/raw/master/Assets/Databricks%20Notebook.png)

*Fig 7: An Overview of how a Databrick Notebook looks like*

![alt text](https://github.com/AchrafAjrhourh/Spark-Detection-Intrusion/raw/master/Assets/Databricks%20Notebook1.png)

*Fig 8: An Overview of Workspace (Notebooks) Manager*

### Loading the Data:

Using Databricks provides us many data sources that we can use. For instance, we can use S3, DBFS (Databricks Files Systems), or other data sources such as Casandra, Amazon Kinesis… 

For this project, we will work with DBFS.

![alt text](https://github.com/AchrafAjrhourh/Spark-Detection-Intrusion/raw/master/Assets/Databricks%20Data%20Soruce.png)

*Fig 9: Databricks Data Sources*

As I said before, in this project we will use DBFS or Databricks File System. To explain more how it works, Databricks provides Community Edition Users with 15G of storage in its File Systems, and after uploading the files to the File System, an absolute path to the data will be provided. Using that path will guarantee easy access to the data.

![alt text](https://github.com/AchrafAjrhourh/Spark-Detection-Intrusion/raw/master/Assets/DBFS%20Overview.png)

*Fig 10: DBFS Overview*

# Building the Schema:

To build a schema for our datasets, there are two ways; either by defining a schema from scratch, or we can use pre-defined function that can do this job for us.

### Defining Schema from Scratch:

![alt text](https://github.com/AchrafAjrhourh/Spark-Detection-Intrusion/raw/master/Assets/Building%20the%20Schema.png)

*Fig 11: Building the Schema using Scala as a programming Language Part I*

![alt text](https://github.com/AchrafAjrhourh/Spark-Detection-Intrusion/raw/master/Assets/Building%20the%20Schema1.png)

*Fig 12: Building the Schema using Scala as a programming Language Part II*

![alt text](https://github.com/AchrafAjrhourh/Spark-Detection-Intrusion/raw/master/Assets/Print%20the%20Schema.png)

*Fig 13: Print the Schema*

![alt text](https://github.com/AchrafAjrhourh/Spark-Detection-Intrusion/raw/master/Assets/Overview%20of%20Table.png)

*Fig 14: An Overview of the Table*

### Building the Schema Using Pre-Defined Function:

![alt text](https://github.com/AchrafAjrhourh/Spark-Detection-Intrusion/raw/master/Assets/Creating%20Training%20Set.png)

*Fig 15: Creating the Training Set DataFrame*

![alt text](https://github.com/AchrafAjrhourh/Spark-Detection-Intrusion/raw/master/Assets/Display%20Dataframe.png)

*Fig16: Display the Dataframe*

![alt text](https://github.com/AchrafAjrhourh/Spark-Detection-Intrusion/raw/master/Assets/Overview%20of%20Schema1.png)

*Fig 17: An Overview of The Schema*

# Confirm the various statistics of the dataset:
### For Training:

![alt text](https://github.com/AchrafAjrhourh/Spark-Detection-Intrusion/raw/master/Assets/Training.png)

*Fig18: dataset statistics for the training set*

### For Testing:

![alt text](https://github.com/AchrafAjrhourh/Spark-Detection-Intrusion/raw/master/Assets/Testing.png)

*Fig19: dataset statistics for the testing set*

### Result:
The above code can be summarized in the following table:

**Category** | **Training Set** | **Testing Set**
--- | --- | ---
Normal | 56,000 | 37,000
Analysis | 2,000 | 677
Backdoor | 1,746 | 583
DoS | 12,264 | 4,089
Exploits | 33,393 | 11,132
Generic | 40,000 | 18,871
Reconnaissance | 10,491 | 3,496
Shellcode | 1,133 | 378
Worms | 130 | 44
Total Records | 175,341 | 82,322

# Computing the Gini Impurity:

n this part, I will calculate the impurity for 5 features because they are the most likely to split our training set. However, the features are:

* is_sm_ips_port
* is_ftp_login
* ct_ftp_cmd
* Service
* ct_state_ttl
* proto
