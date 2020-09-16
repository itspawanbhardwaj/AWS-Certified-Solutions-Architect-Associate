# RDS
---

**1. RDS (OLTP):**
- SQL server
- MySQL
- PostgreSQL
- Oracle
- Aurora
- MariaDB

**2. Data Warehousing (OLAP)**
- Redshift

**3. DynamoDB (NoSQL)**



--------------------

# Multi-AZ

- It allows to have SYNCHRONISED replication (exact copy) of rds production database running in different availability zone. All the changes are synced and replicated automaitcally by amazon.
- If we lose our main rds instance in an avaiability zone, Amazon will automatically update the dns settings and rds endpoint will automatically failover to the rds database in the different availability zone.
- In the event of planned db mainetenance, DB instance failure or an Avaiability zone failure, aws rds will auomatically failover to the standby rds instance so that db operations can resume quickly without adminsistrative interventaion. Same dns endpoint will failover to the standby instance.
- Multi-AZ available for
    - SQL Server
    - Oracle
    - MySQL
    - PostgreSQL
    - MariaDB
- Aurora by its own architecture is fault tolerant
- Multi-AZ for disaster recovery
- You can force a failover from one AZ to another by rebooting the rds instance
-----------------------

# Read Replicas
- Read replicas allow you to have a read-only copy of your production database. This is achieved  by using asynchronous replciation front the primary RDS instance to the read replica. You use read replicas primarily for very read-heavy database workloads
- used for scaling, not for Disastar recovery
- must have automatic backups turned on in order to deploy a read replica.
- you can have up to 5 read replicas copies of any database (but watch out for replication latency)
- you can have read replica of read replica.
- each read replica will have its own DNS end point
- you can have read replica that have Multi-AZ
- You can create read replica of Multi-AZ source database
- read replica can be promoted to be thier own database. this breaks the replication
- You can have a read replica in a second region
- Read Replicas for performance
- Available for
    - MySQL
    - PostgreSQL
    - MariaDB
    - Aurora
-------------------------------------

# Backups
Two types of backups
### **1: Automated backups**: 
- Automated backups allow you to recover your database to any point in time within a "retention period". **The retention period can be between one and 35 Days**. Automated backups will take a full daily snapshot and will also store transaction logs throughout the day. when you do a recovery, AWS will first choose the most recent daily backup, and then apply transactions logs relevant to that day. This allows you to do a point in time recovery down to a second, within the retention period.
- enabled by default
- backup data is stored in s3 and you get free storage space equal to the size of your database.
- backups are taken within a defined window. During the backup window, storage I/O may be suspended while your data is being backed up and you may experience elevated latency

### **2: Snapshot**:
- DB snapshots are done manually
- they are stored even after you delete the original RDS instance, unlike Automated backups

Restoring backups
-----------------
Whenever you restore either an automatically backups or db snapshot, the restored version of the database will be a new RDS instance with a new DNS endpoint.


--------------------------

# Encryption
Supported at rest for
- MySQL
- Oracle
- SQL Server
- PostgreSQL
- MarioDB
- Aurora
 

Encryption is done using the AWS KMS (Key Management Service). Once your RDS instance is encrypted, the data stored at rest in the underlying storage is encrypted, as are its automated backups, read replicas and snapshot


-----------------------
It is good practice to split databases, one for basic queries and one for analytical complex queries.



---------------------------------

**Multi AZ is available for the following databases:**
	SQL Server
	Oracle
	MySQL server
	postgres sql
	mariadb


##### Elastic cache

**Used to increase db and web-apps performance**

ElastiCache is a web service that makes it easy to deploy, operate and scale an in-memory cache in the cloud. The service improves the performance of web applications by allowing you to retrieve information from fast, managed, in-memory caches, instead of relying entirely on slower disk-based databases

ElastiCache supports two open-source in-memory caching engines. Difference between them is not important to know for associate leel but **important** at professional level

Requirement | Memcached | Redis 
--- | --- | ---
Simple cache to offload DB | Yes | Yes
Ability to scale horizontally | Yes | No
Multi-threaded performance | Yes | No
Advanced data types | No | Yes
Ranking/Sorting data sets | No | Yes
Publishing/Subscribing capabilities | No | Yes
Persistence | No | Yes
Multi-AZ | No | Yes
Backup & Restore | No | Yes

- memcached
	* simple cache to offload DB
	* Ability to scale horizontally
	* Multi-threaded performance
	* in memory key value datastore
	* fastest cache db available now
	* The default limit is 20 nodes per cluster.
	* data types: strings and object

