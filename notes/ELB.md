# ELB
---

We can have 
- Internal (private) ELB
- External (public) ELB

We need at least 2 public subnets to provision ELB

##### Types of load balancer:
---
* Application Load Balancer (HTTP, HTTPS, WebSocket)
* Network Load Balancer (TCP, TLS, UDP)
* Classic Load Balancer (HTTP, HTTPS, TCP)

-------------------------------------

- **1: Application load balancer** :  best suited for load balancing of HTTP and HTTPS traffic. They operate at layer 7 and are application-aware. They are intelligent, you can create advanced request routing, sending specified requests to specified requests to specific web servers. 
	- Allows to load balance to multiple applications on same machine
	- Supports redirects (eg http to https)
	- Routing table to different target groups
		- Routing based on url path
		- Routing based on hostname url
		- Routing based on Query string, headers
	- Ideal for micro services and container-based apps
	- Supports multiple ssl certs

- **2: Network load balancer**:  best suited for load balancing of TCP traffic where extreme performance is required. Operating at connection leven (layer 4), Network load balancer are capable of handling millions of requests per second, while maintaining ultra-low latencies.
	- Use for extreme performance
	- Supports multiple ssl certs

- **3: Classic load balancer**: these are the legacy of elastic load balancers, you can load balance HTTP/HTTPS applications and use layer 7- specific features, such as X-forward and sticky sessions.
You can also use strict layer 4 load balancing for applications that rely purely on the TCP protocol.
	- if your application stops responding, the ELB (Classic load balancer) responds with a 504 error.
	- This means that the application is having issues. This could be either at the web server layer or at the database layer.
	- Supports only 1 ssl cert


EC2 instance wont be able to see user public IP address, it will see ELB ip address.
EC2 gets users public IP address from  X-forwarded-for header, for port we have X-forwarded-port and for protocol we have X-Forwarded-Proto



#### Troubleshooting
- 4xx are client induced errors 
- 5xx are application induced errors
- 503 means LB at capacity or no registered target


-----------------------------------------

- Instances monitored by ELB are reported as: InService or OutOfService
- Health checks check the instance health by talking to it
- Have their own DNS name. You are never given an IP Address

Advanced load balancer theory
-----------------------------
- sticky sessions enable your users to stick to the same EC2 instance (works for ALB and CLB)
- cross zone load balancing enables you to load balance across multiple Availability-Zones
- Path patterns allow you to direct traffic to different EC2 instances based on the URL contained in the request.
- Sticky sessions are commonly used when users have to write something to the server, so sticky sessions keep the user on the same ec2


Target Groups
---
- EC2
- ECS
- Lambda
- IP

##### Q: The load balancer is sending all the traffic to one ec2 instance and you notice no traffic is being sent to the second ec2 instance, what will you do?

Disable sticky sessions


--------------------------------------------------

- Elastic Load Balancing supports the **Server Order Preference** option for negotiating connections between a client and a load balancer. 
During the SSL connection negotiatio process, the client and the load balancer present a list of ciphers and protocols that they each support, in order of preference. 
* By default, the first cipher on the client’s list that matches any one of the load balancer’s ciphers is selected for the SSL connection. If the load balancer is configured to support Server Order Preference, then the load balancer selects the first cipher in its list that is in the client’s list of ciphers. This ensures that the load balancer determines which cipher is used for SSL connection. 
If you do not enable Server Order Preference, the order of ciphers presented by the client is used to negotiate connections between the client and the load balancer.

---
##### Q: How do I decide which load balancer to select for my application?

A: Elastic Load Balancing supports three types of load balancers. You can select the appropriate load balancer based on your application needs. 
If you need flexible application management then we recommend you to use Application Load Balancer. 
If extreme performance and static IP is needed for your application then we recommend you to use Network Load Balancer. 
If your application is built within the EC2 Classic network then you should use Classic Load Balancer.


##### Q: Can I privately access Elastic Load Balancing APIs from my Amazon Virtual Private Cloud (VPC) without using public IPs?

A: Yes, you can privately access Elastic Load Balancing APIs from your Amazon Virtual Private Cloud (VPC) by creating VPC endpoints. With VPC endpoints, the routing between the VPC and Elastic Load Balancing APIs is handled by the AWS network without the need for an Internet gateway, NAT gateway, or VPN connection. The latest generation of VPC Endpoints used by Elastic Load Balancing are powered by AWS PrivateLink, an AWS technology enabling the private connectivity between AWS services using Elastic Network Interfaces (ENI) with private IPs in your VPCs. 



Application Load Balancer
-----------------------------

##### Q: Which protocols does an Application Load Balancer support?

A: An Application Load Balancer supports load balancing of applications using HTTP and HTTPS (Secure HTTP) protocols.


##### Q: What TCP ports can I use to load balance?

A: You can perform load balancing for the following TCP ports: 1-65535


##### Q: Does a Classic Load Balancer have the same features and benefits as an Application Load Balancer?

A: While there is some overlap, there is no feature parity between the two types of load balancers. Application Load Balancers are the foundation of our application layer load-balancing platform for the future.

##### Q: Can I use the existing APIs that I use with my Classic Load Balancer with an Application Load Balancer?

A: No. Application Load Balancers require a new set of APIs.

##### Q: How do I manage both Application and Classic Load Balancers simultaneously?

