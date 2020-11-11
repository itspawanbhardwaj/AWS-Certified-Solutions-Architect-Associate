# SNS
-------------

Amazon simple notification service is a web service that makes it easy to set up, operate and send notifications from the cloud.



It provides developers with the highly scalable, flexible coma and cost-effective capability to publish messages from an application and immediately deliver them to subscribers or other applications

Can deliver notifications via sms, emails, push notifications and http endpoint.

It allows you to group multiple recipients using topics. A topic is an access point for allowing recipients to dynamically subscribe for identical copies of the same notification. 
 
One topic can support deliveries to multiple endpoints type for example you can group together IOS Android and SMS recipients. When you publish once to a topic,  SNS delivers appropriately formatted copies of your message to each subscriber.


##### Q: How is Amazon SNS different from Amazon SQS?

* Amazon Simple Queue Service (SQS) and Amazon SNS are both messaging services within AWS, which provide different benefits for developers.
* Amazon SNS allows applications to send time-critical messages to multiple subscribers through a “push” mechanism, eliminating the need to periodically check or “poll” for updates.
* Amazon SQS is a message queue service used by distributed applications to exchange messages through a polling model, and can be used to decouple sending and receiving components. Amazon SQS provides flexibility for distributed components of applications to send and receive messages without requiring each component to be concurrently available.
* A common pattern is to use SNS to publish messages to Amazon SQS queues to reliably send messages to one or many system components asynchronously.

##### Q: How is Amazon SNS different from Amazon MQ?

**Amazon MQ**, **Amazon SQS**, and **Amazon SNS** are messaging services that are suitable for anyone from startups to enterprises. 
* If you're using messaging with existing applications, and want to move your messaging to the cloud quickly and easily, we recommend you consider Amazon MQ. It supports industry-standard APIs and protocols so you can switch from any standards-based message broker to Amazon MQ without rewriting the messaging code in your applications.
* If you are building brand new applications in the cloud, we recommend you consider Amazon SQS and Amazon SNS. Amazon SQS and SNS are lightweight, fully managed message queue and topic services that scale almost infinitely and provide simple, easy-to-use APIs. You can use Amazon SQS and SNS to decouple and scale microservices, distributed systems, and serverless applications, and improve reliability.


##### Q: What is the format of an Amazon SNS topic?
Topic names are limited to **256 characters**. Alphanumeric characters plus hyphens (-) and underscores are allowed. 
Topic names must be unique within an AWS account. After you delete a topic, you can reuse the topic name. When a topic is created, Amazon SNS will assign a unique ARN (Amazon Resource Name) to the topic, which will include the service name (SNS), region, AWS ID of the user and the topic name. The ARN will be returned as part of the API call to create the topic. Whenever a publisher or subscriber needs to perform any action on the topic, they should reference the unique topic ARN.


##### Q: What are the available operations for Amazon SNS and who can perform these operations?

Amazon SNS provides a set of simple APIs to enable event notifications for topic owners, subscribers and publishers.

Owner operations:

- CreateTopic – Create a new topic.
- DeleteTopic – Delete a previously created topic.
- ListTopics – List of topics owned by a particular user (AWS ID).
- ListSubscriptionsByTopic – List of subscriptions for a particular topic
- SetTopicAttributes – Set/modify topic attributes, including setting and modifying publisher/subscriber permissions, transports supported, etc.
- GetTopicAttributes – Get/view existing attributes of a topic
- AddPermission – Grant access to selected users for the specified actions
- RemovePermission – Remove permissions for selected users for the specified actions

Subscriber operations:

- Subscribe – Register a new subscription on a particular topic, which will generate a confirmation message from Amazon SNS
- ConfirmSubscription – Respond to a subscription confirmation message, confirming the subscription request to receive notifications from the subscribed topic
- UnSubscribe – Cancel a previously registered subscription
- ListSubscriptions – List subscriptions owned by a particular user (AWS ID)

Publisher operations:

- Publish: Publish a new message to the topic.



##### Q: Why are there two different APIs to list subscriptions?

The two APIs to list subscriptions perform different functions and return different results:

- The **ListSubscriptionsByTopic** API allows a topic owner to see the list of all subscribers actively registered to a topic.
- The **ListSubscriptions** API allows a user to get a list of all their active subscriptions (to one or more topics).


##### Q: What are the different delivery formats/transports for receiving notifications?

In order for customers to have broad flexibility of delivery mechanisms, Amazon SNS supports notifications over multiple transport protocols. Customers can select one the following transports as part of the subscription requests:

