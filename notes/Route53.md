# Route53
---

**DNS:**
- domain names to IP address
- IP Addresses are used by computers to identify each other on the network. IP Addresses come in 2 different types: IPv4 and IPv6.
- The IPv4 is a 32 bit field and has over 4 billion different Addresses
- IPv6 128bits address space
- Domain names are controlled by the Internet Assigned Number Authority (IANA) is a root zone database.
- DNS primarily uses UDP to serve requests.
- The TCP protocol is used by DNS server when the response data size exceeds 512 bytes or for tasks such as zone transfers.

-----

##### Zone Files
A zone file is a simple text file that contains the mappings between domain names and IP addresses. This is how a DNS server finally identifies which IP address should be contacted
when a user requests a certain domain name.


---

**Domain Registrar:**
- Because all of the names in a given domain name have to be unique there needs to be a way to organize this all so that domain names aren't duplicated. This is where domain registrar come in. A Registrar is an autority that can assign domain names directly under one or more top-level domains. These domains are registred with InterNIC, a service of ICANN, which enforces uniqueness of domain names across the internet.
- Each domain name becomes registred in a central database known as WhoIS database.
---
**SOA: start of authority**

- The name of the server that supplied the data for the zone
- The administrator of the zone
- The current version of the data file
- The default number of seconds for the time-to-live file on resource records.
---

**NS: Name Server Records**

They are used by top level domain servers to direct traffic to the content DNS server which contains the authoritative DNS records

user -----(google.com in browser)---> Top level domain sercer (.com, it has the name server record) ----> NS Record ----> SOA (IP address records)

---

**A Records**

- An "A" record is the fundamental type of DNS Record. The "A" in A record stands for Address. the A record is used by computer to translate the name of the domain to an IP Address.
- AAAA records are used to map a host to an IPv6 address.
---

**TTL**

time-to-live: the length that a DNS record is cached on either the resolving server or the users own local PC.

------

**CName**

A acanonical Name can be used to recolve one domain name to another.

-------------
**Alias Record**

Alias records are used to map resource record sets in your hosted zone to Elastic Load Balancer, Cloudfront distributions or S3 buckets that are configured as websites.

Alias records work like a CNAME record in that you can map one DNS name (www.example.com) to another 'target' DNS name (elb1234.elb.amazonaws.com)

**Key difference**: A CNAME cant be used for  naked domain names (zone apex record, without www.). you cant have a CNAME for http://acloud.guru, it must  be either an A record or an Alias

- ELBs do not have pre-defined IPv4 addresses; you resolve to them using a DNS name
---

##### Pointer (PTR)
A Pointer (PTR) record is essentially the reverse of an A record. PTR records map an IP address to a DNS name, and they are mainly used to check if the server name is associated with the IP address from where the connection was initiated.

##### Sender Policy Framework (SPF)
Sender Policy Framework (SPF) records are used by mail servers to combat spam. An SPF record tells a mail server what IP addresses are authorized to send an email from your domain name. For example, if you wanted to ensure that only your mail server sends emails from your company’s domain, such as example.com, you would create an SPF record with the IP address of your mail server. That way, an email sent from your domain, such as marketing@example.com, would need to have an originating IP address of your company mail server in order to be accepted. This prevents people from spoofing emails from your domain name.

##### Text (TXT)
Text (TXT) records are used to hold text information. This record provides the ability to associate some arbitrary and unformatted text with a host or other name, such as human readable information about a server, network, data center, and other accounting information.

##### Service (SRV)

A Service (SRV) record is a specification of data in the DNS defining the location (the host name and port number) of servers for specified services. The idea behind SRV is that, given a domain name (for example, example.com) and a service name (for example, web [HTTP], which runs on a protocol [TCP]), a DNS query may be issued to find the host name that provides such a service for the domain, which may or may not be within the domain.


---
**Common DNS Types:**
	SOA Records
	NS Records
	A Records
	CNAME Records
	MX Records - mail
	PTR Records - reverse of A records

------------------------

**Simple Routing policy:**

If you choose the simple routing policy you can only have one record with multiple IP Addresses. If you specify multiple values in as record, Route 53 returns all values to the user in a random order.

-----------------------

**weighted routing policy**

Allow you to slipt your traffic based on different weight assigned.

- if a record set fails a health check, it will be removed from the Route53 until it passes the health check
- You can set SNS notifications to  alert you if a health check is failed.

----------------------
**Latency based Routing**

Allows you to route your traffic based on the lowest network latency for your end  user (ie which ever region will give them the fastest response time)

To use latency-based routing, you create a latency resource record set for the Amazon EC2 (or ELB) resource in each region that hosts your website. When Amazon Route 53 receives a query for your site, it selects the latency resource record set for the region that gives the user the lowest latency. Route 53 then responds with the value associated with that resource record set.

-----------------------

**Failover Routing Policy**

	 Failover routing policies are used when you want to create an active/passive setup.
	 Route53 will monitor the health of your primary site using a health check.
	 A Health Check monitors the health of your end points


--------------------------

**Geolocation routing policy**


Geo location routing lets you choose where your traffic will be sent based on the geographic location of your users.
For example, you might want all the queries from europe to be routed to a fleet of EC2 instances that are specifically configured for your Europian customers.

Geoproximity Routing
---------------------

Geo proximity routing lets Amazon Route 53 traffic to your resources based on the geographic location of your users and your resources. You can also optionally choose to route more traffic or less to a given resource by specifying a value, known as a bias. A bias expands or shrinks the size of the geographic region from which traffic is routed to a resource.

------------------------
**Multivalue Answer policy**

Multivalue answer routing lets you configure amazon route 53 to return multiple values such as IP addresses for your web servers, in response to DNS queries, You can specify multiple values for almost any record but Multivalue answer routing also lets you check the health of each resource, so Route53 returns only value for healthy resources.