- redis
	* Redis clusters can only contain a single node; however, you can group multiple clusters together into a replication group.
	* simple cache to offload DB
	* Advanced data types
	* Ranking/Sorting datasets
	* Pub/Sub capability
	* persistance
	* Multi-AZ with auto-failover
	* Read Replica for read availability
	* Availability due to partitioning
	* Backups & restore capability
	* key-value store
	* A cluster consists of 1 to 15 shards
	* Each shard has a primary node and upto 5 replica nodes across multiple AZs for read scaling
	* increase writes by adding shards
	* fully managed and Hardened
	* secure and compliant: VPC
		* Encryption: 
			in-transit: Encrypt all communication between clients, server, nodes
			At-Rest: Encrypt backups on disk and s3
			Supports redis AUTH
			Fully managed: setup via API, CLI or console, automatic certificate issuance and renewal
	* Highly available and reliable: Read replicas, multiple primaries, multi-AZ with automatic failover
	* Easily scalable: Cluster with up to 6.1 TB of in-memory data 
	* Read scaling with replicas
	* Write and memory scaling with sharding
	* Scale out or in
	* Detailed monitoring metrices, CloudWatch integration
	* 
* used to increase database and web application performance

----------------------------------

RDS runs on a virtual machine
cant ssh into RDS instance
Patching of the RDS OS and DB is Amazon's responsibility
RDS is NOT serverless
Aurora is serverless



--------------------
##### Q: How many DB instances can I run with Amazon RDS?

	By default, customers are allowed to have up to a total of 40 Amazon RDS DB instances.
	Of those 40, up to 10 can be Oracle or SQL Server DB instances under the "License Included" model.
	All 40 can be used for Amazon Aurora, MySQL, MariaDB, PostgreSQL and Oracle under the "BYOL" model. Note that RDS for SQL Server has a limit of 30 databases on a single DB instance.
	RDS for Oracle: 1 database per instance; no limit on number of schemas per database imposed by software
	RDS for SQL Server: 30 databases per instance

##### Q: What is a maintenance window? Will my DB instance be available during maintenance events?

	The Amazon RDS maintenance window is your opportunity to control when DB instance modifications, database engine version upgrades, and software patching occurs, in the event they are requested or required.
	If a maintenance event is scheduled for a given week, it will be initiated during the maintenance window you identify.
	If you do not specify a preferred weekly maintenance window when creating your DB instance, a 30 minute default value is assigned
	Running your DB instance as a Multi-AZ deployment can further reduce the impact of a maintenance event.

##### Q: What should I do if my queries seem to be running slowly?

	For production databases we encourage you to enable Enhanced Monitoring, which provides access to over 50 CPU, memory, file system, and disk I/O metrics. You can enable these features on a per-instance basis and you can choose the granularity (all the way down to 1 second). 
	High levels of CPU utilization can reduce query performance and in this case you may want to consider scaling your DB instance class.  
	If you are using RDS for MySQL or MariaDB, you can access the slow query logs for your database to determine if there are slow-running SQL queries and, if so, the performance characteristics of each. You could set the "slow_query_log" DB Parameter and query the mysql.slow_log table to review the slow-running SQL queries.

##### Q: What happens when an RDS DB engine version is deprecated?

	When a minor version of a database engine is deprecated in Amazon RDS, we will provide a three (3) month period after the announcement before beginning automatic upgrades. At the end of the this period, all instances still running the deprecated minor version will be scheduled for automatic upgrade to the latest supported minor version during their scheduled maintenance windows.
	When a major version of database engine is deprecated in Amazon RDS, we will provide a minimum six (6) month period after the announcement of a deprecation for you to initiate an upgrade to a supported major version. At the end of this period, an automatic upgrade to the next major version will be applied to any instances still running the deprecated version during their scheduled maintenance windows.
	Once a major or minor database engine version is no longer supported in Amazon RDS, any DB instance restored from a DB snapshot created with the unsupported version will automatically and immediately be upgraded to a currently supported version.

##### Q: How will I be charged and billed for my use of Amazon RDS?

You pay only for what you use, and there are no minimum or setup fees. You are billed based on:

