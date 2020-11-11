### Snowball
- Physical data transport solution that helps moving TBs or PBs of data in or out of AWS
- ALternative to moving data over the network (and paying network fees)
- Secure, tamper resistant, uses KMS 256 bit encryption
- Tracking using SNS and text messages, E-ink shipping label
- Pay per data trasnfer job
- Usecase: Large data cloud migrations, Disaster recovery
- If it takes more than a week to transfer over the network, use snowball devices


### Process
- Request snowball device from AWS console for delivery
- Install the snowball client on your servers
- Connect the snowball to your servers and copy files using the client
- Shipback the device when done
- Data will be loaded to S3
- Snowball is completely wiped
- Tracking is done via sns, sms and aws console


### Snowball Edge
- Snowball edge add computational capiblity to the device
- 100 TB capacity with either
  - storage optimized - 24 vcpu
  - compute optimized - 52 vcpu and optional gpu
- Supports a custom EC2 AMI so you can perform processing on the gp
- Supports custom lambda functions
- Useful to pre-process data while moving
- Usecase: data migration, iop capture, ml etc


### Snowmobile
- Transfer Exabytes of data (1000 pb)

