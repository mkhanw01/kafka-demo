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
Replication factor: <factor> can be more than available brokers
###

To check messages on kafka topic
```bash
kafka-console-consumer --bootstrap-server <broker(s)> --topic <topic-name> [--from-beginning]
```
example
```bash
kafka-console-consumer --bootstrap-server localhost:9092 --topic spring_topic --from-beginning
```

### Reference Documentation
For further reference, please consider the following sections:

* [Official Apache Maven documentation](https://maven.apache.org/guides/index.html)
* [Spring Boot Maven Plugin Reference Guide](https://docs.spring.io/spring-boot/docs/3.2.2/maven-plugin/reference/html/)
* [Create an OCI image](https://docs.spring.io/spring-boot/docs/3.2.2/maven-plugin/reference/html/#build-image)
* [Spring for Apache Kafka](https://docs.spring.io/spring-boot/docs/3.2.2/reference/htmlsingle/index.html#messaging.kafka)
* [Spring Reactive Web](https://docs.spring.io/spring-boot/docs/3.2.2/reference/htmlsingle/index.html#web.reactive)
* [kafka Documentation](https://docs.spring.io/spring-kafka/reference/index.html)
* [Spring Github kafka](https://github.com/spring-projects/spring-kafka)
* [Medium Doc]()
* * [Apache kafka for beginners](https://medium.com/@patelharshali136/apache-kafka-tutorial-kafka-for-beginners-a58140cef84f)
* * [Apache kafka nutshell](https://medium.com/swlh/apache-kafka-in-a-nutshell-5782b01d9ffb)
* * [Troubleshooting kafka](https://medium.com/wix-engineering/troubleshooting-kafka-for-2000-microservices-at-wix-986ee382fd1e)


### Guides
The following guides illustrate how to use some features concretely:

* [Building a Reactive Restfull Web Service](https://spring.io/guides/gs/reactive-rest-service/)

