## 컬렉션 리스트 🤔

자바 컬렉션은 목록성 데이터를 처리하는 자료 구조를 통칭한다. 자료 구조는 정보를 담는 것을 의미하며 하나의 데이터가 아닌 여러 데이터를 담을 때 사용한다.

배열은 성능상 메모리 효율면에서 가장 좋지만 그 크기가 얼마나 되는지 모르기 때문에 배열만을 사용하는 것은 좋은 방안이 아니다. 이런 불필요한 메모리 낭비를 고려하여 많은 개발자들이 만들어놓은 자료 구조를 이용하면 좋다.

자바에서는 목록, 셋, 큐는 Collection 인터페이스를 구현하고 있다. 이 인터페이스는 java.util 패키지에 선언되어있고 여러 개의 객체를 하나의 객체에 담아 처리할 때 공통적으로 사용되는 여러 메소들을 선언해 놓았다.

![](../images/collection.jpeg)

출처: https://memostack.tistory.com/234

이미지에서 Collection은 Iterable 인터페이스를 확장을 했는데, Iterable 인터페이스를 이용하여 데이터를 순차적으로 가져올 수 있다.

리스트 인터페이스는 배열과 동일하게 순서가 존재한다. 가장 많이 사용하는 클래스로는 <code>ArrayList, Vector, Stack, LinkedList</code>가 있다. 

> 부모 클래스에 선언된 메소드를 사용할 수 있기 때문에 상속 관계를 살펴보는 편이 좋다.

간단하게 살펴만보자. <code>ArrayList</code>와 <code>Vector</code>는 서로 비슷하지만, </code><code>ArrayList</code>는 스레드 안전하지 않고 <code>Vector</code>는 스레드 안전하다. <code>Stack</code>은  LIFO를 지원하기 위해 <code>Vector</code> 클래스를 확장해서 만들었다. <code>LinkedList</code>는 목록에도 속하지만 큐에도 속한다.

## ArrayList 공간 생성자

<code>ArrayList</code>는 생성자가 3개가 존재하는데, 그 중 저장 공간을 갖는 생성자가 존재한다. 공간을 지정하지 않으면 초기 크기는 10이지만 10개 이상의 데이터가 들어가면 크기를 늘이는 작업을 내부적으로 자동으로 수행한다. 언뜻 보면 편리하지만, 이러한 작업이 수행되면 애플리케이션 성능에 영향을 주게 된다. 만약 저장되는 데이터의 크기가 어느 정도 예측된다면 초기 크기를 지정하는 것을 권장한다고 한다.

## ArrayList 복사

복사의 경우에는 조금 특별하다. 복사에는 얕은 복사와 깊은 복사로 나뉜다. 다른 객체에 원본 객체의 주소값만을 할당하는 것을 얇은 복사라면, 객체의 모든 값을 복사하여 복제된 객체에 있는 값을 변경해도 원본에 영향이 없도록 할 때는 깊은 복사라고 한다.

```java
// 얕은 복사
ArrayList<String> listA = new ArrayList<>();
ArrayList<String> listB = listA;
```

```java
// 깊은 복사 1
ArrayList<String> listA = new ArrayList<>();
ArrayList<String> listB = new ArrayList<>(listA);

// 깊은 복사 2
ArrayList<String> listC = new ArrayList<>();
listC.addAll(listA);
```

## ArrayList 배열화

ArrayList를 배열화하는 메소드는 2가지가 있다. 그 중에서도 책에서는 매개 변수로 넘기는 형태의 메소드를 권장한다. 매개 변수가 없는 <code>toArray()</code> 메소드의 경우에는 Object 타입의 배열로만 만들기 때문에 제네릭을 사용하여 선언한 ArrayList 객체를 배열로 생성할 때에는 좋지 않다고 한다.

책의 예시를 가져와보자.

```java
ArrayList<String> list = new ArrayList<>();
list.add("a");
String[] strList = list.toArray(new String[0]);
System.out.println(strList[0]);
```

여기서 재미있는 점은 매개 변수로 변환하려는 타입의 배열을 지정해줄 때 작성한 <code>new String[0]</code>이다. 매개 변수로 넘기는 배열은 타입만을 지정하기 위해서 사용할 수 있지만, 실제로는 매개 변수로 넘긴 객체에 값을 담아준다. 하지만 ArrayList 객체의 데이터 크기가 매개 변수로 넘어간 배열 객체의 크기보다 클 경우에는 매개 변수로 배열의 모든 값이 null로 채워진다.

