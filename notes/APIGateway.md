API Gateway is a fully managed service that makes it easy for developers to publish, maintain, monitor and secure APIs at any scale.
- Expose HTTPS endpoints to define a RESTful API
- Serverless-ly connect to a service like Dambda & DynamoDB
- Send each api endpoint to a different target
- Run efficiently with low cost
- Scale automatically
- Track and control usage by API key
- Throttle requests to prevent attacks
- Connect to CloudWatch to log all requests for monitoring
- Maintain multiple versions of your API
- API Gateway is at High Level
- If using JS/AJAX that uses multiple domains with API gateway, ensure that CORS in enabled in API Gateway
- CORS is enfored by the client



How Do I Deploy
---
- Uses api gateway domain by default
- Can use custom domain
- Now supports AWS Certificate Manager: Free ssl/tls certs


API Gateway Caching
---
You can enable API caching in Amazon API Gateway with cache to your endpoints response. With caching, you can reduce the number of calls made to your endpoint and also improve the latency of the request to your API. When you enable caching for a stage, API Gateway caches responses from your end point for a specific TTL period in seconds. API Gateway then responds response to the request by looking up the endpoint response from the cache instead of making a request to your endpoint.


