### Table of Contents  
[Brief Introduction to Apache Kafka](#kafka-introduction)
  - [When to use Apache Kafka](#kafka-Usecase)
  - [Kafka For images](#for-images)
[Requirements and Installations](#installing-requirements)
[Emphasis](#emphasis)

<a name="kafka-introduction"/>

# Brief Introduction to Apache Kafka

We will send and receive an image using Apache Kafka based on a Publish-Subscribe model. In the Publish-Subscribe model, we have three entities: **Publisher**, **Subscriber**, and **Broker**.

- Publishers are those entities that produce data (could be sensors);
- Subscribers are those entities that consume the data for some work to do on their part;
- Brokers are a data manager

A publisher "pushes" the data into the broker and the subscriber "gets" the data from the broker. Subscribers subscribe to various" topics" according to their needs, and brokers provide the topic's data to these subscribers. The publishers and subscribers are not connected; they are unaware of each other. We need the Publish-Subscribe model because it solves a huge issue in IoT deployment. Suppose we have ten sensors that send data to 10 different raspberry pi devices. If all the sensors send data to all the raspberry pi devices, then we would have 100 connections. Now, suppose the number of sensors and raspberry pi devices is even more significant. Ten thousand sensors send data to ten thousand raspberry pi devices, which makes 100 million connections, a considerable number hard to maintain. With the Publish-Subscribe model, the sensors can publish data to topic A, the subscribers can consume the data from topic A, and the broker handles all the requests. If there are ten thousand sensors sending data to the topic and ten thousand raspberry pi devices consuming the data from topic A, then we need only twenty thousand connections. 

![pub-sub](https://user-images.githubusercontent.com/11557572/196355586-4e4d3c15-4930-40b1-a8b9-cf2fcf7c7668.png)
 _( by [Rahul Siyanwal](https://github.com/rsiyanwal))_
 
Kafka uses Key-Value pairs to send or receive a message. The data is transmitted in Round-Robin Fashion when a key is null. Kafka only accepts a series of bytes as input and a series of bytes as output. Therefore, we need a serializer to transform our data object into bytes. Message Serialization is used in both value and key. Kafka comes with common Serializers that help to convert a data object (Including JSON, String, Int, Float, Avro, Protobuf, etc.) to byte.


![Kafka-Message-Serialization-1](https://user-images.githubusercontent.com/11557572/196374105-6f8a4c43-1379-4efd-9a0b-da2e8a0a3f64.png)<br/>
_( Kafka Message (a) Serialization (b) Deserialization on Publisher and Subscriber nodes; by [Rahul Siyanwal](https://github.com/rsiyanwal))_

For Kafka introduction in much detail please follow the link [Apache Kafka Basics](https://github.com/rsiyanwal/Apache-Kafka-Basics/blob/main/README.md).

<a name="kafka-Usecase"/>

## When to use Apache Kafka
Kafka is better suited for text-based messaging. Kafka configuration limits the size of messages that it's allowed to send. By default, this limit is 1MB. However, we must tweak the configuration a little if we need to send large messages. In this project, we will be sending images of size less than 1MB.
