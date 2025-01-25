---
title: Azure Event Hub
type: docs
weight: 13
prev: docs/az204/azureEventGrid
next: docs/az204/azureMessageBus
---

Hi again! I hope the lab went smoothly and that you saved room for dessert because we're about to dive into **real-time message consumption**. Okay, that might have been a cheesy pun, but let's get serious. We're moving from **Event Grid** to **Event Hubs**, where the distinction between events and messages starts to blur. In Event Hubs, the messages themselves are often the data you're interested in, unlike Event Grid, where the messages are typically notifications about something else.

Event Hubs is designed to handle massive amounts of streaming data, often with multiple consumers processing the data concurrently. In this segment, we'll cover the basics of **Event Hubs**, key features like **Event Hubs Capture**, **throughput**, **scaling**, and how to control access to events.

### Key Concepts in Event Hubs:
- **Event Hubs** is designed for high-scale data streaming, often processing **telemetry data** from many sources. It uses **AMQP** or **HTTPS** to receive event data from producers, which is then divided into **partitions** within an Event Hub namespace.
- The event data is not stored indefinitely. The retention period ranges from **7 to 90 days**, depending on your service tier. However, there’s a solution to this limitation called **Event Hubs Capture**, which allows you to store event data for longer durations, like in **Azure Blob Storage** or **Azure Data Lake** in **Apache Avro format**.
  
### Event Hubs Architecture:
- **Producer**: The entity that sends data to Event Hubs (e.g., an IoT device).
- **Consumer**: The entity that pulls the data from Event Hubs for processing.
- **Partitions**: These are used to organize data and allow for **parallel processing** of events by different consumers.
- **Consumer Groups**: A group of consumers that process a specific view of the data in the hub. Multiple consumer groups can consume the same data independently.

### Throughput and Scaling:
Event Hubs uses **throughput units** (TUs) to measure capacity and control data throughput. You can pre-purchase these units to control how much data Event Hubs can handle. **Auto-inflate** allows Event Hubs to scale automatically by adjusting the number of throughput units as needed.

### Access Control:
To manage access to Event Hubs, you can use **Active Directory** roles combined with **OAuth**. These roles include:
- **Event Hubs Data Sender**: For event producers.
- **Event Hubs Data Receiver**: For event consumers.
- **Event Hubs Owner**: For full permissions, combining the sender and receiver roles.

### Key Vocabulary for the AZ-204 Exam:
1. **Event Hub Producer**: An entity that generates telemetry data, using **HTTPS** or **AMQP** to send data to Event Hubs.
2. **Event Hub Consumer/Receiver**: The entity that reads data from Event Hubs.
3. **Consumer Group**: A group of consumers that processes a specific view of the data stream.
4. **Partition**: A logical division of the data stream that allows for parallel consumption of events.
5. **Throughput Units**: Pre-purchased capacity units that control the throughput of Event Hubs. 
6. **Auto-Inflate**: A feature that allows Event Hubs to scale automatically based on the required throughput.