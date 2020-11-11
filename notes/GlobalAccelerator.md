### Unicast IP vs Anycast IP
- Unicast IP: One server holds one IP
- Anycast IP: All servers hold the same IP address and the client is routed to the nearest one


### AWS GLOBAL ACCELERATOR
(reduces hops/latency when accessing app, e.g accessing app in India from USA)
How it works:
- Leverage AWS internal network to route to your app
- 2 Anycast IP are created for your app
- The Anycast IP send traffic directly to edge locations
- The edge locations send the traffic to your app (thus reduceded hops)

Pros
- Works with Elastic IP, EC2, ALB, NLB, public or private
- Consistent Performance
  - Intelligent routing to the lowest latency and fast regional failover
  - No issue with client cache
  - Internal AWS network
- Health Checks
  - Global accelerator performs a health check of your application
  - Helps make your app global (failover less than 1 min for unhealthy)
  - Great for Disaster Recovery
- Security
  - Only 2 external IP need to be whitelisted
  - DDoS protection (by AWS Shield)
  
  
  
### Global Accelerator vs Cloudfront
- They both uses the AWS global network and its edge locations
- Both services integrate with AWS Shield for DDoS protection
- Cloudfront
  - Improvces performance for both cacheable content (images and videos)
  - Dynamic content (API acceleration and dynamic sites)
  - content is erved at edge
- Global Accelerator
  - Improves performance for a wide range of apps over TCP or UDP
  - Proxying packets at the edge to apps running in one or more AWS regions
  - Good fit for non-http use cases such as gaming (UDP) iot(MQTT) or voip
  - Good for HTTP usecases that requires static ip
  - Good for HTTP use cases that required deterministic and fast regional failover
