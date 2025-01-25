---
title: Azure Event Grid
type: docs
weight: 12
prev: docs/az204/azureCaching
next: docs/az204/azureEventHub
---

Welcome back! In this episode, we’re diving into another essential integration service in Azure: **Azure Event Grid**. Event Grid is a service that facilitates communication between event sources and event handlers (subscribers), streamlining event-driven architectures. In this segment, I’ll show you how to set up both topic and subscription endpoints and walk you through an event-handling workflow in action.

### What is Azure Event Grid?
Azure Event Grid is a communications backplane that connects event sources and event handlers. Event sources, such as **IoT Hub**, **Azure Storage**, **Service Bus**, **Event Hubs**, and custom applications, generate events like device connections or document changes. These events are sent to **topics** (event publishers), while **subscriptions** determine which event handlers (subscribers) should receive these events.

### Key Concepts:
- **Event Sources (Publishers)**: Services or applications that generate events (e.g., a new blob added to a storage container).
- **Topics**: Endpoints for sending events. Topics are created by event sources (e.g., a storage account topic).
- **Subscriptions**: Event handlers that process the events. Subscriptions define the conditions under which events are delivered (e.g., an Azure Function or Logic App).
- **Event Handlers (Subscribers)**: Services that react to events (e.g., Azure Functions, Logic Apps, or Storage Queues).

### Demo: Creating a Topic and Subscription in Azure
Let’s walk through creating a topic and a subscription in the **Azure portal**. For this demo, I’ll use a **storage queue** as the event handler and a **blob container** as the event source.

1. **Create Event Grid Subscription**: Start by creating a subscription for the storage queue, which will act as the event handler. 
2. **Create Topic**: The topic is the endpoint where the event is sent. We’ll choose **Storage Accounts** as the publisher and configure the topic accordingly.
3. **Configure Event Filters**: We’ll set up filters to capture **new blob** events, **blob deletion**, and **changes in blob tier** (e.g., from hot to cool).
4. **Select Event Handler**: Here, we select **Storage Queue** as the event handler and choose the queue that will receive the events.

After creating the topic and subscription, we’ll test the setup by uploading a blob and changing its tier in the storage account. The events—blob creation and tier change—will be sent to the queue for processing.

### Key Vocabulary:
- **Event**: A message describing something that happened (e.g., a blob was added or deleted).
- **Event Publisher**: The source that generates events (e.g., IoT device, storage account).
- **Topic**: The endpoint where events are published.
- **Event Handler (Subscriber)**: The service that processes events (e.g., Logic Apps, Azure Functions).
- **Subscription**: The endpoint that receives events for a specific event handler.

### Testing the Flow:
Once the subscription is set up, I’ll upload a blob and change its tier from hot to cool. These actions will trigger events, which will be captured by the subscription and sent to the storage queue.

---

That's a wrap for Azure Event Grid! It's powerful yet straightforward—connecting your applications and services through event-driven communication. Next up, we have an exciting lab where you can experiment with Azure Event Grid yourself!

---

