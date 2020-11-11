# CDN
---

A content delivery network (CDN) is a system of distributed servers (network) that deliver webpages and other web content to a user based on the geographic locations of the user, the origin of the webpage and a content delivery server.

**Edge location**: This is a location where the content will be cached. this is a separate to an AWS region/AZ

**Origin**: This is the origin of all the files that the CDN will distribute. this can be either an s3 bucket, an EC2 instance, an Elastic load balancer or route53.

**Distribution**: This is the name given the CDN which consists of a collection of edge location.

Amazon cloudfront can be used to deliver your entire website, including dynamic, static, streaming, and interactive content using a global network of edge locations. Requests for your content are automatically routed to the nearest edge location, so content is delivered with the best possible performance.


- RDMP: media streaming
- edge location are not just read only.
- object are cached for TTL(time to live).



#### Geo Restriction
- You can restrict access to your distribution
  - Whitelist: allow access if in the list of approved countries
  - Blacklist: deny access if in the list of banned countries


  - CloudFront
  - GLobal Edge Network
  - Files can be cached for a TTL
  - Great for static content that must be available everywhere
- S3 Cross Region Replication
  - Must be setup for each region you want replication to happen
  - Files are updatred in near real-time
  - Read Only
  - Great for dynamic content that needs to be available at low-latency in few regions
  
  
### CloudFront Signed URL / Signed Cookies
- Allow access to content only via signed url/cookie
- When using cloudfront signed url/cookie we attach a policy with
  - Includes URL expiration
  - Include IP ranges to access data
  - Trusted signers (which AWS acocunts can create signed URLs)
- The URL can be valid from few minutes to years
- Signed url give access to individual file
- Signed access gives access to multiple files
  
  
### CloudFront Signed URL VS S3 Pre-Signed URL
- CloudFront Signed URL
  - Allow access to a path, no matter the origin (could be S3, EC2 etc.)
  - Account wide key-pair, only the root can manage it
  - Can filter bu IP, path, date, expiration
  - Can leverage caching features
- S3 Pre-Signed URL
  - Issue a request as the person who pre-signed the url (the requester got the same rights as the one who signed the url)
  - Uses IAM key for the signing
  - Limited Lifetime

  
-----

Amazon CloudFront provides several mechanisms to allow you to serve private content. These include:
* Signed URLs Use URLs that are valid only between certain times and optionally from certain IP addresses. 
* Signed Cookies Require authentication via public and private key pairs.
* Origin Access Identities (OAI) Restrict access to an Amazon S3 bucket only to a special Amazon CloudFront user associated with your distribution. This is the easiest way to ensure that content in a bucket is only accessed by Amazon CloudFront.
---

##### Q. How does Amazon CloudFront provide higher performance?

Amazon CloudFront employs a global network of edge locations and regional edge caches that cache copies of your content close to your viewers. Amazon CloudFront ensures that end-user requests are served by the closest edge location. As a result, viewer requests travel a short distance, improving performance for your viewers. For files not cached at the edge locations and the regional edge caches, Amazon CloudFront keeps persistent connections with your origin servers so that those files can be fetched from the origin servers as quickly as possible. Finally, Amazon CloudFront uses additional optimizations – e.g. wider TCP initial congestion window – to provide higher performance while delivering your content to viewers.

##### Q. How is Amazon CloudFront different from Amazon S3?

Amazon CloudFront is a good choice for distribution of frequently accessed static content that benefits from edge delivery—like popular website images, videos, media files or software downloads.

##### Q. Can I point my zone apex (example.com versus www.example.com) at my Amazon CloudFront distribution?

Yes. By using Amazon Route 53, AWS’s authoritative DNS service, you can configure an ‘Alias’ record that lets you map the apex or root (example.com) of your DNS name to your Amazon CloudFront distribution. 

##### Q. Does Amazon CloudFront cache POST responses?

Amazon CloudFront does not cache the responses to POST, PUT, DELETE, and PATCH requests – these requests are proxied back to the origin server. You may enable caching for the responses to OPTIONS requests.

##### Q. Does Amazon CloudFront support HTTP/2 without TLS?

**Not currently**. However, most of the modern browsers support HTTP/2 only over an encrypted connection.

##### Q. What is Field-Level Encryption?

Field-Level Encryption is a feature of CloudFront that allows you to securely upload user-submitted data such as credit card numbers to your origin servers. Using this functionality, you can further encrypt sensitive data in an HTTPS from using field-specific encryption keys (which you supply) before a PUT/ POST request is forwarded to your origin. This ensures that sensitive data can only be decrypted and viewed by certain components or services in your application stack.

##### Q: What is Lambda@Edge?

Lambda@Edge allows you to run code at global AWS edge locations without provisioning or managing servers, responding to end users at the lowest network latency. You just upload your Node.js code to AWS Lambda and configure your function to be triggered in response to Amazon CloudFront requests (i.e., when a viewer request lands, when a request is forwarded to or received back from the origin, and right before responding back to the end user). The code is then ready to execute at every AWS edge location when a request for content is received, and scales with the volume of requests across CloudFront edge locations

##### Q: What events can be triggered with Amazon CloudFront?

Your functions will automatically trigger in response to the following Amazon CloudFront events:

- **Viewer Request** - This event occurs when an end user or a device on the Internet makes an HTTP(S) request to CloudFront, and the request arrives at the edge location closest to that user.
- **Viewer Response** - This event occurs when the CloudFront server at the edge is ready to respond to the end user or the device that made the request.
- **Origin Request** - This event occurs when the CloudFront edge server does not already have the requested object in its cache, and the viewer request is ready to be sent to your backend origin webserver (e.g. Amazon EC2, or Application Load Balancer, or Amazon S3).
- **Origin Response** - This event occurs when the CloudFront server at the edge receives a response from your backend origin webserver. 
