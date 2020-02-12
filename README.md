<h2>This is a project to demonstrate a basic Kafka-Spring Boot integration.</h2>

Submodules pipeline build status:
* Message Producer [![Build Status](https://dev.azure.com/yaraslauliaonau/kafka-spring-boot-demo%20Pipeline/_apis/build/status/rednavis.message-producer?branchName=master)](https://dev.azure.com/yaraslauliaonau/kafka-spring-boot-demo%20Pipeline/_build/latest?definitionId=3&branchName=master)
* Message Processor [![Build Status](https://dev.azure.com/yaraslauliaonau/kafka-spring-boot-demo%20Pipeline/_apis/build/status/rednavis.message-processor?branchName=master)](https://dev.azure.com/yaraslauliaonau/kafka-spring-boot-demo%20Pipeline/_build/latest?definitionId=2&branchName=master)
* Message Consumer [![Build Status](https://dev.azure.com/yaraslauliaonau/kafka-spring-boot-demo%20Pipeline/_apis/build/status/rednavis.message-consumer?branchName=master)](https://dev.azure.com/yaraslauliaonau/kafka-spring-boot-demo%20Pipeline/_build/latest?definitionId=1&branchName=master)

<h3>Initial application structure and flow</h3>

![Image of Flow](https://i.ibb.co/F3C94FG/Kafka-Flow.png)

Message producer provides api (see **Swagger**)

<h3>How to start project</h3>

* Clone the project with submodules using following command 
``` 
git clone --recurse-submodules git@github.com:rednavis/kafka-spring-boot-demo.git 
```
* Run these commands to create a network and run Kafka and Zookeeper in docker containers.

```
docker network create kafka
 
docker run -d --net=kafka --name=zookeeper -e ZOOKEEPER_CLIENT_PORT=2181 confluentinc/cp-zookeeper:5.0.0
docker run -d --net=kafka --name=kafka -p 9092:9092 -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://kafka:9092 -e KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR=1 confluentinc/cp-kafka:5.0.0
```

* If you can’t connect, add this line to `/etc/hosts` to ensure proper routing to container network “kafka”

```
127.0.0.1 kafka
```

* Start messaging platforms with docker start command

```
docker start zookeeper
docker start kafka
```

* Start submodules by calling  `./mvnw spring-boot:run`  in each module.

<h3>Swagger</h3>

After starting **message-producer** you can find Swagger UI page [here](localhost:57300/demo/api/swagger-ui.html)
