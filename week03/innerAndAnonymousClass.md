## 내부 클래스, 익명 클래스 🤔

중첩 클래스가 존재하는 가장 큰 이유는 코드를 간단하게 표현하기 위해서다. 중첩 클래스는 자바 기반의 UI 처리를 할 때 사용자의 입력이나 외부의 이벤트에 대한 처리를 하는 곳에서 가장 많이 사용된다.

중첩 클래스는 선언한 방법에 따라 정적, 비정적(내부) 클래스로 나뉜다. 그리고 내부 클래스는 로컬 클래스와 익명 클래스로 나뉜다.

간단하게 정리해보자.

- 한 곳에서만 사용되는 클래스를 논리적으로 묶어서 처리할 필요가 있을 때 사용한다.
- 캡슐화가 필요할 때 사용한다.
- 소스의 가독성과 유지보수성을 높이고 싶을 때 사용한다.
- 외부 클래스를 컴파일하면 내부 클래스들은 자동으로 컴파일된다.

---

## 질문에 답해보자 💁‍♂️

**Q1. Nested 클래스에 속하는 3가지 클래스에는 어떤 것들이 있나요?**

중첩 클래스는 정적 클래스와 비정적(내부) 클래스로 나뉘는데, 비정적 클래스는 로컬 클래스와 익명 클래스로 또 나뉜다.

**Q2. Nested 클래스를 컴파일하면 Nested 클래스 파일의 이름은 어떻게 되나요?**

```
외부 클래스명$내부 클래스명.class
```

**Q3. Static Nested 클래스는 다른 Nested 클래스와 어떤 차이가 있나요?**

인스턴스 없이 내부 클래스의 인스턴스를 바로 생성할 수 있다.

**Q4. Static Nested 클래스의 객체 생성은 어떻게 하나요?**

```java
new Outer.Inner();
```

**Q5. 일반적인 내부 클래스의 객체 생성은 어떻게 하나요?**

```java
Outer.new Inner();
```

**Q6. Nested 클래스를 만드는 이유는 무엇인가요?**

코드의 가독성을 높이기 위해

**Q7. Nested 클래스에서 감싸고 있는 클래스의 private로 선언된 변수에 접근할 수 있나요?**

네

**Q8. 감싸고 있는 클래스에서 Nested 클래스에 선언된 private로 선언된 변수에 접근할 수 있나요?**

아니요