# Kinesis
---

Amazon kinesis is a platform on AWS to send your streaming data to. Kinesis makes it easy to load and analyze streaming data, and also providing the ability for you to build your own custom applications for your business needs.

### What is streaming data?
Streaming data is a data that is generated continously by thousands of data sources, which typacally sens in the data records simultaneously, and in small sizes.

- Once data is added in kinesis, it cant be deleted so data is immutable
- Ability to reprocess the data
- Billing is per shard provisioned
- Shards can be added (resharding) and reduced (merging) 
- Records are ordered per shard
- When Putting records, choose a partition key that is highly distributed to prevent hot partition (otherwise all data will go to the same shard)
- USe batching with put records to reduce costs and increase throughput
- ProvisionedThroughputExceeded if we go over the limits. To handle this
	- Retries with backoff
	- Increase shards
	- Ensure your partition key is good one (hot partition) 
- Hint: if you see words like ETL, Realtime, Big data analytics, iOT etc, it is possibly a kinesis scenario

---
Types:
---
1) Kinesis streams
	- Can store data from 24 hours to 7 days.
	- Kinesis streams consists of shards:
	    - 5 transactions per second for reads, upto a maximum total data read rate of 2 MB per second and up to 1,000 records per second for writes, up to a maximum total data write rate of 1 MB per second.
	 - the data capacity of your stream is a function of the number of shards that you specify for the stream. The total capacity of the stream is the sum of the capacities of its shards.
2) Kinesis firehose
	- no persisance
	- can have lambda functions and process data then output to s3, redhsift or elastic search cluster (optional) or splunk
	- no shards
	- near real time
	- supports many data formats, conversions, transformations, compressions

3) kinesis analytics
	- can analyze the data INSIDE kinesis in real time using sql
	- works with kinesis streams and kinesis firehose and analyze the data on the fly
	- managed: no servers to provision
	
---

Data Streams vs Fire hose
- Streams (hint: for analyzing data streams)
	- Going to write custom code (producer/consumer)
	- Real time
	- Must manage scaling (shard splitting / merging)
	- Data storage for 1 to 7 days, replay capablity, multi consumers
- Firehose (hint: for ingesting data streams to S3, Splunk, Redshift or Elasticsearch)
	- Fully managed, send to S3, Splunk, Redshift or ElasticSearch
	- Serverless data transformations with lambda
	- Near real time (lowest buffer time is 1 min)
	- Automated scaling
	- No data storage


##### Q: What is Amazon Kinesis Data Streams?

* Amazon Kinesis Data Streams enables you to build custom applications that process or analyze streaming data for specialized needs. You can continuously add various types of data such as clickstreams, application logs, and social media to an Amazon Kinesis data stream from hundreds of thousands of sources. Within seconds, the data will be available for your Amazon Kinesis Applications to read and process from the stream.

##### Q: What can I do with Amazon Kinesis Data Streams?

* Amazon Kinesis Data Streams is useful for rapidly moving data off data producers and then continuously processing the data, be it to transform the data before emitting to a data store, run real-time metrics and analytics, or derive more complex data streams for further processing. The following are typical scenarios for using Amazon Kinesis Data Streams:
	##### Accelerated log and data feed intake: 
    * Instead of waiting to batch up the data, you can have your data producers push data to an Amazon Kinesis data stream as soon as the data is produced, preventing data loss in case of data producer failures. For example, system and application logs can be continuously added to a data stream and be available for processing within seconds.
    ##### Real-time metrics and reporting: 
    * You can extract metrics and generate reports from Amazon Kinesis data stream data in real-time. For example, your Amazon Kinesis Application can work on metrics and reporting for system and application logs as the data is streaming in, rather than wait to receive data batches.
    ##### Real-time data analytics: 
    * With Amazon Kinesis Data Streams, you can run real-time streaming data analytics. For example, you can add clickstreams to your Amazon Kinesis data stream and have your Amazon Kinesis Application run analytics in real-time, enabling you to gain insights out of your data at a scale of minutes instead of hours or days.
    ##### Complex stream processing: 
    * You can create Directed Acyclic Graphs (DAGs) of Amazon Kinesis Applications and data streams. In this scenario, one or more Amazon Kinesis Applications can add data to another Amazon Kinesis data stream for further processing, enabling successive stages of stream processing.

#####  Q: What are the limits of Amazon Kinesis Data Streams?
* The throughput of an Amazon Kinesis data stream is designed to scale without limits via increasing the number of shards within a data stream. However, there are certain limits you should keep in mind while using Amazon Kinesis Data Streams:
- By default, Records of a stream are accessible for up to 24 hours from the time they are added to the stream. You can raise this limit to up to 7 days by enabling extended data retention.
- The maximum size of a data blob (the data payload before Base64-encoding) within one record is 1 megabyte (MB).
- Each shard can support up to 1000 PUT records per second.

