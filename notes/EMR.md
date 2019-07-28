# EMR (Elastic Map Reduce)
---

* The master node is launched into a security group that allows Secure Shell (SSH) and service access, while the slave nodes are launched into a separate security group that only permits communication with the master node.


###### Q: What is Presto?
* Presto (or PrestoDB) is an open source, distributed SQL query engine, designed from the ground up for fast analytic queries against data of any size. 
* With Amazon EMR, you can launch Presto clusters in minutes without needing to do node provisioning, cluster setup, Presto configuration, or cluster tuning. EMR enables you to provision one, hundreds, or thousands of compute instances in minutes.


###### Q: What is a cluster step?

* A cluster step is a user-defined unit of processing, mapping roughly to one algorithm that manipulates the data. A step is a Hadoop MapReduce application implemented as a Java jar or a streaming program written in Java, Ruby, Perl, Python, PHP, R, or C++. For example, to count the frequency with which words appear in a document, and output them sorted by the count, the first step would be a MapReduce application which counts the occurrences of each word, and the second step would be a MapReduce application which sorts the output from the first step based on the counts.

###### Q: What are different cluster states?

* STARTING – The cluster provisions, starts, and configures EC2 instances.
* BOOTSTRAPPING – Bootstrap actions are being executed on the cluster.
* RUNNING – A step for the cluster is currently being run.
* WAITING – The cluster is currently active, but has no steps to run.
* TERMINATING - The cluster is in the process of shutting down.
* TERMINATED - The cluster was shut down without error.
* TERMINATED_WITH_ERRORS - The cluster was shut down with errors.

###### Q: What are different step states?

* PENDING – The step is waiting to be run.
* RUNNING – The step is currently running.
* COMPLETED – The step completed successfully.
* CANCELLED – The step was cancelled before running because an earlier step failed or cluster was terminated before it could run.
* FAILED – The step failed while running.

###### Q: Does Amazon EMR support multiple simultaneous cluster?

* Yes. At any time, you can create a new cluster, even if you’re already running one or more clusters.

###### Q: How many clusters can I run simultaneously?
* You can start as many clusters as you like. You are limited to 20 instances across all your clusters. 
* If you need more instances, complete the Amazon EC2 instance request form and your use case and instance increase will be considered. If your Amazon EC2 limit has been already raised, the new limit will be applied to your Amazon EMR clusters.

###### Q: Can I be notified when my cluster is finished?
* You can sign up for up Amazon SNS and have the cluster post to your SNS topic when it is finished. You can also view your cluster progress on the AWS Management Console or you can use the Command Line, SDK, or APIs get a status on the cluster.

###### Q: What programming languages does EMR Notebooks support?
* EMR notebook supports PySpark, SparkR, SparkSQL, Spark (Scala), and Python kernels.

###### Q: What libraries are available with EMR Notebooks?
* Libraries found in the open-source Anaconda repositories are available to import in your code. You can import these libraries and use it locally within notebooks.

###### Q: Can I install custom libraries to use in my notebook code?

* All Spark queries run on your EMR cluster, so you need to install all runtime libraries that your Spark application uses on the cluster. You can use a bootstrap action or a custom AMI to install required libraries when you create a cluster.

###### Q: Can I attach my notebook to a Kerberos enabled EMR cluster?
* No, kerberized EMR clusters are currently not supported.

###### Q: Do you compress logs?
* No. At this time Amazon EMR does not compress logs as it moves them to Amazon S3.

###### Q: If the master node in a cluster goes down, can Amazon EMR recover it?
* No. If the master node goes down, your cluster will be terminated and you’ll have to rerun your job. 

###### Q: Can I persist my data on an EBS volume after a cluster is terminated?
* Currently, Amazon EMR will delete volumes once the cluster is terminated. If you want to persist data outside the lifecycle of a cluster, consider using Amazon S3 as your data store.

###### Q: What kind of EBS volumes can I attach to an instance?

* Amazon EMR allows you to use different EBS Volume Types: General Purpose SSD (GP2), Magnetic and Provisioned IOPS (SSD).

###### Q: What happens to the EBS volumes once I terminate my cluster?
* Amazon EMR will delete the volumes once the EMR cluster is terminated.

###### Q: Can I use encrypted EBS volumes?

No, encrypted volumes are not supported in the current release.

###### Q: Can I push data from EMR into Kinesis stream?

No. The EMR Kinesis connector currently does not support writing data back into a Kinesis stream.