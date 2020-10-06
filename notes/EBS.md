# EBS
---
AWS EBS allows you to create storage volumes and attach them to AWS EC2 instances. Once attached, you can create a file system on top of these volumes, run a database, or use them in any other way you would use a block device. Amazon EBS volumes are placed in a specific availability zone, where they are automatically replicated to protect you from the failure of a single component.

EBS volume types
-----------------
**SSD: solid state drives**

**1) General Purpose SSD (gp2)**
- General purpose SSD volume that balances price and performance for a wide variety of workloads
* Use case:
		Recommended for most workloads
		System boot volumes
		Virtual desktops
		Low-latency interactive apps
		Development and test environments
- Volume:
	- 1GB - 16TB
* max IOPS/volume: 16000
* max throughput/volume : 250MB/s
* max IOPS/instance : 80,000
* max Throughput/Instance : 1750 MB/s
* dominant performance attribute: IOPS

**2) Provisioned IOPS SSD (io1)**
- Highest-performance SSD volume for mission-critical Low-latency or high-throughput workloads
* Use case:
	Critical business applications that require sustained IOPS performance, or more than 16,000 IOPS or 250 MiB/s of throughput per volume
	Large database workloads, such as:
	- MongoDB
	- Cassandra
	- Microsoft SQL Server
	- MySQL
	- PostgreSQL
	- Oracle

* Volume:
	- 4GB - 16TB
- max IOPS/volume: 64000
- max throughput/volume : 1000MB/s
- max IOPS/instance : 80,000
- max Throughput/Instance : 1750 MB/s
- dominant performance attribute: IOPS
---

**Hard disk drives (HDD)**

**3) Throughput Optimized HDD (st1)**
- Low cost HDD volume designed for frequently accessed thoughput intensive workloads.
- Use case:
	- Streaming workloads requiring consistent, fast throughput at a low price
	- Big data
	- Data warehouses
	- Log processing
	- Cannot be a boot volume
* Volume:
	- 500GB - 16TB

- max IOPS/volume: 500
- max throughput/volume : 500MB/s
- max IOPS/instance : 80,000
- max Throughput/Instance : 1750 MB/s
- dominant performance attribute: MiB/s

**4) Cold HDD (sc1)**
- Lowest cost HDD volume designed for less frequently accessed workloads
Use case:
		Throughput-oriented storage for large volumes of data that is infrequently accessed
		Scenarios where the lowest storage cost is important
		Cannot be a boot volume
* Volume:
	- 500GB - 16TB
- max IOPS/volume: 250
- max throughput/volume : 250MB/s
- max IOPS/instance : 80,000
- max Throughput/Instance : 1750 MB/s
- dominant performance attribute: MiB/s

**5) Megnatic:**

		Lowest cost
		Bootable
		data is used infrequently

----------------------------------
- EC2 and EBS will always be in same availability zone.
- Standard volumes cant be modified.
- To move/copy EBS in another availability zone:
	- create snapshot
	- create image/copy (can change volume type)
	- create in different availability zone

- To move/copy EC2 in another availability zone:

        create an AMI
        copy to another availability zone

* When we terminate EC2 instance, root volume gets terminates, the EBS volumes doesnt gets terminated by default
* Snapshots exists in S3, Point in time copy of volumes
* Snapshots are incremental- this means that only the blocks that have changed since your last snapshot are moved to S3
* Should stop EC2 while taking snapshot
* Can change EBS volume type on the fly

---

Encryption: encrypt an unecrypted EBS volume
---
- Create an EBS snapshot of volume
- Encrypt the EBS snapshot (using copy)
- Create new EBS volume from the snapshot (encrypted volume)
- Now you can attach the encrypted volume to the original instance

---
**Volumes vs Snapshot security:**
---
1.	snapshots of encrypted volumes are encrypted automatically
2.	volumes restored from encrypted snapshot are encrypted automatically
3.	You can share snapshots, but only if they are unencrypted.

---

EBS Snapshots
---
- Incremental - only backup changed blocks
- EBS backups use IO, you should not run it when handling a lot of traffic
- Snapshots are stored in S3
- Not necessary to detach volume to do snapshot but recommended
- Can copy snapshots accross AZ or region
- Can make AMI from snapshot
- EBS volumes restored by snapshots need to be pre-warmed
- Snapshots can be automated using Amazon Data Lifecycle Manager


**Snapshot of root volume devices**
---

- to create a snapshot od AWS EBS volume that serves as ROOT device, you should stop the instance before taking the snapshot
- snapshot of encrypted volumes are encrypted automatically
- volumes restored from encrypted snapshots are encrypted automatically
- You can share snapshots, but only if they are unencrypted
	- these snapshots can be shared with other AWS Accounts or made public

---

**You can select your AMI based on:**
	- Region
	- OS
	- Architecture (32-bit or 64-bit)
	- launch permissions
	- Storage for the ROOT device
		-> instance store (Ephemeral storage)
		-> EBS Backed volumes

-----------------------------------------------------

**EBS vs Inatance store**

All AMI are categorized as either backed by EBS or backed by instance store.

For **EBS Volumes**: the root device for an instance launched from the AMI is an Amazon EBS colume created from an Amazon EBS snapshot.

For **instance store volumes**: the root device for an instance launched from the AMI is an instance store colume ceated from a **template stored in AWS S3.**

- Instance store volumes are sometimes called as **Ephemeral Storage.**
- Instance store volumes cannot be stopped. If the underlying host fails, you will loose your data.
- EBS backed volumes can be stopped, you will not lose the data on this instance if it is stopped.
- You can reboot both, you will not lose the data
- be default, both ROOT volumes will be deleted on termination, however with EBS volumes, you can tell AWS to keep the root device volume 


Instance Store Pros
- Better I/O Performance
- Good for buffer/cache/temporary content
- Data survives reboot

Instance Store Cons
- On stop or termination, the instance store is lost
- Cant resize the instance store
- Backups must be operated by the used
- Risk of data loss if hardware fails

If we need high IOPS, higher than 62,000 we will use instance store instead of EBS because instance store can provide upto 3.3 million read and 1.6 million write IOPS


When need more IOPS in EBS, Use Raid 0 (better performance) or Raid 1 (mirroring, fault tolerant)

---
##### Q: What level of performance consistency can I expect to see from my Provisioned IOPS SSD (io1) volumes?

When attached to EBS-optimized instances, Provisioned IOPS SSD (io1) volumes are designed to deliver within 10% of the provisioned IOPS performance 99.9% of the time in a given year. Your exact performance depends on your application’s I/O requirements.

##### Q: Will I be able to access my snapshots using the regular Amazon S3 API?

**No**, snapshots are only available through the Amazon EC2 API.
