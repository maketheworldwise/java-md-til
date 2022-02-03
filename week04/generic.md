## 제네릭 🤔

제네릭은 형 변환시에 발생할 수 있는 문제를 해결할 수 있다.

예를 들어, Object 타입의 변수의 값을 지정하는 Setter를 구현했을 때를 살펴보자. 어떤 참조 자료형을 매개 변수로 보내도 문제는 없지만, Getter로 값을 불러올 때 인스턴스의 변수가 어떤 타입인지에 대해 혼동이 오는 문제가 발생한다.

```java
GenericDto dto1 = new GenericDto();
GenericDto dto2 = new GenericDto();
GenericDto dto3 = new GenericDto();

dto1.setObject(new String());
dto2.setObject(new StringBuffer());
dto3.setObject(new StringBuilder());

String dto1Getter = (String)dto1.getObject();
StringBuffer dto2Getter = (StringBuffer)dto2.getObject();
StringBuilder dto3Getter = (StringBuilder)dto3.getObject();
```

일반적으로는 <code>instanceof</code> 키워드로 해결을 할 수 있지만, 매번 타입을 점검해야하는 불편함이 있어 Java 5 부터는 제네릭이 추가되었다.

즉, 제네릭은 형 변환에서 발생할 수 있는 문제점을 사전에 없애기 위해서 만들어졌다. 사전이라는 것은 실행시에 예외가 발생하는 것을 처리하는 것이 아닌, 컴파일시 점검할 수 있도록 하는 것을 의미한다.

## 제네릭 클래스 만들기

```java
public class GenericDto<T> implements Serializable {
    
    private T object;

    public void setObject(T obj) {
        this.object = obj;
    }

    public T getObject() {
        return object;
    }
}
```

여기서 의미하는 <code>T</code>는 특별한 의미는 없다. 꺽쇠 안에는 현재 존재하는 클래스를 사용해도 되고, 존재하지 않느 것을 사용해도 무관하다. 하지만 되도록 클래스 이름의 명명 규칙과 동일하게 지정하는 편이 좋다.

꺽쇠 안에 들어가는 알파벳은 자바에서도 기본적으로 정의된 규칙이 존재한다.

- E (Element) : 요소, 자바 컬렉션에서 주로 사용됨
- K (Key) : 키
- N (Number) : 숫자
- T (Type) : 타입
- V (Value) : 값
- S, U, V : 두 번째, 세 번째, 네 번째에 선언된 타입

## 메소드의 매개 변수로 넘어가는 제네릭

제네릭은 클래스 타입만 변경한다고 해서 오버로딩이 불가능하다. 따라서 <code>?</code>라는 와일드카드 타입을 이용한다. 와일드 카드는 매개 변수로만 사용하는 것을 권장한다. 만약 인스턴스를 생성할 때 사용한다면 알 수 없는 타입이라는 컴파일 에러가 발생하게 된다. 즉, 어떤 객체를 와일드 카드로 선언하고 그 객체의 값은 가져올 수 있지만, 와일드 카드로 객체를 선언했을 때는 특정 타입으로 값을 지정하는 것이 불가능하다.

 와일드 카드로 매개 변수에 넘어오는 타입이 두세 가지라면 <code>instanceof</code> 키워드로 해당 타입을 확인할 수 있다.

```java
public void printMethod(GenericDto<?> c) {
    Object value = c.getObject();
    if(value instanceof String) {
        System.out.println(value);
    }
}
```

혹은 <code>? extends 타입</code> 바운디드 와일드 카드 문법을 이용하여 와일드 카드로 사용하는 타입을 제한할 수도 있다. 간단하게 이해하기 위해 InheritClass를 상속받는 클래스만 사용할 수 있는 메소드를 작성하자면 다음과 같다. 만약 다른 타입이 들어올 경우 컴파일시에 에러가 발생하므로 반드시 InheritClass와 관련된 상속한 클래스가 넘어가야만 한다.

```java
public void printMethod(GenericDto<? extends InheritClass> c) {
    Object value = c.getObject();
    System.out.println(value);
}
```

## 메소드를 제네릭하게 선언하기

앞에서 배운 와일드 카드의 내용으로는 매개 변수로 사용된 객체에 값을 추가할 수 없다는 단점이 있다. 이 때는 메소드의 선언부에 리턴타입 앞에 제네릭 타입을 선언해주면 해결할 수 있다.

와일드 카드로 타입을 사용하는 것보다 명시적으로 메소드 선언시 타입을 지정해 주면 더 견고한 코드를 만들 수 있다.

```java
public <T> void setValueToC(GenericDto<T> c, T value) {
    c.setValue(value);
    System.out.pritnln(c.getValue());
}
```

물론, 바운디드 와일드 카드도 사용이 가능하다.

```java
public <T extends InheritClass> void setValueToC(GenericDto<T> c, T value)
```

만약 제네릭 타입이 한 개 이상일 경우에는 콤마로 구분하여 나열해주면 된다.

```java
public <S, T extends InheritClass> void setValueToC(GenericDto<T> c, T value, S another)
```

---

## 질문에 답해보자 💁‍♂️

**Q1. 제네릭이 자바에 추가된 이유는 무엇인가요?**

잘못된 타입이 들어올 수 있는 것을 컴파일 단계에서 방지할 수 있기 때문이다. (형 변환)

**Q2. 제네릭 타입의 이름이 T나 E처럼 하나의 캐릭터로 선언되어야 하나요?**

그렇지는 않지만, 자바의 기본 규칙을 사용하는 것을 권장한다.

**Q3. 메소드에서 제네릭 타입을 명시적으로 지정하기 애매할 경우에는 <> 안에 어떤 기호를 넣어 주어야 하나요?**

<code>?</code> 와일드 카드

**Q4. 메소드에서 제네릭 타입을 명시적으로 지정하기에는 애매하지만, 어떤 클래스의 상속을 받은 특정 타입만 가능하다는 것은 나타내려면 <> 안에 어떤 기호를 넣어 주어야 하나요?**

<code>? extends 클래스</code> 바운디드 와일드 카드

**Q5. 제네릭 선언시 wildcard라는 것을 선언했을 때 어떤 제약 사항이 있나요?**

와일드 카드 타입을 오브젝트 타입으로만 사용해야 한다.

**Q6. 메소드를 제네릭하게 선언하려면 리턴 타입 앞에 어떤 것을 추가해 주면 되나요?**

원하는 제네릭 타입을 명시하면 된다.