*  **instance hours** – Based on the class (e.g. db.t2.micro, db.m4.large) of the DB instance consumed. Partial DB instance hours consumed are billed as full hours.
* **Storage (per GB per month)** – Storage capacity you have provisioned to your DB instance. If you scale your provisioned storage capacity within the month, your bill will be pro-rated.
* **I/O requests per month** – Total number of storage I/O requests you have (for Amazon RDS Magnetic Storage and Amazon Aurora only)
* **Provisioned IOPS per month** – Provisioned IOPS rate, regardless of IOPS consumed (for Amazon RDS Provisioned IOPS (SSD) Storage only)
* **Backup Storage** – Backup storage is the storage associated with your automated database backups and any customer-initiated database snapshots. Increasing your backup retention period or taking additional database snapshots increases the backup storage consumed by your database.
* **Data transfer** – Internet data transfer in and out of your DB instance.

##### Q: When does billing of my Amazon RDS DB instances begin and end?

Billing commences for a DB instance as soon as the DB instance is available. Billing continues until the DB instance terminates, which would occur upon deletion or in the event of instance failure.

##### Q: Why does my additional backup storage cost more than allocated DB instance storage?

The storage provisioned to your DB instance for your primary data is located within a single Availability Zone. When your database is backed up, the backup data (including transactions logs) is geo-redundantly replicated across multiple Availability Zones to provide even greater levels of data durability. The price for backup storage beyond your free allocation reflects this extra replication that occurs to maximize the durability of your critical backups.

##### Q: What is a reserved instance (RI)?

Amazon RDS reserved instances give you the option to reserve a DB instance for a one or three year term and in turn receive a significant discount compared to the on-demand instance pricing for the DB instance. There are three RI payment options  -- No Upfront, Partial Upfront, All Upfront -- which enable you to balance the amount you pay upfront with your effective hourly price.  

##### Q: How are reserved instances different from on-demand DB instances?

Functionally, reserved instances and on-demand DB instances are exactly the same. The only difference is how your DB instance(s) are billed: With Reserved Instances, you purchase a one or three year reservation and in return receive a lower effective hourly usage rate (compared with on-demand DB instances) for the duration of the term. Unless you purchase reserved instances in a Region, all DB instances will be billed at on-demand hourly rates.


##### Q: Do reserved instances include a capacity reservation?

Amazon RDS reserved instances are purchased for a Region rather than for a specific Availability Zone. As RIs are not specific to an Availability Zone, they are not capacity reservations. This means that even if capacity is limited in one Availability Zone, reservations can still be purchased in the Region and the discount will apply to matching usage in any Availability Zone within that Region.

##### Q: How many reserved instances can I purchase?

You can purchase up to 40 reserved DB instances.

##### Q: Can I move a reserved instance from one Region or Availability Zone to another?

Each reserved instance is associated with a specific Region, which is fixed for the lifetime of the reservation and cannot be changed. Each reservation can, however, be used in any of the available AZs within the associated Region.


##### Q: Are reserved instances available for Multi-AZ deployments?

Yes. When you purchase a reserved instance, you can select the Multi-AZ option in the DB instance configuration available for purchase.


##### Q: Are reserved instances available for read replicas?

A DB instance reservation can be applied to a read replica, provided the DB instance class and Region are the same.


##### Q: What is the hardware configuration for Amazon RDS storage?

Amazon RDS uses EBS volumes for database and log storage. Depending on the size of storage requested, Amazon RDS automatically stripes across multiple EBS volumes to enhance IOPS performance.

##### Q: What is Amazon RDS General Purpose (SSD) storage?

Amazon RDS General Purpose (SSD) Storage is suitable for a broad range of database workloads that have moderate I/O requirements. With the baseline of 3 IOPS/GB and ability to burst up to 3,000 IOPS, this storage option provides predictable performance to meet the needs of most applications.

##### Q: What is Amazon RDS Provisioned IOPS (SSD) storage?

Amazon RDS Provisioned IOPS (SSD) Storage is an SSD-backed storage option designed to deliver fast, predictable, and consistent I/O performance. With Amazon RDS Provisioned IOPS (SSD) Storage, you specify an IOPS rate when creating a DB instance, and Amazon RDS provisions that IOPS rate for the lifetime of the DB instance. Amazon RDS Provisioned IOPS (SSD) Storage is optimized for I/O-intensive, transactional (OLTP) database workloads. For more details, please see the Amazon RDS User Guide.

##### Q: What is Amazon RDS Magnetic storage?

Amazon RDS magnetic storage is useful for small database workloads where data is accessed less frequently. Magnetic storage is not recommended for production database instances.

