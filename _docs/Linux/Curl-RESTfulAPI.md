---
title: Curl 과 Restful API
category: Linux
comments: true
order: 4
---

JSON형식으로 리퀘스트를 보내며,  
Restful API로 설계된 웹어플의 스트레스 테스트를 하게되었다.

보통 테스트를 위해서 툴을 많이들 쓰는데  
한번의 리퀘스트에 대해서 어떤 리스폰스가 오는가 를 보기 위해선 좋지만,  
동시다발적으로 몇십건의 리퀘스트 요청을 보내야 하며,   
그 리퀘스트에 대한 리스폰스가 각각 몇초 걸리는지 시간을 측정해야 할경우  
GUI환경에서 하기가 어렵다.  
그리하여.. linux환경에서 &를 활용해서   
복수의 처리가 백그라운에서 돌아가게 하는식으로 테스트를 하게되었고..  
서비스의 허용범위와 한계치 까지 테스트 해야하는상황.
- 1만건의 JSON데이터 전송,  1만건의 JSON데이터, 복수 전송
- 10만건의 JSON데이터 전송, 10만건의 JSON데이터 복수전송
- 50만건의 JSON데이터 전송, 50만건의 JSON데이터 복수전송

이런것들을 테스트 해봐야할 사람이라면 참고가 되었으면 한다.
.  
.  
.  



이것저것 주워담은 지식들을 정리  

JSON형식의 POST일경우 가장 기본형

```git
curl -X POST -H "Content-Type: application/json" -d '{"Name":"superman", "Age":"100"}' http://localhost/member
```

- -X : 메서드설정
- -H : 헤더를 보낸다
- -d : 데이터를 전달한다(JSON데이터를 미니파이 하여 한줄짜리로 변경해서 복붙)

JSON형식의 데이터가 저장되어있는 JSON_data.txt를 읽어드려서 리퀘스트 요청  
(JSON_data.txt에 대량 JSON데이터를 담아서 보낼때 좋다)

```git
curl -X POST -H "Content-Type: application/json" -d @JSON_data.txt http://localhost/member
```
위와 같은 요청을 복수로 보낼때에는 &로 계속 이어붙혀도됨
```git
curl -X POST -H "Content-Type: application/json" -d @JSON_data1.txt http://localhost/member & curl -X POST -H "Content-Type: application/json" -d @JSON_data2.txt http://localhost/
```


curl에서 -w 옵션으로 포맷을 설정할수 있다.  
포맷앞에 @를 붙이면 포맷을 지정한 파일을 설정할 수 있다.

```git
$ curl -w "total %{time_toal}\n" http://localhost  #기본적인사용 

$ curl -w @format.txt http://localhost #포맷 지정을 따로 파일로 뺐을경우
```

포맷의 내용은 여러가지 지정 할 수 있는데, 더 자세한것은 man curl 을 참조  
밑의 내용은 cat format.txt 했을때의 내용이다.

```git
http_code           %{http_code}\n
size_upload         %{size_upload}\n
speed_upload        %{speed_upload}\n
size_download       %{size_download}\n
speed_download      %{speed_download}\n
time_pretransfer    %{time_pretransfer}\n
time_starttransfer  %{time_starttransfer}\n
time_total          %{time_total}\n
```

위의 format.txt 를 읽어드려서 리퀘스트 요청한 결과값은 이런식으로 뜬다

```git
http_code           200
size_upload         0
speed_upload        0.000
size_download       3
speed_download      1.000
time_pretransfer    0.002
time_starttransfer  2.166
time_total          2.167
```
http_code 200 이니  ok란 뜻이겠고 400이면 bad request 404면 not found로 생각하면됨  

위의 결과를 리다이렉트 써서 
```git
curl -w "total %{time_toal}\n" http://localhost > response.txt 
```
이런식으로 따로 빼도 되고  

만약 리스폰스 값을 날려버리고 싶으면 -o 옵션에 /dev/null을 줘서 쓰면 된다.  
무거운 처리일경우 상태정보 표시가 나오는데 이것을 보고싶지 않으면 -s 를 붙힌다
- -o : 아웃풋 설정
- -s : 프로그레스나 에러 정보를 보여주지 않는다

```git
curl -s -o /dev/null -w "total %{time_toal}\n" http://localhost > response.txt 
```



아직 해본적은 없지만 유용할것 같은거라 추가 메모  

> http://localhost/helloworld로 요청보내고 응답쿠키를 cookie.txt에 저장

```git
$ curl -c cookie.txt http://localhost/helloworld
```

> http://localhost/hellocurl로 저장한 쿠키를 헤더에 추가해서 리퀘스트 보낸다

```git
$ curl -b cookie.txt http://page2.example.com
```





