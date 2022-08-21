## Understanding Pub/Sub

## Introduction
Pub/Sub or Publish-Subscribe is a form of asynchronous service-to-service communication used in serverless and microservices architectures.

In modern cloud architecture, applications are decoupled into smaller, independent building blocks that are easier to develop, deploy and maintain. Publish/Subscribe (Pub/Sub) messaging provides instant event notifications for these distributed applications.  

Pub/Sub is a highly efficient and reliable way of sending messages. Pub/Sub helps build event-driven architecture or decouple applications to increase performance, reliability, and scalability.

## Architecture
The Publish-Subscribe model allows messages to be broadcast to different parts of a system asynchronously. Pub/Sub architecture generally contains one or more Publishers and Subscribers.

![Pub Sub Architecture](https://cdn.hashnode.com/res/hashnode/image/upload/v1661058151217/PcdTKP8cx.png align="center")

### Topic

> A message topic provides a lightweight mechanism to broadcast asynchronous event notifications.

We can imagine a topic as a medium or like a queue, which holds the messages until they are ready to be processed.

Unlike message queues, which batch messages until they are retrieved, message topics transfer messages with no or very little queuing, and push them out immediately to all subscribers. 

### Subscription
> A named resource representing the stream of messages from a single, specific topic, to be delivered to the subscribing application.

![subscriber_pull.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661059158983/SckBMV9Vg.png align="center")

When a new message is published, a Subscription filters the message as specified. So all messages published on the topic may not qualify for all the filtering rules and will not end up in all the subscriptions.

### Publisher
> An application or service that creates and sends messages to single or multiple topics.

Publishers are connected with the topic using an endpoint and secured by an API key. They create appropriate messages and publish the messages into the Topic/Queue.

Usually, topics arrange the messages in FIFO (First-in-First-out) manner, which means the first message sent by the publisher is received first.

### Subscriber
> An application or service with a `subscription` to single or multiple topics to receive messages from it.

Much like Publishers, Subscribers are connected with the subscription using an endpoint and secured by an API key. 


![many-to-many.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661059559007/bAUBYgV3_.png align="center")

## Use Case

### Ingestion user interaction and server events

We can use Pub/Sub to use user interaction events from end-user apps or server events from our system. We can then use a stream processing tool, which delivers the events to databases.

### Real-time event distribution

Events and raw or processed messages may be made available to multiple applications across our team and organization for real-time processing.

### Replicating data among databases

Pub/Sub is commonly used to distribute change events from databases. These events can be used to construct a view of the database state and state history.

### Parallel processing and workflows 

We can efficiently distribute many tasks among multiple workers by using Pub/Sub messages to connect to Cloud Functions like Lambda.

### Data streaming from applications, services, or IoT devices

Real-time data or events can be published by SaaS applications. These data can then be fed to other applications for storage or for showing to end users.

### Load balancing for reliability

Instances of the same service may be deployed on Virtual machines in multiple zones but subscribe to a common topic. When the service fails in any zone, the others can pick up the load automatically.

## Implementation

### Serverless / Managed Services
Pub/Sub can easily be deployed in any project by leveraging modern cloud services.

1. [**AWS SNS**](https://aws.amazon.com/sns/) - Simple Notification Service is a managed service by AWS to implement Pub/Sub.

2. [**Azure Service Bus**](https://azure.microsoft.com/en-in/services/service-bus/) - Service Bus is a managed service by Microsoft Azure. Service Bus supports both `Queue` and `Topic`.

3. [**GCP Pub/Sub**](https://cloud.google.com/pubsub) - Pub/Sub by Google Cloud Platform provides a managed service for Topic.

### Self-hosted

1. [**Apache Pulsar**](https://pulsar.apache.org/) - Apache Pulsar is a cloud-native, multi-tenant, high-performance solution for server-to-server messaging and queuing built on the publisher-subscribe (pub-sub) pattern.

2. [**Apache Kafka**](https://kafka.apache.org/) - Although Apache Kafka is not originally designed for Pub/Sub, it can be used as a publisher-subscribe (pub-sub) service for its high throughput and low latency.

---

That's it. Feel free to comment.