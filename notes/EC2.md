
# EC2:
---

- instances
- AMIs
- various configuration of CPU, memory, storage and networking
- Firewall
- Static IPv4 address
- VPC
- Tags

**Billing commences** when Amazon EC2 initiates the boot sequence of an AMI instance and billing ends when the instance shuts down.

---
Instances Type (Main Ones)
---
- R: Applications that needs a lot RAM - in-memory cache
- C: Applications that needs good CPU - compute / databases
- M: Applications that are balanced - general/web apps
- I: Applications that needs good local I/O (instance sotrage) - Databases
- G: Applications that needs a GPU - ML

- T2/T3: Burstable instances (upto a capacity)
    - bursts are the spikes of CPU performance, too much load will freeze the machine
    - CPU credits are utilized when a machine bursts
    - If machine stops bursting, credits are accumulated over time
- T2/T3 - unlimited: Unlimited burst
    - Unlimited burst credit balance
    - You pay extra money if you go over your credit balance

---

## Instance purchasing options:

**1) On-Demand Instances:**	
- Pay by the hour that you launch
- Allows you to pay a fixed rate by hour with no commitment
- Perfect for users that want the low costs and flexiblility of Amazon EC2 without any up-front payment or long term commitment
- Application with short term, spiky or unpredictable workloads that can not be interrupted
- Applications being developed or tested on EC2 for the first time

**2) Reserved Instances:**
- Provides you with a capacity reservation and offer a sighnificant discount on the hourly charge for an instance. 1 year or 3 year terms
- Applications with strady state or predictable usuage
- Application that require reserved capability
- Users can make up-front payments to reduce their total computing costs even further:
	- **Standard Rls** (up to 75% off on-demand)
	- **Convertable Rls** (54% off on-demand) features the capacity to change the attribute of RI as long as the exchange results in the creation of reserved instances of equal or greater value.
	- **Schedule Rls** are available to launch within the time window you reserve. This option allow you to match your capacity reservation schedule that only requires a fraction of a day, a week or a month.

Limitations:
- You are limited to purchasing 20 Reserved instances per available zone per month, plus 20 regional Reserved instances. Therefore in a region of 3 available zone, you can purchase 80 reserved instances (20* 3 + 20)


**3) Spot instances:**

- Request unused EC2 instances, which can lower your Amazon EC2 cost significantly.
- if the current spot price > your max price, you can stop or terminate your instance within a 2 minutes grace period
- Applications that have flexible start and end times
- Applications that are only feasible at very low compute prices.
- Users with an urgent need for large amount of additional computing capacity.
- Spot instances are well suited for data analysis, batch jobs, background processing and optional tasks that are failure resilient.
- 20 spot instances per region.
- Spot bid price limit for spot instance is ten times the on-demand price.
- **Block spot**: Block spot instancce during a specified time frame (1 ot 6 hours) without interruptions

**4) Dedicated Hosts:**
- You have control over the physical server. If you have a third party application wherein the licensing is based on the number of cores.
Or if your security policy mandates that you cannot share infrastructure.
- Pay by the hour for instances that run on single-tenant hardware, Dedicated instances will not share hosts with other accounts
- Reduce costs by allowing you to use existing server-bound software licenses.
- Useful for regulatory requirements that may not support multi-tenent virtualization
- Great for licensing which does not support multi-tenency or cloud deployments
- Can be purchased on-demand(hourly)
- Can be purchased as a Reservation for up to 70% off on-demand price

**5) Dedicated instances**
- Dedicated instances are EC2 instances that run in a VPC on hardware thats dedicated to a single customer.
If the customer has multiple AWS accounts, then instances can share the same hardware

##### Dedicated hosts vs dedicated instances
- Dedicated hosts give you additional visibility and control over how instances are placed on a physical layer.
- When you use dedicated hosts, you have control over instances Placement on the host using the host affinity and instance auto-placement setting. 
- If your organization wants to use AWS, but has an existing software licence with hardware compliance requirements, this allows visibility into the hosts hardware so you can meet those requirements.

##### limitations:
- RHEL, SUSE linux and windows AMI offered by AWS or on the AWS marketplace cannot be used with Dedicated hosts.
- Amazon EC2 instance auto recovery is not supported
- the instance that run on a dedicated host can only be launched in a VPC.
- Hosts limits are independent from instance limits. Instance that you are running on dedicated hosts do not count towards your instance limits.
- Auto-scaling groups are not suported.
- RDS instances are not supported
- AWS Free tier is not available for dedicated hosts.
- Placement groups are not supported

