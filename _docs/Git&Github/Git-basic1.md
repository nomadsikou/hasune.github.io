---
title: 기본중의 기본
category: Git&Github
order: 1
---

리포지토리를 만들기 이전에 알아야 할 것.  
- private : 비공개 프로젝트
- public  : 공개 프로젝트(업로드는 제한 할 수 있다)

Github 사용법

■ Gitbash 설치  
>[윈도우용 깃 : https://gitforwindows.org/](https://gitforwindows.org/)  

다운로드 버튼을 누르면 자동으로 다운로드가 진행되고 그 파일을 설치한다  

■ new repsitory 생성  
>github사이트에서 로그인후에 새프로젝트 생성

생성하면 깃의 주소가 나옴. 이 화면에서 일단 멈춰둔다.

■ 로컬환경과 Github를 연결  
자신의 로컬 컴퓨터의 임의의 디렉토리와 웹상의 Github를 연결해주는 과정

임의로 폴더를 만든후 오른쪽 클릭후 git bash here를 선택.  
커맨드 프롬프트가 나온다.

거기서 git init 을 친다.
```git
git init
```

치고난 후 윈도우 상태에서 해당 폴더를 살펴보면.git 이라는 폴더가 생성되어있다.

다음은 리모트 컨트롤할 대상 리포지토리를 추가해준다
```git
git remote add origin (repository address)
```
ex)  
```git
git remote add origin https://github.com/abcdef/abcdef.git
git remote add origin https://github.com/babo/babo-web
```
*아무런 말이 뜨지 않으면 정상적으로 된것임*


>여기서 포인트.  

origin은 리모트 컨트롤 할때 그 대상을 가리키는것 이며 기본지정명 이다.  
즉, 리포지토리 default name이라고 이해하면됨.  
오리진 마스터 라고도 하는데. 마스터는 무엇인가?  
물리적 저장소를 뜻한다. 흔히 DB에서 회원정보 테이블, 회원상세 테이블 이라는 테이블이 있다고 할때, 회원정보 마스터, 회원상세 마스터 라고도 부르는데, 바로 그때의 마스터와 같은 의미라고 보면된다. (Master : 물리적 저장공간을 뜻함)  

*그러므로, origin master 라는것은 git에서 리포지토리명으로 기본설정된 origin이라는 물리적 저장소(master)를 뜻한다.* 


■ push 전엔 pull이 있다
pull전에 push를 하면 모든것을 날려먹는 불운의 결과를 초례하므로
항상 pull후에 push를 하는것을 기억하라

- pull : 깃허브 레포지토리에서 로컬 레포지토리로 땡겨오는것
- push : 깃허브 레포지토리로 올리는것(최종적으로 올리는작업)

아까 지정한 폴더로 레포지토리의 모든것을 한번에 끌어오는 커맨드  
```git
git pull origin master
```

현재 나의 로컬 폴더와 깃과의 상태를 체크해줌  
```git
git status
```

로컬 리포지토리에서 커밋 인덱스에 추가(커밋할 대상을 추가) 밑의 경우는 전부(하위디렉토리와 그안의 파일들까지)추가 할때의 명령어
```git
git add .
```
특정 파일만을 커밋 인덱스에 추가할때에는
```git
git add hello.txt           # hello.txt라는 파일 하나만 추가함
git add hello.txt world.txt # hello.txt 와 world.txt 두개의 파일을 추가함
```

대화상자를 열어서 선택하는 방법도 있다
```git
git add -i # 번호선택 식으로 진행하면되고, 선택된 파일이나 디렉토리는 *(아스타리스크가 붙음)
```

■ 커밋을 하자!  
```git
git commit -m "message" # 변경 내용을 message에 써주면 된다
```

■ 리모트 리포지토리로 올리는것(push)  
로컬리포지토리에서 커밋한 후에, 실질적으로 리모트 리포지토리에 올리는 작업이 push 이다.  
```git
git push origin master
```
이렇게 치면 id와 패스워드를 묻는 창이 뜨고  입력하면 푸쉬가 완료 된다.  

***
포인트 정리.  
pull을 할때는 다음과 같은명령어(한개)
- git pull origin master


push를 할때는 다음과 같은 명령어가 기본적으로 사용됨(4개)  
- git status
- git add .
- git commit -m "message"
- git push origin +master  

***
처음일 경우 이렇게 뜨는데 이럴때는 이메일과 네임 설정을 해줘야한다  
```git
******************************************************************
*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.
********************************************************************
```
이런식으로 쳐주면 됨

```git
git config --global user.email "abcdefg@naver.com"
git config --global user.name "abcdef"  
```

치고난후 컨피그 확인하는 명령어
```git
git config --list
```









