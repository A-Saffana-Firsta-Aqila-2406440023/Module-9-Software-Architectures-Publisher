# Reflection

## 1. How much data your publisher program will send to the message broker in one run?
The publisher sends **5 messages** to the message broker in one run. Each message is a `UserCreatedEventMessage` containing two fields, a `user_id` (e.g., `"1"` through `"5"`) and a `user_name` (e.g., `"2406440023-Amir"`). All 5 messages are published to the same queue named `"user_created"`.

## 2. The url of: `amqp://guest:guest@localhost:5672` is the same as in the subscriber program, what does it mean?
Both the publisher and subscriber using the same URL means they are **connecting to the same RabbitMQ message broker** running on the same machine, which is the foundation of an event-driven architecture. This shared broker is what ties them together. Without it, messages would never be delivered between the two services. However, their roles are different: the publisher only pushes events into the queue, while the subscriber only consumes and processes those events.

## Running RabbitMQ as Message Broker
![Running RabbitMQ](assets/images/Running_RabbitMQ.png)

## Sending and Processing Event
![Sending and Processing Event Pub](assets/images/Sending_Processing_Event_Pub.png)
![Sending and Processing Event Sub](assets/images/Sending_Processing_Event_Sub.png)

**What is happening?**: When the publisher is run, it sends 5 messages to the RabbitMQ message broker. When the subscriber is run, it connects to the same broker and consumes all the queued messages, printing each received message to the terminal. 

In detail, the publisher was run twice, each time sending 5 `UserCreatedEventMessage` events to the RabbitMQ message broker through the `user_created` queue, resulting in a total of 10 messages stored in the broker. When the subscriber was started, it connected to the same broker via the same `amqp://guest:guest@localhost:5672` URL and consumed all 10 queued messages at once, printing each one as `"In Saffana Firsta Aqila's Computer. Message received: ..."`.