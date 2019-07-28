# EFS
---

##### Q. What use cases does Amazon EFS support?
* Amazon EFS is designed to provide performance for a broad spectrum of workloads and applications, including Big Data and analytics, media processing workflows, content management, web serving, and home directories.

##### Q. When should I use Amazon EFS vs. Amazon S3 vs. Amazon Elastic Block Store (EBS)?

Amazon Web Services (AWS) offers cloud storage services to support a wide range of storage workloads.

* **Amazon EFS** is a file storage service for use with Amazon EC2. Amazon EFS provides a file system interface, file system access semantics (such as strong consistency and file locking), and concurrently-accessible storage for up to thousands of Amazon EC2 instances.

* **Amazon EBS** is a block level storage service for use with Amazon EC2. Amazon EBS can deliver performance for workloads that require the lowest-latency access to data from a single EC2 instance.

* Amazon S3 is an object storage service. Amazon S3 makes data available through an Internet API that can be accessed anywhere.

#####  Q. How much data can I store?

Amazon EFS file systems can store petabytes of data. Amazon EFS file systems are elastic, and automatically grow and shrink as you add and remove files. You do not provision file system size or specify a size up front, and you pay only for the storage you use.

##### Q. How many Amazon EC2 instances can connect to a file system?

Amazon EFS supports one to thousands of Amazon EC2 instances connecting to a file system concurrently.

|   | Amazon EFS  | Amazon EBS (io1)  |
| ------------ | ------------ | ------------ |
| Per-operation latency  | Low, consistent  | Lowest, consistent  |
|  Throughput scale | Multiple GBs per second  | Single GB per second |


##### Q. What’s the difference between “General Purpose” and “Max I/O” performance modes? Which one should I choose?

- “**General Purpose**” performance mode is appropriate for most file systems, and is the mode selected by default when you create a file system.
* “**Max I/O**” performance mode is optimized for applications where tens, hundreds, or thousands of EC2 instances are accessing the file system — it scales to higher levels of aggregate throughput and operations per second with a tradeoff of slightly higher latencies for file operations.

##### Q. How do I control which Amazon EC2 instances can access my file system?

When you create a file system, you create endpoints in your VPC called “mount targets.” When mounting from an EC2 instance, your file system’s DNS name, which you provide in your mount command, resolves to a mount target’s IP address. Only resources that can access a mount target can access your file system. You can control the network traffic to and from your file system mount targets using VPC security groups.
