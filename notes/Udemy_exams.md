#### Which services are not scoped in regions?
AWS consoles are region scoped except IAM and S3

##### Which protocols does ELB use to support the load balancing of applications? 
- HTTP, HTTPS, TCP and SSL

##### Is it possible to get a history of all EC2 API calls made on your account for security analysis and operational troubleshooting purposes? 
- Yes, you should turn on the Cloud Trail Console.

##### Are penetration tests allowed as long as they are limited to the customers instances?
Yes, they are allowed but only with approval


##### How many types of block devices does Amazon EC2 support?
- Amazon EC2 supports 2 types of block devices


##### A user wants to increase the durability and availability of the EBS volume. Which of the below mentioned actions should he perform?
- Take regular snapshots

##### Which of the following would you use to list your AWS import/Export jobs? 
- You can list AWS Import/Export jobs with the List Jobs command using the command line client or REST API.

##### Which of the following statements is true regarding attaching network interfaces to your instances in your VPC? 
- Each instance in your VPC has a default network interface that is assigned a private IP address from the IP address range of your VPC. You can create and attach an additional network interface, known as an elastic network interface (ENI), to any instance in your VPC. The number of ENIs you can attach varies by instance type.


##### Mike is appointed as Cloud Consultant in Net crak Inc. Net crak has the following VPCs set-up in the US East Region: A VPC with CIDR block 10.10.0.0/16, a subnet in that VPC with CIDR block 10.10.1.0/24 A VPC with CIDR block 10.40.0.0/16, a subnet in that VPC with CIDR block 10.40.1.0/24 Netcrak Inc is trying to establish network connection between two subnets, a subnet with CIDR block 10.10.1.0/24 and another subnet with CIDR block 10.40.1.0/24. Which one of the following solutions should Mke recommend to Netcrak Inc? 
- A VPC peering connection is a networking connection between two VPCs that enables you to route traffic between them using private IP addresses. EC2 instances in either VPC can communicate with each other as if they are within the same network. You can create a VPC peering connection between your own VPC, or with a VPC in another AWS account within a single region. AWS uses the existing infrastructure of a VPC to create a VPC peering connection, it is neither a gateway nor a VPN connection, and does not rely on a separate piece of physical hardware.

##### In Amazon EC2, what is the limit of Reserved Instances per Availability Zone each month? 

- There are 20 Reserved Instances per Availability Zone in each month

##### Which of the following best describes the function of an AWS Storage Gateway?
- AWS Storage Gateway connects an on-premises software appliance with cloudbased storage to provide seamless integration with data security features between your on-premises IT environment and the Amazon Web Services (AWS) storage infrastructure. You can use the service to store data in the AWS cloud for scalable and cost-effective storage that helps maintain data security. AWS Storage Gateway offers both volume-based and tape-based storage solutions: Volume gateways Gateway-cached volumes Gateway-stored volumes Gateway-virtual tape library (VTL)


##### Which of the following is not a benefit of using multipart uploads? 
- Multipart upload in Amazon S3 allows you to upload a single object as a set of parts. Each part is a contiguous portion office objects data. 
- You can upload these object parts independently and in any order. If transmission of any part fails, you can re-transmit that part without affecting other parts. After all parts of your object are uploaded, Amazon S3 assembles these parts and creates the object. 
- In general, when your object size reaches 100 MB, you should consider using multipart uploads instead of uploading the object in a single operation. Using multipart upload provides the following advantages:
	1. Improved throughput— You can upload parts in parallel to improve throughput. 
	2. Quick recovery from any network issues-Smaller part size minimizes the impact of restarting a failed upload due to a network error. 
	3. Pause and resume object uploads—You can upload object parts overtime. Once you initiate a multipart upload there is no expiry; you must explicitly complete or abort the multipart upload.
	4. Begin an upload before you know the final object size--You can upload an object as you are creating it.


##### When does the billing of an Amazon EC2 system begin? 
- Billing commences when Amazon EC2 initiates the boot sequence of an AM instance. Billing ends when the instance terminates, which could occur through a web services command, by running shutdown, or through instance failure. When you stop an instance, Amazon shuts it down but does not charge hourly usage for a stopped instance, or data transfer fees, but charges for the storage for any Amazon EBS volumes.

##### Cloud HSM requirements?
- AWS Cloud HSM provides secure cryptographic key storage to customers by making hardware security modules (HSM) available in the AWS cloud. 
- AWS Cloud HSM requires the following environment before an HSM appliance can be provisioned. 
	1. A virtual private cloud (VPC) in the region where you want the AWS Cloud HSM service. 
	1. One private subnet (a subnet with no Internet gateway) in the VPC. The HSM appliance is provisioned into this subnet. 
	3. One public subnet (a subnet with an Internet gateway attached). The control instances are attached to this subnet. 
	4. An AWS Identity and Access Management (IAM) role that delegates access to your AWS resources to AWS Cloud HSM. An EC2 instance, in the same VPC as the HSM appliance, that has the Safe Net client software installed. This instance is referred to as the control instance and is used to connect to and manage the HSM appliance. 
	5. A security group that has port 22 (for SSH) or port 3389 (for RDP) open to your network. This security group is attached to your control instances so you can access them remotely.

