### Hybrid Cloud for storage
- Part of infrastructure is on the cloud
- Part of infrastructure is on-premise
- S3 is a proprietary storage technology, so to expose the S3 data on-premise, we use AWS Storage Gateway



### AWS Storage Gateway
- Purpose: bridge between on-premise data and cloud data in S3
- Usecase: Disaster recovery, backup and restore, tiered storage
- 3 types of storage gateway
  - File gateway (exam hint: File access or NFS SMB Protocol) 
    - Configured S3 buckets are accessible using the NFS and SMB protocol
    - Supports S3 standard, S3 IA, S3 One Zone IA
    - Bucket access using IAM roles for each file gateway
    - most recently used data is cached in the file gateway
    - Can be mounted on many servers
  - Volume gateway (exam hint: volume or block storage or iSCSI protocol)
    - Block Storage using iSCSI protocol backed by S3 (imp to remember protocol name)
    - Backed by EBS snapshots which can help restore on-premise volumes (cached or store)
      - Cached Volumes: low latency access to most recent data
      - Stored volumes: entire dataset is on-premise, scheduled backups to S3
  - Tape gateway (exam hint: backups with iSCSI or tapes or VTL)
    - Used by companies using physical tapes
    - Virtual Tape Library (VTL) backed by S3 and Glacier
    - Backup data using existing tape-based processes (and iSCSI interface)
    - works with leading backup software vendors
