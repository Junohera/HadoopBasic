### 토픽을 제어 명령어 테스트

##### Delete Topic
``` bash
kafka-topics --delete --zookeeper ${host}:${port} --topic ${topicName}
kafka-topics --delete --zookeeper server02.hadoop.com:2181 --topic SmartCar-Topic
```

##### Create Topic
``` bash
kafka-topics --create --zookeeper ${host}:${port} --replication-factor 1 --partitions 1 --topic  ${topicName}
kafka-topics --create --zookeeper server02.hadoop.com:2181 --replication-factor 1 --partitions 1 --topic  SmartCar-Topic
```

##### Read Topic
``` bash
kafka-console-consumer --bootstrap-server server02.hadoop.com:9092 --topic SmartCar-Topic --partition 0
```

> 사실상 카프카를 제어할 일이 없도록 설계하고, 설계된대로 설정을 하는 것이 베스트이지만 혹시 모를 일에 대비하여 생성 제거정도는 알면 좋을듯? & 카프카테스트
