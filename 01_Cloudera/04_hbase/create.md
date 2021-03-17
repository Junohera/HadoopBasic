### 테이블 생성
``` bash
hbase org.apache.hadoop.hbase.util.RegionSplitter DriverCarInfo HexStringSplit -c 2 -f cf1
```
> HexStringSplit : 리전스플릿개수