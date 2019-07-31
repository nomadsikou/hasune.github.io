---
title: Linux 실행/처리 시간측정
category: Linux
comments: true
order: 7
---

가끔 쉘 실행시키고 얼마나 걸리는지 측정해봐야할 상황이 생긴다.  
- 타임테이블을 작성하고 그 계획대로 움직여야 할 때

이런 저런 자료를 찾다가, 실제로도 사용해보고 가장 괜찮았던것 2가지를 퍼왔다.

처리가 끝났을때의 시간 - 처리가 시작할때의 시간 = 걸리는 시간
(단위 세컨드)

timecheck.sh

```git
#!/bin/bash

start_time=`date +%s`

### 측정하고싶은 처리나 커맨드 기입 ###
sleep 10

end_time=`date +%s`

run_time=$((end_time - start_time))

echo $run_time
```

두번째 방법은 배쉬쉘 다루면서 처음본다.  
배쉬쉘에는 SECONDS라는 변수가 있으며 쉘을 기동할때부터 자동으로 카운트가 된다.  
그런데 이 변수를 임의 설정이 가능하다.  
쉘을 실행시키는 순간부터 0으로 리셋해놓고  
처리가 끝나는 지점에서 SECONDS를 출력

timecheck2.sh

```git
#!/bin/bash

# 초기화
SECONDS=0

### 측정하고싶은 처리나 커맨드 기입 ###
sleep 10

run_time=$SECONDS

echo $run_time
```

