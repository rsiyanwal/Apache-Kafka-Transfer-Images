# Introduction 
We are going to send and receive and image using Apache Kafka which is based on a Publish-Subscribe model. In Publish-Subscribe model, we have three entities: **Publisher**, **Subscriber** and **Broker**. 
- Publishers are those entities which produces data (could be sensors);
- Subscribers are those entities which consumes the data for some work to do on their part; 
- Brokers are data manager
A publisher ”pushes” the data into the broker and the subscriber ”gets” the data from broker. Subscribers subscribe to various ”topics” according to their need and brokers provides the data of the topic to these subscribers. The publishers and subscribers are not connected to each other, they are not even aware of each other. We need PublishSubscribe model because it solves a huge issue in IoT deployment. Suppose, we have 10 sensors which sends data to 10 different raspberry pi devices. If all the sensors are sending data to all the raspberry pi devices then we would have 100 connections. Now, suppose the number of sensors and raspberry pi devices are even bigger. Let’s say 10,000 sensors are sending data to 10,000 raspberry pi devices which gives a total of 10,00,00,000 connection.

