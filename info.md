# Hadoop Basic :angel:


### 설치 목록
1. [Eclipse](http://www.eclipse.org/downloads/)
1. [VirtualBox](https://www.virtualbox.org/)
1. [Putty](https://www.putty.org)
1. [FileZilla](https://filezilla-project.org/download.php)

## network 설정

### 1. CentOS Network
```vi /etc/sysconfig/network-scripts/ifcfg-eth0```
```
DEVICE=eth0
HWADDR=XX:XX:XX:XX:XX:XX
TYPE=Ethernet
ONBOOT=yes
BOOTPROTO=static
IPADDR=192.168.56.101
NETMASK=255.255.255.0
GATEWAY=192.168.56.1
NETWORK=192.168.56.0
```

### 2. 70-persistent-net.rules 내용 전부삭제

```vi /etc/udev/rules.d/70-persistent-net.rules```

### 3. network restart
```service network restart```
> 잘 수정했다면 전부 OK

### 4. ip check
```ifconfig eth0```
> 1번에 입력한 값이 적용되었는지 확인

## package install 4 ssh

### 초기상태에서는 yum조차 없음.
```
echo "http://vault.centos.org/6.10/os/x86_64/" > /var/cache/yum/x86_64/6/base/mirrorlist.txt
echo "http://vault.centos.org/6.10/extras/x86_64/" > /var/cache/yum/x86_64/6/extras/mirrorlist.txt
echo "http://vault.centos.org/6.10/updates/x86_64/" > /var/cache/yum/x86_64/6/updates/mirrorlist.txt
echo "http://vault.centos.org/6.10/sclo/x86_64/rh" > /var/cache/yum/x86_64/6/centos-sclo-rh/mirrorlist.txt
echo "http://vault.centos.org/6.10/sclo/x86_64/sclo" > /var/cache/yum/x86_64/6/centos-sclo-sclo/mirrorlist.txt
```
> 아마 echo 밑의 두줄은 
No Such file or directory가 출력될 것이나, 무시 :angry:
###
yum install openssh*
service ss