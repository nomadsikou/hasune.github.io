---
title: 혼방 데이터 삭제하고 상황 회피
category: Accident&Trouble
comments: true
order: 1
---

조기조치가 가능한 일이었지만, 사고 후 회피와 방치로 인해서  
너무나 심각한 상황까지 가게되었고 감당이 안되는 상황까지 일이 번져버린 사건  
(개인적으로는 주작이 의심되지만, 주작치고는 조금 디테일함)  

우선 첫날..  


![Delete](./honbang-delete.png)

---

이렇게 시간이 흐르고 다음날이 되었는데  
.  
.  
.  
아직까지 문제의 심각성을 파악못하고 있음..

![Delete](./honbang-delete.png)

---

- 민/형사 상의 고소를 당할수도 있게 되어버리고
- 소속회사의 손배소 문제와, 심할경후 파산까지도 고려해야되는 상황이 됨

![Delete](./honbang-delete-finally.png)

---

보통 배치처리가 이런식으로 거미줄처럼 서로 연결되어있고　　
![Job-net](./job-net.png)

특정 처리의 결과에 따라서 nest하거나 할때  
하나의 처리가 단순하게 오류로 멈추는것은 괜찮지만,  
잘못된 데이터를 처리하여 넘기게 되면, 다음 다음처리들이 말도 안되게 꼬임.

아마 그런 상황이 아니었을까???

ABX0090 ...  OK  
ABD0010 ...  OK  
TTD0190 ...  OK(ABEND이면 차라리 괜찮음)  
TTD0191 ...  OK(ABEND이면 차라리 괜찮음)  
TTD0192 ...  OK(ABEND이면 차라리 괜찮음)  

>[링크 : JP1에서의 JobNet와 Nest에 관해](http://itdoc.hitachi.co.jp/manuals/3020/30203S0133/AJSZ0006.HTM)  

- Nest job-net : 루트 잡넷의 하위 잡넷으로 정의 되어있는것을 뜻함
- Abend : 이상 종료를 뜻함

