---
title: alias설정
category: Linux
comments: true
order: 6
---

유저 혹은 홈 디렉토리에 .bashrc에 alias를 기재한다.  
같은 디렉토리에 .bash_profile이 있는데  
이놈이 터미널 처음 킬때 해당 유저의 설정을 읽어드리는데  
이놈의 제일 마지막줄에 source ~/.bashrc 이렇게 써놓으면  
.bashrc에 기재되어있는 내용을 불러와서 설정해줌.  

gitbash 같은경우는 .bashrc나 .bash_profile 파일이 없을 경우가 있으니  
그럴때 touch 로 만들고 적당히 수정해줄것

```git
$cat ~/.bashrc

# Linux Command
alias ll='ls -l'
alias la='ls -a'
alias lrt='ls -lrt'
alias tf='tail -f'
alias dir='ls'
alias cls='clear'

# Ruby
alias bejs='bundle exec jekyll serve' 
alias bejc='bundle exec jekyll clean' 
alias js='jekyll serve' 
alias jsnet='jekyll serve --h 0.0.0.0' 
```