**6) Capicity reservations:**

Reserve capacity for your instances in a specified availablity zone for any duration.

Status check:
---

**1)  System status check:** 
* These checks monitor the AWS system required to use this instance and ensure they are function properly.
* make sure hypervisor is up, network gets to the hypervisor 

**2) Instance status checks:**
* These checks monitor your software  and network configuration for this instance.
* Checks thraffic gets to the OS

---

**Terminiation protection** is turned off by default, you must turn it on
On an EBS-backed instance, the default action is for the root EBS volume to be deleted when the instance is terminated.
* EBS Root volumes of your DEFAULT AMI's **cannot be encrypted**. You can also use a third party tool to encrypt the root volume, or this can be done when creating AMI in the AWS console or using the API.

---

##### PLACEMENT GROUP
---

EC2 instance placement strategy can be defined using placement groups

**Clustered placement Group:** 
*its a grouping of instances within a single availablity zone (and same hardware). Placement grpups are recomended for applications that need low network latency, high network throughput or both (but high risk).
* Only certain instances can be launched in to a clustered placement groups.
* Pros: High network throughput with low latency
* Cons: High risk. All instances fail at same time
* Usecase:
    * Big data job that needs to complete fast
    * Apps that need low latency

**Spread Placement groups**: 
*A spread placement group is a group of instances that are each placed on distinct underlying hardware (max 7 instances per group per AZ).
* Spread placement groups are recommended for applications that have a small number of critical instances that should be kept separate from each other.
* Can't merge placement groups
* Cant move an existing instance into a placement group. You can create an AMI from your existing instance, and then launch a new instance from the AMI into a placement group.
* Pros:
    * Can span across multiple AZ
    * Reduced risk
* Cons:
    * Limited to 7 instances per AZ per placement group
* Usecase:
    * High Availability Apps
    * Critical apps where each instance must be isolated from failure of each other

**Partition Placement Groups**: 
* Spread instances accross many different partitions within an AZ. Scales to 100s of EC2 instances per group and upto 7 partitions per AZ. In Partition placement groups, instances are still spread and one partition is isolated from one another instead of individual instances.
* Usecase: Distributed big data apps like Cassandra hadoop kafka etc

AMI
---
---
- You can share an AMI with another AWS account
- Sharing an AMI does not effect the ownership of the AMI
- To copy an AMI, you need to launch the instance first
- If you copy an AMI that has been shared with your account, you are the owner of the target AMI in your account
- To copy an AMI that was shared with you from another account, the owner of the soource AMI must grant you read permissions for the storage that backs the AMI, either the associated EBS snapshot or S3 bucket

Limits
- You cant copy an encrypted AMI that was shared with you form another account. Instead, if the underlying snapshot of encryption key were share with you, you can copy the snapshot while re-encrypting it with a key of your own. You own the copied snapshot and can register it as a new AMI
- You cant copy an AMI with an associated billingProduct code that was shared with you from another account. To copy a shared AMI with a billingProduct code, launch EC2 instance in your account using shared AMI and then create an AMI from the instance.


---
##### Network and security of Amazon EC2
---

**Amazon EC2 key pairs:**
- Amazon EC2 uses public-key cryptography to encrypt and decrypt login information.

**Amazon EC2 Security Groups:**
- A security group acts as a virtual firewall that controls the traffic for one or more instances.
- When you launch an instance, you associate one or more security groups with the instance. You add rules to each security group that allow traffic to or from its associated instances.
- You can modify the rules for a security group at any time; the new rules are automatically applied to all the instances that are associated with the security group.
- When AWS decide whether to allow traffic to reach aninstance, AWS evaluates all the rules from all the security groups that are associated with the instance.

**Security Group Rules**
- By default, security groups allow all outbound traffic.
- You can't change the outbound rules for an EC2 classic security group.
- Security group rules are always permissive, you cant add rules that deny access.
- Security groups are stateful.
- You can add and remove rules at any time.

**Controlling Access to Amazon EC2 Resources**
- Your security credentials identify you to services in AWS and grant you unlimited use of your AWS resources,  such as your Amazon EC2 resources.
- You can use feature of Amazon EC2 and AWS IAM to allow other users, services, and applications to use your amaxon EC2 resources without sharing your security credentials.
- You can choose to allow full or limited use of your Amazon EC2 resources.

