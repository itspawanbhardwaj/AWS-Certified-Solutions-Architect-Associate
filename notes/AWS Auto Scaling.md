# Amazon EC2 Auto Scaling
---

Amazon EC2 Auto Scaling is a fully managed service designed to launch or terminate Amazon EC2 instances automatically to help ensure you have the correct number of Amazon EC2 instances available to handle the load for your application. Amazon EC2 Auto Scaling helps you maintain application availability through fleet management for EC2 instances, which detects and replaces unhealthy instances, and by scaling your Amazon EC2 capacity up or down automatically according to conditions you define. You can use Amazon EC2 Auto Scaling to automatically increase the number of Amazon EC2 instances during demand spikes to maintain performance and decrease capacity during lulls to reduce costs.


1) launch configuration
	- Create a configuration to launch EC2 instances

2) auto scaling group
	- launch EC2 using launch configurations
	- select a ELB
	- it will automatically start the EC2 machines, no need to create instances as we were doing in ELB
	- instances are created if they are unavailable/failed
	- when you delete Auto scaling groups, the instances associated to it are deleted automatically



# AWS Auto Scaling
---

#### Scaling Policies
- **Target Tracking Scaling:** Most easy to setup, e.g want the avg cpu utilization to be  around 40%
- **Simple/Step Scaling:** when a cloudwatch alarm is triggered (CPU>70%), then add 2 units. If cloudwatch alarm is triggered (CPU<30%) remove one unit.
- **Scheduled Actions:** anticipate scaling based on known usage patterns

#### Scaling Cooldown
- Cooldown period helps to ensure that ASG does not launch or terminate additionals instances before the previous scaling activity  takes effect.
- In addition to default cooldown for ASG, we can create cooldowns that apply to specific simple/step scaling policy

#### ASG Life-cycle Hooks
- You have ability to perform extra steps before the instance goes to in service
- You have ability to perform extra steps before the instance termintates


-------------


##### Q. What is AWS Auto Scaling?
AWS Auto Scaling is a new AWS service that helps you optimize the performance of your applications while lowering infrastructure costs by easily and safely scaling multiple AWS resources. It simplifies the scaling experience by allowing you to scale collections of related resources that support your application with just a few clicks. AWS Auto Scaling helps you configure consistent and congruent scaling policies across the full infrastructure stack backing your application. AWS Auto Scaling will automatically scale resources as needed to align to your selected scaling strategy, so you maintain performance and pay only for the resources you actually need.

##### Q. When should I use AWS Auto Scaling?

You should use AWS Auto Scaling if you have an application that uses one or more scalable resources and experiences variable load. A good example would be an e-commerce web application that receives variable traffic through the day. It follows a standard three tier architecture with Elastic Load Balancing for distributing incoming traffic, Amazon EC2 for the compute layer, and DynamoDB for the data layer. In this case, AWS Auto Scaling will scale one or more EC2 Auto Scaling groups and DynamoDB tables that are powering the application in response to the demand curve.


##### Q. When should I use AWS Auto Scaling vs. Amazon EC2 Auto Scaling?

You should use AWS Auto Scaling to manage scaling for multiple resources across multiple services. AWS Auto Scaling lets you define dynamic scaling policies for multiple EC2 Auto Scaling groups or other resources using predefined scaling strategies. Using AWS Auto Scaling to configure scaling policies for all of the scalable resources in your application is faster than managing scaling policies for each resource via its individual service console. It’s also easier, as AWS Auto Scaling includes predefined scaling strategies that simplify the setup of scaling policies. You should also use AWS Auto Scaling if you want to create predictive scaling for EC2 resources.

You should use EC2 Auto Scaling if you only need to scale Amazon EC2 Auto Scaling groups, or if you are only interested in maintaining the health of your EC2 fleet. You should also use EC2 Auto Scaling if you need to create or configure Amazon EC2 Auto Scaling groups, or if you need to set up scheduled or step scaling policies (as AWS Auto Scaling supports only target tracking scaling policies).

EC2 Auto Scaling groups must be created and configured outside of AWS Auto Scaling, such as through the EC2 console, Auto Scaling API or via CloudFormation. AWS Auto Scaling can help you configure dynamic scaling policies for your existing EC2 Auto Scaling groups.




