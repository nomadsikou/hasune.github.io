---
title: Github에 Push가 거부될때
category: Git&Github
comments: true
order: 6
---

깃허브를 이용해 복수의 블로그를 만들다보니  
한 컴퓨터에서 여러 깃허브 유저에 푸쉬작업을 해야할 상황이 생겼다.  

```git
git config --global user.email "change user.email"
git config --global user.name "change user.name"
```

이런식으로 바꾸고 푸쉬하니 
```git
error: The requested URL returned error: 403 Forbidden while accessing https://github.com/aaaa/aaa.git
```
이런식으로 뜨길래  

구글을 뒤적거려서 
밑에와 같이도 해봤다.
```git
git remote set-url origin https://aaa@github.com/aaa/aaa.git
```
그런데 이렇게 뜨더라  -_-;;;

```git
$ git push origin master
remote: Permission to aaa/aaa.git denied to helloworld.
fatal: unable to access 'https://github.com/aaa/aaa.git/': The requested URL returned error: 403
```

그 래 서 !!
ssh방식으로 하는 것도 있어서 시도해봤다!
 - ssh키젠 쳐서 엔터 몇번 치고
 - 그다음에 cat ~/.ssh/id_rsa.pub 쳐서 나온내용 복사후에
 - 깃헙 페이지 오른쪽 젤위에 settings 들어가서
 - SSH and GPG keys 누르고 New SSH key눌러서 붙혀넣기!!!  
 (ssh방식 인증으로 하실분은 이렇게 하는 방법도 있습니다.)

```git
$ssh-keygen
.
.
.
.
생략
.
.
$cat ~/.ssh/id_rsa.pub
ssh-rsa abcderfadfasdfsdafasdfdfdasfdsfasdfasdfadsf .......
```

그러나 역시...
```git
$ git push origin master
remote: Permission to aaa/aaa.git denied to helloworld.
fatal: unable to access 'https://github.com/aaa/aaa.git/': The requested URL returned error: 403
```

이런 개나리 십장생 !!!! ㅂㅈ데갲ㄷ베ㅐㅕㅁㅇ니ㅏ륌너럊데ㅐㅕ걎뎍   

여러가지 해결 방법 중에서 무시하고 넘어간 딱 하나의 방법이 있었는데  
>Windows 자격 증명 관리

요놈에서 git관련을 삭제 해주는 것이였다.

블로그들 보면 아주 간단하게 나와있는데......   
문제는 윈도우10에서 이 메뉴가 어딨냐고;;;  
(자주 쓰는 메뉴가 아니면 어버버 한답니다)

두번다시 이와같은 상황이 발생했을때 어버버 하지 않을 각오로..  
예쁘게 포스팅 합니다.  
(나와같이 별거 아니지만 개고생 하는 다른 개발자들을 위해서도.. ㅋㅋ)  

■ 윈도우키 + E    를 누르세요 

![Gitbash-push-denied](./solution-denied1.png)

■ 이렇게 탐색기가 뜰겁니다.  
거기서 내PC 에서 오른쪽 클릭하시고   
속성을 누르세요  

![Gitbash-push-denied](./solution-denied2.png)

■ 그럼 이렇게 화면이 나오는데  
거기서 왼쪽 젤 위에 제어판 홈  을 누르세요

![Gitbash-push-denied](./solution-denied3.png)

■ 그럼 이렇게 화면이 나오는데  
거기서 오른쪽 위쪽 메뉴  사용자 계정을 누르세요

![Gitbash-push-denied](./solution-denied4.png)

■ 그럼 이렇게 화면이 나오는데  
거기서 오른쪽 두번째 메뉴로 있는 Windows 자격 증명 관리 를 누르세요

![Gitbash-push-denied](./solution-denied5.png)

■ 그럼 이렇게 화면이 나오는데  
거기서 git어쩌구 써있는놈을 지우면 됩니다. 

■ 지우고 난 후에  
```git
git push origin master 
```
일케치면  
로그인 유저 아이디와 패스워드 물어보는데  
push 대상의 유저 아이디와 패스워드 입력하면 됩니다.

만세!!!!!












