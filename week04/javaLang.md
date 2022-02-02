## 자바랭 🤔

기본적으로 자바로 개발할 때 패키지를 지정할 때에는 같은 역할 및 용도로 묶어 구분해야한다. 그 중에서도 자바랭 패키지는 import 하지않아도 사용할 수 있다.

## 자주 발견하는 에러

- <code>OutOfMemoryError</code>
- <code>StackOverflowError</code>

자바는 가상 머신에서 메모리를 관리하지만, 프로그램을 잘못 작성하거나 설정이 제대로 되어 있지 않을 경우에는 <code>OutOfMemoryError</code>가, 호출된 메소드의 깊이가 너무 깊을 때는 <code>StackOverflowError</code>가 발생한다. (자바에서는 스택 영역에서 어떤 메소드가 어떤 메소드를 호출했는지에 대한 정보를 관리)

## 숫자 클래스

숫자를 처리하는 클래스는 대부분 기본 자료형을 많이 사용한다. 이 기본 자료형은 힙 영역이 아닌 스택 영역에 저장되어 관리된다. 따라서 계산할 때 보다 빠른 처리가 가능하다. 

<code>Character</code>와 <code>Boolean</code>을 제외한 숫자를 처리하는 클래스들은 Wrapper 클래스라고하며, 모두 <code>Number</code>라는 추상 클래스를 확장한다.

자바 컴파일러에서 자동으로 형 변환을 해주기 때문에 참조 자료형이지만 기본 자료형처럼 사용할 수 있다. <code>Character</code> 클래스를 제외하고는 <code>parse()</code>와 <code>valueOf()</code> 두 개의 공통적인 메소드를 제공한다.

두 메소드는 공통적으로 String과 같은 문자열을 숫자 타입으로 변환하지만 <code>parse()</code> 메소드는 기본 자료형을 반환하고 <code>valueOf()</code> 메소드는 참조 자료형을 반환한다. 여기서 재미있는 점은, 참조 자료형을 반환을 하더라도 숫자끼리 더하기 연산이 된다는 것이다. 그 이유는 참조 자료형 중에서 <code>Byte, Short, Integer, Long, Float, Double</code> 타입들은 필요시 기본 자료형처럼 사용할 수 있기 때문이다. 따라서 <code>new</code> 키워드를 이용하여 객체를 만들지 않아도 값을 할당할 수 있다.

## 왜 혼동되게 숫자를 처리하는 참조 자료형을 만들었을까?

- 매개 변수를 참조 자료형으로만 받는 메소드를 처리하기 위해서
- 제네릭과 같이 기본 자료형을 사용하지 않는 기능을 사용하기 위해서
- MIN_VALUE와 MAX_VALUE 상수 값을 사용하기 위해서
- 문자열을 숫자로, 숫잘르 문자열로 쉽게 변환하고 2, 8, 10, 16 진수 변환을 쉽게 처리하기 위해서
  
기본 자료형을 참조 자료형으로 만든 클래스들은 <code>Boolean</code> 클래스를 제외하고 모두 MIN_VALUE와 MAX_VALUE 상수를 가지고 있다.

## System 클래스

- 시스템 속성값 관리
- 시스템 환경값 조회
- GC 수행
- JVM 종료
- 현재 시간 조회
- 기타 관리용 메소드들

이 중에서도 GC 수행과 JVM 종료 메소드는 절대로 수행해서는 안된다. 환경값 <code>env</code>는 변경하지는 못하고 읽기만 가능하며 대부분 OS나 장비에 관련된 것들이다.

현재 시간 조회에서 <code>currentTimeMillis()</code> 메소드는 현재 시간을 나타낼 때 유용한 메소드다. UTC 기준으로 1970년 1월 1일 00:00부터 지금까지의 밀리초 단위의 차이를 출력한다. <code>nanoTime()</code> 메소드의 경우 시간의 차이를 측정하기 위한 용도로 사용된다.

System 클래스의 <code>out</code> 메소드에서 중요한 점만 짚고 넘어가자. <code>print()</code>, <code>println()</code> 메소드의 경우 단순히 참조 자료형의 <code>toString()</code> 메소드 결과를 출력하지 않고 String의 <code>valueOf()</code> 메소드를 호출하여 결과를 받은 후 출력한다. 따라서 <code>print()</code>와 <code>println()</code> 메소드에 null인 객체가 들어가면 <code>String.valueOf(object)</code> 메소드가 호출되어 아무런 문제 없이 출력이 된다.

(객체를 출력할 때는 <code>toString()</code>을 사용하는 것보다는 <code>valueOf()</code>를 사용하는 것이 훨씬 안전하다.)

---

## 질문에 답해보자 💁‍♂️

**Q1. 자바 패키지 중 같은 패키지에 있는 클래스를 제외하고 별도로 import 하지 않아도 되는 패키지는 무엇인가요?**

<code>java.lang</code>

**Q2. 자바의 메모리가 부족해서 발생하는 에러는 무엇인가요?**

<code>OutOfMemoryError</code>

**Q3. 메소드 호출 관계가 너무 많아서 발생하는 에러는 무엇인가요?**

<code>StackOverflowError</code>

**Q4. java.lang 패키지에 선언되어 있는 3개의 어노테이션에는 어떤 것들이 있고, 각각의 역할은 무엇인가요?**

<code>@Deprecated</code>은 더이상 사용되지 않음을 컴파일러에게 알려주는 역할을 수행하고 <code>@Override</code>는 해당 메소드가 부모 클래스에 있는 메소드를 오버라이딩했다는 것을 명시적으로 선언하고 <code>@SuppressWarning</code>은 경고에 대해 알고 있고 이에 해당하는 내용을 감수하겠다고 선언하는 것을 의미한다.

**Q5. Double과 Integer 같은 숫자 타입에서 처리할 수 있는 최대, 최소값을 알 수 있는 상수의 이름은 무엇인가요?**

MIN_VALUE, MAX_VALUE

**Q6. Integer 값을 2진법으로 표현하려면 어떤 메소드를 사용해야하나요?**

<code>toBinaryString()</code>

**Q7. Integer 값을 16진법으로 표현하려면 어떤 메소드를 사용해야하나요?**

<code>toHexString()</code>

**Q8. 속성(Properties)과 환경(Environment) 값의 차이는 무엇인가요?**

속성은 <code>java.util</code> 패키지에 속하며 <code>HashTable</code>의 상속을 받는다. 속성은 추가할 수 있고 변경할 수 있으나 환경은 읽기만 가능하다.

**Q9. System.out과 System.err에서 사용할 수 있는 메소드들을 확인하려면 어떤 클래스를 찾아봐야 하나요?**

<code>PrintStream</code> 클래스

**Q10. System 클래스에서 현재 시간을 조회하는 용도로 사용하는 메소드 이름은 무엇인가요?**

<code>currentTimeMillis()</code> 메소드

**Q11. System 클래스에서 시간 측정 용도로 사용하는 메소드 이름은 무엇인가요?**

<code>nanoTime()</code> 메소드

**Q12. System.out.print() 메소드와 System.out.println() 메소드의 차이는 무엇인가요?**

줄바꿈

**Q13. System.out.println() 메소드에 객체가 매개 변수로 넘어 왔을 때 String의 어떤 메소드가 호출되어 결과를 출력하나요? 그리고 그 메소드를 사용하는 이유는 무엇인가요?**

<code>valueOf()</code> 메소드가 호출되고 객체가 null일 경우 <code>toString()</code> 메소드를 사용하면 예외가 발생할 수 있기에 <code>toString()</code> 메소드보다 안전하다.