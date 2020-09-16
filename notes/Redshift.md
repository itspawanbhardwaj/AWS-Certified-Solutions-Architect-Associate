# Redshift
---

Amazon redshift is a fast and powerful, fuly managed, petabyte scale dta warehouse service in the cloud. Customers can start small for just $0.25 per hour with no commitments or upfront costs and scale to a petabyte or more for $1000 per tb per year, less than a tenth of most other data warehousing solutions.

Redshift can be configured as follows:

- Single node (160GB)
- Multi-node:
    - Leader node(manages client connections and receives queries)
    - Compute node(stored and performs queries and computations.) upto 128 compute nodes behind leader node


Advanced Compression:
---
Columnar data stores can be compressed much more than row-based data stored because similar data is stored sequentially on disk. Amazon redshift employs multi compression techniques and can offer achieve signifficant compression relative to traditional relational data stores. In addition, Amazon redshift doesnt require indexes or materialized views, and so uses less space than traditional relation database systems. When loading data into an empty table, Amazon redshift automatically samples your data and selects the most appropriate compression scheme.

Massive Parallel Procesing (MPP)
---
- Amazon redshift automatically distributes data and query load across all nodes.
- Amazon redshift makes it easy to add nodes to your data warehouse and enables you to maintain fast query performances as your data warehouse grows.

Backups
---
- Enabled by default with a 1 day retention period
- maximnum retention period is 35 days
- Redshift always attempts to maintain at least three copies of your data (the original and replica on the compute nodes and a backup in S3)
- Redshift can also asynchronously replicate your snapshots to S3 in another region for disaster recovery

Redshift is prices as follows:
---
- Compute node hours (total number of hours you run across all your compute nodes for the billing period. You are billed for one unit per node per hour, so a 3-node data warehouse cluster running persistently for an entire month would incur 2,160 instance hours. you will not be charged for leader node hours, only compute nodes will include charges)
- Backups
- Data transfer (Only within VPC, not outside it)

Security
---
- Encrypted in transit using SSL
- Encrypted at rest using AES-256 encryption
- By default redshift takes care of key management
	- Manage your own keys through HSM (Hardware Security Module)
	- KMS

Redshift Availibility
---
- Currently only available in 1 AZ
- Can resotre snapshots to a new AZ in the event of an outage


Amazon Redshift uses a **four-tier, key-based architecture** for encryption. These keys consist of data encryption keys, a database key, a cluster key, and a master key.
- Data encryption keys encrypt data blocks in the cluster. Each data block is assigned a randomly-generated AES256 key. These keys are encrypted by using the database key for the cluster.
- The database key encrypts data encryption keys in the cluster. The database key is a randomly-generated AES-256 key. It is stored on disk in a separate network from the Amazon Redshift cluster and encrypted by a master key. Amazon Redshift passes the database key across a secure channel and keeps it in memory in the cluster.
- The cluster key encrypts the database key for the Amazon Redshift cluster. You can use either AWS or a Hardware Security Module (HSM) to store the cluster key. HSMs provide direct control of key generation and management and make key management separate and distinct from the application and the database.
- The master key encrypts the cluster key if it is stored in AWS. The master key encrypts the cluster-key-encrypted database key if the cluster key is stored in an HSM.

--------------------

##### Q: When would I use Amazon Redshift vs. Amazon RDS?
* Both Amazon Redshift and Amazon RDS enable you to run traditional relational databases in the cloud while offloading database administration. * * Customers use Amazon RDS databases both for online-transaction processing (OLTP) and for reporting and analysis.
* Amazon Redshift harnesses the scale and resources of multiple nodes and uses a variety of optimizations to provide order of magnitude improvements over traditional databases for analytic and reporting workloads against very large data sets.
* Amazon Redshift provides an excellent scale-out option as your data and query complexity grows or if you want to prevent your reporting and analytic processing from interfering with the performance of your OLTP workload.

##### Q: When would I use Amazon Redshift or Redshift Spectrum vs. Amazon EMR?

* You should use **Amazon EMR** if you use custom code to process and analyze extremely large datasets with big data processing frameworks such as Apache Spark, Hadoop, Presto, or Hbase. Amazon EMR gives you full control over the configuration of your clusters and the software you install on them.

* Data warehouses like **Amazon Redshift** are designed for a different type of analytics altogether. Data warehouses are designed to pull together data from lots of different sources, like inventory, financial, and retail sales systems. In order to ensure that reporting is consistently accurate across the entire company, data warehouses store data in a highly structured fashion. This structure builds data consistency rules directly into the tables of the database. Amazon Redshift is the best service to use when you need to perform complex queries on massive collections of structured data and get superfast performance.

* While **Redshift Spectrum** is great for running queries against data in Amazon Redshift and S3, it really isn’t a fit for the types of use cases that enterprises typically ask from processing frameworks like Amazon EMR. Amazon EMR goes far beyond just running SQL queries. Amazon EMR is a managed service that lets you process and analyze extremely large data sets using the latest versions of popular big data processing frameworks, such as Spark, Hadoop, and Presto, on fully customizable clusters. With Amazon EMR you can run a wide variety of scale-out data processing tasks for applications such as machine learning, graph analytics, data transformation, streaming data, and virtually anything you can code.