**VPC**

**Elastic IP Address**
- An Elastic IP Address is a static IPV4 address designed for dynamic cloud computing. An Elastic IP address is associated with your AWS account.
- An Elastic IP address is a public IPv4 address, which is rechable from the internet. If your instance does not have a public IPv4 address, you can associate an Elastic IP address with your instance to enable communication with the internet.
- To use an EIP address, you first allocate one to your account, and then associate it with your instance or a network interface.
- When you associate an Elastic IP address with an instance or its primary network interface, the instance's public IPv4 address (if it had one) is released back into Amazon's pool of public IPv4 addresses. you can not reuse a public IPv4 address.
- You can disassociate an EIP address from a resource, and reassociste it with a different resource.
- A disassoicate EIP address remains allocated to your account until you explicitly release it.
- AN EIP address is for use in a specific region only.
- When you associate an EIP address with an instance that previously had a public IPv4 address, the public DNS hostname of the instance changes to match the EIP address.

**Elastic Network Interface**
An Elastic network interface (refered to as a network intsrface in this document) is a virtual network interface that you can attach to an instance in a VPC. Network interface are available only for instances running in a VPC.
A network interface can include the following attributes:
- A primary private IPv4 address.
- One or more secondary private IPv4 address.
- One Elastic IP Address (IPv4)
- One public IPv4
- one or more IPv6
- one or more security groups
- a MAC address
- a source to destination check flag.
- bound to specific AZ
 
You can create ENI independently and attach them on the fly on EC2 instances for failover


EC2-Classic Security: Groups Control outgoing instance traffic
VPC Security: Groups Control outgoing and incoming instance traffic


EC2 Hibernete
---
- The in-memory (RAM) state is preserved (in the ebs volume)
- The instance boot is much faster
- The root ebs volume must be encrypted
- Only supports Cx, Mx, Rx at the moment.
- Instance ram size must be less than 150 gb
- Must be EBS and encrypted
- Can not be hibernated more than 60 days

EC2 Instance Metadata
---
EC2 Metadata (eg ial policies etc) can be found at the url 169.254.169.254/latest/meta-data


---
##### Q: What is the difference between using the local instance store and Amazon Elastic Block Store (Amazon EBS) for the root device?

* When you launch your Amazon **EC2 instances** you have the ability to store your root device data on Amazon EBS or the local instance store. *By using Amazon EBS, data on the root device will persist independently from the lifetime of the instance*. This enables you to *stop and restart* the instance at a subsequent time, which is similar to shutting down your laptop and restarting it when you need it again.

* Alternatively, the local instance store only persists during the life of the instance. This is an inexpensive way to launch instances where *data is not stored to the root device*. For example, some customers use this option to run large web sites where each instance is a clone to handle web traffic.

##### Q: How many instances can I run in Amazon EC2?
* You are limited to running up to a total of **20 On-Demand** instances across the instance family, purchasing 20 Reserved Instances, and requesting Spot Instances per your dynamic Spot limit per region.

##### Q: Does Amazon EC2 use ECC memory?
* In our experience, ECC memory is necessary for server infrastructure, and all the hardware underlying Amazon EC2 uses ECC memory.

---

The EC2 instance types are generally categorized into 5 types by the Amazon. They are:

	Accelerated Computing (P3, P2, G3, F1)
	General Purpose – (T2, M4, M3)
	Compute Optimized – (C5, C4, C3)
	Memory Optimized – (X1, R4, R3)
	Storage optimized-(I3)
	Dense-storage Instances – (D2)

**Accelerated Computing instances**

##### Q: What are Accelerated Computing instances?

* Accelerated Computing instance family is *a family of instances which use hardware accelerators, or co-processors, to perform some functions, such as floating-point number calculation and graphics processing, more efficiently than is possible in software running on CPUs*. 
* Amazon EC2 provides three types of Accelerated Computing instances – **GPU compute instances** for general-purpose computing, **GPU graphics instances** for graphics intensive applications, and **FPGA programmable** hardware compute instances for advanced scientific workloads.

##### Q. When should I use GPU Graphics and Compute instances?

