# Kafka Practice

## 설치

```bash
https://www.apache.org/dyn/closer.cgi?path=/kafka/0.8.2.0/kafka_2.10-0.8.2.0.tgz
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


## Topic 생성

```bash
bin/kafka-topics.sh \
  --create \
  --zookeeper localhost:2181 \
  --replication-factor 1 \
  --partitions 1 \
  --topic test
```

##

```bash
bin/kafka-topics.sh \
  --list \
  --zookeeper localhost:2181
```
