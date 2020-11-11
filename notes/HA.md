Remember the following

 - Always design for failure
 - Use multiple AZ's and multiple regions where ever you can
 - Know the difference between scaling out and scaling up
 - - Scaling Out: Is where we add additional ec2 instances
 - - Scaling Up: Is where we increase resoucres inside our EC2 like changing t2.micro to large
 - Know the difference between multi AC and read replicas for RDS
 - Read the question carefully and always considered as a cost element paragraph know the difference S3 storage classes
 
HA WordPress Site Architecture Configuration
---

### Building Resilience Overview
We will design arch in such a way
- EC2 (writer node) that will be accessed by ip by admins to add content and blogs to the website. It will push all the changes (new content) to S3.
- A fleet of EC2 (reader nodes) that will be access by users via Route 53. It will constantly pull all the updated content from S3 and display to the users.

### Complete Setup

- Goto VPC and create two security groups:
    - WebDMZ: Port 80 and 22 opened for all traffic
    - RDS: Port 3306 opened for WebDMZ sg
- Create RDS instance
    - Select MySQL
    - Select Dev/Test use case
    - Allow Multi-AZ 
    - Select General purpose SSD in storage type otherwise you'll be billed for IOPS
    - Put in default VPC
    - Public accessiblity: No
    - In VPC sg, select RDS sg created earlier 
- Create IAM role for EC2 and grant S3 full access
- Create two S3 buckets, one to store code and other to store media
    - Make S3 media bucket public by updating policy or public access settings
- Create a CloudFront Distribution. Add S3 media bucket in the origin because it will be serving media.
- Create EC2 Instance (This will be golden instance and we will create other reader nodes from snapshot of this golden instance)
    - Assign IAM role for S3 full access
    - Install apache, PHP, MySQL, WordPress. When setting up wordpress, enter RDS endpoint in database host. 
    - Create a healthy.html inside wordpress. This will be used to check status by ELB
    - Create a .htaccess file
        - It rewrites the url to serve media from CloudFront instead of EC2, i.e,  ```rewriterule ^wp-content/uploads/(.*)$ http://CLOUDFRONT_DOMAIN_NAME/$1 [r=301,nc]```
        - Enable Rewrite Engine in Apache
    - Create first post on wordpress and upload some images
        - All the media is uploaded to wp-content/uploads/
    - Create a CronTab job to push all files and folders from wp-content/uploads/* to S3 media bucket (our goal is that all the media will be served by cloudfront instead of EC2 to increase speed and always have a backup of data i.e, failure tolerant)
    - Create a CronTab job to push the code to S3 after every 1 minute (for redundancy. If our current Ec2 goes out, Autoscaling group can take the updated code from S3 while provisioning new EC2 thus use the code as a restore point)
- Create a new Target Group and add EC2 instance in the target group
- Create an Application Load Balancer
    - Create ELB accorss all available regions (in VPC)
    - Select WebDMZ sg
    - Enter /healthy.html in health check path
    - Register target group created earlier in ALB targets
- Goto Route 53
    - Create hosted zone
    - Register domain name and point it to ELB
- Create EC2 Instance (This will be reader nodes. We will create these reader nodes from snapshot of the golden instance created earlier)
    - Create a CronTab job to PULL all files and folders from S3 media bucket
    - Create a CronTab job to PULL the code from S3 after every 1 minute
- Create a Launch Configuration Group
    - Select snapshot of golden EC2 instance
    - Grant IAM role for S3 complete access
    - Add a bootstrap script to download latest copy of code when launching
    - Choose WebDMZ sg
- Create an auto-scaling group
    - Enter group size
    - Select all subnets available
    - In advance, select receive traffic from load balancers and select target group we created earlier
    - Select ELB health check
    - Configure scaling policies (you can select CPU for metric and enter 80 in tager value i.e, provision an instance when cpu utilization hits 80%). Reduce the warmup time to 60 secs (just so that you can boot instances faster to see the results quicker)
- Remove writer golden node from targer group because admin will access it via IP and we don't want route53 to send traffic to it via domain name



#### Q: You have a website that requires a minimum of of 6 instances and it must be highly available. You must also be able to tolerate the failure of one availability zone ful shop what is the ideal architecture for this environment while also being the most cost effective?

A: 2 AZ with 3 instances in each AZ (Wrong. Min 6 instances required)
B: 3 AZ with 3 instances each (Correct)
C: 1 AZ with 6 instances AZ (Wrong: One AZ only)
D: 3 AZ with 2 instances in each AZ (Wrong: If one AZ goes down, only 4 available instances)