##### Q: When should I use Amazon Kinesis Data Streams, and when should I use Amazon SQS?

We recommend Amazon Kinesis Data Streams for use cases with requirements that are similar to the following:

* Routing related records to the same record processor (as in streaming MapReduce). For example, counting and aggregation are simpler when all records for a given key are routed to the same record processor.
* Ordering of records. For example, you want to transfer log data from the application host to the processing/archival host while maintaining the order of log statements.
* Ability for multiple applications to consume the same stream concurrently. For example, you have one application that updates a real-time dashboard and another that archives data to Amazon Redshift. You want both applications to consume data from the same stream concurrently and independently.
* Ability to consume records in the same order a few hours later. For example, you have a billing application and an audit application that runs a few hours behind the billing application. Because Amazon Kinesis Data Streams stores data for up to 7 days, you can run the audit application up to 7 days behind the billing application.

We recommend Amazon SQS for use cases with requirements that are similar to the following:

* Messaging semantics (such as message-level ack/fail) and visibility timeout. For example, you have a queue of work items and want to track the successful completion of each item independently. Amazon SQS tracks the ack/fail, so the application does not have to maintain a persistent checkpoint/cursor. Amazon SQS will delete acked messages and redeliver failed messages after a configured visibility timeout.
* Individual message delay. For example, you have a job queue and need to schedule individual jobs with a delay. With Amazon SQS, you can configure individual messages to have a delay of up to 15 minutes.
* Dynamically increasing concurrency/throughput at read time. For example, you have a work queue and want to add more readers until the backlog is cleared. With Amazon Kinesis Data Streams, you can scale up to a sufficient number of shards (note, however, that you'll need to provision enough shards ahead of time).
* Leveraging Amazon SQS’s ability to scale transparently. For example, you buffer requests and the load changes as a result of occasional load spikes or the natural growth of your business. Because each buffered request can be processed independently, Amazon SQS can scale transparently to handle the load without any provisioning instructions from you.


##### Q: What is Amazon Kinesis Producer Library (KPL)?

* Amazon Kinesis Producer Library (KPL) is an easy to use and highly configurable library that helps you put data into an Amazon Kinesis data stream. KPL presents a simple, asynchronous, and reliable interface that enables you to quickly achieve high producer throughput with minimal client resources.

##### Q: What is Amazon Kinesis Agent?

* Amazon Kinesis Agent is a pre-built Java application that offers an easy way to collect and send data to your Amazon Kinesis data stream. You can install the agent on Linux-based server environments such as web servers, log servers, and database servers. The agent monitors certain files and continuously sends data to your data stream. 


##### Q: What is enhanced fan-out?

* Enhanced fan-out is an optional feature for Kinesis Data Streams consumers that provides logical 2 MB/sec throughput pipes between consumers and shards. This allows customers to scale the number of consumers reading from a data stream in parallel, while maintaining high performance.

##### Q: What is an Amazon Kinesis Application?

* An Amazon Kinesis Application is a data consumer that reads and processes data from an Amazon Kinesis data stream. You can build your applications using either Amazon Kinesis Data Analytics, Amazon Kinesis API or Amazon Kinesis Client Library (KCL).

##### Q: What is Amazon Kinesis Storm Spout?

* Amazon Kinesis Storm Spout is a pre-built library that helps you easily integrate Amazon Kinesis Data Streams with Apache Storm. The current version of Amazon Kinesis Storm Spout fetches data from Amazon Kinesis data stream and emits it as tuples. You will add the spout to your Storm topology to leverage Amazon Kinesis Data Streams as a reliable, scalable, stream capture, storage, and replay service.

##### Q: Why should I use server-side encryption instead of client-side encryption?

Customers often choose server-side encryption over client-side encryption for one of the following reasons:
* It hard to enforce client-side encryption
* They want a second layer of security on top of client-side encryption
* It is hard to implement client-side key management schemes

##### Q: What is server-side encryption?

* Server-side encryption for Kinesis Data Streams automatically encrypts data using a user specified AWS KMS master key (CMK) before it is written to the data stream storage layer, and decrypts the data after it is retrieved from storage. Encryption makes writes impossible and the payload and the partition key unreadable unless the user writing or reading from the data stream has the permission to use the key selected for encryption on the data stream. As a result, server-side encryption can make it easier to meet internal security and compliance requirements governing your data.

##### Q: Is there an additional cost associated with the use of server-side encryption?
Yes, however if you are using the AWS-managed CMK for Kinesis and are not exceeding the free tier KMS API usage costs, then your use of server-side encryption is free. The following describes the costs by resource:
Keys:
* The AWS-managed CMK for Kinesis (alias = “aws/kinesis”) is free.
* User generated KMS keys are subject to KMS key costs.
