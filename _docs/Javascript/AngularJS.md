---
title: AngularJS 설치와 사용
category: Javascript
comments: true
order: 1
---

플젝에서 갑자기 백단/프론트단 다 손봐야하는 안건을 맡게됐는데,  
오랜만에 JSP, Ajax, Javascript를 다 다뤄야 하는상황이라 빡씨게 공부해야..  
근데 JS쪽은 담당 기능중 하나가 AngularJS로 구현된 페이지라 개념좀 잡아야함  

- HTML템플릿 기능을 갖고있다
- 쌍방 데이터 바인딩이 가능하다
- DI의존주입에 의해 모듈관리 기능이 있다
- 루팅 기능이 있다.
- Ajax통신 기능이 있다  

■ HTML템플릿  
- 중괄호 2개짜리(익스프레션 구문)를 써서 로직을 기술하는것이 가능(예제 생략)

■ 쌍방 데이터 바인딩  
- 모델과 인풋필드를 바인딩 함으로써 자바스크립트에 의한 모델변경과 유저입력에 의한 필드변경이 쌍방향으로 가능함

```html
<input type="text" ng-model="message">
<div>{{message}}</div>
```
■ DI의존주입
- 가장 간단한 패턴  

```html
<div ng-app>
  <div ng-controller="HogeCtrl">（생략）</div>
</div>
```

```js
function HogeCtrl($scope) {
  //생략
}
```

- 조금 복잡한 형태  
- 모듈을 작성하고  그것에 .controller 메소드 형식  

```html
<div ng-app="myApp">
  <div ng-controller="HogeCtrl">（생략）</div>
</div>
```

```js
var myApp = angular.module('myApp', []);
myApp.controller('HogeCtrl', ['$scope', function($scope) {
  //생략
}]);
```

- $inject Annotation패턴  

```html
<div ng-app>
  <div ng-controller="HogeCtrl">（생략）</div>
</div>
```

```js
function HogeCtrl($scope) {
  //생략
}
HogeCtrl.$inject = ['$scope'];
```

■ 루팅

■ Ajax사용


■ AngularJS 의 사용  
html태그나 body태그 혹은 div태그 물려서 많이 사용
```html
<html ng-app="example" >
<!-- 혹은 -->
<body ng-app="example" >
<!-- 혹은 -->
<div ng-app>
  <div ng-controller="HogeCtrl">（略）</div>
</div>
```