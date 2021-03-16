[하둡 기본 경로](http://server01.hadoop.com:9870/)

### logger 에서 hdfs로 옮겼을 경우
1. jar 교체가 필요
1. server2의 '/opt/cloudera/parcels/CDH-6.3.2-1.cdh6.3.2.p0.1605554/lib/flume-ng/lib' 위치에 bigdata.smartcar.flume-1.0.jar를 업로드

### 대상폴더로 이동전 tail실행 후 이동 실행
``` bash
tail -f /var/log/flume-ng/flume-cmf-flume-AGENT-server02.hadoop.com.log
mv /home/pilot-pjt/working/SmartCar/SmartCarStatusInfo_20210313.txt /home/pilot-pjt/working/car-batch-log/
```

### command

#### 목록 확인
``` bash
hdfs dfs -ls -R /pilot-pjt/collect/car-batch-log
```

#### 특정 로그파일 확인
``` bash
hdfs dfs -cat ${출력된 디렉터리/파일명.log}
hdfs dfs -tail ${출력된 디렉터리/파일명.log}
```