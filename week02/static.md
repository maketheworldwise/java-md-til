## static? 🤔

static 메소드는 객체를 생성하지 않고 바로 호출할 수 있다. 단, static 메소드는 클래스 변수만 사용할 수 있다.

하단의 코드를 컴파일하게 되면 "static이 아닌 변수 이름을 static context에서 참조할 수 없다" 라는 오류를 확인할 수 있다.

```java
// 문제의 코드
public class StaticClass {
    String name = "static";
    public static void staticMethod() {
        System.out.println(name);
    }
}
```

문제를 해결하려면 <code>static</code> 예약어를 제거하고 객체를 생성하여 호출을 하거나, 인스턴스 변수에 <code>static</code> 예약어를 붙이면 해결할 수 있다.

하지만 <code>static</code> 예약어를 함부로 붙여서는 안된다. 클래스 변수가 되면 모든 객체가 하나의 값만을 바라보기 때문이다.

## static 블록

<code>static</code> 예약어는 객체가 생성되면서 한 번만 불려야 하는 코드가 있을 때도 사용한다. 즉, static 블록은 객체가 생성되기 전에 한 번만 호출되고 그 이후에는 호출하려해도 호출을 할 수 없다. 

static 블록의 특징을 살펴보자.

- 메소드나 생성자 내에서는 선언할 수 없다.
- static 블록은 여러 개를 선언할 수 있다.
- static 블록은 선언된 순서대로 호출된다.
- static 블록 안에서는 static 한 것들(변수, 메소드)만 호출할 수 있다.
- 클래스에 대한 참조가 발생하자마자 호출이 된다.
- 클래스를 초기화할 때 반드시 수행되어야 하는 작업이 있을 경우 유용하게 사용할 수 있다.

책의 예시를 가져와보자.

```java
public class StaticBlock {
    static int data = 1;

    public StaticBlock() {
        System.out.println("생성자 호출");
    }

    static {
        System.out.println("첫 번째 static 블록");
        data = 3;
    }

    static {
        System.out.println("두 번째 static 블록");
        data = 5;
    }

    public static int getData() {
        return data;
    }
}
```

```java
StaticBlock block1 = new StaticBlock();
System.out.println("----------------");
StaticBlock block2 = new StaticBlock();
```

```
첫 번째 static 블록
두 번째 static 블록
생성자 호출
----------------
생성자 호출
```