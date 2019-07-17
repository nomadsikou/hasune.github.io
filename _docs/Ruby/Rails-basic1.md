---
title: Rails 기초
category: Ruby
comments: true
order: 1
---

루비에서 많이 쓰이는 RubyGems
- devise    :  유저등록이나 로그인 인증
- omniauth  :  Oauth기능
- kaminari  :  일람화면 페이징 기능


프로젝트 생성
```git
rails new projectname
```

로컬서버 기동  
```git
rails s
```
- 루비의 로컬서버 기동은 puma라는 놈이 한다.  
- 자바의 tomcat 같은놈이라고 보면됨
  
home이라는 컨트롤러 생성  
- generate라고 다 안쓰고 g 라고 써도 된다.
```git
rails generate controller home
rails g controller home
```
이건 어디 만들어지냐면  
app폴더의 컨트롤러스에. 이름_컨트롤러.rb 로 만들어진다  
컨트롤러 클래스 안에있는 메서드는 액션이라고 부른다

```rb
class HomeController < ApplicationController
    def index
    end

    def hi
        @show_message = true
        @message = "run away"
    end

    def result
        @plus_result = params[:num1].to_i + params[:num2].to_i
    end

end
```

이런식으로 작성했다고 하자  
hi라는 메서드는 액션 메서드라 부른다  

이제 액션 메서드에 상응하는 뷰를 만들어줘야한다  

views폴더를 보면.   
아까 컨트롤러 생성할때 home이라는 네임으로 컨트롤러를 생성했으므로  
view의 하위에 home폴더가 있다.  
거기서 오른쪽 클릭해서 뉴파일 해서 home폴더안에 뷰를 만들어줘야한다
index.erb라고 만들어준다

컨트롤러의 액션(메소드)명과 뷰의 파일명이 같으면 자동으로 매핑해준다  
view는 화면단 내용을 작성하면 된다

그다음 마지막으로 routes.rb를 작성한다

```rb
root ‘home#index’
```
루트 home컨트롤러 안에 있는 index라는 액션과 연결해 주세요 라는 내용임

컨트롤러에서 view쪽으로 값을 전달하는 방법!!  
컨트롤러의 액션 내부에 작성한다  
```rb
@message = “run away”
```

이제 뷰에서
```rb
<p> <% %> </p>
```
이런식으로 작성  
```rb
<% 요안은 루비코드 작성 가능함 %>
```
참고로 erb 는 임베디드 루비 의 약자로써 erb안에는 루비코드도 적을수 있다

---

위에까지는 컨트롤러안의 액션(매서드) 안에 변수를 뷰로 보내는것이였고

이번에는  
Form 태그로 request 메세지에 담아서 보낸다  
params로 읽는다  
url로 request메세지에 담아서 보낸다 

를 배워보자

Form 태그는  아이디 비번 입력이라덩가 아니면 검색창이라덩가
html의 폼태그를 말하고 그것에 들어간 데이터를 받아서 어떻게 할것인가임  
```html
<form method=“post” action=“/login”>
	<input type=“text” name=“id”>
	<input type=“password” name=“pw”>
	<input type=“checkbox” name=“remember”>
	<input type =“submit”>
</form>
```
submit은 제출버튼임

폼태그는 정보를 묶어서 보내는 태그.  폼과 input으로 이루어져있다

Form -> method : 어떤방식으로 정보를 전달할건지 (get or post)  
Action : 어디로 정보를 전달할건지 (url)  
Input(정보를받는태그) -> type : 어떤 종류의 정보를 받을건지   
Name : 정보의 이름

위의 코드는  
이런식으로 보여지는데  
폼 안에 
아이디, 패스워드, 체크박스라는 인풋 테그들이 있다
————————————————  
Id :   
Password :    
submit  
————————————————

중요  
겟방식은 주소창에 요청내용이 모두 노출됨. 보안성이 취약함  
예를들어 네이버 검색창에서 검색하면 위에 주소에 검색어가 뜸  
보여주면 안되는정보를 요청할경우에는 포스트를 써야한다
```rb
params[:id] #=> “xxxxx”  
params[:pw] #=> “xxxxx”  
params[:remember] #=> true  
```
레일스에서는 이런식으로 값을 받게된다  
input의 name에 적었던것으로 식별한다

---
실습

계산기 만들기  
엑스 + 와이 = 제출  
결과 페이지
1. 컨트롤러 생성
2. 액션 작성
3. 루트 알비 작성
4. 뷰 작성

모델 생성하는법
```rb   
rails generate model post 
```

모델이 만들어진 후에는

config/migrate 폴더의 migration파일을 수정해준다  
```rb
rake db:migrate
```
를 쳐서 컴터가 마이그래이션 파일을 읽어서
테이블을 만들어준다