GPU instances work best for applications with massive parallelism such as workloads using thousands of threads. Graphics processing is an example with huge computational requirements, where each of the tasks is relatively small, the set of operations performed form a pipeline, and the throughput of this pipeline is more important than the latency of the individual operations. To be able build applications that exploit this level of parallelism, one needs GPU device specific knowledge by understanding how to program against various graphics APIs (DirectX, OpenGL) or GPU compute programming models (CUDA, OpenCL).

**Compute Optimized instances**

##### Q. When should I use Compute Optimized instances?

Compute Optimized instances are designed for applications that benefit from high compute power. These applications include compute-intensive applications like high-performance web servers, high-performance computing (HPC), scientific modelling, distributed analytics and machine learning inference.


**General Purpose instances**

##### Q: What are Amazon EC2 A1 instances?

* Amazon EC2 A1 instances are new general purpose instances powered by the AWS Graviton Processors that are custom designed by AWS.

##### Q: What are the specifications of the new AWS Graviton Processors?

* **AWS Graviton** processors are a new line of processors that are custom designed by AWS utilizing Amazon’s extensive expertise in building platform solutions for cloud applications running at scale.
* These processors are based on the **64-bit Arm** instruction set and feature Arm Neoverse cores as well as custom silicon designed by AWS. The cores operate at a frequency of 2.3 GHz.

##### Q: When should I use A1 instances?

* A1 instances deliver significant cost savings for customer workloads that are supported by the extensive Arm ecosystem and can fit within the available memory footprint.
* A1 instances are ideal for scale-out applications such as web servers, containerized microservices, caching fleets, and distributed data stores. These instances will also appeal to developers, enthusiasts, and educators across the Arm developer community.
* Most applications that make use of open source software like Apache HTTP Server, Perl, PHP, Ruby, Python, NodeJS, and Java easily run on multiple processor architectures due to the support of Linux based operating systems. We encourage customers running such applications to give A1 instances a try.
* Applications that require higher compute and network performance, require higher memory, or have dependencies on x86 architecture will be better suited for existing instances like the M5, C5, or R5 instances. 


##### Q: Do A1 instances support the AWS Nitro System?

* **Yes**, A1 instances will be powered by the AWS Nitro System, a combination of dedicated hardware and Nitro hypervisor.

**High Memory instances**

##### Q. What are EC2 High Memory instances?

* Amazon EC2 High Memory instances offer **6 TB, 9 TB, or 12 TB** of memory in a single instance.
* These instances are designed to run large in-memory databases, including production installations of **SAP HANA**, in the cloud.
* EC2 High Memory instances are the first Amazon EC2 instances powered by an 8-socket platform with latest generation **Intel® Xeon® Platinum 8176M (Skylake)** processors that are optimized for mission-critical enterprise workloads. EC2 High Memory instances deliver high networking throughput and low-latency with 25 Gbps of aggregate network bandwidth using Amazon Elastic Network Adapter (ENA)-based Enhanced Networking. EC2 High Memory instances are EBS-Optimized by default, and support encrypted and unencrypted EBS volumes.

**Storage Optimized instances**

##### Q. What is a Dense-storage Instance?

* Dense-storage instances are designed for workloads that require high sequential read and write access to very large data sets, such as Hadoop distributed computing, massively parallel processing data warehousing, and log processing applications.
* The Dense-storage instances offer the best price/GB-storage and price/disk-throughput across other EC2 instances.

##### Q. How do Dense-storage and HDD-storage instances compare to High I/O instances?

High I/O instances (I2) are targeted at workloads that demand low latency and high random I/O in addition to moderate storage density and provide the best price/IOPS across other EC2 instance types. Dense-storage instances (D2) and HDD-storage instances (H1) are optimized for applications that require high sequential read/write access and low cost storage for very large data sets and provide the best price/GB-storage and price/disk-throughput across other EC2 instances.

----

**STORAGE**
---
**Amazon Elastic Block Storage**

##### Q: What happens to my data when a system terminates?

* The data stored on a local instance store will persist only as long as that instance is alive. However, data that is stored on an Amazon EBS volume will persist independently of the life of the instance. Therefore, we recommend that you use the local instance store for temporary data and, for data requiring a higher level of durability, we recommend using Amazon EBS volumes or backing up the data to Amazon S3.
* If you are using an Amazon EBS volume as a root partition, you will need to set the Delete On Terminate flag to "N" if you want your Amazon EBS volume to persist outside the life of the instance.