##### Q: What is target tracking?

Target tracking is a new type of scaling policy that you can use to set up dynamic scaling for your application in just a few simple steps. With target tracking, you select a load metric for your application, such as CPU utilization or request count, set the target value, and Amazon EC2 Auto Scaling adjusts the number of EC2 instances in your ASG as needed to maintain that target.

##### Q: What happens to my Amazon EC2 instances if I delete my ASG?

If you have an EC2 Auto Scaling group (ASG) with running instances and you choose to delete the ASG, the instances will be terminated and the ASG will be deleted.

##### Q: What is a launch configuration?

A launch configuration is a template that an EC2 Auto Scaling group uses to launch EC2 instances.

##### Q: Can I launch different types of EC2 instances in same EC2 Auto Scaling group?

EC2 Auto Scaling groups optimize for the case when all your instance types are the same. You can use the AttachInstances API to attach instances of different types to an Auto Scaling group, and you can also update your launch configuration so that any new instances in the group will be launched with a different instance type. However, this will not affect any of the existing instances.

##### Q: If I have data installed in an EC2 Auto Scaling group, and a new instance is dynamically created later, is the data copied over to the new instances?

Data is not automatically copied from existing instances to new instances. You can use lifecycle hooks to copy the data, or an Amazon RDS database including replicas.


##### Q: When I create an EC2 Auto Scaling group from an existing instance, does it create a new AMI (Amazon Machine Image)?
When you create an Auto Scaling group from an existing instance, it does not create a new AMI. 

##### Q: What are lifecycle hooks?

Lifecycle hooks let you take action before an instance goes into service or before it gets terminated. This can be especially useful if you are not baking your software environment into an Amazon Machine Image (AMI). For example, launch hooks can perform software configuration on an instance to ensure that it’s fully prepared to handle traffic before Amazon EC2 Auto Scaling proceeds to connect it to your load balancer. One way to do this is by connecting the launch hook to an AWS Lambda function that invokes RunCommand on the instance. Terminate hooks can be useful for collecting important data from an instance before it goes away. For example, you could use a terminate hook to preserve your fleet’s log files by copying them to an Amazon S3 bucket when instances go out of service.


##### Q: Can I use Amazon EC2 Auto Scaling for health checks and to replace unhealthy instances if I’m not using Elastic Load Balancing (ELB)? 
You don't have to use ELB to use Auto Scaling. You can use the EC2 health check to identify and replace unhealthy instances.


##### Q: Do the Elastic Load Balancing (ELB) health checks work with Application Load Balancers and Network Load Balancers? Will an instance be marked as unhealthy if any target group associated with it becomes unhealthy? 

Yes, Amazon EC2 Auto Scaling works with Application Load Balancers and Network Load Balancers including their health check feature.

##### Q: If you don’t use Elastic Load Balancing (ELB) how would users be directed to the other servers in a group if there was a failure?

You can integrate with Route53 (which Amazon EC2 Auto Scaling does not currently support out of the box, but many customers use). You can also use your own reverse proxy, or for internal microservices, can use service discovery solutions.


##### Q. When should I use AWS Auto Scaling vs. Auto Scaling for individual services?

You should use AWS Auto Scaling to manage scaling for multiple resources across multiple services. AWS Auto Scaling enables unified scaling for multiple resources, and has predefined guidance that helps make it easier and faster to configure scaling. If you prefer, you can instead choose to use the individual service consoles, Auto Scaling API, or Application Auto Scaling API to scale individual AWS services. You should also use the individual consoles or API if you want to setup step scaling policies or scheduled scaling, as AWS Auto Scaling creates target tracking scaling policies only. 


##### Q. What is Predictive Scaling?

Predictive Scaling is a feature of AWS Auto Scaling that looks at historic traffic patterns and forecasts them into the future to schedule changes in the number of EC2 instances at the appropriate times going forward. Predictive Scaling uses machine learning models to forecast daily and weekly patterns.

Auto Scaling enhanced with Predictive Scaling delivers faster, simpler, and more accurate capacity provisioning resulting in lower cost and more responsive applications. By predicting traffic changes, Predictive Scaling provisions EC2 instances in advance of changing traffic, making Auto Scaling faster and more accurate. 
