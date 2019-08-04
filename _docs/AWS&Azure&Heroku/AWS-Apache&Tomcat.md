---
title: AWS Apache Tomcat
category: AWS&Azure&Heroku
comments: true
order: 2
---

AWS EC2(프리티어) 생성시에  
쌩?? 리눅스가 생성되므로  

JDK HTTPD TOMCAT 다 깔고 설정 해야한다.  
누군가에게는 정말 기초적이고 쉬운것일 수 있지만  
누군가에게는 수많은 블로그를 뒤적거리게 만드는 것일수도 있기에..  

한방에 딱!  끝내는 방법으로 포스팅을!!  
(사실은 내가 또 까먹기때문에, 담번에 할때 한방에 하고싶어서 라는)  


■ 설치리스트

- java 1.8
- httpd
- tomcat 8.5



>잡다한 버전확인이나 버전선택 테스트 페이지 확인 이딴거 다 빼고 알맹이만적음

계속 sudo 쓰기 귀찮으니까 루트 비번설정부터(겁나 길고 어렵고 복잡한 놈으로써야함)
```git
sudo su
passwd root
#안전빵 하고싶으면 작업 끝나고 passwd -d root 로 비번 날려도됨

#자바형님부터 설치
yum install java-1.8.0-openjdk
#아파치 형님의 http데몬 설치
yum install httpd


#톰캣 삼촌 유저 맹글기
useradd -s /sbin/nologin tomcat

#톰캣 삼촌 설치
cd /tmp
wget https://www-eu.apache.org/dist/tomcat/tomcat-8/v8.5.43/bin/apache-tomcat-8.5.43.tar.gz
tar zxvf apache-tomcat-8.5.43.tar.gz

#톰캣 삼촌 이사가기
mv apache-tomcat-8.5.43 /opt

#톰캣 삼촌에게 소유자 그룹 넘기기
chown -R tomcat:tomcat /opt/apache-tomcat-8.5.43

#톰캣 삼촌 링크걸기(여러버전 깔아놓고 이런식으로 쓸놈을 링크 걸면된다)
ln -s /opt/apache-tomcat-8.5.43 /opt/tomcat

#톰캣 삼촌 링크 소유자도 바꿔주기
chown -h tomcat:tomcat /opt/tomcat

#톰캣 삼촌 로그 링크걸기
ln -s /opt/tomcat/logs /var/log/tomcat

#톰캣 삼촌 링크 소유자도 바꿔주기
chown -h tomcat:tomcat /var/log/tomcat

#톰캣 삼촌 OS서비스로 등록해주기
cat /usr/lib/systemd/system/tomcat.service

# Systemd unit file for default tomcat
#
# To create clones of this service:
# DO NOTHING, use tomcat@.service instead.

[Unit]
Description=Apache Tomcat Web Application Container
After=syslog.target network.target

[Service]
Type=oneshot
PIDFile=/opt/tomcat/tomcat.pid
RemainAfterExit=yes
#EnvironmentFile=/etc/tomcat/tomcat.conf
#Environment="NAME="
#EnvironmentFile=-/etc/sysconfig/tomcat
ExecStart=/opt/tomcat/bin/startup.sh
ExecStop=/opt/tomcat/bin/shutdown.sh
ExecReStart=/opt/tomcat/bin/shutdown.sh;/opt/tomcat/bin/startup.sh
SuccessExitStatus=143
User=tomcat
Group=tomcat

[Install]
WantedBy=multi-user.target

```

```git
systemctl enabale httpd
systemctl enabale tomcat
```

재부팅 후에
```git
/opt/tomcat/bin/version.sh

sing CATALINA_BASE:   /opt/tomcat
Using CATALINA_HOME:   /opt/tomcat
Using CATALINA_TMPDIR: /opt/tomcat/temp
Using JRE_HOME:        /
Using CLASSPATH:       /opt/tomcat/bin/bootstrap.jar:/opt/tomcat/bin/tomcat-juli.jar
Server version: Apache Tomcat/8.5.43
Server built:   Jul 4 2019 20:53:15 UTC
Server number:  8.5.43.0
OS Name:        Linux
OS Version:     4.14.123-111.109.amzn2.x86_64
Architecture:   amd64
JVM Version:    1.8.0_201-b09
JVM Vendor:     Oracle Corporation
```
이런식으로 나오믄 짝짝짝 완성 

>돌리고싶은 서비스는 /opt/tomcat/webapps 에 넣어놓고(확장자 war파일)  
>jar xvf 파일명.war  이런식으로 풀어주고 쓰면된다.  
>안풀어줘도 되는데 tomcat에서는 풀어주고 쓰는걸 권고함

```git
cat /opt/tomcat/conf/server.xml
.
.
.

<Host name="localhost"  appBase="webapps"
      unpackWARs="true" autoDeploy="true">
.
.

```
보통 문제없지만 요놈도 한번 봐줄 필요는 있다.  

- unpackWARs는 tomcat삼촌이 정해진 시간마다 war파일을 감시하는데  
  war의 변경이 감지되면 자동으로 unpack할건지의 여부
  tomcat삼촌이 jar xvf 를 하는셈이나 마찬가지라서 기존 파일을 덮어쓰기해버리니 주의할것

- autoDeploy는 디플로이중에도 파일변경되면 그것을 적용할지 여부  
(단 xml같은 설정파일은 tomcat 재기동을 해야만함 ruby의 yml같은 개념임)

- Host name은 /etc/hosts 살펴보고 해주면 되고
appBase는 /opt/tomcat/  에서 어플 있는 디렉토리

> 마지막으로 AWS의 보안 그룹에서 8080포트를 열어준다. 