- In AWS Cloud HSM, you can perform a remote backup/restore of a Luna SA partition if you have purchased a Luna Backup HSM.
- The AWS Cloud HSM service defines a resource known as a high-availability (HA) partition group, which is a virtual partition that represents a group of partitions, typically distributed between several physical HSMs for high-availability
- In relation to AWS Cloud HSM, High-availability (HA) recovery is hands-off resumption by failed HA group members. Prior to the introduction of this function, the HA feature provided redundancy and performance, but required that a failed/lost group member be manualy reinstated.


##### An EC2 instance is connected to an ENI (Elastic Network Interface) in one subnet. What happens when you attach an ENI of a different subnet to this EC2 instance?  
- AWS allows you create an elastic network interface (ENI), attach an ENI to an EC2 instance, detach an ENI from an EC2 instance and attach this ENI to another EC2 instance. The attributes of a network traffic follow the ENI which is attached to an EC2 instance or detached from an EC2 instance. When you move an ENI from one EC2 instance to another, network traffic is redirected to the new EC2 instance. You can create and attach additional ENIs to an EC2 instance. Attaching multiple network interfaces (ENIs) to an EC2 instance is useful to: Create a management network. Use network and security appliances in your VPC. Create dual-homed instances with workloads/roles on distinct subnets Create a low-budget, highavailability solution

##### What is the time period with which metric data is sent to Cloud Watch when detailed monitoring is enabled on an Amazon EC2 instance? 
- By default, Amazon EC2 metric data is automatically sent to Cloud Watch in 5-minute periods. However, you can, enable detailed monitoring on an Amazon EC2 instance, which sends data to Cloud Watch in 1-minute periods

##### You are using Amazon SES as an email solution but are unsure of what its limitations are. Which statement below is correct in regards to that? 
- Amazon Simple Email Service (Amazon SES) is a highly scalable and cost-effective email- sending service for businesses and developers. Amazon SES eliminates the complexity and expense of building an in-house email solution or licensing, installing, and operating a third- party email service for this type of email communication. Every Amazon SES sender has a unique set of sending limits, which are calculated by Amazon SES on an ongoing basis: Sending quota — the maximum number of emails you can send in a 24-hour period. Maximum send rate — the maximum number of emails you can send per second. New Amazon SES users who have received production access can send up to **10,000 emails per 24-hour period, at a maximum rate of 5 emails per second**. Amazon SES automatically adjusts these limits upward, as long as you send highquality email. If your existing quota is not adequate for your needs and the system has not automatically increased your quota, you can submit an SES Sending Quota Increase case at any time. Sending limits are based on recipients rather than on messages. You can check your sending limits at any time by using the Amazon SES console. Note that if your email is detected to be of poor or questionable quality (e.g., high complaint rates, high bounce rates, spam, or abusive content), Amazon SES might temporarily or permanently reduce your permitted send volume, or take other action as AWS deems appropriate


##### A major client who has been spending a lot of money on his internet service provider asks you to set up an AWS Direct Connection to try and save him some money. You know he needs high-speed connect Myth. Which connection port speeds are available on AWS Direct Connect? 
- AWS Direct Connect is a network service that provides an alternative to using the internet to utilize AWS cloud services. Using AWS Direct Connect, data that would have previously been transported over the Internet can now be delivered through a private network connection between AWS and your datacenter or corporate network. 1Gbps and 10Gbps ports are available. Speeds of 50Mbps, 100Mbps, 200Mbps, 300Mbps, 400Mbps, and 500Mbps can be ordered from any APN partners supporting AWS Direct Connect.


##### You have three Amazon EC2 instances with Elastic IP addresses in the US East (Virginia) region, and you want to distribute requests across all three IPs evenly for users for whom US East (Virginia) is the appropriate region. How many EC2 instances would be sufficient to distribute requests in other regions? 
- If your application is running on Amazon EC2 instances in two or more Amazon EC2 regions, and if you have more than one Amazon EC2 instance in one or more regions, you can use latency-based routing to route traffic to the correct region and then use weighted resource record sets to route traffic to instances within the region based on weights that you specify. For example, suppose you have three Amazon EC2 instances with Elastic IP addresses in the US East (Virginia) region and you want to distribute requests across all three IPs evenly for users for whom US East (Virginia) is the appropriate region. Just one Amazon EC2 instance is sufficient in the other regions, although you can apply the same technique to many regions at once.