##### Q: What kind of performance can I expect from Amazon EBS volumes?

Amazon EBS provides four current generation volume types and are divided into two major categories: 
1. **SSD-backed storage**  are designed for transactional, IOPS-intensive database workloads, boot volumes, and workloads that require high IOPS. SSD-backed volumes include *Provisioned IOPS SSD (io1) and General Purpose SSD (gp2)*.
2. **HDD-backed** storage  are designed for throughput-intensive and big-data workloads, large I/O sizes, and sequential I/O patterns. HDD-backed volumes include *Throughput Optimized HDD (st1)* and *Cold HDD (sc1).* 
* These volume types differ in performance characteristics and price, allowing you to tailor your storage performance and cost to the needs of your applications.


**Amazon Elastic File System (EFS)**

* Amazon EFS uses the NFSv4.1 protocol.

**NVMe Instance storage**

##### Q: Which instance types offer NVMe instance storage?

Today, I3, C5d, M5d and F1 instances offer NVMe instance storage.

##### Q: Can I disable NVMe instance storage encryption?

* **No**, NVMe instance storage encryption is always on, and cannot be disabled.

##### Q: Does Amazon EC2 NVMe instance storage support AWS Key Management Service (KMS)?

* **No**, disk encryption on NVMe instance storage does not support integration with AWS KMS system. Customers cannot bring in their own keys to use with NVMe instance storage. 

**Elastic Fabric Adapter (EFA)**

##### Q: Why should I use EFA?

* **EFA** brings the *scalability, flexibility, and elasticity* of cloud to tightly-coupled HPC applications. With EFA, tightly-coupled HPC applications have access to lower and more consistent latency and higher throughput than traditional TCP channels, enabling them to scale better. EFA support can be enabled dynamically, on-demand on any supported EC2 instance without pre-reservation, giving you the flexibility to respond to changing business/workload priorities.

##### Q: Which instance types support EFA?

* EFA is currently available on the C5n.18xlarge, and P3dn.24xl instance sizes. Support for more instance types and sizes being added in the coming months.

##### Q: What are the differences between an EFA ENI and an ENA ENI?

* An **ENA ENI** provides traditional IP networking features necessary to support VPC networking.
* An EFA ENI provides all the functionality of an ENA ENI, plus hardware support for applications to communicate directly with the EFA ENI without involving the instance kernel (OS-bypass communication) using an extended programming interface. Due to the advanced capabilities of the EFA ENI, EFA ENIs can only be attached at launch or to stopped instances.

**Elastic IP**

##### Q: Why am I limited to 5 Elastic IP addresses per region?

Public (IPV4) internet addresses are a scarce resource. There is only a limited amount of public IP space available, and Amazon EC2 is committed to helping use that space efficiently.

##### Q: Do I need one Elastic IP address for every instance that I have running?

* **No**. You do not need an Elastic IP address for all your instances. By default, every instance comes with a private IP address and an internet routable public IP address. 
* The private IP address remains associated with the network interface when the instance is stopped and restarted, and is released when the instance is terminated.
* The public address is associated exclusively with the instance until it is stopped, terminated or replaced with an Elastic IP address.

##### Q: How long does it take to remap an Elastic IP address?

The remap process currently takes several minutes from when you instruct us to remap the Elastic IP until it fully propagates through our system.

**Elastic Load Balancing**

##### Q: What load balancing options does the Elastic Load Balancing service offer?

Elastic Load Balancing offers two types of load balancers that both feature high availability, automatic scaling, and robust security. These include the **Classic Load Balancer** that routes traffic based on either application or network level information, and the **Application Load Balancer** that routes traffic based on advanced application level information that includes the content of the request.

##### Q: When should I use the Classic Load Balancer and when should I use the Application Load Balancer?

* The Classic Load Balancer is ideal for simple load balancing of traffic across multiple EC2 instances, while the Application Load Balancer is ideal for applications needing advanced routing capabilities, microservices, and container-based architectures.

##### Q: What is the difference between hibernate and stop?

* In the case of hibernate, your instance gets hibernated and the RAM data persisted. In the case of Stop, your instance gets shutdown and RAM is cleared.

##### Q: How much does it cost to hibernate an instance?

* Hibernating instances are charged at standard EBS rates for storage. As with a stopped instance, you do not incur instance usage fees while an instance is hibernating.
