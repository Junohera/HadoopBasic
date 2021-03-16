### change Mirror site
```
echo "http://vault.centos.org/6.10/os/x86_64/" > /var/cache/yum/x86_64/6/base/mirrorlist.txt
echo "http://vault.centos.org/6.10/extras/x86_64/" > /var/cache/yum/x86_64/6/extras/mirrorlist.txt
echo "http://vault.centos.org/6.10/updates/x86_64/" > /var/cache/yum/x86_64/6/updates/mirrorlist.txt
echo "http://vault.centos.org/6.10/sclo/x86_64/rh" > /var/cache/yum/x86_64/6/centos-sclo-rh/mirrorlist.txt
echo "http://vault.centos.org/6.10/sclo/x86_64/sclo" > /var/cache/yum/x86_64/6/centos-sclo-sclo/mirrorlist.txt
```

### ready 4 redis install
```
yum install -y gcc*
yum install -y tcl
```
> Complete!

### redis install

```
cd /home/pilot-pjt
wget http://download.redis.io/releases/redis-5.0.7.tar.gz
tar -xvf redis-5.0.7.tar.gz
cd /home/pilot-pjt/redis-5.0.7
make
make install
cd /home/pilot-pjt/redis-5.0.7/utils
chmod 755 install_server.sh

./install_server.sh
```
> enter enter enter enter !!!!!

### check redis server runYn
```
vi /var/log/redis_6379.log
service redis_6379 status
service redis_6379 start
service redis_6379 stop
```

### check conf
1. 바인딩 IP 제한 해제 : bind 127.0.0.1 주석처리
1. 패스워드 입력 해제 : protected-mode yes -> no
```
vi /etc/redis/6379.conf

service redis_6379 restart
```

### redis test
```
redis-cli
set key:1 Hello!BigData
get key:1
del key:1
quit
```