##### In Amazon Cloud Front, if you use Amazon EC2 instances and other custom origins with Cloud Front, it is recommended to? 
- In Amazon Cloud Front, you should use an Elastic Load Balancing load balancer to handle traffic across multiple Amazon EC2 instances and to isolate your application from changes to Amazon EC2 instances. When you create your Cloud Front distribution, specify the URL of the load balancer for the domain name of your origin server.

##### What is the data model of Dynamo DB? 
- The data model of Dynamo DB is: 
Table, a collection of Items;
items, with Keys and one or more Attribute;
Attributes, with Name and Value.

##### Amazon Elastic Load Balancing is used to manage traffic on a fleet of Amazon EC2 instances, distributing traffic to instances across all availability zones within a region. Elastic Load Balancing has all the advantages of an on-premises load balancer, plus several security benefits. Which of the following is not an advantage of ELB over an on-premise load balancer? 
- Amazon Elastic Load Balancing is used to manage traffic on a fleet of Amazon EC2 instances, distributing traffic to instances across all availability zones within a region. Elastic Load Balancing has all the advantages of an on-premises load balancer, plus several security benefits:
* Takes over the encryption and decryption work from the Amazon EC2 instances and manages it centrally on the load balancer Offers clients a single point of contact, and can also serve as the first line of defense against attacks on your network When used in an Amazon VPC
* Supports creation and management of security groups associated with your Elastic Load Balancing to provide additional networking and security options Supports end-to-end traffic encryption using TLS (previously SSL) on those networks that use secure HTTP (HTTPS) connections. 
* When TLS is used, the TLS server certificate used to terminate client connections can be managed centrally on the load balancer, rather than on every individual instance.

##### What happens to Amazon EBS root device volumes, by default, when an instance terminates? 
- By default, Amazon EBS root device volumes are automatically deleted when the instance terminates

##### A user is sending bulk emails using AWS SES. The emails are not reaching some of the targeted audience because they are not authorized by the ISPs. How can the user ensure that the emails are all delivered? 
- Domain Keys Identified Mail (DKIM) is a standard that allows senders to sign their email messages and ISPS, and use those signatures to verify that those messages are legitimate and have not been modified by a third party in transit.

##### In Amazon Elastic Compute Cloud, which of the following is used for communication between instances in the same network (EC2-Classic or a VPC)?
- A private IP address is an IP address that‟s not reachable over the Internet. You can use private IP addresses for communication between instances in the same network (EC2Classic or a VPC).

##### You want to use AWS Import/Export to send data from your S3 bucket to several of your branch offices. What should you do if you want to send 10 storage units to AWS? 
- When using Amazon Import/Export, a separate job request needs to be submitted for each physical device even if they belong to the same import or export job.


##### You need to measure the performance of your EBS volumes as they seem to be under performing. You have come up with a measurement of 1,024 KB I/O but your colleague tells you that EBS volume performance is measured in IOPS. How many IOPS Is equal to 1, 024 KB I/O?
- Several factors can affect the performance of Amazon EBS volumes, such as *instance configuration, 110 characteristics, workload demand, and storage configuration*. IOPS are Input/output operations per second. Amazon EBS measures each I/O operation per second (that is 256 KB or smaller) as one IOPS. I/O operations that are larger than 256 KB are counted in 256 KB capacity units. For example, a 1,024 KB I/O operation would count as 4 IOPS. When you provision a 4,000 lops volume and attach it to an EBS-optimized instance that can provide the necessary bandwidth, you can transfer up to 4, 000 chunks of data per second (provided that the I/O does not exceed the 128 MB/s per volume throughput limit of General Purpose (SSD) and Provisioned IOPS (SSD) volumes)

##### In Amazon Route 53, you can create a hosted zone for a top-level domain (TLD)?
- In Amazon Route 53, you cannot create a hosted zone for a top-level domain (TID).

##### A major customer has asked you to set up his AWS infrastructure so that it will be easy to recover in the case of a disaster of some sort. Which of the following is important when thinking about being able to quickly launch resources in AWS to ensure business continuity in case of a disaster?
- In the event of a disaster to your AWS infrastructure you should be able to quickly launch resources in Amazon Web Services (AWS) to ensure business continuity. The following are some key steps you should have in place for preparation: 
	1. Set up Amazon EC2 instances to replicate or mirror data. 
	2. Ensure that you have all supporting custom software packages available in AWS. 
	3. Create and maintain AMIs of key servers where fast recovery is required. 
	4. Regularly run these servers, test them, and apply any software updates and configuration changes. 
	5. Consider automating the provisioning of AWS resources.

##### You are setting up a very complex financial services grid and so far it has 5 Elastic IP (EIP) addresses. You go to assign another EIP address, but all accounts are limited to 5 Elastic IP addresses per region by default, so you aren‟t able to. What is the reason for this? 
- Public (IPv4) internet address are a scare resource.

