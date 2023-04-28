### Table of Contents  
[Brief Introduction to Apache Kafka](#kafka-introduction)
  - [When to use Apache Kafka](#kafka-Usecase)
  - [Kafka For images](#for-images)
[Requirements and Installations](#installing-requirements)
[Emphasis](#emphasis)

<a name="kafka-introduction"/>

# Brief Introduction to Apache Kafka

Our approach to sending and receiving images involves Apache Kafka and utilizes the Publish-Subscribe model, consisting of three entities: **Publishers**, **Subscribers**, and **Brokers**.

- Publishers produce data, such as sensor readings or in this case, images.
- Subscribers consume the data and perform their designated tasks.
- Brokers function as data managers.

The Publish-Subscribe model is essential in IoT deployment as it addresses a significant issue. The publisher "pushes" data into the broker, and subscribers "get" the data from the broker. Subscribers can subscribe to different "topics" based on their requirements, and brokers provide the topic's data to these subscribers. Publishers and subscribers are not directly connected and have no awareness of each other.

Consider ten sensors sending data to ten different Raspberry Pi devices. If all sensors send data to all devices, it would require 100 connections. This number increases significantly with more sensors and devices, such as ten thousand sensors sending data to ten thousand Raspberry Pi devices, requiring 100 million connections, which is challenging to maintain.

However, with the Publish-Subscribe model, sensors can publish data to topic A, and subscribers can consume data from topic A, with the broker handling all requests. This means that if ten thousand sensors publish data to topic A, and ten thousand Raspberry Pi devices consume data from topic A, only twenty thousand connections are needed.

![pub-sub](https://user-images.githubusercontent.com/11557572/196355586-4e4d3c15-4930-40b1-a8b9-cf2fcf7c7668.png)
 _( by [Rahul Siyanwal](https://github.com/rsiyanwal))_
 
Key-Value pairs are used by Kafka to send or receive messages. If the key is null, the data is transmitted in Round-Robin fashion. Kafka only accepts input and output as a series of bytes. Thus, data objects must be converted into bytes using a serializer. Message Serialization is used for both values and keys. Kafka offers common serializers to convert various data objects (including JSON, String, Int, Float, Avro, Protobuf, etc.) into bytes.

![Kafka-Message-Serialization-1](https://user-images.githubusercontent.com/11557572/196374105-6f8a4c43-1379-4efd-9a0b-da2e8a0a3f64.png)<br/>
_( Kafka Message (a) Serialization (b) Deserialization on Publisher and Subscriber nodes; by [Rahul Siyanwal](https://github.com/rsiyanwal))_

For Kafka introduction in much detail please follow the link [Apache Kafka Basics](https://github.com/rsiyanwal/Apache-Kafka-Basics/blob/main/README.md).

<a name="kafka-Usecase"/>

## When to use Apache Kafka
Kafka is well-suited for text-based messaging, and its configuration sets limits on message size. The default size limit is 1MB, so adjustments to the configuration are necessary for sending larger messages. However, for this project, we will be transmitting images that are smaller than 1MB in size.
