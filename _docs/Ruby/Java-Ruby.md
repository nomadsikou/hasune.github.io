---
title: 자바와 루비 차이점
category: Ruby
comments: true
order: 3
---

## 클래스  

자바의 경우
```git
class LikeJava {

}
```

루비의 경우  
중괄호가 없고,  end로 닫아준다
```git
class LikeRuby

end
```
---
## 생성자

자바의 경우
```git
class LikeJava {
    LikeJava(){}
}
```

루비의 경우  
initialize메소드를 사용한다
```git
class LikeRuby
    def initialize()

    end
end
```
---
## 인스턴스

자바의 경우
LikeJava라는 클래스타입의 객체를 likeJava라는 참조변수로 생성
```git
LikeJava likeJava = new LikeJava();
```

루비의 경우  
클래스 타입을 지정하지 않고 바로 참조변수로써 생성
```git
likeRuby = LikeRuby.new()
likeRuby = LikeRuby.new
```
---
## 클래스 메소드(클래스 내부에 static형 메소드일때)

자바의 경우
```git
class LikeJava {
    static void hello() {
        System.out.println("hello world");
    }
}

LikeJava.hello();
```

루비의 경우  
static이 아닌 self. 를 메소드 앞에 붙혀준다
```git
class LikeRuby
    def self.hello()
        puts "hello world"
    end
end

LikeRuby.hello
```
---
## 인스턴스형 메소드(가장 많이 쓰이는 형태)

자바의 경우
```git
class LikeJava {
    void hello() {
        System.out.println("hello world");
    }
}

LikeJava likeJava = new LikeJava();
likeJava.hello();
```

루비의 경우  

```git
class LikeRuby
    def hello()
        puts "hello world"
    end
end

likeRuby = LikeRuby.new

likeRuby.hello
```

---

## 접근제어자

자바의 경우
```git
class LikeJava {
    public String banana;
    private String apple;
    protected String kiwi;
    
    public String write() {
    }

    private int delete() {
    }

    protected void check() {
    }

}
```

루비의 경우  
쫌 신기하다.. 적응이... ㅋㅋ
```git
class LikeRuby
    def write

    end
    public :write

    def delete

    end
    protected :delete

    def check

    end
    private :check
end
```

>가장크게 다가오는 차이점은 형선언이 없다는것  
>배열도 마찬가지로 자바에서는 int[] a = {1,2,3}; 이던것이  
>루비에서는 a = [1,2,3]  식으로 쓴다는것.   
>null -> nil  
>import -> require