따라서 책에서는 매개 변수로 넘겨줄 배열을 미리 선언한 뒤 넣어주는 방식을 권장했다.

```java
ArrayList<String> list = new ArrayList<>();
list.add("a");
list.add("b");
list.add("c");

String[] tempArr = new String[3];
String[] strList = list.toArray(tempArr);
for(String temp : strList) {
    System.out.println(temp);
}
```

## ArrayList의 trimToSize()

이 메소드는 특별하다. 이 메소드는 ArrayList 객체 공간의 크기를 데이터의 개수만큼으로 변경해준다. 즉, 저장할 수 있는 공간은 만들어 두었지만, 데이터가 저장되어 있지 않으 ㄹ때 해당 공간을 없애버린다. 일반적인 경우에는 사용할 일이 없지만, 객체를 원격으로 전송하거나 파일로 저장하는 일이 있을 때 이 메소드를 한 번 호출함으로서, 데이터의 크기를 줄일 수 있다.

## ArrayList의 스레드 안전화

ArrayList는 스레드 안전하지 않다. 만약 스레드에서도 안전하게 만들려면 다음과 같이 생성해주면 된다.

```java
List list = Collections.synchronizedList(new ArrayList(...));
```

## LIFO 기능 구현화 (Stack)

LIFO 기능을 위해서는 Stack보다는 더 빠른 ArrayDeque 클래스를 사용하는 편이 좋다고 한다. 물론 스레드 안전하지 못한다. 성능은 떨어지지만 스레드에 안전한 LIFO 기능을 원한다면 Stack을 사용하면 된다.

Stack 클래스는 자바에서 상속을 잘못 받은 클래스라고 한다. JDK 1.0 부터 존재했지만 원래 취지라면 LIFO를 생각했을 때, Vector에 속해서는 안된다고 한다. 하지만 자바의 하위 호환성을 위해 상속관계를 유지하고 있다고 생각하면 된다고 한다.

---

## 질문에 답해보자 💁‍♂️

**Q1. Collection 인터페이스를 구현하는 대표적인 3개의 자료 구조에는 어떤 것들이 있나요?**

List, Queue, Set

**Q2. 배열과 같이 순서가 있는 목록형을 나타내는 대표 인터페이스는 무엇인가요?**

ArrayList

**Q3. ArrayList라는 클래스의 생성자 중 매개 변수가 없는 기본 생성자를 사용하려면 기본적으로 몇 개의 저장 공간을 가지나요?**

10

**Q4. 만약 ArrayList 클래스의 저장 공간 개수를 처음부터 지정하려면 어떤 생성자를 사용하면 되나요?**

```java
new ArrayList(int initialCapacity);
```

**Q5. ArrayList 객체를 생성할 때 제네릭을 사용하는 이유는 무엇인가요?**

컴파일 시 타입을 잘못 지정한 부분을 고려해서

**Q6. ArrayList에 데이터를 담는 메소드 이름 두 가지는 무엇인가요?**

```java
add();
addAll();
```

**Q7. Collection 인터페이스를 구현한 클래스의 객체에서 사용할 수 있는 for 루프의 구조는 어떻게 되나요?**

```java
ArrayList<String> strList = new ArrayList<>();
for(String str : strList) {
    System.out.pritnln(str);
}
```

**Q8. Collection 인터페이스를 구현한 클래스의 객체 크기를 확인하는 메소드 이름은 무엇인가요?**

```java
size();
```

**Q9. ArrayList에서 특정 위치에 있는 데이터를 확인하는 메소드는 무엇인가요?**

```java
get();
```

**Q10. ArrayList에서 특정 위치에 있는 데이터를 삭제하는 메소드는 무엇인가요?**

```java
remove();
```

**Q11. ArrayList에서 특정 위치에 있는 데이터를 수정하는 메소드는 무엇인가요?**

```java
set();
```
**Q12. java.util 패키지에 있는 Stack이라는 클래스는 어떤 클래스를 확장한 것인가요?**

List 인터페이스를 구현하고 있는 Vector 클래스를 상속

**Q13. Stack 클래스에서 데이터를 담는 메소드는 무엇인가요?**

```java
push();
```

**Q14. Stack 클래스에서 가장 위에 있는 데이터를 확인만 하는 메소드는 무엇인가요?**

```java
peek();
```

**Q15. Stack 클래스에서 가장 위에 있는 데이터를 삭제하고 리턴하는 메소드는 무엇인가요?**

```java
pop();
```
