# How to choose Azure services for working with messages in your application

## Options for working with messages in Azure
- Azure Storage Queue
- Azure Service Bus
- Azure Notification Hubs
- Azure Event Grid
- Azure Event Hubs
- Azure IoT Hub
- Azure Logic Apps
- Azure SignalR Service

### Azure Storage Queue
- Message lifetime <= 7 days
- Queue size > 80 GB
- Transaction logs
- Message size <= 64KB

### Azure Service Bus 
- Message lifetime > 7 days
- Guaranteed (FIFO) ordered
- Duplicate detection
- Message size <= 1MB>

#### Queues
Put a message on the queue and one application takes it out for processing

#### Topics
Put a message on the queue and multiple applications can take it out for processing


### Azure Notification Hubs
Put a message to send notifications to Andrioid, iOS, Windows and all sort of other platform network notification services without having to write plumbing to talk to those notification services.

### Azure Event Grid
Subscribe to events and push those events to somewhere. For example, subscribe to an event in Azure storage when Blob gets uploaded and use that event to kickoff an Azure Function to process something.

### Azure Event Hubs
Ingest massive amounts of messages and push them off to be analyzed.

### Azure IoT Hub
Take in a lot of messages and have them analyzed but it can also communicate back (bi-directional messaging).

### Azure Logic Apps
Create processes in Azure. Easy to use.

### Azure SignalR Service
Connect clients together in real time and send messages to each other.

## Different Types of Messages

### Intent 

#### Command
Services: Storage Queues, Service Bus, IoT Hub, Logic Apps, SignalR
- You want something to happen
- Could get a message back 
    - Increase temperature on thermostat

### Facts

#### Discrete data
Services: Event Grid, SignalR, Notification Hubs
- Does not happen continually
    - Door open / closed

#### Stream of data
Services: Event Hub, IoT Hub
- Continuous stream of data
- Data is related to each other 
    - Temperature data

## Summary
![image](https://user-images.githubusercontent.com/35857179/79098315-513ff800-7d94-11ea-8cb3-059fbfcf7475.png)
