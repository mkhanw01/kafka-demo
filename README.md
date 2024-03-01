# Read Me First
The following was discovered as part of building this project:

* The original package name 'com.waseem.kafka.kafkademo'.

# Getting Started
Run the following command in a terminal/console to install kafka via brew and start kafka
```bash
brew install kafka
```
```bash
brew services start kafka
```
Run the following command in a terminal/console to install zookeeper via brew and start zookeeper
```bash
brew install zookeeper
```
```bash
zookeeper-server-start /usr/local/etc/kafka/zookeeper.properties
```
List the topics on kafka
```bash
kafka-topics --list --bootstrap-server localhost:9092
```
Create kafka-topic
```bash
kafka-topics --create --topic test_topic --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1
```

### Note
Replication factor: <factor> can't be more than available brokers
###

To check messages on kafka topic
```bash
kafka-console-consumer --bootstrap-server <broker(s)> --topic <topic-name> [--from-beginning]
```
example
```bash
kafka-console-consumer --bootstrap-server localhost:9092 --topic spring_topic --from-beginning
```
## Some key factor
- Maintain the message ordering, which we can't achieve in the traditional queue.
- Retention requirements aren’t as strong as event streaming platforms have.
- Traditional Message queues follow the point-to-point model.
### Point-to-Point model: 
A message is sent to the message queue and consumed by one and only one consumer.
![Point-to-Point](/Users/waseem.kh/work/kafka-demo/src/main/resources/images/one-to-one-model.png)

### Publish-subscribe model: 
A message is sent to a topic and received by the consumers subscribing to this topic. 
![Publish-subscribe](/Users/waseem.kh/work/kafka-demo/src/main/resources/images/pub-sub.png)

### Topics, partitions, brokers & offset
#### Topics:
Messages are persisted by the *topics*
#### Partitions:
Partitions *(sharding)*,A partition as a small subset of the messages for a topic. 
Divide a topic into partitions and deliver messages evenly across the partitions.
#### Brokers:
Servers that holds the partition is called the *brokers*.
#### offset:
The position of a message into the partition is called an *offset*.
### Consumer groups:
It is a set of consumers, working together to consume messages from the topics.
- Consumer Group A subscribes to Topic A, while Consumer Group B subscribes to both Topic A and B.
- When Topic A is subscribed to by both Consumer Groups A and B, it means the same message is read by multiple consumers. However, within Group A, Partition 1 is read by Consumer 1, and Partition 2 is read by Consumer 2. This partition division within the same group raises a question: Why not allow both consumers in Group A to read from both partitions? The reason for partition division is to ensure the reading order of messages. Allowing both consumers to read from both partitions could lead to one consuming messages faster than the other, disrupting the order.
- Therefore, we impose a constraint where a single partition can only be consumed by one consumer within the same group.
![Consumer-Groups](/Users/waseem.kh/work/kafka-demo/src/main/resources/images/consumer-group.png)


### Producer Flow
The producer client library integrates both the routing layer and the buffer component, 
- Enhancing its functionality. This consolidation not only ensures lower latency but also streamlines operations within the producer client library. 
- With its sophisticated logic, the library efficiently determines the appropriate partition for message transmission. 
- Additionally, by leveraging batching techniques, it significantly boosts throughput, enhancing overall performance.
  ![Producer-Flow](/Users/waseem.kh/work/kafka-demo/src/main/resources/images/producer-flow.png)

### Consumer Flow
The consumer specifies it's offset in a partition and receives back a chunk of events beginning from 
that position.
- A new consumer wants to join group 1 and let's say wants to subscribe to topic A. It will first hash the group name and find the corresponding broker for the consumer group. Every consumer group will have a broker coordinator. Once the Coordinator Broker is identified a subscription request is made by the consumer.
- The coordinator after receiving the request will assign a particular partition to the consumer.
- The consumer now starts receiving messages from the last consumed offset which is maintained by the consumed state in state storage in the broker. If a consumer wants to receive messages from the beginning a special request can be made and a separate state for the consumer will be maintained.
- Consumer once processed the message will commit the offset to the broker
![Consumer-Flow](/Users/waseem.kh/work/kafka-demo/src/main/resources/images/consumer-group.png)
#### Push vs pull
Whether brokers should push data to the consumers, or consumers should pull data from the brokers.

### Consumer Rebalancing 
This will decides which consumer is responsible for which subset of partitions. The process could occur when a consumer joins,leave,crashes or when partitions are adjusted.
- Assume there is 2 consumers in the group, and 4 partitions in the subscribed topic.
![Consumer-Rebalancing](/Users/waseem.kh/work/kafka-demo/src/main/resources/images/consumer-rebalancing.png)

### Complete Diagram
![Kafka-Overview](/Users/waseem.kh/work/kafka-demo/src/main/resources/images/kafka-overview.png)

### Reference Documentation
For further reference, please consider the following sections:

* [Official Apache Maven documentation](https://maven.apache.org/guides/index.html)
* [Spring Boot Maven Plugin Reference Guide](https://docs.spring.io/spring-boot/docs/3.2.2/maven-plugin/reference/html/)
* [Create an OCI image](https://docs.spring.io/spring-boot/docs/3.2.2/maven-plugin/reference/html/#build-image)
* [Spring for Apache Kafka](https://docs.spring.io/spring-boot/docs/3.2.2/reference/htmlsingle/index.html#messaging.kafka)
* [Spring Reactive Web](https://docs.spring.io/spring-boot/docs/3.2.2/reference/htmlsingle/index.html#web.reactive)
* [kafka Documentation](https://docs.spring.io/spring-kafka/reference/index.html)
* [Spring Github kafka](https://github.com/spring-projects/spring-kafka)



### Guides
The following guides illustrate how to use some features concretely:

* [Building a Reactive Restfull Web Service](https://spring.io/guides/gs/reactive-rest-service/)