* You can use **Redshift Spectrum** together with **EMR**. Redshift Spectrum uses the same approach to store table definitions as Amazon EMR. Redshift Spectrum can support the same Apache Hive Metastore used by Amazon EMR to locate data and table definitions. If you’re using Amazon EMR and have a Hive Metastore already, you just have to configure your Amazon Redshift cluster to use it. You can then start querying that data right away along with your Amazon EMR jobs. So, if you’re already using EMR to process a large data store, you can use Redshift Spectrum to query that data right at the same time without interfering with your Amazon EMR jobs.

Query services, data warehouses, and complex data processing frameworks all have their place, and they are used for different things. You just need to choose the right tool for the job.

##### Q: When should I use Amazon Athena vs. Redshift Spectrum?

* **Amazon Athena** is the simplest way to give any employee the ability to run ad-hoc queries on data in Amazon S3. **Athena is serverless**, so there is no infrastructure to setup or manage, and you can start analyzing your data immediately.

* If you have frequently accessed data, that needs to be stored in a consistent, highly structured format, then you should use a data warehouse like Amazon Redshift. This gives you the flexibility to store your structured, frequently accessed data in Amazon Redshift, and use Redshift Spectrum to extend your Amazon Redshift queries out to the entire universe of data in your Amazon S3 data lake. This gives you the freedom to store your data where you want, in the format you want, and have it available for processing when you need.

##### Q: What happens to my data warehouse cluster availability and data durability if a drive on one of my nodes fails?

Your Amazon Redshift data warehouse cluster will remain available in the event of a drive failure however you may see a slight decline in performance for certain queries. In the event of a drive failure, Amazon Redshift will transparently use a replica of the data on that drive which is stored on other drives within that node. In addition, Amazon Redshift will attempt to move your data to a healthy drive or will replace your node if it is unable to do so. Single node clusters do not support data replication. In the event of a drive failure you will need to restore the cluster from snapshot on S3. We recommend using at least two nodes for production.

##### Q: What happens to my data warehouse cluster availability and data durability in the event of individual node failure?

Amazon Redshift will automatically detect and replace a failed node in your data warehouse cluster. The data warehouse cluster will be unavailable for queries and updates until a replacement node is provisioned and added to the DB. Amazon Redshift makes your replacement node available immediately and loads your most frequently accessed data from S3 first to allow you to resume querying your data as quickly as possible. Single node clusters do not support data replication. In the event of a drive failure you will need to restore the cluster from snapshot on S3. We recommend using at least two nodes for production.


##### Q: What happens to my data warehouse cluster availability and data durability if my data warehouse cluster's Availability Zone (AZ) has an outage?

If your Amazon Redshift data warehouse cluster's Availability Zone becomes unavailable, you will not be able to use your cluster until power and network access to the AZ are restored. Your data warehouse cluster's data is preserved so you can start using your Amazon Redshift data warehouse as soon as the AZ becomes available again. In addition, you can also choose to restore any existing snapshots to a new AZ in the same Region. Amazon Redshift will restore your most frequently accessed data first so you can resume queries as quickly as possible.

##### Q: Does Amazon Redshift support Multi-AZ Deployments?

Currently, Amazon Redshift only supports Single-AZ deployments. You can run data warehouse clusters in multiple AZ's by loading data into two Amazon Redshift data warehouse clusters in separate AZs from the same set of Amazon S3 input files. With Redshift Spectrum, you can spin up multiple clusters across AZs and access data in Amazon S3 without having to load it into your cluster. In addition, you can also restore a data warehouse cluster to a different AZ from your data warehouse cluster snapshots.

##### Q: What happens to my backups if I delete my data warehouse cluster?

When you delete a data warehouse cluster, you have the ability to specify whether a final snapshot is created upon deletion, which enables a restore of the deleted data warehouse cluster at a later date. All previously created manual snapshots of your data warehouse cluster will be retained and billed at standard Amazon S3 rates, unless you choose to delete them.

##### Q: What is Elastic Resize and how is it different from Concurrency Scaling?

Elastic Resize adds or removes nodes from a single Redshift cluster within minutes to manage its query throughput. For example, an ETL workload for certain hours in a day or month-end reporting may need additional Redshift resources to complete on time. Concurrency Scaling adds additional cluster resources to increase the overall query concurrency.

##### Q: What data formats and compression formats does Redshift Spectrum support?

Redshift Spectrum currently supports many open source data formats, including Avro, CSV, Grok, Ion, JSON, ORC, Parquet, RCFile, RegexSerDe, SequenceFile, TextFile, and TSV.

Redshift Spectrum currently supports **Gzip and Snappy** compression.

##### Q: I notice that some queries accessing data in my cluster are running slower than my Redshift Spectrum queries. Why is that?

Amazon Redshift queries are run on your cluster resources against local disk. Redshift Spectrum queries run using per-query scale-out resources against data in S3. For most queries, local disk will be faster, but for queries that scan a lot of data and do minimal compute processing, we can apply a lot of Redshift Spectrum workers and complete them quickly.

##### Q: What is a maintenance window? Will my data warehouse cluster be available during software maintenance?

Amazon Redshift periodically performs maintenance to apply fixes, enhancements and new features to your cluster. You can change the scheduled maintenance windows by modifying the cluster, either programmatically or by using the Redshift Console. During these maintenance windows, your Amazon Redshift cluster is not available for normal operations.
