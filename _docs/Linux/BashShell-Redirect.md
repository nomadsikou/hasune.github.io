---
title: BashShell 리다이렉트 정리
category: Linux
comments: true
order: 3
---

■ 제일 많이 쓰이는 가장 기본형 

```git
sh process-timecheck.sh > timecheck-result.txt
```
process-timecheck.sh 쉘을 실행시켜서 그 결과값을 timecheck-result.txt에 담아라

■ 조금 다른놈

```git
sh process-timecheck2.sh >> timecheck-result.txt
```
process-timecheck2.sh 쉘을 실행시켜 그 결과값을 timecheck-result.txt마지막 줄에 추가 시켜라  

좀더 쉽게 이해하기 위해서 배쉬쉘을 두개를 켜고  

```git
touch test.txt
tail -f test.txt 
```
이런식으로 쳐놓고,  
다른 배쉬 쉘에서
```git
echo abc >> test.txt
```
이런식으로 치면 위에 tail -f 한놈에 한줄씩 추가되는것이 눈에 보임!  

■ 배치 처리나 백단에서 종종 보이는놈

```git
sh executor.sh > /dev/null 2>&1
```
표준 출력이든 표준 에러든 어떤 로그도 담지않는다.

■ 배치처리에서 DB 연동해서 조금 길고 복잡한처리에서 자주 나오는놈  
일단 개념을 위해서 가장 기본형은
```git
cat > sample.txt << EOF
>hello
>world
>EOF
```
- EOF라는 문자열을 만날때까지 처리가 계속 된다.
- 입력값을 EOF만날때까지 계속 sample.txt에 담는다.

이것의 응용판은 밑에와 같은 스타일로 많이 썼던것 같다.  

```git
sqlplus -s $ORACLE_CONNECTION << EOF

INSERT INTO USERS(
    ID
  , NAME
)
SELECT A.ID
     , A.NAME
  FROM USERS2 A
 WHERE NOT EXISTS (
           SELECT * FROM USERS B WHERE A.ID = B.ID
       )
;

COMMIT;

EXIT;

EOF
```
- 현장에서는 컬럼이 50개? CASE형님과 JOIN형님도 함께 등장해서 조금 빡쌨다는..  
- 마지막에 롤백도 있었던걸로 기억이.. 
- 오라클이면 declare 나오고 변수선언을 =: 이런식으로 하고  begin end 로 했었다능~









