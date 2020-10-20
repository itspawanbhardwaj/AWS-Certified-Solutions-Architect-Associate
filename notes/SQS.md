# SQS
---

* SQS is a web service that gives you access to a message queue that can be used to store messages while waiting for a computer to process them.

* SQS is a distributed queue system that enables web service application to quickly and reliably queue messages that one component in the application generates to be consumed by another component. A queue is a temporary repository for messages that are awaiting processing.

* Using SQS, you can decouple the components of an application so they run independently, easing message management between components. Any component of a distributed application can store messages in a fail-safe queue.
* Messages can contain up to 256 KB of text in any format. Any component can later retrieve the messages programmatically using the SQS API.
* The queue acts as a buffer between the component producing and saving data, and the component recieving the data for processing. This means the queue resolves issues that arise if the producer is producing work faster than the consumer can process it, or if the producer or consumer are only intermittently connected to the network.
* Delay Queue: Delay a message upto 15 mins (default is 0 seconds)
* ChangeMessageVisiblity API to change the visiblity while processing a message
* DeleteMessage API to tell sqs the message was processed successfully


##### Types of queues:
1) Standard queues (unlimited transaction)
    - Amazon sqs offer the standard as the default queue type. Standard you lets you have a nearly unlimited number of transactions per second. Standard queues guarantee that a message is delivered at least one. however, occasionally (because of the highly distributed architecture that allows high throughput) more than one copy of a message might be delivered out of order. Standard gives provide test effort or drawing which ensures that messages are generally delivered in the same order as they are sent.


2) FIFO queues (300 transaction per second)
    - The FIFO queue complements the  standard Q stop the most important features of this cute type are FIFO  delivery and exactly-once processing. The  order in which messages are sent and received is strictly preserved and a message is delivered once and remains available until a consumer processes and deletes it. duplicate are not introduced into the cube
    - FIFO queues also support message groups that Allow multiple ordered messages groups within a single queue. FIFO queues are limited to 300 transactions per second but have all the capabilities of the standard queues

------

- SQS is pull based, not pushed based. ie, EC2 will pull msgs from sqs, sqs will not push msgs to EC2
- Msgs are 256 kb in size. We can go utpo 2GB but in that case S3 will be used to store
- **Visibility time:** Visibility Timeout is the amount of time that the message is in which will in the sqs queue after a reader picks up that message. Provided the job is process before the visibility Timeout expires, the message will then be deleted from the queue. If the job is not processed within that time the message will become visible again and other reader will process it. This could result in the same message being delivered twice.
- **SQS long polling:** SQS long polling is a way to retrieve mesages from your SQS queue. while the regular short polling returns immediately (even if the message queue being polled is empty), long polling doesnt returns a responses until a message arrives in the message queue, or the long poll times out. (it saves money)
- **Dead Letter Queues:** Amazon SQS provides support for dead letter queues. A dead letter queue is a queue that other (source) queues can target to send messages that for some reason could not be successfully processed (redrive policy).
A primary benefit of using a dead letter queue is the ability to sideline and isolate the unsuccessfully processed messages. You can then analyze any messages sent to the dead letter queue to try to determine the cause of failure.
- Messages can be kept on the queue from 1 mint to 14 days; 
- The default retention period is 4 days
- The default time for an Amazon SQS visibility timeout is 30 seconds.
- The maximum time for an Amazon SQS visibility timeout is 12 hours.
- The maximum time for an Amazon SQS long polling timeout is 20 seconds.
- The default message retention period that can be set in Amazon SQS is four days.
- The longest configurable message retention period for Amazon SQS is 14 days.
- Topic names should typically be available for reuse approximately 30–60 seconds after the previous topic with the same name has been deleted. The exact time will depend on the number of subscriptions active on the topic; topics with a few subscribers will be


##### Q: How is Amazon SQS different from Amazon SNS?

* Amazon SNS allows applications to send time-critical messages to multiple subscribers through a “push” mechanism, eliminating the need to periodically check or “poll” for updates. Amazon SQS is a message queue service used by distributed applications to exchange messages through a polling model, and can be used to decouple sending and receiving components.

##### Q: How is Amazon SQS different from Amazon MQ?
* If you're using messaging with existing applications, and want to move your messaging to the cloud quickly and easily, we recommend you consider Amazon MQ. It supports industry-standard APIs and protocols so you can switch from any standards-based message broker to Amazon MQ without rewriting the messaging code in your applications. 
* If you are building brand new applications in the cloud, we recommend you consider Amazon SQS and Amazon SNS. Amazon SQS and SNS are lightweight, fully managed message queue and topic services that scale almost infinitely and provide simple, easy-to-use APIs.

##### Q: Does Amazon SQS provide message ordering?
* Yes. FIFO (first-in-first-out) queues preserve the exact order in which messages are sent and received. If you use a FIFO queue, you don't have to place sequencing information in your messages.

* Standard queues provide a loose-FIFO capability that attempts to preserve the order of messages. However, because standard queues are designed to be massively scalable using a highly distributed architecture, receiving messages in the exact order they are sent is not guaranteed.

##### Q: Does Amazon SQS guarantee delivery of messages?

* Standard queues provide at-least-once delivery, which means that each message is delivered at least once.

* FIFO queues provide exactly-once processing, which means that each message is delivered once and remains available until a consumer processes it and deletes it. Duplicates are not introduced into the queue.

##### Q: Can I use Amazon SQS with other AWS services?

