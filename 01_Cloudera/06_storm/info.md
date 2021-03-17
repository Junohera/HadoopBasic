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