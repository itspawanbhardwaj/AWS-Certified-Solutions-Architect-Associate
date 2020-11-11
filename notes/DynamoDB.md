# DynamoDB
---

- Amazon DynamoDB is a fast and flexible NoSQL database service for all applications that need consistant, single-digit millisecond latency at any scale.
- It is a fully managed database and supposts both document and key-value data models.
- Its flexible data model and reliable performance make it a great fit for mobile, web, gaming, ad-tech,Iot and many other applications.
- Stored on SSD storage
- Spread across 3 geographical distinct data center
- Eventual consistant read
- Strongly consistant read
- Indexes: Global and local secondary indixes
- DynamoDB Acceleration(DAX)- in-memory cache for dynamodb. Fully managed. Millions of request per second for dynamodb and you want to reduce latency to access to the DynamoDB table.
- Cant be deployed in multi region
- All data items are stored on Solid State Drives (SSDs) and are automatically replicated across multiple Availability Zones in a region to provide built-in high availability and data durability.
- DynamoDB Streams:  Changes in DynamoDB (CRUD) can end up in a dynamodb stream. Cross region replication is implemented using streams. This stream can be read by Lambda and then
	- React to them in real time eg welcome mail to new users
	- Analytics
	- Create derivative table or views
	- Insert in elastic search
- Transcations: All or nothing type of operation. Coordinated insertion, update and delete accross multiple tables
- On Demand: Instead of provisioning RCU and WCU,use on demand. Scales automatically. 2.5x more expensive. Used when traffic is unpredictable
- Global table: Cross region replication. Dynamodb streams must be enabled 


Consistency model:
---
**Eventually consistest Reads** (default) (read from all the node)
- Consistence accross all copies of data is usually reached within a second. 
- Repeating read after a short time should return the updated data (Best read performance)

**Strongly consistest reads** (read from primary node)
- A strongly consistent read reutrns a result that reflects all writes the received a successful response prior to the read, (as soon as the update is made, less than a second)

Partition
---

**Partition**: Sort Key uses two attributes together to uniquely identify an item.
* Within unordered hash index, data is arranged by the sort key
* No limit on the number of items per partition key, except if you have local secondary indexes.
* Partitions are three-way replicated.(Eventually consistest read is recommended)

Local secondary Index vs Global secondary index
-----------------------------------------------
* Local secondary index allow you to resort the data in the partition.
* Global secondary index allow you to create completely new aggregation of the data. We regroup resort re-aggregate.
* GSI updates are Eventually consistest
* LSI are strongly consistest
* Local secondary indexes can only be created when the table is being created.
* You can only have one local secondary index.

---------------

Scaling NoSQL
-------------
- auto scales

Partitions key should be:
	- column with large number of distinct values 
	- items are uniformly requested and randomly distributed

Sort Key
	- Model 1:n and n:n relationship
	- Levarage range queries

Nature of Usecase:
	OLTP/OLAP/ DSS

Transactions API
---
- TransactWriteItems
	- Synchronous update, put, delete and check. Automic and automated rollbacks
	- Up to 10 items within a transaction
	- Supports multiple tables
	- Complex conditional checks
- Dosent lives in VPC

---
##### Q: What is the consistency model of DynamoDB?

When reading data from DynamoDB, users can specify whether they want the read to be eventually consistent or strongly consistent:

	Eventually consistent reads (the default) – The eventual consistency option maximizes your read throughput. However, an eventually consistent read might not reflect the results of a recently completed write. All copies of data usually reach consistency within a second. Repeating a read after a short time should return the updated data.
	Strongly consistent reads — In addition to eventual consistency, DynamoDB also gives you the flexibility and control to request a strongly consistent read if your application, or an element of your application, requires it. A strongly consistent read returns a result that reflects all writes that received a successful response before the read.

