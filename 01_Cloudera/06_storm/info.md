### storm install

```
cd /home/pilot-pjt
wget http://archive.apache.org/dist/storm/apache-storm-1.2.3/apache-storm-1.2.3.tar.gz
tar -xvf apache-storm-1.2.3.tar.gz
ln -s apache-storm-1.2.3 storm
```

### storm.yaml(맨 밑에 내용 추가) 
```
cd /home/pilot-pjt/storm/conf
vi storm.yaml
```
``` yaml
storm.zookeeper.servers:
 - "server02.hadoop.com"

storm.local.dir: "/home/pilot-pjt/storm/data"

nimbus.seeds: ["server02.hadoop.com"]

supervisor.slots.ports :
 - 6700

ui.port: 8088
```

### modify log Level
```
cd /home/pilot-pjt/storm/log4j2
vi cluster.xml
vi worker.xml
```
```
# ASIS:
level="info"
# TOBE:
level="error"
```

### set bash_profile
```
vi /root/.bash_profile
```
```
PATH=$PATH:/home/pilot-pjt/storm/bin
```

### load bash_profile
```
source /root/.bash_profile
```

### java version check
``` bash
java -version
```

### if not 1.8
``` bash
rm /usr/bin/java
rm /usr/bin/javac
ln -s /usr/java/jdk1.8.0_181-cludera/bin/javac /usr/bin/javac
ln -s /usr/java/jdk1.8.0_181-cludera/bin/javac /usr/bin/java
```

### 리눅스 기동시점 스크립트 등록
1. storm-nimbus
1. storm-supervisor
1. storm-ui
> server2의 /etc/rc.d/init.d에 위 세파일을 각각 업로드
``` bash
chmod 755 /etc/rc.d/init.d/storm-nimbus
chmod 755 /etc/rc.d/init.d/storm-supervisor
chmod 755 /etc/rc.d/init.d/storm-ui
```
> 업로드 후 권한변경


### 서비스 등록 스크립트 취급폴더 생성
``` bash
mkdir /var/log/storm
mkdir /var/run/storm
```

### 아까 올린 service 실행
``` bash
service storm-nimbus start
service storm-supervisor start
service storm-ui start
# 서비스 시작시간이 걸리므로 status로 확인
service storm-nimbus status
service storm-supervisor status
service storm-ui status
```
[storm-ui link](http://server02.hadoop.com:8088/)

### Storm jar 업로드
/home/pilot-pjt/working에 bigdata.smartcar.storm-1.0.jar 업로드

### Storm 실행
``` bash
storm jar bigdata.smartcar.storm-1.0.jar com.wikibook.bigdata.smartcar.storm.SmartCarDriverTopology DriverCarInfo
```

### Storm Topology 배포 확인
[storm-ui link](http://server02.hadoop.com:8088/)의 Topology Summary에 추가된 항목 확인가능

### Storm Topology 제거필요시
``` bash
storm kill "${TopologyName}"
```

### hbase 적재 데이터 확인
``` bash
hbase shell
count 'DriverCarInfo'
scan 'DriverCarInfo', {LIMIT=>20}
scan 'DriverCarInfo', {STARTROW=>'00031061301202-Y0005', LIMIT=>1}
```

### redis 적재 데이터 확인
``` bash
redis-cli
smembers 20210316
```
> 과속차량 확인

### redis jar 업로드
1. /home/pilot-pjt/working에 bigdata.smartcar.redis-1.0.jar업로드

### redis jar 실행
``` bash
cd /home/pilot-pjt/working
java -cp bigdata.smartcar.redis-1.0.jar com.wikibook.bigdata.smartcar.redis.OverSpeedCarInfo 20210316
```