```
cd /home/pilot-pjt/working/
java -cp ${jar} ${class} ${yyyyMMdd} ${size} &
mv /home/pilot-pjt/working/SmartCar/SmartCarStatusInfo_20210313.txt /home/pilot-pjt/working/car-batch-log/
kafka-console-consumer --bootstrap-server server02.hadoop.com:9092 --topic SmartCar-Topic --partition 0
tail -f /var/log/flume-ng/flume-cmf-flume-AGENT-server02.hadoop.com.log
ps -ef | smartcar.log
```
```
cd /home/pilot-pjt/working/
java -cp bigdata.smartcar.loggen-1.0.jar com.wikibook.bigdata.smartcar.loggen.DriverLogMain 20210313 100 &
java -cp bigdata.smartcar.loggen-1.0.jar com.wikibook.bigdata.smartcar.loggen.CarLogMain 20210313 100 &
mv /home/pilot-pjt/working/SmartCar/SmartCarStatusInfo_20210313.txt /home/pilot-pjt/working/car-batch-log/
kafka-console-consumer --bootstrap-server server02.hadoop.com:9092 --topic SmartCar-Topic --partition 0
tail -f /var/log/flume-ng/flume-cmf-flume-AGENT-server02.hadoop.com.log
ps -ef | smartcar.log
```