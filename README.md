# Reflection

# 1. How much data your publisher program will send to the message broker in one run?
The publisher sends **5 messages** to the message broker in one run. Each message is a `UserCreatedEventMessage` containing two fields, a `user_id` (e.g., `"1"` through `"5"`) and a `user_name` (e.g., `"2406440023-Amir"`). All 5 messages are published to the same queue named `"user_created"`.

# 2. The url of: `amqp://guest:guest@localhost:5672` is the same as in the subscriber program, what does it mean?
Both the publisher and subscriber using the same URL means they are **connecting to the same RabbitMQ message broker** running on the same machine, which is the foundation of an event-driven architecture. This shared broker is what ties them together. Without it, messages would never be delivered between the two services. However, their roles are different: the publisher only pushes events into the queue, while the subscriber only consumes and processes those events.