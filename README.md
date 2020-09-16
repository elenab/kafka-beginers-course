# Kafka Java Programming 101

## Startup Demos

* Producer
* Producer with Keys
* Producer with Callback
* Consumer
* Consumer Groups
* Consumer with Threads
* Consumer Seek and Assign


## Kafka Twitter Exercise
Kafka Producer that gets data from Twitter tweets and inserts them into our kafka topic in real time.\
Kafka consumer which takes data from kafka and puts it into ElasticSearch

Project goal:

![Project Goal](goal.png?raw=true "Screenshot")

#### Twitter Producer
The Twitter Producer gets data from Twitter based on some keywords and put them in a Kafka topic of your choice
Twitter Java Client: https://github.com/twitter/hbc
Twitter API Credentials: https://developer.twitter.com/

#### ElasticSearch Consumer

The ElasticSearch Consumer gets data from your twitter topic and inserts it into ElasticSearch
ElasticSearch Java Client: https://www.elastic.co/guide/en/elasticsearch/client/java-rest/6.4/java-rest-high.html
ElasticSearch setup:
https://www.elastic.co/guide/en/elasticsearch/reference/current/setup.html

This project was creating while taking [Apache Kafka Series - Learn Apache Kafka for Beginners v2](https://www.udemy.com/course/apache-kafka/) course on Udemy.\

## Useful  Kafka CLI commands:


### Zookeeper
Start zookeeper (make sure nothing is running on port 2181)\

```sh
zookeeper-server-start config/zookeeper.properties
```

### Start kafka:
```sh
kafka-server-start config/server.properties
```

### Topics:

Create:\
```sh
kafka-topics --zookeeper 127.0.0.1:2181 --topic first_topic --create --partitions 3 --replication-factor 1
kafka-topics --zookeeper 127.0.0.1:2181 --topic second_topic --create --partitions 6 --replication-factor 1
 ```

List:\
`kafka-topics --zookeeper 127.0.0.1:2181 --list`

Describe:\
`kafka-topics --zookeeper 127.0.0.1:2181 --topic new_topic_2 --describe`

Delete:\
`kafka-topics --zookeeper 127.0.0.1:2181 --topic second_topic --delete`


### Producing

`kafka-console-producer --broker-list 127.0.0.1:9092 --topic first_topic`

With properties\
`kafka-console-producer --broker-list 127.0.0.1:9092 --topic first_topic --producer-property acks=all`

### Consuming
`kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic`

Consuming from beginning\
`kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --from-beginning`

Consumer in groups\
`kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-first-application`

Start another consumer part of the same group. See messages being spread\
`kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-first-application`

Start another consumer part of a different group from beginning\
`kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-second-application --from-beginning`


### Consumer groups

List consumer groups:\
`kafka-consumer-groups --bootstrap-server localhost:9092 --list`

Describe one specific group:\
`kafka-consumer-groups --bootstrap-server localhost:9092 --describe --group my-first-application`

Reset offsets to earliest dry run:\
`kafka-consumer-groups --bootstrap-server localhost:9092 --group my-first-application --reset-offsets --to-earliest --topic first_topic`

Reset offsets to earliest execute:\
 `kafka-consumer-groups --bootstrap-server localhost:9092 --group my-first-application --reset-offsets --to-earliest --topic first_topic --execute`

Shift offset by two:\
`kafka-consumer-groups --bootstrap-server localhost:9092 --group my-first-application --reset-offsets --shift-by -2 --execute --topic first_topic`

