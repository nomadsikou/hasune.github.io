---
title: lombok 라이브러리
category: Java
comments: true
order: 4
---

새로 투입된 플젝에서  
참 재미있는 친구를 쓰고 있길래 자료를 좀 찾아봤다.

lombok.jar 읽으면 롬복??  
어노테이션을 쓰는것만으로 getter, setter, toString, equals 등을 컴파일할때 자동생성  

공식 다운로드 페이지
>[https://projectlombok.org/download](https://projectlombok.org/download)

설치법  
다운로드 받은 lombok.jar을 현재 프로젝트의 라이브러리 폴더로 이동  
- lombok.jar를 더블클릭 하거나
- lombok.jar 이 있는곳으로 cmd로 이동하여 java -jar lombok.jar 를 친다.

![lombok-install](./lombok-install-cmd.png)

실행하면 밑에처럼 화면이 뜨고  
Specify location을 눌러서 현재 실행중인 이클립스의 실행파일을 선택  
Install / Update를 눌러서 설치해준다

![lombok-install-screen](./lombok-install.png)

■ lombok에서의 Getter / Setter　　

```java
// Book.java
public class Book {

    private String bookName;
    private String author;
    private Integer price;
}
```

일반적인 겟터 셋터의 경우  
이런식으로 코드를 작성한 후  
오른쪽 클릭 -> 소스 -> 겟터 및 셋터 생성 -> 원하는것 선택  
이런식으로 진행하는데  
그렇게 하면 Book.java라는 소스는 이렇게 된다.


```java
// Book.java
public class Book {

    private String bookName;
    private String author;
    private Integer price;
    public String getBookName() {
        return bookName;
    }
    public void setBookName(String bookName) {
        this.bookName = bookName;
    }
    public String getAuthor() {
        return author;
    }
    public void setAuthor(String author) {
        this.author = author;
    }
    public Integer getPrice() {
        return price;
    }
    public void setPrice(Integer price) {
        this.price = price;
    }
}
```

lombok을 사용할 경우

```java
// Book.java
@Getter
@Setter
public class Book {

    private String bookName;
    private String author;
    private Integer price;
}
```
Book.java 에 어노데이션을 써주는것 만으로  
컴파일된 Book.class가 겟터, 셋터가 생성되어져서 컴파일된다.  
(코드가 간결해지고, 그동안 귀찮았던 작업을 안해도 된다.)

```java
// Book.class
public class Book {

    private String bookName;
    private String author;
    private Integer price;

    public String getBookName() {
        return bookName;
    }
    
    public void setBookName(String bookName) {
        this.bookName = bookName;
    }
	
    public String getAuthor() {
        return author;
    }
    
    public void setAuthor(String author) {
        this.author = author;
    }
    
    public Integer getPrice() {
        return price;
    }
    
    public void setPrice(Integer price) {
        this.price = price;
    }
}
```

위와 같은 예로 몇가지 더 살펴보자.

■ lombok에서의 ToString  

@ToString : toString()을 오버라이드하여 재정의  
(exclude = "price") : price라는 필드를 제외한다

```java
// Book.java
@ToString(exclude = "price")
public class Book {

    private String bookName;
    private String author;
    private Integer price;
}
```

컴파일 할때 밑과같이 자동으로 해준다
```java
// Book.class
public class Book {

    private String bookName;
    private String author;
    private Integer price;
	
    @Override
    public String toString() {
        return "Book [bookName=" + bookName + ", author=" + author + "]";
    }
}

```

■ lombok에서의 Constructor

- @NoArgsConstructor 기본 생성자를 자동생성

```java
// Book.java
@NoArgsConstructor
public class Book {

    private String bookName;
    private String author;
    private Integer price;
}

```
컴파일 할때 밑과 같이 자동으로 해준다.

```java
// Book.class
public class Book {

    private String bookName;
    private String author;
    private Integer price;

    public Book() {
    };
}

```

- @AllArgsConstructor 모든 필드에 대해서 인수값을 초기화값으로 하는 생성자를 자동생성

```java
// Book.java
@AllArgsConstructor
public class Book {

    private String bookName;
    private String author;
    private Integer price;
}

```
컴파일 할때 밑과 같이 자동으로 해준다.

```java
// Book.class
public class Book {

    private String bookName;
    private String author;
    private Integer price;

    public Book(String bookName, String author, Integer price) {
		this.bookName = bookName;
		this.author = author;
		this.price = price;
    }
}
```

- @NoArgsConstructor 와 @AllArgsConstructor 를 조합할 경우

```java
// Book.java
@NoArgsConstructor
@AllArgsConstructor
public class Book {

    private String bookName;
    private String author;
    private Integer price;
}

```

컴파일 할때 밑과 같이 자동으로 해준다.

```java
// Book.class
public class Book {

    private String bookName;
    private String author;
    private Integer price;

    public Book() {
    };

    public Book(String bookName, String author, Integer price) {
		this.bookName = bookName;
		this.author = author;
		this.price = price;
    }
}
```

- @RequiredArgsConstructor 파이널 필드에 대해서만 인수값을 초기화값으로 하는 생성자를 자동생성

```java
// Book.java
@RequiredArgsConstructor
public class Book {

    private final String bookName;
    private final String author;
    private Integer price;
}

```

컴파일 할때 밑과 같이 자동으로 해준다.

```java
// Book.class
public class Book {

    private final String bookName;
    private final String author;
    private Integer price;

    public Book() {
    };

    public Book(String bookName, String author) {
        this.bookName = bookName;
        this.author = author;
    }
}
```

오늘은 여기까지..  

이퀄스와 해쉬코드는 다음에~

