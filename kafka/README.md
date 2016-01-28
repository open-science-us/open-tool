# [Apache Kafka](http://kafka.apache.org)

## Installation an Configuration on Mac
~~~
cd /work/kafka

curl -OL http://apache.mirrors.hoobly.com/kafka/0.9.0.0/kafka_2.10-0.9.0.0.tgz

tar xzvf kafka_2.10-0.9.0.0.tgz

cd kafka_2.10-0.9.0.0

mkdir zk_data

mkdir data

vi config/zookeeper.properties

dataDir=/work/kafka/kafka_2.10-0.9.0.0/zk_data


vi config/server.properties

log.dirs=/work/kafka/kafka_2.10-0.9.0.0/data


bin/zookeeper-server-start.sh config/zookeeper.properties &

bin/kafka-server-start.sh config/server.properties &

bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test

bin/kafka-topics.sh --list --zookeeper localhost:2181


bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test

bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic test --from-beginning
~~~
