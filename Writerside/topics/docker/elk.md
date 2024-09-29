**准备 docker-compose 文件
```docker-compose
services:
    elasticsearch:
        image: docker.elastic.co/elasticsearch/elasticsearch:7.10.1
        container_name: elasticsearch
        environment:
            - node.name=elasticsearch
            - cluster.name=docker-cluster
            - discovery.type=single-node
            - bootstrap.memory_lock=true
            - 'ES_JAVA_OPTS=-Xms512m -Xmx512m'
        ulimits:
            memlock:
                soft: -1
                hard: -1
        volumes:
            - esdata:/usr/share/elasticsearch/data
        ports:
            - '9200:9200'
            - '9300:9300'
        networks:
            - elk

    logstash:
        image: docker.elastic.co/logstash/logstash:7.10.1
        container_name: logstash
        volumes:
            - ./logstash/pipeline:/usr/share/logstash/pipeline
        ports:
            - '5000:5000'
            - '9600:9600'
        networks:
            - elk
        depends_on:
            - elasticsearch

    kibana:
        image: docker.elastic.co/kibana/kibana:7.10.1
        container_name: kibana
        environment:
            - ELASTICSEARCH_URL=http://elasticsearch:9200
        ports:
            - '5601:5601'
        networks:
            - elk
        depends_on:
            - elasticsearch

networks:
    elk:
        driver: bridge

volumes:
    esdata:
        driver: local

```

**在工作目录表中创建 logstash.conf
```conf
input {
  beats {
    port => 5044
  }
}

filter {
  if [type] == "syslog" {
    grok {
      match => { "message" => "%{SYSLOGLINE}" }
    }
    date {
      match => [ "timestamp", "MMM  d HH:mm:ss", "MMM dd HH:mm:ss" ]
    }
  }
}

output {
  elasticsearch {
    hosts => ["http://elasticsearch:9200"]
    index => "%{[@metadata][beat]}-%{+YYYY.MM.dd}"
  }
}
```

**部署
```bash
docker-compose -f your-docker-compose-file-name up -d
```