A: The ELB Console will allow you to manage Application and Classic Load Balancers from the same interface. If you are using the CLI or an SDK, you will use a different ‘service’ for Application Load Balancers. For example, in the CLI you will describe your Classic Load Balancers using `aws elb describe-load-balancers` and your Application Load Balancers using `aws elbv2 describe-load-balancers`.


##### Q: Can I convert my Classic Load Balancer to an Application Load Balancer (and vice versa)?

A: No, you cannot convert one load balancer type into another.
You can migrate to Application Load Balancer from Classic Load Balancer.

##### Q: Can I use an Application Load Balancer as a Layer-4 load balancer?

A: No. If you need Layer-4 features, you should use Network Load Balancer.

##### Q: Is IPv6 supported with an Application Load Balancer?

A: Yes, IPv6 is supported with an Application Load Balancer.

##### Q. How can I protect my web applications behind a load balancer from web attacks?

A: You can integrate your Application Load Balancer with AWS WAF, a web application firewall that helps protect web applications from attacks by allowing you to configure rules based on IP addresses, HTTP headers, and custom URI strings. Using these rules, AWS WAF can block, allow, or monitor (count) web requests for your web application. Please see AWS WAF developer guide for more information

##### Q: How can I load balance to EC2-Classic instances?

A: You cannot load balance to EC2-Classic Instances when registering their Instance IDs as targets. However if you link these EC2-Classic instances to the load balancer's VPC using ClassicLink and use the private IPs of these EC2-Classic instances as targets, then you can load balance to the EC2-Classic instances. If you are using EC2 Classic instances today with a Classic Load Balancer, you can easily migrate to an Application Load Balancer.

### Network Load Balancer
----------------------

##### Q: Can I create a TCP (Layer 4) listener for my Network Load Balancer?

A: Yes. Network Load Balancers support only TCP (Layer 4) listeners and TLS listeners.

##### Q: What are the key features available with the Network Load Balancer?

A: Network Load Balancer provides TCP (Layer 4) load balancing. It is architected to handle millions of requests/sec, sudden volatile traffic patterns and provides extremely low latencies. In addition Network Load Balancer also supports TLS termination, preserves the source IP of the clients, and provides stable IP support and Zonal isolation. It also supports long-running connections that are very useful for WebSocket type applications.

##### Q: How does Network Load Balancer compare to what I get with the TCP listener on a Classic Load Balancer?

A: Network Load Balancer preserves the source IP of the client which in the Classic Load Balancer is not preserved. Customers can use proxy protocol with Classic Load Balancer to get the source IP. Network Load Balancer automatically provides a static IP per Availability Zone to the load balancer and also enables assigning an Elastic IP to the load balancer per Availability Zone. This is not supported with Classic Load Balancer.

##### Q: Can I migrate to Network Load Balancer from Classic Load Balancer?

A: Yes. You can migrate to Network Load Balancer from Classic Load Balancer.

##### Q: Does Network Load Balancer support DNS regional and zonal fail-over?

A: Yes,

##### Q: Can I create my Network Load Balancer in a single Availability Zone?

A: Yes

##### Q: Can I have a Network Load Balancer with a mix of ELB-provided IPs and Elastic IPs or assigned private IPs?

A: No.

##### Q: Can I assign more than one EIP to my Network Load Balancer in each subnet?

A: No. For each associated subnet that a Network Load Balancer is in, the Network Load Balancer can only support a single public/internet facing IP address.

##### Q: If I remove/delete a Network Load Balancer what will happen to the Elastic IP addresses that were associated with it?

A: The Elastic IP Addresses that were associated with your load balancer will be returned to your allocated pool and made available for future use.

##### Q: How can I load balance to EC2-Classic instances?

A: You cannot load balance to EC2-Classic Instances when registering their Instance IDs as targets. However if you link these EC2-Classic instances to the load balancer's VPC using ClassicLink and use the private IPs of these EC2-Classic instances as targets, then you can load balance to the EC2-Classic instances. If you are using EC2 Classic instances today with a Classic Load Balancer, you can easily migrate to a Network Load Balancer.

##### Q: How do I enable cross-zone load balancing in Network Load Balancer?

A: You can enable cross-zone loading balancing only after creating your Network Load Balancer. You achieve this by editing the load balancing attributes section and then by selecting the cross-zone load balancing support checkbox.

##### Q: Is there any impact of cross-zone load balancing on Network Load Balancer limits?

A: Yes. Network Load Balancer currently supports 200 targets per Availability Zone. For example, if you are in 2 Availability-Zones, you can have up to 400 targets registered with Network Load Balancer. If cross-zone load balancing is on, then the maximum targets reduces from 200 per Availability Zone to 200 per load balancer. So, in the example above when cross-zone load balancing is on, even though your load balancer is in 2 Availability Zones, you are limited to 200 targets that can be registered to the load balancer.


### Classic Load Balancer
---------------------

##### Q: Which protocols does the Classic Load Balancer support?

A: The Classic Load Balancer supports load balancing of applications using HTTP, HTTPS (Secure HTTP), SSL (Secure TCP) and TCP protocols.

##### Q: What TCP ports can I load balance?

A: You can perform load balancing for the following TCP ports:

[EC2-VPC] 1-65535
[EC2-Classic] 25, 80, 443, 465, 587, 1024-65535
