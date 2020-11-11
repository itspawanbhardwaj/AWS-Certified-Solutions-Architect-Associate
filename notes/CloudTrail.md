# Cloud trail
---
Logs every API call

AWS Cloud trail is a web service that records AWS API calls for your account and delivers log files to you.The recorded information includes:

	The identity of the API caller
	The time of the API call
	The source IP Address of the API caller
	The request  parameters
	The response elements returned by the AWS service

* CloudTrail is enabled by default for past 90 days.
* CloudTrail is region level service

---

##### Q: What search filters can I use to view my account activity?

You can specify Time range and one of the following attributes: Event name, User name, Resource name, Event source, Event ID, and Resource type.

##### Q: What additional CloudTrail features are available by setting up CloudTrail and creating a trail?

By setting up a CloudTrail trail you can deliver your CloudTrail events to Amazon S3, Amazon CloudWatch Logs, and Amazon CloudWatch Events. This enables you to leverage features to help you archive, analyze, and respond to changes in your AWS resources.

##### Q: Can I turn CloudTrail Event History off for my account?

* For any CloudTrail trails that you have created, you can stop logging or delete the trails which will also stop the delivery of account activity to the S3 bucket you had designated as part of your trail configuration as well as delivery to CloudWatch Logs if configured.
* Account activity for the **past 90 days** will still be collected and visible within the CloudTrail console and through the AWS CLI.

##### Q: Where are my log files stored and processed before they are delivered to my Amazon S3 bucket?

* Activity information for services with regional end points (EC2, RDS etc.) is captured and processed in the same region as to which the action is made and delivered to the region associated with your Amazon S3 bucket.
* Action information for services with single end points (IAM, STS, etc.) is captured in the region where the end point is located, processed in the region where the CloudTrail trail is configured and delivered to the region associated with your Amazon S3 bucket.

##### Q: How long will it take for CloudTrail to replicate the trail configuration to all regions?

* Typically, it will take less than **30 seconds** to replicate the trail configuration to all regions.

##### Q: How many trails can I create in an AWS region?

* You can create up to **five** trails in an AWS region. A trail that applies to all regions exists in each region and is counted as one trail in each region.

##### Q: How long does it take CloudTrail to deliver an event for an API call?

* Typically, CloudTrail delivers an event within **15 minutes** of the API call.

##### Q: How often will CloudTrail deliver log files to my Amazon S3 bucket?

* CloudTrail delivers log files to your S3 bucket approximately every **5 minutes**. CloudTrail does not deliver log files if no API calls are made on your account.
