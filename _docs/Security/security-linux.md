---
title: 보안을 염두한 Linux관리
category: Security
comments: true
order: 4
---

■ 그럭저럭 시큐어한 리눅스 서버구축  
나름대로 대충 요약및 번역  
[そこそこセキュアなlinuxサーバーを作る](https://qiita.com/cocuh/items/e7c305ccffb6841d109c)  

---
--- 
■ SSHD편


- 별 5개짜리 ★★★★★
- SSH표준포트 22는 너무 흔하니 반드시 바꿀것!
>SSH표준 포트가 22번인데 너무 일반적이여서 bot공격의 대상이 되기 쉽다.  
>(그렇지.. 중국 형님들이 bot공격 어마무시하게 잘 하시지..)  
>그러하므로 22번 이외의 포트로 번호를 바꿔주는것이 좋다.  
>대채 포트번호는 /etc/services 에 있는놈들 이외의 놈으로 해주면 되는데  
>smtp라덩가 http등 유명한 놈들은 피해서 하는것이 좋다.  

ex)
```git
Port 1865
```  
  
  
- 별 4개짜리 ★★★★
- SSH로는 root권한 로그인이 불가능하게 설정
>sudo 라덩가 su 로 루트 권한이 되는것은 가능하나, 접속으로는 불가능하게 할것
>default 치가 yes로 되어있는데 이것을 no 로 바꿔준다.

ex)
```git
/etc/ssh/sshd_config
PermitRootLogin no
```

- 별 4개짜리 ★★★★
- 패스워드 입력식 인증방식일경우 사전공격(dictionary attack)의 대상이 되므로 가능하면 사용하지 않는것이 좋다

>대채 인증방식으로는 공개키 인증방식이 있다.
>공개키 방식으로 자신이 접속할 수 있도록 ~/.ssh/authorized_keys에 등록한후 끊지 않으면 접속이 닫히므로 주의가 요구된다
>ssh-keygen 커맨드로 비밀키를 작성후, 클라이언트의 ~/.ssh/config에 등록하면 편리하다
>공개키 등록은 ssh-copy-id커맨드를 사용하면 편하게 등록할 수 있다.

ex)  
```git
/etc/ssh/sshd_config
PasswordAuthentication no
ChallengeResponseAuthentication no
PermitEmptyPasswords no  #공백 입력일 경우의 로그인 불허가
```

- 별 3개짜리 ★★★
- SSH접속이 가능한 유저를 한정한다.

>AllowUsers로는 Whitelist방식으로 설정이 가능하고
>DenyUsers로는 Blacklist방식으로 설정이 가능하다
>예를들어 웹어플을 web_app라는 유저 권한으로 운영할때
>직접 web_app유저로 ssh접속할 필요는 없기 때문에 ssh불가능 하도록 설정한다

```git
/etc/ssh/sshd_config
AllowUsers hogeuser git
# DenyUsers web_app
```

- 별 2개짜리 ★★
- SSHD의 프로토콜을 2로 한다

>SSHD프로토콜 1의 경우에는 취약성이 발견되어서 서포터 안된다고 한다.
>요즘에는 보통 기본값이 2로 되어있다. (그대로 내비두면 될듯)
>오래된 리눅스버젼에서는 확인해볼 필요가 있다.

```git
/etc/ssh/sshd_config
Protocol 2
```

- 인증시의 시간이나 인증시도 횟수를 제한한다

>접속하고 인증할때까지의 유예시간(LoginGraceTime)과
>인증시도 횟수(MaxAuthTries) 를 설정해두자

```git
/etc/ssh/sshd_config
LoginGraceTime 30
MaxAuthTries 3
```

- sshguard, fail2ban 을 도입한다
>sshguard, fail2ban은 공격을 감지하여 일정시간 액세스 거부를 할수 있다
>ssh포트를 변경하지 않고 22번 포트 그대로 쓸때는 도입을 검토해볼 필요가 있다

---
---

■ firewall(iptables)편

firewall은 허가하지 않은 포트나 프로토콜을 액세스 거부하거나  
로그를 기록하거나 하는것이 가능하다.  
iptables만으로도 방대하므로 깊게 공부할 필요가 있을때는 따로 자료를 찾을것.  
man iptables 나 man iptables-extensitions 혹은  
마스터링 TCP/IP라는 불후의 명저가 있다.. ㅋㅋ  
(내 책장에 장식품 ㅋㅋ)

- 별 5개짜리 ★★★★★
- 사용하지 않는 포트를 닫는다.

>iptables를 사용한다면 /etc/iptables/iptables.rules(ipv4)
>/etc/iptables/ip6tables.rules(ipv6)설정파일이 있다
>데비안 계열이면 /etc/iptables/rules.v4 인경우도 있다
>밑의 경우는 iptables를 통해서 80번포트와 1234(ssh)포트를 열고있음

```git
/etc/iptables/iptables.rules
*filter
:INPUT DROP [0:0]
:FORWARD DROP [0:0]
:OUTPUT ACCEPT [0:0]
-A INPUT -p icmp -j ACCEPT 
-A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT 
-A INPUT -i lo -j ACCEPT 

# Allow HTTP connection(port:80)
-A INPUT -p tcp --dport 80 -j ACCEPT

# Allow SSH connection(port:1234)
-A INPUT -p tcp --dport 1234 -j ACCEPT

-A INPUT -p tcp -j REJECT --reject-with tcp-reset 
-A INPUT -p udp -j REJECT --reject-with icmp-port-unreachable 
-A INPUT -j REJECT --reject-with icmp-proto-unreachable 
COMMIT
```


.  
.  
.  
일단 오늘은 요까지.. 잠온다.. 담에 또 이어서 적자..