##### Q: How do I choose among the Amazon RDS storage types?
- Choose the storage type most suited for your workload.
- High-performance OLTP workloads: Amazon RDS Provisioned IOPS (SSD) Storage
- Database workloads with moderate I/O requirements: Amazon RDS General Purpose (SSD) Storage


##### Q: What are the minimum and maximum IOPS supported by Amazon RDS?

The IOPS supported by Amazon RDS varies by database engine.

##### Q: What is the difference between automated backups and DB Snapshots?

Amazon RDS provides two different methods for backing up and restoring your DB instance(s) automated backups and database snapshots (DB Snapshots).

The automated backup feature of Amazon RDS enables point-in-time recovery of your DB instance. When automated backups are turned on for your DB Instance, Amazon RDS automatically performs a full daily snapshot of your data (during your preferred backup window) and captures transaction logs (as updates to your DB Instance are made). When you initiate a point-in-time recovery, transaction logs are applied to the most appropriate daily backup in order to restore your DB instance to the specific time you requested. Amazon RDS retains backups of a DB Instance for a limited, user-specified period of time called the retention period, which by default is 7 days but can be set to up to 35 days. You can initiate a point-in-time restore and specify any second during your retention period, up to the Latest Restorable Time. You can use the DescribeDBInstances API to return the latest restorable time for you DB instance, which is typically within the last five minutes. Alternatively, you can find the Latest Restorable Time for a DB instance by selecting it in the AWS Management Console and looking in the “Description” tab in the lower panel of the Console.

DB Snapshots are user-initiated and enable you to back up your DB instance in a known state as frequently as you wish, and then restore to that specific state at any time. DB Snapshots can be created with the AWS Management Console, CreateDBSnapshot API, or create-db-snapshot command and are kept until you explicitly delete them.


##### Q: Do I need to enable backups for my DB Instance or is it done automatically?

By default, Amazon RDS enables automated backups of your DB Instance with a 7 day retention period. Free backup storage is limited to the size of your provisioned database and only applies to active DB Instances. 

##### Q: What is a backup window and why do I need it? Is my database available during the backup window?

The preferred backup window is the user-defined period of time during which your DB Instance is backed up. Amazon RDS uses these periodic data backups in conjunction with your transaction logs to enable you to restore your DB Instance to any second during your retention period, up to the LatestRestorableTime (typically up to the last few minutes). During the backup window, storage I/O may be briefly suspended while the backup process initializes (typically under a few seconds) and you may experience a brief period of elevated latency. There is no I/O suspension for Multi-AZ DB deployments, since the backup is taken from the standby.

Automated backups are deleted when the DB instance is deleted. Only manually created DB Snapshots are retained after the DB Instance is deleted.

##### Q: How is using Amazon RDS inside a VPC different from using it on the EC2-Classic platform (non-VPC)?

If your AWS account was created before 2013-12-04, you may be able to run Amazon RDS in an Amazon Elastic Compute Cloud (EC2)-Classic environment. The basic functionality of Amazon RDS is the same regardless of whether EC2-Classic or EC2-VPC is used. Amazon RDS manages backups, software patching, automatic failure detection, read replicas and recovery whether your DB Instances are deployed inside or outside a VPC.

##### Q: What is a DB Subnet Group and why do I need one?

A DB Subnet Group is a collection of subnets that you may want to designate for your RDS DB Instances in a VPC. Each DB Subnet Group should have at least one subnet for every Availability Zone in a given Region. When creating a DB Instance in VPC, you will need to select a DB Subnet Group. Amazon RDS then uses that DB Subnet Group and your preferred Availability Zone to select a subnet and an IP address within that subnet. Amazon RDS creates and associates an Elastic Network Interface to your DB Instance with that IP address.
Please note that, we strongly recommend you use the DNS Name to connect to your DB Instance as the underlying IP address can change (e.g., during failover).

##### Q: Can I move my existing DB instances outside VPC into my VPC?

If your DB instance is not in a VPC, you can use the AWS Management Console to easily move your DB instance into a VPC. See the Amazon RDS User Guide for more details. 
You can also take a snapshot of your DB Instance outside VPC and restore it to VPC by specifying the DB Subnet Group you want to use. 
Alternatively, you can perform a “Restore to Point in Time” operation as well.

##### Q: Can I move my existing DB instances from inside VPC to outside VPC?

Migration of DB Instances from inside to outside VPC is not supported. For security reasons, a DB Snapshot of a DB Instance inside VPC cannot be restored to outside VPC. The same is true with “Restore to Point in Time” functionality. 