##### A user has created an application which will be hosted on EC2. The application makes calls to Dynamo DB to fetch certain data. The application is using the Dynamo DB SDK to connect with from the EC2 instance. Which of the below mentioned statements is true with respect to the best practice for security in this scenario?
- With AWS IAM a user is creating an application which runs on an EC2 instance and makes requests to AWS, such as Dynamo DB or S3 calls. Here it is recommended that the user should not create an IAM user and pass the user‟s credentials to the application or embed those credentials inside the application. Instead, the user should use roles for EC2 and give that role access to Dynamo DB & S3. When the roles are attached to EC2, it will give temporary security credentials to the application hosted on that EC2, to connect with Dynamo DB & S3.

##### In Amazon EC2, while sharing an Amazon EBS snapshot, can the snapshots with AWS marketplace product codes be public? 
- Snapshots with AWS Marketplace product codes cant be made public.

##### You need to set up a complex network infrastructure for your organization that will be reasonably easy to deploy, replicate, control, and track changes on, Which AWS service would be best to use to help you accomplish this?
- AWS Cloud Formation is a service that helps you model and set up your Amazon Web Services resources so that you can spend less time managing those resources and more time focusing on your applications that run in AWS. You create a template that describes all the AWS resources that you want (like Amazon EC2 instances or Amazon RDS DB instances), and AWS Cloud Formation takes care of provisioning and configuring those resources for you. You do not need to individually create and configure AWS resources and figure out what dependent on what. AWS Cloud Formation handles all of that.

##### You are building a system to distribute confidential documents to employees. Using Cloud Front, what method could be used to serve content that is stored In S3, but not publically accessible from S3 directly? 
- You restrict access to Amazon S3 content by creating an origin access identity, which is a special Cloud Front user.

##### Which of the following statements is true in regards to what ability launching your instances into a VPC instead of EC2-Classic gives you? 
- By launching your instances into a VPC instead of EC2-Classic, you gain the ability to: Assign static private IP addresses to your instances that persist across stalls and stops Assign multiple IP addresses to your Instances Define network interfaces, and attach one or more network interfaces to your instances Change security group membership for your instances while they are running Control the outbound traffic from your instances (egress filtering) in addition to controlling the inbound traffic to them (ingress filtering) Add an additional layer of access control to your instances in the form of network access control lists (ACL) Run your instances on single-tenant hardware

##### You are architecting an auto-scalable batch processing system using video processing pipelines and Amazon Simple Queue Service (Amazon SQS) for a customer. You are unsure of the limitations of SQS and need to find out. What do you think is a correct statement about the limitations of Amazon SQS? 
- Amazon Simple Queue Service (Amazon SQS) is a messaging queue service that handles message or workflows between other components in a system. Amazon SQS supports an unlimited number of queues and unlimited number of messages per queue for each user. Please be aware that Amazon SQS automatically deletes messages that have been in the queue for more than 4 days.

##### You are setting up your first Amazon Virtual Private Cloud (Amazon VPC) so you decide to use the VPC wizard in the AWS console to help make it easier for you. Which of the following statements is correct regarding instances that you launch into a default subnet via the VPC wizard? 
- Instances that you launch into a default subnet receive both a public IP address and a private IP address. 
- Instances in a default subnet also receive both public and private DNS hostnames. 
- Instances that you launch into a non default subnet in a default VPC don't receive a public IP address or a DNS hostname. You can change your subnets default public IP addressing behavior

##### After selling up several database instances in Amazon Relational Database Service (Amazon RDS) you decide that you need to track the performance and health of your databases. How can you do this? 
- Amazon Relational Database Service (Amazon RDS) is a web service that makes it easier to set up. operate, and scale a relational database In the cloud. It provides cost-efficient, resizable capacity for an industry-standard relational database and manages common database administration tasks. There are several ways you can track the performance and health of a database or a DB instance. You can: 
	- Use the free Amazon Cloud Watch service to monitor the performance and health of a DB instance. 
	- Subscribe to Amazon RDS events to be notified when changes occur with a DB instance, DB snapshot, DB parameter group, or DB security group. 
	- View, download, or watch database log files using the Amazon RDS console or Amazon RDS APIs. 
	- You can also query some database log files that are loaded Into database tables. 
	- Use the AWS Cloud Trail service to record AWS calls made by your AWS account. The calls are recorded in log files and stored in an Amazon S3 bucket.

##### By default, what is the maximum number of Auto Scaling groups that AWS will allow?
- 20

