# Kafka Java Programming 101

## Useful CLI commands:

### Start kafka:
```sh
kafka-server-start config/server.properties
```

### Zookeeper:

```sh
zookeeper-server-start config/zookeeper.properties
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


### Producer:\

`kafka-console-producer --broker-list 127.0.0.1:9092 --topic first_topic --producer-property acks=all`

### Consumer:\
` kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-third-application`

### Consumer groups:

List:\
`kafka-consumer-groups --bootstrap-server localhost:9092 --list`

Describe:\
`kafka-consumer-groups --bootstrap-server localhost:9092 --describe --group my-first-application`

Reset offsets to earliest dry run:\
`kafka-consumer-groups --bootstrap-server localhost:9092 --group my-first-application --reset-offsets --to-earliest --execute --topic first_topic`

Reset offsets to earliest execute:\
 `kafka-consumer-groups --bootstrap-server localhost:9092 --group my-first-application --reset-offsets --to-earliest --execute`

Shift offset by two:\
`kafka-consumer-groups --bootstrap-server localhost:9092 --group my-first-application --reset-offsets --shift-by -2 --execute --topic first_topic`

