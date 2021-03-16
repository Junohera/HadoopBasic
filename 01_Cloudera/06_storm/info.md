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
