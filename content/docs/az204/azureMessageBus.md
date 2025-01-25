---
title: Azure Message Bus
type: docs
weight: 14
prev: docs/az204/azureEventHub
next: docs/az204/
---

Hi again! I’m guessing you’re back for more because Azure events and messaging are just too fascinating to stop exploring, right? Well, let’s keep going! In this segment, we’ll compare **messages** to **events** and discuss the Azure services that are best suited for each. We’ll also explore **Service Bus Queues**, take a look at **Azure Queue Storage** (which we saw earlier as a subscriber in Azure Event Grid), and go over how to choose the most appropriate queue resource for your needs.

### Messages vs. Events:
The main difference between messages and events is that **messages** are the data itself, while **events** are often about something else. Events are typically lightweight notifications of a condition or state change, and the publisher doesn't expect a particular response. On the other hand, **messages** come with an expectation about how the consumer will handle them, and there’s usually a contract between the producer and consumer.

- **Event Grid**: Works in the **event** space and is ideal for reactive programming, event-driven, and event-sourcing patterns. It's great when you need to react to status changes (like file uploads, new user sign-ups, etc.).
- **Event Hubs**: Focuses on **event streaming** and excels as a big data distributed streaming pipeline. If telemetry or distributed data streaming is required, Event Hubs is often the right choice.

### Azure Queue Resources:
Now, let’s explore **Azure Storage Queues** and **Service Bus Queues**. 

#### Azure Storage Queues:
**Azure Storage Queues** shine when you need to store messages and can either tolerate or prefer asynchronous processing. They're great for handling large volumes of messages and work well when you need long-term persistence. If you see questions about **batch processing** or **persisted message storage**, **Azure Storage Queues** are the go-to choice.

#### Azure Service Bus Queues:
**Azure Service Bus Queues** are built for **enterprise-grade messaging**, like **order processing** or complex transaction handling. Service Bus Queues support larger message bodies than Azure Storage Queues, but they aren't designed for storing large collections of messages. If you need **enterprise features** like **transactions**, **at-most-once** and **at-least-once** delivery guarantees, **role-based access control**, or **FIFO** (First In, First Out), **Service Bus Queues** are ideal.

### Demo – Setting Up Service Bus Queues:
Here’s a quick demo showing how to set up **Azure Service Bus Queues** using the Azure CLI. The first step is to create the **Service Bus namespace**:
```bash
az servicebus namespace create --resource-group <resource_group> --name <namespace_name> --location <location>
```
Once the namespace is ready, you can create a queue within it:
```bash
az servicebus queue create --resource-group <resource_group> --namespace-name <namespace_name> --name <queue_name>
```
From here, you can send messages to the queue and de‑queue them once they arrive. This process helps demonstrate how the queue operates with both a producer and consumer.

### Azure Storage Queues – A Quick Look:
Earlier, you saw **Azure Storage Queues** used with **Event Grid** for handling event messages. Here’s a quick demo to show how you can interact with Storage Queues using **Azure CLI**.

You can **peek** at the messages without removing them from the queue:
```bash
az storage message peek --queue-name <queue_name> --account-name <storage_account> --num-messages 1
```
And if you want to **de‑queue** a message, you can use:
```bash
az storage message get --queue-name <queue_name> --account-name <storage_account> --visibility-timeout 3m
```
This will make the message invisible to other consumers for 3 minutes, after which it can be processed again if not deleted.

### Choosing the Right Queue:
When deciding which queue to use, consider these criteria:

- **Use Service Bus Queues** if you need:
  - Long polling receive operations.
  - **FIFO** and **auto-duplicate detection**.
  - **Large message sizes**.
  - **Enterprise features** (transactions, role-based access control, etc.).

- **Use Storage Queues** if you need:
  - Long-term **message persistence**.
  - **Progress tracking** for processing (you can check if a message was de‑queued previously).
  - Simplicity and ease of use—**Storage Queues** have a gentler learning curve.

### Summary of Today’s Topics:
- **Event Grid** and **Event Hubs** were introduced for event-based messaging and event streaming, respectively.
- We compared **Service Bus Queues** (for enterprise messaging) with **Azure Storage Queues** (for message persistence).
- You saw how to set up and interact with both **Service Bus Queues** and **Storage Queues** using the **Azure CLI**.