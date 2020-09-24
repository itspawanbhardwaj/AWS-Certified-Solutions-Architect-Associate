# VPC
---
http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-vpc.html

Amazon virtual private cloud (VPC) lets you provisional logically isolated section of the Amazon Web Services (AWS) cloud where you can launch aws resources in a virtual network that you define. You have complete control over your virtual networking environment including selection of your own IP address range, creation of subnets and configuration of route table and network gateways.


VPC Peering
---
- Allows you to connect one vpc with another via a direct network route using private IP addresses
- Instances behave as if they were on the same private network
- You can peer vpc with other AWS accounts as well as with other vpc's in the same account
- Peering is in a star configuration that is one Central vpc peers with 4 others. NO TRANSITIVE PEERING. (Transitive peering means you can't peer through one VPC to another)
- You can peer between regions

Security groups
---------------
- first line of defence
- stateful
- all inbound traffic is blocked by default
- All outbound traffic is allowed
- changes in security groups take effect immediately
- you can have any number of EC2 instances with in a security group
- You can have multiple security groups attached to EC2 instances
- cannot block IP address
- cannot deny a rule
------------------------------------------

Subnets:
---
A subnet is a range of IP Addresses in your VPC. You can launch AWS resources into a subnet that you select. 
Use a Public subnet for resources that must be connected to the internet, and a private subnet for resources that wont be connected to the internet.


------------------------------------------

**What can we do with VPC:**
---
- Launch instance into a subnet of your choosing
- Assign custom IP address ranges in each subnet
- Configure route tables between subnets
- create internet gateway and attach it to our VPC
- Much better security control over your AWS resources
- security groups: Instance level
- NACL: Subnets level 

----------------

**Remember the following:**
---
- Think of a VPC as a logical datacenter in AWS
- Consists of IGWs (or virtual private gateways), Route tables, network access control lists, subnets and Security groups
- 1 subnet can be in 1 AZ
- 1 AZ can have Multiple subnets
- Security groups are stateful; Network Access Control Lists are stateless
- NO TRANSITIVE PEERING

------------------------------------

**on creating VPC following are created:**
---
- route table (VPC can have multiple route table)
- NACL
- Security group

**manually create:**
---
- subnet (AZ, can be attached to 1 route table)
- internet gateway (only 1 internet gateway can be attached to 1 VPC)

------------------

NAT instances
---------------------
- When creating nat instances, disable source/destinaiton check on the instance.
- NAT instances must be a route out of the private subnet to the NAT instance, in order for this to work.
- The amount of traffic that NAT instance can support depends on the instance size. if you are bottlenecking, increase the instance size.
- You can create high availibility using autoscaling groups, multiple subnets in different AZ, and a script to automate failover.
- behind the security groups

NAT Gateway:
------------
- Redudant inside the availibility zone
- preffered by the enterprise
- starts at 5GBps and scales currently to 45Gbps
- No need to patch
- Not assocoates with security groups
- Automatically assigned a public ip address
- Remember to update your route tables
- No need to disable Source/ destinaiton checks

If you have resources in multiple availability zones and they share one nat gateway, in the event that the nat gateway's availability zone is down, resources in the other availability zones loose internet access. To create an availability zone-independent architecture, create and nat gateway in each availability zone and configure your routing to ensure that resources use the nat gateway in the same availability zone.

-----------------------------

NACL: network account control access list
----------------------------------------------

- **Ephemeral ports**: An Ephemeral port is a short lived transport protocol port for internet protocol communications.
- NAT Gateway uses 124-65535 ports
- VPC automatically comes with a default network ACL, and by default it allows all outbound and inbound traffic.
- You can create custom network ACLs. By default, each custom network ACL denies all inbound and outbound traffic until you add rules.
- Each subnet in your VPC must be associated with a network ACL. If you dont explicitly associate a subnet with a network ACL, the subnet is automatically associated with the default network ACL.
- Block IP Addresses using network ACLs not security groups
- you can associate a network ACL with multiple subnets, however a subnet can be associates with only one network ACL at a time. When you associate a network ACL with a subnet, the previous association is removed.
- Network ACLs contain a numbered list of rules that is evaluated in order, starting with the lowest numbered rule.
- Network ACLs have sepatare inbound and outbound rules, and each rule can either allow or deny traffic.
- Natwork ACLs are stateless; responses to allowed inbound traffic are subject to the rules for outbound traffic.

------------------------

VPC Flow Logs
----------------

VPC Flow logs is a feature that enables you to capture information about the IP traffic going to and from network interface in your VPC. Flow log data is stored using Amazon cloudwatch logs/s3 bucket. After you have crated a flow log, you can view and retrieve its data in cloudwatch logs

- You cannot enable flow logs for VPCs that are peered with your VPC unless the peer VPC is in your account.
- You cannot TAG a flow log.
- After you have created a flow log, you cannot change its configuration; for example, you cant associate a different IAM role with the flow log.


**VPC Flow logs levels:**
- VPC
- Subnet
- Network interface level

**Not all IP traffic is monitored:**
- Traffic generated by instances when they  contact the Amazon DNS server. if you use your own DNS server, then all traffic to DNS server is logged.
- Traffic generated by a windows instance for Amazon windows licence activation.
- Traffic to and from 169.254.169.254 for instance metadata
- DHCP traffic
- Traffic to the reserved IP Address for the default VPC router.

--------------------------------------------

Bastian hosts:
---------------
A bastian host is a special purpose computer on a network specifically designed and configured to withstand attacks. The computer generally hosts a single appliation, for example a proxy server, and all other services are removed or limited to reduce the threat to the computer. It is hardened in this manner primarily due to its location and purpose, which is either on the outside of a firewall or in a demilitarized zone and usually involces access from untrusted networks or computers.


- A NAT gateway or NAT instance is used to provide internet traffic to EC2 instances in a private subnets.
- A bastion is used to securely administer EC2 instances (using SSH or RDP). bastion are called Jump boxes in aurtralia
- you cannot use a NAT Gateway as a bastion host
-----------------------------


Direct connect
--------------
AWS Direct connect is a cloud service solution that makes it easy to establish a dedicated network connection from your premises to AWS. Using AWS direct connect, you can establish private connectivity between AWS and your datacenter, office or colocation environment, which in many cases can reduce your network costs, increase bandwidth throughput, and provide a more consistent network experience than internet-based connections.

- direct connect directly connects your data center to AWS
- useful for high throughput workloads (ie lots of network traffic)
- Or if you need a stable and reliable secure connection

---------------------------------------------

VPC endpoints:
---
Vpc endpoint enables you to privately connect your vpc to supported aws services and vpc endpoint services powered by private link without requiring an internet Gateway, nat device, VPN connection, or AWS direct connect connection. Instances in your vpc do not require public IP addresses to communicate with resources in the service. Traffic between your vpc and the other service does not leave the Amazon network. 

Endpoints are virtual devices. They are horizontally scaled, redundant, and highly available vpc component that allow communication between instances in your vpc and services without imposing availability risk or bandwidth constraint on your network Traffic.

There are two types of VPC endpoints

**interface endpoints:**
* An interface endpoint is an elastic network interface with a private IP address that serves as an entry point for traffic destined to a supported services.

**Gateway endpoints:**
- Amazon S3
- DynamoDB

----------------------

##### Amazon VPC limits:
- The default limit of VPC per region is 5.
- The default limit network ACLs per VPC is 200. You can associate one network ACL to one or more subjets in a VPC.
- The default limit of Subnet per VPC is 200.
- Route table per VPC limit is 200.
- IPv4 CIDR blocks per VPC: This limit is made up of your primary CIDR block plus 4 secondary CIDR blocks.
- The default limit of Elastic IP addresses per region is 5.
- you can effectively have 6 flow logs per network interface if you create 2 flowlogs for the subnet and 2 flow logs for the VPC in which your network interface resides. This limit cannot be increased.
- The default limit of Customer gateway per region is 50.
- Network Interface per instance limit varies by instance type.
- Security groups per VPC per region limit is 500.

---------------------
EXAM POINTS:

* The minimum size subnet that you can have in an Amazon VPC is /28.
* If you want secure connections between on-premise and AWS- Use AWS Managed virtual private network connections.
* The maximum size subnet that you can have in a VPC is /16
* When you provision an Amazon VPC, all subnets can communicate with each other by default.
* You may only have one IGW for each Amazon VPC
* A DHCP option set allows customers to define DNS servers for DNS name resolution, establish domain names for instances within an Amazon VPC, define NTP servers, and define the NetBIOS name servers.
* IPsec is the security protocol supported by Amazon VPC
* Attaching an ENI associated with a different subnet to an instance can make the instance dual-homed.
* A VPG is the VPN concentrator on the AWS side of the VPN connection between the two networks. A CGW represents a physical device or a software application on the customer’s side of the VPN connection. The VPN connection must be initiated from the CGW side, and the connection consists of two IPSec tunnels.
----------------------

##### Q. What are the components of Amazon VPC?

Amazon VPC comprises a variety of objects that will be familiar to customers with existing networks:

- **A Virtual Private Cloud**: A logically isolated virtual network in the AWS cloud. You define a VPC’s IP address space from ranges you select.
- Subnet: A segment of a VPC’s IP address range where you can place groups of isolated resources.
- **Internet Gateway**: The Amazon VPC side of a connection to the public Internet.
- **NAT Gateway**: A highly available, managed Network Address Translation (NAT) service for your resources in a private subnet to access the Internet.
- **Virtual private gateway**: The Amazon VPC side of a VPN connection.
- **Peering Connection**: A peering connection enables you to route traffic via private IP addresses between two peered VPCs.
- **VPC Endpoints**: Enables private connectivity to services hosted in AWS, from within your VPC without using an Internet Gateway, VPN, Network Address Translation (NAT) devices, or firewall proxies.
- **Egress-only Internet Gateway**: A stateful gateway to provide egress only access for IPv6 traffic from the VPC to the Internet.



##### Q. What are the different types of VPC endpoints available on Amazon VPC?

- VPC endpoints enable you to privately connect your VPC to services hosted on AWS without requiring an Internet gateway, a NAT device, VPN, or firewall proxies. Endpoints are horizontally scalable and highly available virtual devices that allow communication between instances in your VPC and AWS services. Amazon VPC offers two different types of endpoints: gateway type endpoints and interface type endpoints.

- **Gateway type endpoints** are available only for AWS services including S3 and DynamoDB. These endpoints will add an entry to your route table you selected and route the traffic to the supported services through Amazon’s private network.

- **Interface type endpoints** provide private connectivity to services powered by PrivateLink, being AWS services, your own services or SaaS solutions, and supports connectivity over Direct Connect. More AWS and SaaS solutions will be supported by these endpoints in the future. 


##### Q. What are the connectivity options for my Amazon VPC?

You may connect your Amazon VPC to:

- The internet (via an internet gateway)
- Your corporate data center using an AWS Site-to-Site VPN connection (via the virtual private gateway)
- Both the internet and your corporate data center (utilizing both an internet gateway and a virtual private gateway)
- Other AWS services (via internet gateway, NAT, virtual private gateway, or VPC endpoints)
- Other Amazon VPCs (via VPC peering connections)

##### Q. How do instances in a VPC access the Internet?

You can use public IP addresses, including Elastic IP addresses (EIPs), to give instances in the VPC the ability to both directly communicate outbound to the Internet and to receive unsolicited inbound traffic from the Internet (e.g., web servers). You can also use the solutions in the next question.
 
##### Q. How do instances without public IP addresses access the Internet

Instances without public IP addresses can access the Internet in one of two ways:
- Instances without public IP addresses can route their traffic through a NAT gateway or a NAT instance to access the Internet. These instances use the public IP address of the NAT gateway or NAT instance to traverse the Internet. The NAT gateway or NAT instance allows outbound communication but doesn’t allow machines on the Internet to initiate a connection to the privately addressed instances.
- For VPCs with a hardware VPN connection or Direct Connect connection, instances can route their Internet traffic down the virtual private gateway to your existing datacenter. From there, it can access the Internet via your existing egress points and network security/monitoring devices.

##### Q. Does traffic go over the internet when two instances communicate using public IP addresses?

- Traffic between two EC2 instances in the same AWS Region stays within the AWS network, even when it goes over public IP addresses.
- Traffic between EC2 instances in different AWS Regions stays within the AWS network, if there is an Inter-Region VPC Peering connection between the VPCs where the two instances reside.
- Traffic between EC2 instances in different AWS Regions where there is no Inter-Region VPC Peering connection between the VPCs where these instances reside, is not guaranteed to stay within the AWS network.

##### Q. How large of a VPC can I create?

Currently, Amazon VPC supports five (5) IP address ranges, one (1) primary and four (4) secondary for IPv4. Each of these ranges can be between /28 (in CIDR notation) and /16 in size. The IP address ranges of your VPC should not overlap with the IP address ranges of your existing network.

For IPv6, the VPC is a fixed size of /56 (in CIDR notation). A VPC can have both IPv4 and IPv6 CIDR blocks associated to it.


##### Q. How many subnets can I create per VPC?

* Currently you can create 200 subnets per VPC.

##### Q. Is there a limit on how large or small a subnet can be?

The minimum size of a subnet is a /28 (or 14 IP addresses.) for IPv4. Subnets cannot be larger than the VPC in which they are created.

For IPv6, the subnet size is fixed to be a /64. Only one IPv6 CIDR block can be allocated to a subnet.


##### Q. Can I change the private IP addresses of an Amazon EC2 instance while it is running and/or stopped within a VPC?

Primary private IP addresses are retained for the instance's or interface's lifetime. Secondary private IP addresses can be assigned, unassigned, or moved between interfaces or instances at any time.

##### Q. Can I assign any IP address to an instance?

You can assign any IP address to your instance as long as it is:

- Part of the associated subnet's IP address range
- Not reserved by Amazon for IP networking purposes
- Not currently assigned to another interface

##### Q. What are the differences between security groups in a VPC and network ACLs in a VPC?

Security groups in a VPC specify which traffic is allowed to or from an Amazon EC2 instance. Network ACLs operate at the subnet level and evaluate traffic entering and exiting a subnet. Network ACLs can be used to set both Allow and Deny rules. Network ACLs do not filter traffic between instances in the same subnet. In addition, network ACLs perform stateless filtering while security groups perform stateful filtering.


##### Q. Can Amazon EC2 instances within a VPC in one region communicate with Amazon EC2 instances within a VPC in another region?

Yes. Instances in one region can communicate with each other using Inter-Region VPC Peering, public IP addresses, NAT gateway, NAT instances, VPN Connections or Direct Connect connections.

##### Q. Can a subnet span Availability Zones?

**No**. A subnet must reside within a single Availability Zone.

##### Q. Can I use my existing Amazon EBS snapshots?

Yes, you may use Amazon EBS snapshots if they are located in the same region as your VPC. 

##### Q. Can I use my existing AMIs in Amazon VPC?

You can use AMIs in Amazon VPC that are registered within the same region as your VPC.

##### Q. I have an existing EC2-Classic account. Can I get a default VPC?

The simplest way to get a default VPC is to create a new account in a region that is enabled for default VPCs, or use an existing account in a region you've never been to before, as long as the Supported Platforms attribute for that account in that region is set to "EC2-VPC".

##### Q. How many VPCs, subnets, Elastic IP addresses, and internet gateways can I create?

You can have:

- Five Amazon VPCs per AWS account per region
- Two hundred subnets per Amazon VPC
- Five Amazon VPC Elastic IP addresses per AWS account per region
- One internet gateway per Amazon VPC

##### Q. Are there AWS Services that cannot be used over Inter-Region VPC Peering?

Network Load Balancers, AWS PrivateLink and Elastic File System cannot be used over Inter-Region VPC Peering.
