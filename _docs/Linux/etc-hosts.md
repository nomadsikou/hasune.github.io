---
title: Linux에서 /etc/hosts 에 대해
category: Linux
order: 5
---

linux에서 /etc/hosts 를 살펴보면

```git
cat /etc/hosts

##결과

192.168.1.1  Oracle DB
192.168.1.2  file server

```
이런식으로 나와있는데

흔히 DNS서버와 같은 개념으로 이해하면 된다.  

Oracle DB라는 주소로 접속하면, 192.168.1.1로 리다이렉트 된다.

즉, /etc/hosts는   
ip주소와 호스트명을 1:1 대응식으로 적어놓는 곳

/etc/hosts.allow 와 /etc/hosts.deny
허용과 거부를 기재하는 곳  
정확히 말하면 액세스를 허용하는 호스트를 기재하는 곳 

예를들어
```git
ALL:192.168.1.100
```
/etc/hosts.allow에 이런식으로 적혀있으면  
모든 서비스를 192.168.1.100으로 접속한놈에게 허용 하겠다는것.  
deny는 그 반대로 인식하면 됨.

주의.  
- allow와 deny 양쪽에 같은것을 적으면 허용이 됨
- allow와 deny 양쪽에 다 적지않으면 허용이 됨
- linux는 allow를 먼저 참조하고 그다음에 deny를 참조함 