* Yes. You can make your applications more flexible and scalable by using Amazon SQS with compute services such as Amazon EC2, Amazon EC2 Container Service (Amazon ECS), and AWS Lambda, as well as with storage and database services such as Amazon Simple Storage Service (Amazon S3) and Amazon DynamoDB.

##### Q: Can I use Java Message Service (JMS) with Amazon SQS?

* Yes. You can take advantage of the scale, low cost, and high availability of Amazon SQS without the worry and high overhead of running your own JMS cluster.

Amazon provides the Amazon SQS Java Messaging Library that implements the JMS 1.1 specification and uses Amazon SQS as the JMS provider. 

##### Q: What is a visibility timeout?

* The visibility timeout is a period of time during which Amazon SQS prevents other consuming components from receiving and processing a message. 

##### Q: What is the typical latency for Amazon SQS?

* Typical latencies for SendMessage, ReceiveMessage, and DeleteMessage API requests are in the tens or low hundreds of milliseconds.

##### Q: For anonymous access, what is the value of the SenderId attribute for a message?

* When the AWS account ID is not available (for example, when an anonymous user sends a message), Amazon SQS provides the IP address.

##### Q: What is Amazon SQS long polling?

* Amazon SQS long polling is a way to retrieve messages from your Amazon SQS queues. While the regular short polling returns immediately, even if the message queue being polled is empty, long polling doesn’t return a response until a message arrives in the message queue, or the long poll times out.

* Long-polling ReceiveMessage calls are billed exactly the same as short-polling ReceiveMessage calls.

##### Q: When should I use Amazon SQS long polling, and when should I use Amazon SQS short polling?

* In almost all cases, Amazon SQS long polling is preferable to short polling. Long-polling requests let your queue consumers receive messages as soon as they arrive in your queue while reducing the number of empty ReceiveMessageResponse instances returned.

* Amazon SQS long polling results in higher performance at reduced cost in the majority of use cases. However, if your application expects an immediate response from a ReceiveMessage call, you might not be able to take advantage of long polling without some modifications to your application.

* For example, if your application uses a single thread to poll multiple queues, switching from short polling to long polling will probably not work, because the single thread will wait for the long-poll timeout on any empty queues, delaying the processing of any queues that might contain messages.

* In such an application, it is a good practice to use a single thread to process only one queue, allowing the application to take advantage of the benefits that Amazon SQS long polling provides.

##### Q: Are the Amazon SQS queues I used previously changing to FIFO queues?
* No. Amazon SQS standard queues (the new name for existing queues) remain unchanged, and you can still create standard queues. These queues continue to provide the highest scalability and throughput; however, you will not get ordering guarantees and duplicates might occur.

* Standard queues are appropriate for many scenarios, such as work distribution with multiple idempotent consumers.

##### Q: Can I convert my existing standard queue to a FIFO queue?

* No. You must choose the queue type when you create it. However, it is possible to move to a FIFO queue. 

* FIFO queues aren't currently compatible with the Amazon SQS Buffered Asynchronous Client.

* FIFO queues are compatible with the Amazon SQS Extended Client Library for Java and the Amazon SQS Java Message Service (JMS) client.



##### Q: Which AWS CloudWatch metrics do Amazon SQS FIFO queues support?

* FIFO queues support all metrics that standard queues support. For FIFO queues, all approximate metrics return accurate counts. For example, the following AWS CloudWatch metrics are supported:
    * ApproximateNumberOfMessagesDelayed - The number of messages in the queue that are delayed and not available for reading immediately.
    *   ApproximateNumberOfMessagesVisible - The number of messages available for retrieval from the queue.
    * ApproximateNumberOfMessagesNotVisible - The number of messages that are in flight (sent to a client but have not yet been deleted or have not yet reached the end of their visibility window).

##### Q: Do Amazon SQS FIFO queues support multiple producers?

* Yes. One or more producers can send messages to a FIFO queue. Messages are stored in the order that they were successfully received by Amazon SQS.
* If multiple producers send messages in parallel, without waiting for the success response from SendMessage or SendMessageBatch actions, the order between producers might not be preserved. The response of SendMessage or SendMessageBatch actions contains the final ordering sequence that FIFO queues use to place messages in the queue, so your multiple-parallel-producer code can determine the final order of messages in the queue.

##### Q: Do Amazon SQS FIFO queues support multiple consumers?

* By design, Amazon SQS FIFO queues don't serve messages from the same message group to more than one consumer at a time. However, if your FIFO queue has multiple message groups, you can take advantage of parallel consumers, allowing Amazon SQS to serve messages from different message groups to different consumers.

##### Q: Can I use a dead letter queue with FIFO queues?

* Yes. However, you must use a FIFO dead letter queue with a FIFO queue. (Similarly, you can use only a standard dead letter queue with a standard queue.)

##### Q: Can a deleted message be received again?
* No. FIFO queues never introduce duplicate messages.

* For standard queues, under rare circumstances, you might receive a previously-deleted message a second time. 

##### Q: Can I share messages between queues in different regions?
* No. Each Amazon SQS message queue is independent within each region.

##### Q: When should I use the SetQueueAttributes operation with JSON objects?
* The SetQueueAttributes operation supports the full access policy language. For example, you can use the policy language to restrict access to a message queue by IP address and time of day.

##### Q: When should I use the permissions API?
* The permissions API provides an interface for sharing access to a message queue to developers. However, this API cannot allow conditional access or more advanced use cases.

##### Q: Is there a size limit on the name of Amazon SQS message queues?
* Queue names are limited to 80 characters.

##### Q: Can I reuse a message queue name?
* A message queue's name must be unique within an AWS account and region. You can reuse a message queue's name after you delete the message queue.

