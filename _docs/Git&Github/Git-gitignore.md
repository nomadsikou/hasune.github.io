---
title: Git에서 .gitignore의 필요성
category: Git&Github
comments: true
order: 7
---

.gitignore 라는 파일이  
깃으로 관리하는 폴더에 존재하는데  
말 그대로 깃으로 관리하는 목록중에서 무시(제외하는거나 마찬가지)하는 설정.  

대체로 이런놈들을 대상으로 해주면 좋음

- 자주자주 바뀌거나(필요없는 파일)
- 빌드를 통해서 생성된 파일(디플로이 할필요없거나, 대상이 아닌것들)
- 순수하게 관리 목록에서 제외하고 싶은 파일이나 폴더
- 더미 파일

macOS의 경우에는
- .DS_Store
- .AppleDouble
- .LSOverride

지킬 블로그를 깃헙에 커밋할 경우에는
- .sass-cache/
- .jekyll-metadata
- Gemfile.lock


그리하여....  
나의 지킬 블로그 루트디렉토리에는
```git
$cat .gitignore
_site/
.sass-cache/
.jekyll-metadata
Gemfile.lock

### macOS ###
*.DS_Store
.AppleDouble
.LSOverride

```
요렇게~~ 예쁘게 박아놓음










