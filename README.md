Kafka (incl. Zookeeper) in Docker
===

This repository provides everything you need to run Kafka in Docker.<br>
It's a fork from https://github.com/spotify/docker-kafka, since the original one is not getting updated anymore.

Why?
---
The main hurdle of running Kafka in Docker is that it depends on Zookeeper.
Compared to other Kafka docker images, this one runs both Zookeeper and Kafka
in the same container. This means:

* No dependency on an external Zookeeper host, or linking to another container
* Zookeeper and Kafka are configured to work together out of the box

Run
---

```bash
docker run -d --rm --network docker_network --name kafka --env ADVERTISED_HOST=localhost --env ADVERTISED_PORT=9092 --env TOPICS=my-topic_1,my-topic_2 -p 2181:2181 -p 9092:9092 danielklossek/kafka-zookeeper
```

```bash
export KAFKA=`docker-machine ip \`docker-machine active\``:9092
kafka-console-producer.sh --broker-list $KAFKA --topic test
```

```bash
export ZOOKEEPER=`docker-machine ip \`docker-machine active\``:2181
kafka-console-consumer.sh --zookeeper $ZOOKEEPER --topic test
```

Public Builds
---

https://hub.docker.com/r/danielklossek/kafka-zookeeper

Build from Source
---
    docker build -t danielklossek/kafka-zookeeper kafka/

