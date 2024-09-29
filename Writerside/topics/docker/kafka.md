
**安装 Docker 和 Docker Compose
```bash
apt update
apt install docker.io
apt install docker-compose
```

**创建 Docker Compose 文件
- 在工作目录中创建一个 docker-compose.yml 文件，内容如下：
```docker-compose
services:
  zookeeper:
    image: wurstmeister/zookeeper:latest
    container_name: zookeeper
    ports:
      - "2181:2181"
  
  kafka:
    image: wurstmeister/kafka:latest
    container_name: kafka
    ports:
      - "9092:9092"
    environment:
      KAFKA_ADVERTISED_LISTENERS: INSIDE://kafka:9092,OUTSIDE://localhost:9092
      KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: INSIDE:PLAINTEXT,OUTSIDE:PLAINTEXT
      KAFKA_LISTENERS: INSIDE://0.0.0.0:9092,OUTSIDE://0.0.0.0:9092
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
    depends_on:
      - zookeeper
```

**启动 Kafka 和 Zookeeper
- 在包含 docker-compose.yml 文件的目录中，运行以下命令以启动 Kafka 和 Zookeeper：
```bash
docker-compose up -d
```

**验证
```bash
# 创建主题
docker exec -it kafka kafka-topics.sh
# 发送消息到主题
docker exec -it kafka kafka-console-producer.sh --topic test --bootstrap-server localhost:9092
# 消费消息
docker exec -it kafka kafka-console-consumer.sh --topic test --from-beginning --bootstrap-server localhost:9092
```

**停止 Kafka 和 Zookeepe
```bash
docker-compose down
```