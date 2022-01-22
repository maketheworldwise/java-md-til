## 오브젝트 클래스? 🤔

자바에서는 기본적으로 아무런 상속을 받지 않으면 <code>java.lang.Object</code> 클래스를 확장한다. 그 이유는 Object 클래스에 있는 메소드들을 통해서 클래스의 기본적인 행동을 정의할 수 있기 때문이다.

Object 클래스에 선언되어 있는 메소드는 객체를 처리하기 위한 메소드와 쓰레드를 위한 메소드로 나뉜다.

객체를 처리하기 위한 메소드들은 다음과 같다.

- public String toString()
- public boolean equals(Object obj)
- public int hashCode()
- public Class<?> getClass()
- protected Object clone()
- protected void finalize()

쓰레드를 위한 메소드는 다음과 같다.

- public void notify()
- public void notifyAll()
- public void wait()
- public void wait(long timeout)
- public void wait(long timeout, int nanos)

## toString()

이 메소드는 자동으로 호출되는 경우가 2가지 있다.

- <code>System.out.println()</code> 메소드에 매개 변수로 들어갈 때
- 객체에 대하여 더하기 연산을 하는 경우

이전에 공부할 때는 참조 자료형에는 String만 더하기 연산이 가능하다고 했었다. String을 제외한 참조 자료형에 더하기 연산을 수행하면 자동으로 <code>toString()</code> 메소드가 호츨되어 객체의 위치에는 String 값이 놓이게 된다.

Object 클래스에 구현된 <code>toString()</code> 은 '@'를 기준으로 클래스이름과 <code>hashCode()</code> 메소드의 결과로 나온 int 타입 값을 16진수로 변환하여 더해준 뒤 출력해준다.

```java
getClass().getName() + '@' + Integer.toHexString(hashCode())
```

책에서는 DTO를 사용할 때는 아무리 개발 일정이 촉박하더라도 이 메소드를 오버라이딩하는 것이 좋다고 한다.

## equals()

"=="은 값을 비교하는 것이 아닌 주소값을 비교하는 연산을 수행한다. 즉, "=="을 통해서 같은지 확인이 안되기 때문에 이 메소드를 사용한다는 의미다. 이 메소드를 올바르게 사용하려면, 반드시 해당 클래스에 오버라이딩이 되어있어야 한다.

만약 오버라이딩이 되어있지 않을 경우 <code>equals()</code>메소드에서는 <code>hashCode()</code> 값을 비교하기 때문에 원하는 결과를 얻지 못한다. 따라서 클래스의 인스턴스 변수값들이 동일하더라도 서로 다른 생성자로 객체를 생성하면 해시 코드가 달라 객체가 다르다는 결과가 나온다.

단, 이 메소드를 오버라이딩할 때는 <code>hashCode()</code> 메소드도 같이 오버라이딩을 해주어야 한다. 그 이유는 <code>equals()</code>메소드를 통해 값이 같다는 것을 알아도 주소값이 같다는 것이 아니기 때문이다.

개인적으로는 <code>equals()</code> 메소드는 내부적으로 주소값과 값을 비교한다는 정도로 이해하면 될 것 같다.

## hashCode()

이 메소드는 기본적으로 객체의 메모리 주소를 16진수로 반환해준다. 만약 두 객체가 동일하다면 이 메소드의 결과도 동일해야만한다. 따라서 위에서 언급했듯, <code>equals()</code> 뿐만이 아니라 이 메소드도 같이 오버라이딩을 해주어야 한다.

책에서는 직접 메소드를 작성하는 것을 권장하지 않는다고 한다. <code>hashCode()</code>조건들을 정리해보자.

- 애플리케이션이 수행되는 동안에 어떤 객체에 대해서 이 메소드가 호출될 때에는 항상 동일한 int 값을 반환해주어야 한다. 하지만 자바를 실행할 때마다 같은 값일 필요는 없다.
- 어떤 두 객체에 대해 <code>equals()</code> 메소드를 비교한 결과가 true라면, 두 객체의 <code>hashCode()</code> 메소드의 결과도 동일해야한다.
- <code>equals()</code>의 결과가 false일 때, <code>hashCode()</code>의 값도 무조건 다를 필요는 없으나 서로 다른 결과를 제공하면 hashtable의 성능을 향상시키는데 도움이 된다.

---

## 질문에 답해보자 💁‍♂️

**Q1. 모든 클래스의 최상위 부모 클래스인 Object 클래스는 어떤 패키지에 선언되어 있나요?**

```java
java.lang.Object
```

**Q2. 클래스가 어떻게 선언되어 있는지 확인할 수 있는 명령어(실행 파일)의 이름은 무엇인가요?**

```java
javap
```

**Q3. Object 클래스에 선언되어 있는 모든 메소드는 여러분들이 Overriding해야 하나요?**

아니요

**Q4. Object 클래스의 clone() 메소드의 용도는 무엇인가요?**

복제

**Q5. System.out.println() 메소드를 사용하여 클래스를 출력했을 때 호출되는 Object 클래스에 있는 메소드는 무엇인가요?**

```java
toString()
```

**Q6. 객체의 주소를 비교하는 것이 아닌, 값을 비교하려면 Object 클래스에 선언되어 있는 어떤 메소드를 overriding해야 하나요?**

```java
equals()
```

**Q7. Object 클래스에 선언되어 있는 hashCode()라는 메소드는 어떤 타입의 값을 리턴하나요?**

int