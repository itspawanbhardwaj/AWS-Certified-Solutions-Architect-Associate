Remember the following

 - Always design for failure
 - Use multiple AZ's and multiple regions where ever you can
 - Know the difference between scaling out and scaling up
 - - Scaling Out: Is where we add additional ec2 instances
 - - Scaling Up: Is where we increase resoucres inside our EC2 like changing t2.micro to large
 - Know the difference between multi AC and read replicas for RDS
 - Read the question carefully and always considered as a cost element paragraph know the difference S3 storage classes
 
 
#### Q: You have a website that requires a minimum of of 6 instances and it must be highly available. You must also be able to tolerate the failure of one availability zone ful shop what is the ideal architecture for this environment while also being the most cost effective?

A: 2 AZ with 3 instances in each AZ (Wrong. Min 6 instances required)
B: 3 AZ with 3 instances each (Correct)
C: 1 AZ with 6 instances AZ (Wrong: One AZ only)
D: 3 AZ with 2 instances in each AZ (Wrong: If one AZ goes down, only 4 available instances)
