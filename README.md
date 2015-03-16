# Kafka Practice

## 설치

```bash
wget http://mirror.apache-kr.org/kafka/0.8.2.0/kafka_2.10-0.8.2.0.tgz
```

### 압축해제
```bash
tar -xzf kafka_2.10-0.8.2.0.tgz
cd kafka_2.10-0.8.2.0
```

## 서버 구동

### zookeeper

```bash
bin/zookeeper-server-start.sh config/zookeeper.properties
```

### kafka server
```bash
$ bin/kafka-server-start.sh config/server.properties
```


## Topic

```bash
bin/kafka-topics.sh
```

### 생성

```bash
bin/kafka-topics.sh \
  --create \
  --zookeeper localhost:2181 \
  --replication-factor 1 \
  --partitions 1 \
  --topic test
```

### 목록

```bash
bin/kafka-topics.sh \
  --list \
  --zookeeper localhost:2181
```

### 설명

```bash
bin/kafka-topics.sh \
  --describe \
  --topic test \
  --zookeeper localhost:2181
```

## Producer

### send message

```bash
$ bin/kafka-console-consumer.sh \
  --zookeeper localhost:2181 \
  --topic test \
  --from-beginning
```

## Consumer

### consume

```bash
$ bin/kafka-console-producer.sh \
  --broker-list localhost:9092 \
  --topic test
```
## Multi Broker

### create with replication num 2

```bash
$
```

### create with partition num 3

```bash
$
```

### config 수정
```bash
$ cp config/server.properties config/server-1.properties
$ cp config/server.properties config/server-2.properties
```

```
config/server-1.properties:
    broker.id=1
    port=9093
    log.dir=/tmp/kafka-logs-1

config/server-2.properties:
    broker.id=2
    port=9094
    log.dir=/tmp/kafka-logs-2
```

### start node
```
$ bin/kafka-server-start.sh config/server-1.properties &
$ bin/kafka-server-start.sh config/server-1.properties &
```

### topic 생성
```bash
$ bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 3 --partitions 1 --topic my-replicated-topic
```

### describe topic

```bash
$ bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic my-replicated-topic
```

## falut-tolerance

### kill process

```bash
$ ps -ef | grep server-1
# kill {process}
```

### describe topic

```bash
$ bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic my-replicated-topic
```

### consume

```bash
$ bin/kafka-console-consumer.sh --zookeeper localhost:2181 --from-beginning --topic my-replicated-topic
```

## Monitoring(quantifind)

### download

```bash
$ wget https://github.com/quantifind/KafkaOffsetMonitor/releases/latest
$ mv latest KafkaOffsetMonitor-assembly-0.2.1.jar
```

### 실행

```bash
$ java -cp KafkaOffsetMonitor-assembly-0.2.1.jar \
     com.quantifind.kafka.offsetapp.OffsetGetterWeb \
     --zk zk-server1,zk-server2 \
     --port 8080 \
     --refresh 10.seconds \
     --retain 2.days
```
