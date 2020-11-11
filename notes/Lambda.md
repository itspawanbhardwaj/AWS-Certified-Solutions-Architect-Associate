AWS Lambda is a computer service where you can upload your code and create a Lambda function. Aws that takes care of provisioning and managing the server that you use to 1 the court will stop you don't have to worry about operating system, patching, scaling etc.

Lambda can be used in following ways
- As an event-driven compute service where AWS Lambda runs your code in response to events. Lambda runs your code in response to events. These events could be changes to data in S3 bucket or DynamoDB table.
- As a compute service to run your code in response to HTTP requests using API Gateway or API calls made using AWS SDKs. This is what we use at A Cloud Guru.


#### Lambda@Edge
- Deploy lambda functions alongside your cloudfront cdn
- Lambda is deployed globally


Pricing
---
- Number of requests. First 1 million requests are free. $0.20 per 1 million requests thereafter
- Duration. Duration is calculated from the time your code begins executing until it returns or terminatesm rounded up to nearest 100ms. The price depends upon the amount of memory allocated to lambda function. You are charged $0.00001667 for every GB-second used.

Exam tips
---
- Architectures can get extremely complicated, AWS X-Ray allows you to debug what is happening
- Lambda scales out (not up) automatically. (i.e 5 different invocations will scale out to 5 different lambda function invocations)
- Lambda functions are independent, 1 event = 1 function
- Lmabda is serverless
- Know what services are serverless
- Lambda function can trigger other lambda function, 1 event can = x functions if functions trigger other fucntions
- Lambda can do things globally, you can use it to backup S3 buckets to other S3 buckets etc.
- Know your triggers (RDS cannot trigger lambda)