##### Having set up a website to automatically be redirected to a backup website if it fails, you realize that there are different types of failovers that are possible. You need all your resources to be available the majority of the time. Using Amazon Route 53 which configuration would best suit this requirement? 
- You can set up a variety of failover configurations using Amazon Route 53 alias: weighted, latency, go location routing, and failover resource record sets. 
- Active-active failover: Use this failover configuration when you want all of your resources to be available the majority of the time. When a resource becomes unavailable, Amazon Route 53 can detect that it‟s unhealthy and stop including it when responding to queries. 
- Active-passive failover: Use this failover configuration when you want a primary group of resources to be available the majority of the time and you want a secondary group of resources to be on standby in case all of the primary resources become unavailable. When responding to queries, Amazon Route 53 includes only the healthy primary resources. If all of the primary resources are unhealthy, Amazon Route 53 begins to include only the healthy secondary resources in response to DNS queries. 
- Activeactive-passive and other mixed configurations: You can combine alias and non-alias resource record sets to produce a variety of Amazon Route 53 behaviors.

##### A customer enquires about whether all his data is secure on AWS and is especially concerned about Elastic Map Reduce (EMR) so you need to inform him of some of the security features in place for AWS. Which of the below statements would be an incorrect response to your customers enquiry? 
- Amazon S3 provides authentication mechanisms to ensure that stored data is secured against unauthorized access. Unless the customer who is uploading the data specifies otherwise, only that customer can access the data. Amazon EMR customers can also choose to send data to Amazon S3 using the HTTPS protocol for secure transmission. In addition, Amazon EMR always uses HTTPS to send data between Amazon S3 and Amazon EC2. For added security, customers may encrypt the input data before they upload it to Amazon S3 (using any common data compression tool); they then need to add a decryption step to the beginning of their cluster when Amazon EMR fetches the data from Amazon S3.

##### A user has created a subnet In VPC and launched an EC2 Instance within It. The user has not selected the option to assign the IP address while launching the instance. The user has 3 elastic IPs and is trying to assign one of the Elastic Ps to the VPC instance from the console. The console does not show any instance in the IP assignment screen. What is a possible reason that the instance Is unavailable in the assigned IP console? 
- A Virtual Private Cloud (VPC) is a virtual network dedicated to the user‟s AWS account. A user can create a subnet with VPC and launch instances inside that subnet. When the user is launching an instance he needs to select an option which attaches a public IP to the instance. If the user has not selected the option to attach the public IP then it will only have a private IP when launched. If the user wants to connect to an instance from the internet he should create an elastic IP with VPC. If the elastic IP is a part of EC2 Classic it cannot be assigned to a VPC instance

##### A user has attached 1 EBS volume to a VPC instance. The user wants to achieve the best fault tolerance of data possible. Which of the below mentioned options can help achieve fault tolerance? 
- The user can join multiple provisioned IOPS volumes together in a RAID 1 configuration to achieve better fault tolerance. RAID 1 does not provide a write performance improvement; it requires more bandwidth than non RAID configurations since the data is written simultaneously to multiple volumes.

