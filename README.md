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
>> XX:XX:XX:XX:XX:XX 부분은 VirtualBox에서 보관해둔 MAC주소로 대체하여 기입

### 2. 70-persistent-net.rules 내용 전부삭제

```vi /etc/udev/rules.d/70-persistent-net.rules```

### 3. network restart
```service network restart```
> 잘 수정했다면 전부 OK

### 4. ip check
```ifconfig eth0```
> 1번에 입력한 값이 적용되었는지 확인

## package install 4 ssh

### yum이 없을경우, 아래 echo문 실행
```
echo "http://vault.centos.org/6.10/os/x86_64/" > /var/cache/yum/x86_64/6/base/mirrorlist.txt
echo "http://vault.centos.org/6.10/extras/x86_64/" > /var/cache/yum/x86_64/6/extras/mirrorlist.txt
echo "http://vault.centos.org/6.10/updates/x86_64/" > /var/cache/yum/x86_64/6/updates/mirrorlist.txt
echo "http://vault.centos.org/6.10/sclo/x86_64/rh" > /var/cache/yum/x86_64/6/centos-sclo-rh/mirrorlist.txt
echo "http://vault.centos.org/6.10/sclo/x86_64/sclo" > /var/cache/yum/x86_64/6/centos-sclo-sclo/mirrorlist.txt
```
> 아마 echo 밑의 두줄은 
No Such file or directory가 출력될 것이나, 무시 :angry:
### opehssh 설치
```
    yum install openssh*
    service sshd restart
    chkconfig sshd on
    reboot
```
> 설치도중 Is this ok [y/N]: 이 나오면 y로 진행
>>__명령어 도중 Fail한건이 떨어지는데 정상이므로 안심.__

### reboot 후
```
su root
# pass word 입력
service network restart
```
> OK 4건시 완료
### ssh설정 완료이므로 편하게 원격으로 접속하자 :+1:


## 마지막 설정
### putty 접속 후 관리자
```
# 관리자로 접속
su root
```

## 여기서부터 집중해서 마무리

#### vi /etc/hosts 내용 수정
```vi /etc/hosts```
```
127.0.0.1 localhost server01
192.168.56.101 server01.hadoop.com server01
192.168.56.102 server02.hadoop.com server02
192.168.56.103 server03.hadoop.com server03
```

#### vi /etc/sysconfig/network 내용 수정
```vi /etc/sysconfig/network```
```
NETWORKING=yes
NETWORKING_IPV6=no
HOSTNAME=server01.hadoop.com
```

#### service network restart

#### vi /etc/selinux/config 내용 수정
```vi /etc/selinux/config```
```
~기존 내용~
SELINUX=disabled
~기존 내용~
```

#### service iptables stop
#### chkconfig iptables off
#### chkconfig ip6tables off
#### sysctl -w vm.swappiness=100



#### vi /etc/sysctl.conf 내용 추가
```vi /etc/sysctl.conf```
```
~기존 내용~
vm.swappiness=100
```

#### vi /etc/rc.local 내용 추가
```vi /etc/rc.local```
```
echo never > /sys/kernel/mm/transparent_hugepage/enabled
echo never > /sys/kernel/mm/transparent_hugepage/defrag
```

#### vi /etc/security/limits.conf 내용 추가

```
~기존내용~
root soft nofile 65536
root hard nofile 65536
*    soft nofile 65536
*    hard nofile 65536
root soft nproc  32768
root hard nproc  32768
*    soft nproc  32768
*    hard nproc  32768
```

```reboot```

## 복제 ㄱ
