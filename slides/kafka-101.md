#### Kafka 101 - Hands On

[comment]: # (A comment starting with three or more !!! marks a slide break.)
[comment]: # (!!!)

#### Install confluent platform

Link - [Confluent's official website](https://www.confluent.io/get-started/?product=software).

[comment]: # (!!!)

#### Getting started with confluent platform

```shell
cd ~/Documents/confluent-6.2.0
```

[comment]: # (!!!)

Help

```shell
bin/confluent local --help
```

```shell
Use the "confluent local" commands to try out Confluent Platform by running a single-node instance locally on your machine. Keep in mind, these commands require Java to run.

Usage:
  confluent local [command]

Available Commands:
  current     Get the path of the current Confluent run.
  destroy     Delete the data and logs for the current Confluent run.
  services    Manage Confluent Platform services.
  version     Print the Confluent Platform version.

Global Flags:
  -h, --help            Show help for this command.
  -v, --verbose count   Increase verbosity (-v for warn, -vv for info, -vvv for debug, -vvvv for trace).

Use "confluent local [command] --help" for more information about a command.
```

[comment]: # (!!!)

Start Services

```shell
bin/confluent local services --help
```

```shell
bin/confluent local services start
```

```shell [2-3|4-5|6-7|8-9|10-11|12-13|14-15]
Using CONFLUENT_CURRENT: /var/folders/n1/zs8c9zw95ng2qy812fwv5rjh0000gn/T/confluent.646371
Starting ZooKeeper
ZooKeeper is [UP]
Starting Kafka
Kafka is [UP]
Starting Schema Registry
Schema Registry is [UP]
Starting Kafka REST
Kafka REST is [UP]
Starting Connect
Connect is [UP]
Starting ksqlDB Server
ksqlDB Server is [UP]
Starting Control Center
Control Center is [UP]
```

[comment]: # (!!!)

Check that kafka is running in local

```shell
telnet localhost 9092
```

[comment]: # (!!!)

View the control center UI at [http://localhost:9021](http://localhost:9021)

[comment]: # (!!!)

List kafka topics in the cluster

```shell
bin/kafka-topics \
  --list \
  --bootstrap-server localhost:9092
```

[comment]: # (!!!)

Create a kafka topic

```shell
bin/kafka-topics \
  --create \
  --bootstrap-server localhost:9092 \
  --topic local_test_topic
```

```shell
bin/kafka-topics \
  --list \
  --bootstrap-server localhost:9092 \
  | grep 'local_test_topic'
```

[comment]: # (!!!)

Describe kafka topic

```shell
bin/kafka-topics \
  --describe \
  --bootstrap-server localhost:9092 \
  --topic local_test_topic
```

```shell
Topic: local_test_topic	TopicId: nvBH0kr7SKqX15Y0izcP4Q	PartitionCount: 1	ReplicationFactor: 1	Configs: segment.bytes=1073741824
	Topic: local_test_topic	Partition: 0	Leader: 0	Replicas: 0	Isr: 0	Offline: 
```

[comment]: # (!!!)

Produce to the kafka topic

```shell
bin/kafka-console-producer \
  --bootstrap-server localhost:9092 \
  --topic local_test_topic \
  --property parse.key=true \
  --property key.separator=
```

[comment]: # (!!!)

Consume from the kafka topic

```shell
bin/kafka-console-consumer \
  --bootstrap-server localhost:9092 \
  --topic local_test_topic
```

[comment]: # (!!!)

Delete a kafka topic

```shell
bin/kafka-topics \
  --delete \
  --bootstrap-server localhost:9092 \
  --topic local_test_topic
```

[comment]: # (!!!)

Stop confluent platform

```shell
bin/confluent local services stop
```
