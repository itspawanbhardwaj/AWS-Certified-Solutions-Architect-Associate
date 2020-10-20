### AWS FSx for Windows (File Server)

EFS is a shared POSIX system for Linux (FSx is for windows)
- FSx for Windows is a fully managed file system share drive
- Supports SMB protocol & Windows NTFS
- Microsoft Active Directory integration, ACLs, user quotas
- Built on SSD, scale upto 10s of GB/s, millions of IOPS, 100s PB of data
- Can be accesses from your on-premise infrastructure
- Can be configured to be multi-az
- Data is backed-up daily to S3


### AWS FSx for Lustre
- Lustre is  a type of parallel disctibuted file system, for parge-scale computing
- The name lustre is derived from Linux and Cluster
- ML, High Performance Computing (HPC)
- Video Processing, Financial Modeling, Electronic Design Automation
- Scales upto 100s GB/s, Millions of IOPS, sub-ms latencies
- Seamless integration with S3
  - Can read S3 as a file system (Through FSx)
  - Can write the output of the computations back to S3
- Can be used from on-premise servers