- **“HTTP”, “HTTPS”** – Subscribers specify a URL as part of the subscription registration; notifications will be delivered through an HTTP POST to the specified URL.
- ”**Email**”, “**Email-JSON**” – Messages are sent to registered addresses as email. Email-JSON sends notifications as a JSON object, while Email sends text-based email.
- “**SQS**” – Users can specify an SQS standard queue as the endpoint; Amazon SNS will enqueue a notification message to the specified queue (which subscribers can then process using SQS APIs such as ReceiveMessage, DeleteMessage, etc.). Note that FIFO queues are not currently supported.
- “**SMS**” – Messages are sent to registered phone numbers as SMS text messages.

##### Q: How would a user subscribe for notifications to be delivered over email?

To receive email notifications for a particular topic, a subscriber should specify “Email” or “Email-JSON” as the protocol and provide a valid email address as the end-point. This can be done using the AWS Management Console or by calling the Amazon SNS API directly. Amazon SNS will then send an email with a confirmation link to the specified email address, and require the user monitoring the email address to explicitly opt-in for receiving email notifications from that particular topic. Once the user confirms the subscription by clicking the provided link, all messages published to the topic will be delivered to that email address.

##### Q: Are Amazon SQS FIFO queues compatible with Amazon Simple Notification Service (SNS)?
Amazon SNS does not currently support forwarding messages to Amazon SQS FIFO queues. You can use SNS to forward messages to standard queues.

##### Q: How would a developer setup an Amazon SQS queue to receive Amazon SNS notifications?

- To have Amazon SNS deliver notifications to an SQS queue, a developer should subscribe to a topic specifying “SQS” as the transport and a valid SQS standard queue as the end-point. In order to allow the SQS queue to receive notifications from Amazon SNS, the SQS queue owner must subscribe the SQS queue to the Topic for Amazon SNS to successfully deliver messages to the queue.

- If the user owns both the Amazon SNS topic being subscribed to and the SQS queue receiving the notifications, nothing further is required. Any message published to the topic will automatically be delivered to the specified SQS queue. If the user owning the SQS queue is not the owner of the topic, Amazon SNS will require an explicit confirmation to the subscription request.



##### Q: How can I fanout identical messages to multiple SQS queues?

* Create an SNS topic first using SNS. Then create and subscribe multiple SQS standard queues to the SNS topic. Now whenever a message is sent to the SNS topic, the message will be fanned out to the SQS queues, i.e. SNS will deliver the message to all the SQS queues that are subscribed to the topic.

#####  Q: What is the format of structured notification messages sent by Amazon SNS?

The notification message sent by Amazon SNS for deliveries over HTTP, HTTPS, Email-JSON and SQS transport protocols will consist of a simple JSON object, which will include the following information:

- MessageId: A Universally Unique Identifier, unique for each notification published.
- Timestamp: The time (in GMT) at which the notification was published.
- TopicArn: The topic to which this message was published
- Type: The type of the delivery message, set to “Notification” for notification deliveries.
- UnsubscribeURL: A link to unsubscribe the end-point from this topic, and prevent receiving any further notifications.
- Message: The payload (body) of the message, as received from the publisher.
- Subject: The Subject field – if one was included as an optional parameter to the publish API call along with the message.
- Signature: Base64-encoded “SHA1withRSA” signature of the Message, MessageId, Subject (if present), Type, Timestamp, and Topic values.
- SignatureVersion: Version of the Amazon SNS signature used.
- Notification messages sent over the “Email” transport only contain the payload (message body) as received from the publisher.


##### Q: How durable is my data once published to Amazon SNS?

SNS provides durable storage of all messages that it receives. Upon receiving a publish request, SNS stores multiple copies (to disk) of the message across multiple Availability Zones before acknowledging receipt of the request to the sender. Each AWS Region has multiple, isolated locations known as Availability Zones. Although rare, should a failure occur in one zone, the operation of SNS and the durability of your messages continue without disruption.

##### Q: Will a notification contain more than one message?

No, all notification messages will contain a single published message.


##### Q: Will messages be delivered to me in the exact order they were published?

The Amazon SNS service will attempt to deliver messages from the publisher in the order they were published into the topic. However, network issues could potentially result in out-of-order messages at the subscriber end.

##### Q: Can a message be deleted after being published?

No, once a message has been successfully published to a topic, it cannot be recalled.


**Supported protocols**
-> HTTP
-> HTTPS
-> Email
-> Email JSON
-> Amazon SQS
-> Application
-> AWS Lambda
-> SMS

---
**SNS vs SQS**
- both are messaging system
- SNS: PUSH
- SQS: POLL