##### A user has configured ELB with two EBS backed EC2 instances. The user is trying to understand the DNS access and IP support for ELB. Which of the below mentioned statements may not help the user understand the IP mechanism supported by ELB? 
- Elastic Load Balancing supports both Internet Protocol version 6 (IPv6) and Internet Protocol version 4 (IPv4). Clients can connect to the user‟s load balancer using either lPv4 or lPv6 (In EC2-Clinstances uses only lPv4. The user can use the Dual stack-prefixed DNS name to enable IPv6 support for communications between the client and the load balancers. Thus, the clients are able to access the load balancer using either lPv4 or lPv6 as their individual connect Myth needs dictate.


##### Can resource record sets in a hosted zone have a different domain suffix (for example, www.blog.  acme.com and www.acme.ca)?  
- The resource record sets contained in a hosted zone must share the same suffix. For example, the example.com hosted zone can contain resource record sets for www.example.com and wvvw.aws.example.com sub domains, but it cannot contain resource record sets for a www.example.ca sub domain

##### A user is accessing an EC2 instance on the SSH port for IP 1 0.20.30.40. Which one is a secure way to configure that the instance can be accessed only from this IP? 
- In AWS EC2, while configuring a security group, the user needs to specify the IP address in CIDR notation. The CIDR IP range 10.20.30.40/32 says it is for a single IP 10.20.30.40. If the user specifies the IP as 10.20.30.40 only, the security group will not accept and ask it in a CIRD format

##### A user wants to achieve High Availability with Postqre SQL DB. Which of the below mentioned functionalities helps achieve HA?
- The Multi AZ feature allows the user to achieve High Availability. For Multi AZ, Amazon RDS automatically provisions and maintains a synchronous standby replica in a different Availability

##### A user has created photo editing software and hosted it on EC2. The software accepts requests from the user about the photo format and resolution and sends a message to S3 to enhance the picture accordingly. Which of the below mentioned AWS services will help make a scalable software with the AWS infrastructure in this scenario? 
- Amazon Simple Queue Service (SQS) is a fast, reliable, scalable, and fully managed message queuing service. SQS provides a simple and cost-effective way to decouple the components of an application. The user can configure SQS, which will decouple the call between the EC2 application and S3. Thus, the application does not keep waiting for S3 to provide the data.

##### A user has launched one EC2 Instance In the US East region and one In the US West region. The user has launched an RDS instance in the US East region. How can the user configure access from both the EC2 instances to RDS?
- The user cannot authorize an Amazon EC2 security group if it is in a different AWS Region than the RDS DB instance. The user can authorize an IP range or specify an Amazon EC2 security group in the same region that refers to an IP address In another region. In this case allow IP of US West inside US East‟s security group and open the RDS security group for US East region

##### Which of the following statements is true of tagging an Amazon EC2 resource? 
- You can assign tags only to resources that already exist. You can‟t terminate, stop, or delete a resource based solely on its tags; you must specify the resource identifier.

##### Select the correct statement: Within Amazon EC2, when using Linux instances, the device name JDEV/SDAL is?
- Within Amazon EC2, when using a Linux instance, the device name /dev/SDAL is reserved for the root device

##### You need to create an Amazon Machine Image (AMI) for a customer for an application which does not appear to be part of the standard AWS AM template that you can see in the AWS console. What are the alternative possibilities for creating an AM on AWS?  
- You can purchase an AMI from a third party, including AMIs that come with service contracts from organizations such as Red Hat. You can also create an AMI and sell It to other Amazon EC2 users. After you create an AMI, you can keep it private so that only you can use it, or you can share it with a specified list of AWS accounts. You can also make your custom AMI public so that the community can use it. Building a safe, secure, usable AMI for public consumption is a fairly straightforward process, if you follow a few simple guidelines.

##### Which one of the following answers is not a possible state of Amazon Cloud Watch Alarm? 
- Amazon Cloud Watch Alarms have three possible states: 
	OK: The metric Is within the defined threshold 
	ALARM: The metric is outside of the defined threshold 
	INSUFFICIENT_DATA: The alarm has just started, the metric is not available, or not enough data is available for the metric to determine the alarm state

##### What is the default maximum number of Access Keys per user? 
- The default maximum number of Access Keys per user is 2. ​

##### You have just set up a large site for a client which involved a huge database which you set up with Amazon RDS to run as a Multi-AZ deployment. You now start to worry about what will happen if the database Instance fails. Which statement best describes how this database will function if there is a database failure? 
- When you create or modify your DB Instance to run as a Multi-AZ deployment, Amazon RDS automatically provisions and maintains a synchronous standby replica in a different Availability Zone. Updates to your DB Instance are synchronously replicated across Availability Zones to the standby in order to keep both in sync and protect your latest database updates against DB Instance failure. 
- During certain types of planned maintenance, or in the unlikely event of DB Instance failure or Availability Zone failure, Amazon RDS will automatically failover to the standby so that you can resume database writes and reads as soon as the standby is promoted. 
Since the name record for your DB Instance remains the same, you application can resume database operation without the need for manual administrative intervention. 
- With Multi-AZ deployments, replication is transparent: you do not interact directly with the standby, and it cannot be used to serve read traffic. If you are using Amazon RDS for My SQL and are looking to scale read traffic beyond the capacity constraints of a single DB Instance, you can deploy one or more Read Replicas.

##### A user comes to you and wants access to Amazon Cloud Watch but only wants to monitor a specific Load Balancer. Is it possible to give him access to a specific set of instances or a  specific Load Balancer?
- Amazon Cloud Watch integrates with AWS Identity and Access Management (IAM) so that you can specify which Cloud Watch actions a user in your AWS Account can perform. For example, you could create a policy that gives only certain users in your organization permission to use Get Metric Statistics. They could then use the action to retrieve data about your cloud resources. You can‟t use IAM to control access to Cloud Watch data for specific resources. For example, you can‟t give a user access to Cloud Watch data for only a specific set of instances or a specific Load Balancer. Permissions granted using  IAM cover all the cloud resources you use with Cloud Watch. In addition, you can‟t use IAM roles with the Amazon Cloud Watch command line tools. Using Amazon Cloud Watch with AM doesn‟t change how you use Cloud Watch. There are no changes to Cloud Watch actions, and no new Cloud Watch actions related to users and access control.

##### In the context of AWS support, why must an EC2 instance be unreachable for 20 minutes rather than allowing customers to open tickets immediately?
- because most reach ability issues are solved by automated processes in less than 20 minutes

##### You are migrating an internal server on your PC to an EC2 instance with EBS volume. Your server disk usage is around 500GB so you just copied all your data to a 2TB disk to be used with AWS Import/Export. Where will the data be imported once it arrives at Amazon?
- An import to Amazon EBS will have different results depending on whether the capacity of your storage device is less than or equal to 1 TB or greater than 1 TB. The maximum size of an Amazon EBS snapshot is 1 TB, so if the device image is larger than 1 TB, the image is chunked and stored on Amazon S3. The target location is determined based on the total capacity of the device, not the amount of data on the device. A client needs you to import some existing infrastructure from a dedicated hosting provider to AWS to try and save on the cost of running his current website. He also needs an automated process that manages backups, software patching, automatic failure detection, and recovery.

##### Do Amazon EBS volumes persist independently from the running life of an Amazon EC2 instance?
- An Amazon EBS volume behaves like a raw, unformatted, external block device that you can attach to a single instance. The volume persists independently from the running life of an Amazon EC2 instance.

##### Can a user get a notification of each instance start I terminate configured with Auto Scaling?
- The user can get notifications using SNS if he has configured the notifications while creating the Auto Scaling group.



## Important points:

- When a storage device has reached the end of its useful life, AWS procedures include a decommissioning process that is designed to prevent customer data from being exposed to unauthorized individuals. AWS uses the techniques detailed in **DOD 5220.22-M** (“National Industrial Security Program Operating Manual or **NIST 800-88** (Guidelines for Media Sanitization) to destroy data as part of the decommissioning process. M decommissioned magnetic storage devices are degaussed and physically destroyed in accordance with industry-standard practices.
- A DB instance outage can occur when a DB instance is rebooted, when the DB instance is put into a state that prevents access to it, and when the database is restarted. A reboot can occur when you manualy reboot your DB instance or when you change a DB instance setting that requires a reboot before it can take effect. A DB instance reboot occurs Immediately when one of the following occurs: You change the backup retention period for a DB instance from 0 to a nonzero value or from a nonzero value to 0 and set Apply Immediately to true. You change the DB instance class, and Apply Immediately is set to true. You change storage type from standard to PIOPS, and Apply Immediately is set to true. 
- A DB instance reboot occurs during the maintenance window when one of the following occurs: You change the backup retention period for a DB instance from 0 to a nonzero value or from a nonzero value to 0, and Apply Immediately Is set to false. You change the DB instance class, and Apply Immediately Is set to false.
- After you launch an instance in EC2-Classlc, you can‟t change its security groups. However, you can add rules to or remove rules from a security group, and those changes are automatically applied to all instances that are associated with the security group.
- Dynamo DB supports two types of secondary indexes: 
	**Local secondary index** — an index that has the same hash key as the table, but a different range key. A local secondary index is “local” in the sense that every partition of a local secondary index is scoped to a table partition that has the same hash key. 
	**Global secondary index** — an index with a hash and range key that can be different from those on the table. A global secondary index is considered “global” because queries on the index can span all of the data in a table, across all partitions.
- AWS Import/Export supports: Import to Amazon S3 Export from Amazon S3 Import to Amazon EBS Import to Amazon Glacier AWS Import/Export does not currently support export from Amazon EBS or Amazon Glacier.
- In EBS workload demand plays an important role in getting the most out of your General Purpose (SSD) and Provisioned IOPS (SSD) volumes. In order for your volumes to deliver the amount of IOPS that are available, they need to have enough I/O requests sent to them. There is a relationship between the demand on the volumes, the amount of IOPS that are available to them, and the latency of the request (the amount of time it takes for the I/O operation to complete). Latency is the true end-to-end client time of an I/O operation; in other words, when the client sends a 10, how long does it take to get an acknowledgement from the storage subsystem that the 10 read or write is complete. If your I/O latency is higher than you require, check your average queue length to make sure that your application is not trying to drive more IOPS than you have provisioned. You can maintain high IOPS while keeping latency down by maintaining a low average queue length (which is achieved by provisioning more IOPS for your volume)
- When launching an instance with EC2, AWS recommends not to select the availability zone (AZ). AWS specifies that the default Availability Zone should be accepted. This is because it enables AWS to select the best Availability Zone based on the system health and available capacity. If the user launches additional instances, only then an Availability Zone should be specified. This is to specify the same or different AZ from the running instances. term recovery, you can recover the backups to Amazon.
- In Amazon EC2 Container Service, Dockers is the only container platform supported by EC2 Container Service presently.
- In Elastic Load Balancing a health configuration uses information such as protocol, ping port, ping path (URL), response timeout period, and health check interval to determine the health state of the instances registered with the load balancer. Currently, HTTP on port 80 is the default health check.
- Amazon ECS contains the following components: 
	A Cluster is a logical grouping of container instances that you can place tasks on. 
	A Container instance is an Amazon EC2 instance that is running the Amazon ECS agent and has been registered into a cluster. 
	A Task definition Is a description of an application that contains one or more container definitions. 
	A Scheduler is the method used for placing tasks on container instances. 
	A Service is an Amazon ECS service that allows you to run and maintain a specified number of instances of a task definition simultaneously. 
	A Task is an instantiation of a task definition that is running on a container instance. 
	A Container is a Linux container that was created as part of a task.
-In Amazon Web Service, the user can achieve HA by deploying instances in multiple zones. The elastic IP helps the user achieve HA when one of the instances is down but still keeps the same URL. The AM helps launching the new Instance. The PIOPS is for the performance of EBS and does not help for HA.
- Best Practices for Configuring Network Interfaces 
	You can attach a network interface to an instance when it‟s running (hot attach), 
	when it‟s stopped (warm attach), 
	or when the instance is being launched (cold attach). 
	You can detach secondary (Etho) network interfaces when the Instance is running or stopped. 
	However, you can‟t detach the primary (Etho) interface. 
	You can attach a network interface in one subnet to an instance in another subnet in the same VPC, however, both the network interface and the instance must reside in the same Availability Zone. 
	When launching an instance from the CLI or API, you can specify the network interfaces to attach to the instance for both the primary (ethO) and additional network interfaces. 
	Launching an instance with multiple network interfaces automatically configures interfaces, private IP addresses, and route tables on the operating system of the In stance. 
	A warm or hot attach of an additional network interface may require you to manualy bring up the second interface, configure the private IP address, and modify the route table accordingly. (Instances running Amazon Linux automatically recognize the warm or hot attach and configure themselves.) Attaching another network interface to an instance is not a method to Increase or double the network bandwidth to or from the dual-homed instance.
- In EC2-Classic, you can associate an instance with up to 500 security groups and add up to 100 rules to a security group.
- In the EC2-Classic platform, when you associate an Elastic IP Address (EIP) with an instance, the instance‟s current public IP address is released to the EC2-Classic public IP address pool. If you disassociate an EIP from the instance, the instance is automatically assigned a new public IP address within a few minutes. In addition, stopping the instance also disassociates the EIP from it. But in the EC2-VPC platform, when you associate an EIP with an instance in a default Virtual Private Cloud (VPC), or an instance in which you assigned a public IP to the etno network interface during launch, its current public IP address is released to the EC2•VPC public IP address pool. If you disassociate an EIP from the instance, the instance is automatically assigned a new public IP address within a few minutes. However, if you have attached a second network interface to the instance, the instance is not automatically assigned a new public IP address; you‟ll have to associate an EIP with it manualy. 
- To create a VPC peering connection with another VPC, you need to be aware of the following limitations and rules: 
	You cannot create a VPC peering connection between VPCs that have matching or overlapping CIDR blocks. 
	You cannot create a VPC peering connection between VPCs in different regions. 
	You have a limit on the number active and pending VPC peering connections that you can have per VPC. 
	VPC peering does not support transitive peering relationships; in a VPC peering connection, your VPC will not have access to any other VPCs that the peer VPC may be peered with. This includes VPC peering connections that are established entirely within your own AWS account.
	You cannot have more than one VPC peering connection between the same two VPCs at the same time. 
	The Maximum Transmission Unit (MTU) across a VPC peering connection is 1500 bytes. 
	A placement group can span peered VPCs; however, you will not get fullbisection bandwidth between instances in peered VPC.
	Unique cast reverse path forwarding in VPC peering connections is not supported. 
	You cannot reference a security group from the peer VPC as a source or destination for ingress or egress rules in your security group. Instead, reference CIDR blocks of the peer VPC as the source or destination of your security groups ingress or egress rules. Private DNS values cannot be resolved between instances in peered VPCs.
- A Hosted Zone refers to a selection of resource record sets hosted by Route 53.

---

**Amazon EBS–Optimized Instances**
EBS–optimized instances deliver dedicated bandwidth to Amazon EBS, with options between 425 Mbps and 14,000 Mbps, depending on the instance type you use. 
When attached to an EBS–optimized instance, General Purpose SSD (gp2) volumes are designed to deliver within 10% of their baseline and burst performance 99% of the time in a given year, and Provisioned IOPS SSD (io1) volumes are designed to deliver within 10% of their provisioned performance 99.9% of the time in a given year. 
Both Throughput Optimized HDD (st1) and Cold HDD (sc1) guarantee performance consistency of 90% of burst throughput 99% of the time in a given year. 
Non-compliant periods are approximately uniformly distributed, targeting 99% of expected total throughput each hour. 

**ClassicLink**
ClassicLink allows you to link EC2-Classic instances to a VPC in your account, within the same region. 
If you associate the VPC security groups with a EC2-Classic instance, this enables communication between your EC2-Classic instance and instances in your VPC using private IPv4 addresses. ClassicLink removes the need to make use of public IPv4 addresses or Elastic IP addresses to enable communication between instances in these platforms.