-----
##### Hosted Zones
A hosted zone is a collection of resource record sets hosted by Amazon Route 53. Like a traditional DNS zone file, a hosted zone represents resource record sets that are managed together under a single domain name. Each hosted zone has its own metadata and configuration information. 
There are two types of hosted zones: private and public. 
	A private hosted zone is a container that holds information about how you want to route traffic for a domain and its subdomains within one or more Amazon Virtual Private Clouds (Amazon VPCs). 
	A public hosted zone is a container that holds information about how you want to route traffic on the Internet for a domain (for example, example.com) and its subdomains (for example, apex.example.com and acme.example.com).

---
##### Q. What is the difference between a Domain and a Hosted Zone?

A domain is a general DNS concept. Domain names are easily recognizable names for numerically addressed Internet resources. For example, amazon.com is a domain. A hosted zone is an Amazon Route 53 concept. A hosted zone is analogous to a traditional DNS zone file; it represents a collection of records that can be managed together, belonging to a single parent domain name. All resource record sets within a hosted zone must have the hosted zone’s domain name as a suffix. For example, the amazon.com hosted zone may contain records named www.amazon.com, and www.aws.amazon.com, but not a record named www.amazon.ca. You can use the Route 53 Management Console or API to create, inspect, modify, and delete hosted zones. You can also use the Management Console or API to register new domain names and transfer existing domain names into Route 53’s management.


##### Q. Why do I see two charges for the same hosted zone in the same month?

Hosted zones have a grace period of 12 hours--if you delete a hosted zone within 12 hours after you create it, we don't charge you for the hosted zone. After the grace period ends, we immediately charge the standard monthly fee for a hosted zone. If you create a hosted zone on the last day of the month (for example, January 31st), the charge for January might appear on the February invoice, along with the charge for February.


##### Q. Does Amazon Route 53 provide query logging capability?

You can configure Amazon Route 53 to log information about the queries that Amazon Route 53 receives including date-time stamp, domain name, query type, location etc.  When you configure query logging, Amazon Route 53 starts to send logs to CloudWatch Logs. You use CloudWatch Logs tools to access the query logs.


##### Q. Does Amazon Route 53 use an anycast network?

Yes. Anycast is a networking and routing technology that helps your end users’ DNS queries get answered from the optimal Route 53 location given network conditions. As a result, your users get high availability and improved performance with Route 53.



##### Q. Does Amazon Route 53 also provide website hosting?

No. Amazon Route 53 is an authoritative DNS service and does not provide website hosting. However, you can use Amazon Simple Storage Service (Amazon S3) to host a static website. To host a dynamic website or other web applications, you can use Amazon Elastic Compute Cloud (Amazon EC2), which provides flexibility, control, and significant cost savings over traditional web hosting solutions. 


##### Q. Which DNS record types does Amazon Route 53 support?

Amazon Route 53 currently supports the following DNS record types:

- A (address record)
- AAAA (IPv6 address record)
- CNAME (canonical name record)
- CAA (certification authority authorization)
- MX (mail exchange record)
- NAPTR (name authority pointer record)
- NS (name server record)
- PTR (pointer record)
- SOA (start of authority record)
- SPF (sender policy framework)
- SRV (service locator)
- TXT (text record)

Amazon Route 53 also offers alias records, which are an Amazon Route 53-specific extension to DNS. You can create alias records to route traffic to selected AWS resources, including Amazon Elastic Load Balancing load balancers, Amazon CloudFront distributions, AWS Elastic Beanstalk environments, API Gateways, VPC interface endpoints, and Amazon S3 buckets that are configured as websites. Alias record typically have a type of A or AAAA, but they work like a CNAME record. Using an alias record, you can map your record name (example.com) to the DNS name for an AWS resource(elb1234.elb.amazonaws.com). Resolvers see the A or AAAA record and the IP address of the AWS resource.



##### Q. How quickly will changes I make to my DNS settings on Amazon Route 53 propagate globally?

Amazon Route 53 is designed to propagate updates you make to your DNS records to its world-wide network of authoritative DNS servers within 60 seconds under normal conditions. 

##### Q. Can I use AWS CloudTrail logs to roll back changes to my hosted zones?

No. We recommend that you do not use CloudTrail logs to roll back changes to your hosted zones, because reconstruction of your zone change history using your CloudTrail logs may be incomplete.


##### Q. Does Amazon Route 53 support DNSSEC?

Amazon Route 53 does not support DNSSEC for DNS at this time. But Amazon Route 53 allows DNSSEC on domain registration.

##### Q. What is the difference between Latency Based Routing and Geo DNS?

Geo DNS bases routing decisions on the geographic location of the requests. In some cases, geography is a good proxy for latency; but there are certainly situations where it is not. LatencyBased Routing utilizes latency measurements between viewer networks and AWS datacenters. These measurements are used to determine which endpoint to direct users toward.

If your goal is to minimize end-user latency, we recommend using Latency Based Routing. If you have compliance, localization requirements, or other use cases that require stable routing from a specific geography to a specific endpoint, we recommend using Geo DNS.

##### Q. Is there a charge for traffic policies that don’t have a policy record?

No. We only charge for policy records; there is no charge for creating the traffic policy itself.


##### Q. What is Private DNS?

Private DNS is a Route 53 feature that lets you have authoritative DNS within your VPCs without exposing your DNS records (including the name of the resource and its IP address(es) to the Internet.

##### Q. Can I still use Private DNS if I’m not using VPC?

No. Route 53 Private DNS uses VPC to manage visibility and provide DNS resolution for private DNS hosted zones. To take advantage of Route 53 Private DNS, you must configure a VPC and migrate your resources into it.