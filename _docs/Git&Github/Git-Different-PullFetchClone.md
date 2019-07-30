---
title: Pull Fetch Clone Fork
category: Git&Github
comments: true
order: 4
---

Clone 과 pull과 fetch 도대체 뭐가 다름??

■ clone
```git
git clone url
```
이런식으로 클론 하는데  
클론일 경우에는   
- git init
- git remote add origin url  


등을 생략해도 된다.  
즉, 그냥 폴더 들어가서 클론하면 잡다한거 안치고 바로 리모트에서 카피뜬다 


■ fetch 단순히 업데이트  
pull 은  fetch + merge 이다.  
그래서 머지 해버리기때문에 pull은 젤 처음 빼고는 될수 있음 쓰지 않는게 좋다고.. 한다?

■ ️️fork  
누군가의 리모트 리포지토리를 나의 리모트 리포지토리로 pull함.
fork를 하면 누가 포크해갔는지 원작자에게 뜬다고함.  

(나도 뭔가 하나 잘 맹글어서 누군가가 퍼가고 싶은 리포지토리 맹글어보자.. 언젠가는.. ㅋㅋ)  

누군가의 리포지토리를 복사떠서 작업하고 싶으면  
순서가, fork -> (내 리모트 리포지토리에 복사되면) -> clone   
이런 순으로 작업하면 된다.



