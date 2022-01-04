## main() 메소드는 뭘까? 🤔

```java
public static void main(String[] args) {}
```
<code>main()</code>메소드는 자바 프로그램의 진입점이다. 따라서 실행되는 모든 프로그램에 있는 수 많은 클래스들 중에서 적어도 하나의 자바 클래스에는 <code>main()</code>메소드가 반드시 존재한다.

만약 <code>main()</code>메소드없이 실행이 된다면, <code>NoSuchMethodError: main</code> 메시지를 확인할 수 있다.

---

## 질문에 답해보자 💁‍♂️

**Q1. main() 메소드의 메소드 이름 앞에는 어떤 예약어들이 들어 가나요?**

```java
public static void
```

**Q2. main() 메소드의 매개 변수에는 어떤 값이 들어가나요?**

```java
String[] args
```

**Q3. 만약 여러분들이 만든 클래스에 main() 메소드가 없다면, java 명령어로 그 클래스를 수행할 수 있나요?**

 아니요

**Q4. System.out.println() 메소드는 어떤 용도로 사용하나요?**

 출력

**Q5. System.out.print() 메소드는 System.out.println() 메소드와 어떤 차이가 있나요?**
 
 줄바꿈

**Q6. // 는 무엇을 하는 데 사용하는 기호인가요?**

주석

**Q7. /*로 시작하고 */로 끝나는 사이에 있는 소스들은 어떻게 되나요?**

주석

**Q8. 메소드를 선언할 때 반드시 있어야 하는 세 가지는 무엇인가요?**

접근 제어자, 리턴 타입, 메소드 이름