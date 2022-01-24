## 어노테이션 🤔

어노테이션은 메타데이터라고 불리며 JDK 5 부터 등장했다. 어노테이션이 존재하는 이유는 다음과 같다.

- 컴파일러에게 정보를 알려주거나
- 컴파일할 때와 설치시의 작업을 지정하거나
- 실행할 때 별도의 처리가 필요할 때

대표적으로 <code>@Override, @Deprecated, @SupressWarnings</code>가 있다.

어노테이션은 제약사항, 용도, 행위, 처리를 표현하기 위해 사용하는 것일 뿐이며, 선언할 때에도 미리 만들어 놓은 어노테이션을 확장하는 것이 불가능하다. 어노테이션이 변환된 모습은 컴파일 단계에서 생성되기 때문에 역컴파일을 하지 않는 이상 직접 확인할 수 없다.

## 어노테이션을 선언하기 위한 메타 어노테이션

### @Target

```java
@Target(ElementType.METHOD)
```

어노테이션을 어떤 것에 적용할지를 선언할 때 사용한다. 요소 타입으로는 <code>CONSTRUCTOR, FIELD, LOCAL_VARIABLE, METHOD, PACKAGE, PARAMETER, TYPE(클래스, 인터페이스, ENUM)</code>이 있다.

### @Retention

```java
@Retention(RententionPolicy.RUNTIME)
```

얼마나 오래 어노테이션 정보가 유지되는지를 선언할 때 사용한다. 적용 가능한 대상은 <code>SOURCE, CLASS, RUNTIME</code>가 있다.

### @Documented

정보가 JavaDocs(API) 문서에 포함된다는 것을 선언할 때 사용한다.

### @Inherited

모든 자식 클래스에서 부모 클래스의 어노테이션을 사용 가능하다는 것을 선언한다.

### @interface

어노테이션을 선언할 때 사용한다.

### default

<code>default</code> 예약어를 사용할 경우에는 뒤에 있는 값이 이 어노테이션을 사용할 때의 기본값이 된다.

### 전체적인 구현

```java
// 어노테이션
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface UserAnnotation {
    public int number();
    public String text() default "Custom Annotation";
}
```

```java
// 사용법
@UserAnnotation(number = 2, text = "text")
public void annotationTest() {

}
```

```java
// 어노테이션 확인
public void checkAnnotation(Class useClass) {
    Method[] methods = useClass.getDeclaredMethods();
    for(Method tempMethod : methods) {
        UserAnnotation annotation = tempMethod.getAnnotation(UserAnnotation.class);
        if(annotation != null) {
            int number = annotation.number();
            String text = annotation.text();
            System.out.println(tempMethod.getName() + "() : number = " + number + "text = " + text);
        } else {
            System.out.println(tempMethod.getName() + "() : annotation is null");
        }
    }
}
```

---

## 질문에 답해보자 💁‍♂️


**Q1. @Override 어노테이션의 용도는 무엇인가요?**

부모 클래스로부터 메소드를 오버라이딩을 했음을 명시적으로 선언한다. (재정의)

**Q2. @SupressWarnings 어노테이션의 용도는 무엇인가요?**

경고를 위한 용도다.

**Q3. @Deprecated 어노테이션의 용도는 무엇인가요?**

더 이상 사용되지 않음을 컴파일러에게 알려주는 역할을 수행한다.

**Q4. 어노테이션을 선언할 때 사용하는 어노테이션을 무엇이라고 부르나요?**

메타어노테이션

**Q5. 4번의 답에 있는 어노테이션들을 사용할 때 import 해야 하는 패키지는 무엇인가요?**

```java
java.lang.annotation
```

**Q6. @Target 어노테이션의 용도는 무엇인가요?**

어디에 어노테이션을 적용할 수 있는지 선언

**Q7. @Retention 어노테이션의 용도는 무엇인가요?**

얼마나 오래 어노테이션 정보가 유지되는지를 선언

**Q8. @Inherited 어노테이션의 용도는 무엇인가요?**

모든 자식 클래스에서 부모 클래스의 어노테이션을 사용 가능하다는 것을 선언

**Q9. 어노테이션을 선언할 때에는 class 대신 어떤 예약어를 사용해야 하나요?**

```java
@interface
```