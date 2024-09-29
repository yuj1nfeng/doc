###### 安装 JDK
```bash
sudo apt-get install openjdk-8-jdk
```

###### 下载 Kafka
- 访问 [Apache Kafka](https://kafka.apache.org/downloads) 下载最新版本的 Kafka。
- 也可以使用 wget 命令下载：
```bash
wget https://downloads.apache.org/kafka/3.6.0/kafka_2.13-3.6.0.tgz
```

###### 解压 Kafka
```bash
tar -xzf kafka_2.13-3.6.0.tgz
```

###### 移动 Kafka 到 /usr/local/kafka
```bash
mv kafka_2.13-3.6.0 /usr/local/kafka
```

###### 启动 Zookeeper
```bash
cd /usr/local/kafka
bin/zookeeper-server-start.sh config/zookeeper.properties
```

###### 启动 Kafka
```bash
cd /usr/local/kafka
bin/kafka-server-start.sh config/server.properties
```

###### 创建 Kafka 主题
```bash
cd /usr/local/kafka
bin/kafka-topics.sh --create --topic test --bootstrap-server localhost:9092
```

###### 列出所有 Kafka 主题
```bash
bin/kafka-topics.sh --list --bootstrap-server localhost:9092
```

###### 启动 Kafka 生产者
```bash
cd /usr/local/kafka
bin/kafka-console-producer.sh --topic test --bootstrap-server localhost:9092
```

###### 启动 Kafka 消费者
```bash
cd /usr/local/kafka
bin/kafka-console-consumer.sh --topic test --from-beginning --bootstrap-server localhost:9092
```

###### 停止 Kafka
```bash
bin/kafka-server-stop.sh
```

###### 停止 Zookeeper
```bash
bin/zookeeper-server-stop.sh
``` 


###### Zookeeper 服务
- 创建 /etc/systemd/system/zookeeper.service
```
vim /etc/systemd/system/zookeeper.service
```
- 添加以下内容
```ini
[Unit]
Description=Zookeeper
Documentation=http://zookeeper.apache.org/doc/current/
After=network.target

[Service]
Type=simple
ExecStart=/usr/local/kafka/bin/zookeeper-server-start.sh /usr/local/kafka/config/zookeeper.properties
ExecStop=/usr/local/kafka/bin/zookeeper-server-stop.sh
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
- 重载 systemd
```bash
systemctl daemon-reload
```
###### Kafka 服务
- 创建 /etc/systemd/system/kafka.service
```
vim /etc/systemd/system/kafka.service
```
- 添加以下内容
```ini
[Unit]
Description=Kafka
Requires=zookeeper.service
After=zookeeper.service

[Service]
Type=simple
ExecStart=/usr/local/kafka/bin/kafka-server-start.sh /usr/local/kafka/config/server.properties
ExecStop=/usr/local/kafka/bin/kafka-server-stop.sh
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
- 重载 systemd
```bash
systemctl daemon-reload
```

###### 启动服务
```bash
systemctl start zookeeper
systemctl start kafka
```

###### 设置开机启动
```bash
systemctl enable zookeeper
systemctl enable kafka
```