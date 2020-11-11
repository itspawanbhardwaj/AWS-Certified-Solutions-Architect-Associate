Aurora
---

Amazon Aurora is a MySQL compatible relational database engine that combines the speed and availability of high-end commercial databases with the simplicity and cost-effectiveness of open source databases Amazon Aurora provides up to five times better performance than MySQL at a price point one tenth that of a commercial database while delivering similar performance and availability.


Amazon Aurora MySQL delivers up to five times the performance of MySQL without requiring any changes to most MySQL applications; similarly, Amazon Aurora PostgreSQL delivers up to three times the performance of PostgreSQL. Amazon RDS manages your Amazon Aurora databases, handling time-consuming tasks such as provisioning, patching, backup, recovery, failure detection and repair.

- Starts with 10GB, Scale in 10GB increments to 64TB (storage autoscaling)
- Compute resources can scale upto 32vCPU and 244GB of Memory
- 2 copies of your data is contained in each availability zone, with minimum of 3 availability zones. 6 copies of your data.

Scaling
--------
- Aurora is designed to transparently handle the loss of upto two copies of data without affecting database write availability and upto three copies without affecting read availability.
- Aurora storage is also self-healing. Data blocks and discs are continously scanned for errors and repaired automatically.

Types of replica
----------------
- Aurora replicas (currently 15)
- MySQL read replicas (currently 5)


Backups
----------
- Automatic **backups** are always enabled on Aurora. backups do not impact the database performance
- You can also take **snapshots** with Aurora. This also does not impact on performance.
- You can share snapshots with other AWS account
------

##### Q: What are the minimum and maximum storage limits of an Amazon Aurora database?
The minimum storage is **10GB**. Based on your database usage, your Amazon Aurora storage will automatically grow, up to **64 TB**, in **10GB increments** with no impact to database performance. There is no need to provision storage in advance.


#####  Q: Can I take DB Snapshots and keep them around as long as I want?
**Yes**, and there is no performance impact when taking snapshots. Note that **restoring data from DB Snapshots requires creating a new DB Instance**.

##### Q. Can I share my Aurora snapshots across different regions?
**No**. Your shared Aurora snapshots will only be accessible by accounts in the same region as the account that shares them.

##### Q: Can I share an encrypted Aurora snapshot?
**Yes**, you can share encrypted Aurora snapshots.

 
|  **Feature** | **Amazon Aurora Replicas**  |  **MySQL Replicas** |
| ------------ | ------------ | ------------ |
|**Number of replicas**| Up to 15| Up to 5|
|**Replication type**| Asynchronous (milliseconds)| Asynchronous (seconds)|
|**Performance impact on primary**| Low| High|
|**Replica location**| In-region|Cross-region|
|**Act as failover target**| Yes (no data loss)| Yes (potentially minutes of data loss)|
|**Automated failover**| Yes| No|
|**Support for user-defined replication delay**| No| Yes|
|**Support for different data or schema vs. primary**| No| Yes|



##### Q: If I have a primary database and an Amazon Aurora Replica actively taking read traffic and a failover occurs, what happens?

Amazon RDS will automatically detect a problem with your primary instance and begin routing your read/write traffic to an Amazon Aurora Replica. On average, this failover will complete within 30 seconds. In addition, the read traffic that your Aurora Replicas were serving will be briefly interrupted.


##### Q: Can I set up replication between my Aurora MySQL database and an external MySQL database?

* **Yes**, you can set up **binlog replication** between an Aurora MySQL instance and an external MySQL database. The other database can run on Amazon RDS, or as a self-managed database on AWS, or completely outside of AWS.

* If you're running Aurora MySQL 5.7, consider setting up **GTID-based binlog replication**. This will provide complete consistency so your replication won’t miss transactions or generate conflicts, even after failover or downtime.

##### Q: What is Amazon Aurora Global Database?

Amazon Aurora Global Database is a feature that allows a single Amazon Aurora database to span multiple AWS regions. It replicates your data with no impact on database performance, enables fast local reads in each region with typical latency of less than a second, and provides disaster recovery from region-wide outages. In the unlikely event of a regional degradation or outage, a secondary region can be promoted to full read/write capabilities in less than 1 minute.
* This feature is available for Amazon Aurora MySQL.

##### Q: If I use Aurora Global Database, can I also use logical replication (binlog) on the primary database?

**Yes**. If your goal is to analyze database activity, consider using Aurora advanced auditing, general logs, and slow query logs instead, to avoid impacting the performance of your database.

##### Q: What is Amazon Aurora Multi-Master?
Amazon Aurora Multi-Master is a new feature of the Aurora MySQL-compatible edition that adds the ability to scale out write performance across multiple Availability Zones, allowing applications to direct read/write workloads to multiple instances in a database cluster and operate with higher availability.
