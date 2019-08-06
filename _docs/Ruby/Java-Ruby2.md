---
title: 자바와 루비 차이점 두번째
category: Ruby
comments: true
order: 4
---

>따로 마련한 이유는 코드로 조금 자세히 볼필요가 있어서!  
>일단 자바코드에 대한 이해를 좀 한다음에..

## == 과 equals()

[참고사이트](https://jeong-pro.tistory.com/172)

자바에서의 == 는  
primitive type(int, double, boolean, ...)일 때는 값이 같은지 비교하고,  
객체, reference type일 때는 가리키는 주소가 같은지를 검사.

코드로 보자
```java
package codeplay;

public class WhatIsEquals {

	public static void main(String[] args) {

		String str1 = "hello";
		String str2 = "hello";
		System.out.println(str1 == str2);//true
		String str3 = new String("hello");
		String str4 = new String("hello");
		String str5 = str4;
		System.out.println(str3 == str4);//false
		System.out.println(str4 == str5);//true
	}
}
```
실제로 실행시키면 이렇게 나왔다
```git
true
false
true
```
>str1이 가리키는 주소("hello"의 주소)와   
>str2가 가리키는 주소("hello"의 주소)가 같기 때문에 true  
>str3과 str4는 생성자를 이용해서 생성한 객체로   
>각각의 메모리에 "hello"라는 String을 만든 것과 같다.주소가 달라 false

위의 코드는 자바 처음 배울때 한번씩 본적 있을것이다.  
나는 여기서 primitive type일때는 어떻게 될지 궁금했다

```java
package codeplay;

public class WhatIsEquals {

	public static void main(String[] args) {

		int int1 = 25;
		int int2 = 25;
		System.out.println(int1 == int2);//true
		int int3 = new Integer(13);
		int int4 = new Integer(13);
		int int5 = int4;
		System.out.println(int3 == int4);//true
		System.out.println(int4 == int5);//true
	}
}
```
```git
true
true
true
```
허허.. 이건 또 몰랐었네   
근데 위에 소스코드에서 int가 아닌 Integer를 쓰게되면  
true  
false  
true  
가 나온다.  
이것도 int는 프리미티브 타입이고 Integer은 정수형 객체라는 뜻이 된다.  
(Integer는 뤱퍼 클래스라고 많이들 부름)

각설하고,
- == 는.  즉 리퍼런스 타입(객체) 일때만 주소가 같은지 검사한다.

---
이번엔 equals() 메서드 : 이놈은 객체의 내용이 같은지 검사해줌


이건뭐... 워낙 많이 쓰이고 딱히 어려울게 없으니 설명은 패스~  

```java
package codeplay;

public class WhatIsEquals {

	public static void main(String[] args) {

		String str1 = "hello";
		String str2 = "hello";
		System.out.println(str1.equals(str2));//true
		String str3 = new String("hello");
		String str4 = new String("hello");
		System.out.println(str3.equals(str4));//true
	}
}
```

---

## 이제 루비다

```ruby
str1 = "hello"
str2 = "hello"
puts str1 == str2
puts str1.equal?(str2)
```
```git
true
false
```
오잉???   
그러하다.. 자바의 정 반대이다

- 루비에서의 ==       는 자바의 equals()랑 같은 의미
- 루비에서의 equal?() 는 자바의 ==

>간단하게 외우려면, 자바랑 루비의 ==과 equals()는 반대이고  
>루비에서는 equals()가 아닌 equal?() 라고 씀

나의 개인적인 생각인데,  
자바도 루비도 아무것도 모르는 상태에서 어떤것이 더 이해하기 쉬운가?  
라는 물음에, 나는 루비가 더 이해하기 쉽다고 본다.  
str1.equal?(str2)  <-- str1이랑 str2랑 주소값도 같음??   이게 더 이해하기 쉽다.

