# Topic: AWS-QUEUE

### Overview

> Amazon Simple Queue Service (Amazon SQS) offers a secure, durable, and available hosted queue that lets you integrate and decouple distributed software systems and components. Amazon SQS offers common constructs such as dead-letter [queues](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-dead-letter-queues.html) and [cost allocation tags](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-queue-tags.html). It provides a generic web services API that you can access using any programming language that the AWS SDK supports.

> Amazon SQS supports both standard [standard](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/standard-queues.html) and FIFO queues [FIFO queues](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/FIFO-queues.html). For more information, see [Queue types](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/welcome.html#sqs-queue-types).

### Steps to Create a Queue

#### Stage One: Access Queues Dashboard

> From the AWS management console, select SQS (Simple Queue Service), or you can directly go to the ***Queues dashboard***. Start the Create queue wizard from there.

![image](https://user-images.githubusercontent.com/40290711/170339168-413de440-90be-4767-ae77-6c5f74aceabf.png)

#### Stage Two: Create a Queue

> 1. A queue can be created quickly in four steps:

> General details - Provide a case-sensitive name, and choose the type of queue - Standard or FIFO, you want to create. A standard queue supports an unlimited number of transactions per second (TPS) for each API action (SendMessage, ReceiveMessage, or DeleteMessage). Whereas, FIFO queues support up to 3000 messages per second while strictly preserving the message order.

![image](https://user-images.githubusercontent.com/40290711/170339437-48276046-3f08-40fd-b403-266fc7a31d2b.png)

> 2. Configuration details - You can set the following items:

- Visibility timeout - The time-duration (0 seconds - 12 hours) after which a consumer message can become visible to the other consumers. Generally, the consumer must process and delete a message from the queue.


- Message retention period - The duration (1 minute - 14 days) for which the queue retains a message that does not get deleted. Amazon SQS will automatically delete messages that have been in a queue for more than the specified period.


- Delivery delay - The time (0 seconds - 15 minutes) to intentionally delay the delivery of each (new) message added to the queue. According to AWS:

> If your consumers need additional time to process messages, you must delay each new message coming to the queue.

- Maximum message size - It should be between 1 KB and 256 KB.

![image](https://user-images.githubusercontent.com/40290711/170341746-19c362ec-77e6-4366-980f-fd2c542b9c8f.png)

> 3. Access policy - You can define specifically who can send/receive messages to/from your queue. Choose the queue owner, or specified AWS accounts, IAM users, and roles as sender/receiver. The access policy can also be defined in JSON format.

![image](https://user-images.githubusercontent.com/40290711/170342395-e9108b72-0fb6-4ff4-abeb-e889b4ced80d.png)

> 4. Click on the create queue button.

![image](https://user-images.githubusercontent.com/40290711/170343399-44c3c395-96c9-4046-a2e4-aa3af17a671e.png)


#### Check the details of the Existing Queue

> Select a queue from the Queues dashboard to view the basic details and configuration.

![image](https://user-images.githubusercontent.com/40290711/170347575-f5ae5a12-3cfd-4200-aef7-5aacb0274160.png)

> In the snapshot above, the URL is an essential field to use in your application components. In addition, you can also view details about the Lambda triggers, and the access policy. You can even monitor various metrics, such as approximate age of message, the number of messages sent/received/delayed/deleted/empty receives, and size consumed by sent messages.

### Stage 4: Send and receive messages

> For the selected queue, you can either send/receive messages or configure Lambda function trigger. Let's see how to send and receive messages using a Standard queue.

- 1. Send message
> Specify the message body and delay duration while sending a message. As stated earlier, you must add a delay to each new message, if your consumers need additional time to process messages. In other words, your consumer will receive the message only after the duration specified here.

> You can also mention the metadata, such as timestamps, geospatial data, signatures, and identifiers in the form of Message attributes.

> In a FIFO queue, there is an additional concept of message group, to ensures that the messages belonging to a particular group are processed in a strict order.

![image](https://user-images.githubusercontent.com/40290711/170352097-3e67cd4a-0092-4919-ba30-3a83187eb0ca.png)

- 2 Receive messages
> A consumer cannot choose a specific message to receive. Instead, a consumer polls to receive up to 10 number of messages from the queue. The snapshot below shows a message received after polling. The default polling duration is set to 30 seconds.

> Next, click on the message ID to view the message details, body, and metadata. Later, delete the message manually, if not in use.

![image](https://user-images.githubusercontent.com/40290711/170352638-45b9d5dc-0b64-4aef-9eef-37a182cc2297.png)
> Snapshot: **Poll for messages** to recieve messages

![image](https://user-images.githubusercontent.com/40290711/170353230-84ee7b70-4645-4c31-b941-2ca0b79e90fe.png)
> Snapshot: View the message details, body, and metadata.

***Note***: SQS pricing is based on the count and size of messages, and the interactions with Amazon S3 and the AWS Key Management Service.

# END
