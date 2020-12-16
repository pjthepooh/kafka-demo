# kafka-demo

## Download Kafka Binary
Download Kafka binary files from https://kafka.apache.org/downloads (This repo uses 2.6.0). Unzip file and keep the `confif/` directory, which will be used by brew version Kafka. Shell scripts in `bin/` are binary executables for Kafka, which can be used instead of brew Kafka.

If use binary instead of brew, expose the path, add the following startup file (e.g. `.bash_profile`, `.zshrc`)
```shell
export PATH=$PATH:{path_to_kafka_bin}/kafka_2.13-2.6.0/bin
```

## Installation
```shell
brew install kafka
```

## Start Kafka
#### Start Zookeeper Server
```shell
zookeeper-server-start config/zookeeper.properties
```
Zookeeper server binds to port 2181 by default

#### Start Kafka Server
```shell
kafka-server-start config/server.properties
```
Kafka server binds to port 9092 by default

## Kafka CLI
#### Topic
```shell
kafka-topics --zookeeper localhost:2181
kafka-topics --zookeeper localhost:2181 --create --topic first_topic --partition 3 --replication-factor 1
kafka-topics --zookeeper localhost:2181 --list
kafka-topics --zookeeper localhost:2181 --topic first-topic --describe
kafka-topics --zookeeper localhost:2181 --topic first-topic --delete
```
Note `replication-factor` needs to be smaller or equal to the number of broker

#### Producer
```shell
kafka-console-producer --broker-list localhost:9092 --topic first_topic
kafka-console-producer --broker-list localhost:9092 --topic first_topic --producer-property acks=all
```

#### Consumer
```shell
kafka-console-consumer --bootstrap-server localhost:9092 --topic first_topic
kafka-console-consumer --bootstrap-server localhost:9092 --topic first_topic --from-beginning
kafka-console-consumer --bootstrap-server localhost:9092 --topic first_topic --group group-A
```

#### Consumer Groups
```shell
kafka-consumer-groups --bootstrap-server localhost:9092 --list
kafka-consumer-groups --bootstrap-server localhost:9092 --describe --group group-A
kafka-consumer-groups --bootstrap-server localhost:9092 --group group-A --topic first_topic --reset-offsets --to-earliest --execute
```