##### Q: What precautions should I take to ensure that my DB Instances in VPC are accessible by my application?

You are responsible for modifying routing tables and networking ACLs in your VPC to ensure that your DB instance is reachable from your client instances in the VPC.
For Multi-AZ deployments, after failover, your client EC2 instance and RDS DB Instance may be in different Availability Zones. You should configure your networking ACLs to ensure that cross-AZ communication is possible.

##### Q: Can I change the DB Subnet Group of my DB Instance?

An existing DB Subnet Group can be updated to add more subnets, either for existing Availability Zones or for new Availability Zones added since the creation of the DB Instance. Removing subnets from an existing DB Subnet Group can cause unavailability for instances if they are running in a particular AZ that gets removed from the subnet group.

##### Q: How can I monitor the configuration of my Amazon RDS resources?

You can use AWS Config to continuously record configurations changes to Amazon RDS DB Instances, DB Subnet Groups, DB Snapshots, DB Security Groups, and Event Subscriptions and receive notification of changes through Amazon Simple Notification Service (SNS). You can also create AWS Config Rules to evaluate whether these RDS resources have the desired configurations.

##### Q: Are there any performance implications of running my DB instance as a Multi-AZ deployment?

You may observe elevated latencies relative to a standard DB instance deployment in a single Availability Zone as a result of the synchronous data replication performed on your behalf.

##### Q: When running my DB instance as a Multi-AZ deployment, can I use the standby for read or write operations?

No, a Multi-AZ standby cannot serve read requests



##### Q: Will my standby be in the same Region as my primary?

Yes. Your standby is automatically provisioned in a different Availability Zone of the same Region as your DB instance primary.

##### Q: Can I see which Availability Zone my primary is currently located in?

Yes, you can gain visibility into the location of the current primary by using the AWS Management Console or DescribeDBInstances API.

##### Q: How many read replicas can I create for a given source DB instance?

Amazon RDS for MySQL, MariaDB, PostgreSQL, and Oracle allow you to create up to 5 read replicas for a given source DB instance.

##### Q: Can I create a read replica in an AWS Region different from that of the source DB instance?

Yes, Amazon RDS supports cross-region read replicas. The amount of time between when data is written to the source DB instance and when it is available in the read replica will depend on the network latency between the two regions.

##### Q: Do Amazon RDS read replicas support synchronous replication?

No. Read replicas in Amazon RDS for MySQL, MariaDB, PostgreSQL, and Oracle are implemented using those engines' native asynchronous replication. Amazon Aurora uses a different, but still asynchronous, replication mechanism.

##### Q: Can I use a read replica to enhance database write availability or protect the data on my source DB instance against failure scenarios?

If you are looking to use replication to increase database write availability and protect recent database updates against various failure conditions, we recommend you run your DB instance as a Multi-AZ deployment. With Amazon RDS Read Replicas, which employ supported engines' native, asynchronous replication, database writes occur on a read replica after they have already occurred on the source DB instance, and this replication “lag” can vary significantly. In contrast, the replication used by Multi-AZ deployments is synchronous, meaning that all database writes are concurrent on the primary and standby. This protects your latest database updates, since they should be available on the standby in the event failover is required. In addition, with Multi-AZ deployments replication is fully managed. Amazon RDS automatically monitors for DB instance failure conditions or Availability Zone failure and initiates automatic failover to the standby (or to a read replica, in the case of Amazon Aurora) if an outage occurs.



##### Q: If my read replica(s) use a Multi-AZ DB instance deployment as a source, what happens if Multi-AZ failover occurs?

In the event of Multi-AZ failover, any associated and available read replicas will automatically resume replication once failover has completed (acquiring updates from the newly promoted primary).

##### Q: Can I create a read replica of another read replica?

Amazon Aurora, Amazon RDS for MySQL and MariaDB: You can create a second-tier read replica from an existing first-tier read replica. By creating a second-tier read replica, you may be able to move some of the replication load from the master database instance to a first-tier Read Replica. Please note that a second-tier Read Replica may lag further behind the master because of additional replication latency introduced as transactions are replicated from the master to the first tier replica and then to the second-tier replica.
Amazon RDS for PostgreSQL, Amazon RDS for Oracle: Read Replicas of Read Replicas are not currently supported.


##### Q: What are the two steps to reduce database overload and make db perform better?

1. Add read replicas and create read replicas of read replicas
2. Use Elasticache


