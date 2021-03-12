# ClouderaManager 설정

>> info.md를 통해 n대의 서버를 구성했다면 ssh접속부터 시작

- cloudera-manager설치부분은 정책상 변경되었으므로 하기의 다운로드링크부터 진행
- 서버설정은 info.md까지 동일하나 cloudera-manager설치는 하기의 링크로 생략하고 진행

## 설정된 프로젝트 부터 시작할 경우,
1. [프로젝트 다운로드 링크](https://github.com/wikibook/bigdata2nd/archive/master.zip)
1. [가상머신 환경 다운로드 링크](https://drive.google.com/u/0/uc?id=1oLikMIC6bzt0jNV0n49YNOM0foNPXDZh&export=download)
1. VirtualBox에 다운로드받은 폴더로부터  Server1과 Server2 추가
1.  내 컴퓨터의 host를 추가
    - 관리자권한으로 notepad실행
    - C:\Windows\System32\drivers\etc\hosts에 하기 내용 추가 후 저장(보안프로그램이 있다면 잠시 off)
    ```
    ~기존 내용~
    192.168.56.101	server01.hadoop.com
    192.168.56.102	server02.hadoop.com
    192.168.56.103	server03.hadoop.com
    ```

## Cloudera Manager Login
1. [link](http://server01.hadoop.com:7180/)
