#SWF:
---


Amazon simple workflow service is a web service that makes it easy to co-ordinate work across distributed application components. SWF enables applications for a range of use cases, including media processing former web application backends farmer business process workflows farmer and analytics five lines to be design as a coordination of task


Task represent invocation of previous processing steps in an application which can be performed by executable code, web service calls, human actions, and scripts.

To distinguis between SWF and SQS scenarios, always remember if the scenario includes human or manual interaction, SWF will be used.

##### SWF vs SQS
- SQS has a retention period of up to 14 days, with SWF, workflow executions can last up to 1 year.
- Amazon SQF presents a task- oriented API, whereas Amazon SQS offers a message-oriented API.
- Amazon SQF ensures that a task is assigned only once and is never duplicated. with Amazon SQS, you need to handel duplicated messages and may also need to ensure that a message is processed only once(default sqs).
- SWF keeps track if all the tasks and events in an application. With SQS, you need to implement your own application- level tracking, especially if you need to implement your own application- level tracking, especially if your application uses multiple queues.

SWF Actors:
-----------
- Workflow starters: an application that can initiate (start) a workflow. Could be your e-commerce website following the placement of an order, or a mobile app searching for bus times.
- Deciders: Control the flow of activity tasks in a workflow execution. if somethins has failed/finished in a workflow, a decider decided what to do next.
- Activity workers- carry out the activity tasks.

-----

Q: What is Amazon SWF?
Amazon Simple Workflow Service (SWF) is a web service that makes it easy to coordinate work across distributed application components. Amazon SWF enables applications for a range of use cases, including media processing, web application back-ends, business process workflows, and analytics pipelines, to be designed as a coordination of tasks. Tasks represent invocations of various processing steps in an application which can be performed by executable code, web service calls, human actions, and scripts.

The coordination of tasks involves managing execution dependencies, scheduling, and concurrency in accordance with the logical flow of the application. With Amazon SWF, developers get full control over implementing processing steps and coordinating the tasks that drive them, without worrying about underlying complexities such as tracking their progress and keeping their state. Amazon SWF also provides the AWS Flow Framework to help developers use asynchronous programming in the development of their applications. By using Amazon SWF, developers benefit from ease of programming and have the ability to improve their applications’ resource usage, latencies, and throughputs.


Q: When should I use Amazon SWF vs. AWS Step Functions?

AWS Step Functions is a fully managed service that makes it easy to coordinate the components of distributed applications and microservices using visual workflows. Instead of writing a Decider program, you define state machines in JSON. AWS customers should consider using Step Functions for new applications. If Step Functions does not fit your needs, then you should consider Amazon Simple Workflow (SWF). Amazon SWF provides you complete control over your orchestration logic, but increases the complexity of developing applications. You may write decider programs in the programming language of your choice, or you may use the Flow framework to use programming constructs that structure asynchronous interactions for you. AWS will continue to provide the Amazon SWF service, Flow framework, and support all Amazon SWF customers.


Q: How is Amazon SWF different from Amazon SQS?

Both Amazon SQS and Amazon SWF are services that facilitate the integration of applications or microservices:

Amazon Simple Queue Service (Amazon SQS) offers reliable, highly-scalable hosted queues for storing messages while they travel between applications or microservices. Amazon SQS lets you move data between distributed application components and helps you decouple these components.
Amazon Simple Workflow Service (Amazon SWF) is a web service that makes it easy to coordinate work across distributed application components.
The following are the main differences between Amazon SQS and Amazon SWF:

Amazon SWF API actions are task-oriented. Amazon SQS API actions are message-oriented.
Amazon SWF keeps track of all tasks and events in an application. Amazon SQS requires you to implement your own application-level tracking, especially if your application uses multiple queues.
The Amazon SWF Console and visibility APIs provide an application-centric view that lets you search for executions, drill down into an execution’s details, and administer executions. Amazon SQS requires implementing such additional functionality.
Amazon SWF offers several features that facilitate application development, such as passing data between tasks, signaling, and flexibility in distributing tasks. Amazon SQS requires you to implement some application-level functionality.
In addition to a core SDK that calls service APIs, Amazon SWF provides the AWS Flow Framework with which you can write distributed applications using programming constructs that structure asynchronous interactions.
While you can use Amazon SQS to build basic workflows to coordinate your distributed application, you can get this facility out-of-the-box with Amazon SWF, alongside other application-level capabilities.

We recommend trying both Amazon SQS and Amazon SWF to determine which solution best fits your needs.

----------------------------------------
