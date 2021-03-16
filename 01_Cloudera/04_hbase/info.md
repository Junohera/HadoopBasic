# HBASE
> 기존의 데이터베이스와 다른 점은 이름에서도 알수 있다시피 완전한 1차정규화를 통해 열을 기준으로 데이터를 바라본다

### 잘 설치되었는지 확인
```
hbase shell
```
### wait..

### create table and add column & get
```
create 'smartcar_test_table', 'cf'
put 'smartcar_test_table', 'row-key1', 'cf:model', 'Z0001'
put 'smartcar_test_table', 'row-key1', 'cf:no', '12345'
get 'smartcar_test_table', 'row-key1'
```

### drop table & exit
```
disable 'smartcar_test_table'
drop 'smartcar_test_table'
exit
```