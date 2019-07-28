---
title: Git에서 Branch관리
category: Git&Github
comments: true
order: 2
---

깃과 깃허브를 사용하면서,   

실제로 제대로 사용하기 위한 첫 단계가   

Branch작업을 능숙하게 쓰는것임.  

필연적으로 master가 나오고 origin/master가 나오게되며,  

각 마스터에서 브런치를 따고 병합하는 일련의 과정속에서 컨플릭트가 
발생하고  

그것을 해결하는것이 핵심.   

일단 컨플릭트는 다음에 다루기로 하고  

이번에는 브런치와 마지만 다루어 보자.  
>들어가기에 앞서,  
어떤 프로젝트를 진행할때  
- 코딩이면 코딩 
- 디자인이면 디자인
- 트러블슈팅이면 트러블슈팅  

이런식으로 애시당초 처음부터(pull이나,클론 혹은 fetch후)  
나누어서 브랜치를 따놓고 작업하면, 나중에 정말 편하다.



■ 브런치 작성
```git
git branch branch-name
```

■ 브런치 리스트를 보여준다
```git
git branch
```
■ Remote쪽 브런치 리스트를 보여준다
```git
git branch -r
```
■ Remote쪽과 로컬쪽의 브런치 리스트를 다 보여준다
```git
git branch -a
```

■ 브런치를 작성함과 동시에 그 브런치로 변환
```git
git checkout -b branch-name
```

■ 브런치로 변환
```git
git checkout branch-name
```

■ 브런치 삭제
```git
git branch -d branch-name
```

■ 브런치 삭제(마지 상태와 상관없이 지워버림)
```git
git branch -D branch-name
```

---
■ 머지

머지를 하기전에는 각 브랜치들에서  
git status를 눌러보고 혹시 빠진것이 있는지 꼼꼼히 살펴본후 진행할 것

```git
git checkout master # master브런치로 이동후(대빵브런치로이동)
git merge src       # src라는 브랜치를 master쪽에 합침
git merge design    # design이라는 브랜치를 master쪽에 합침
git merge prototype # prototype라는 브랜치를 master쪽에 합침
```

---

마지막으로..  
머지 작업이 제대로 잘 끝나고난 후  
더이상 사용하지 않는 브랜치는 바로바로 삭제를~
```git
git branch 
*master
UsedBranch   <-- 머지 끝나고 더이상 안쓰는놈이라고 할때

git branch -d UsedBranch
```