## 참조 자료형 배열 기본값? 🤔

우선 모든 배열은 참조 자료형이다. 또한 배열에서는 기본 자료형의 기본값이 동일하게 적용된다.

```java
byteArrayDefault[0] = 0
shrotArrayDefault[0] = 0
intArrayDefault[0] = 0
longArrayDefault[0] = 0
floatArrayDefault[0] = 0.0
doubleArrayDefault[0] = 0.0
charArrayDefault[0] = ₩u0000
booleanArrayDefault[0] = false
```

하지만 String과 같은 참조 자료형은 초기화를 하지 않으면 <code>null</code> 로 설정되며, 배열에 객체를 넣고 출력하는 경우 <code>toString()</code> 메소드를 만들어주지 않으면 타입이름@고유번호 형태의 결과가 나온다.

```java
stringArray[0] = null

// ArrayClass[] array = new ArrayClass[2];
// array[0] = new ArrayClass();
array[0] = ArrayClass@c17164
```

## 배열을 그냥 출력해보면?

배열의 위치를 지정하지 않고 출력하면 알 수 없는 내용이 출력되는 것을 확인할 수 있다.

```java
public class ArrayPrint {
    public static void main(String[] args) {
        ArrayPrint array = new ArrayPrint();
        array.printString();
    }

    public void printString() {
        System.out.println("strings=" + new String[0]);
        System.out.println("array=" + new ArrayPrint[0]);
    }
}
```

```
strings=[Ljava.lang.String;@1540e19d
array=[LArrayPrint;@677327b6
````

- [L : 가장 앞의 대괄호는 해당 객체가 배열이라는 의미이며, 그 다음에 있는 L은 해당 배열은 참조 자료형이라는 의미다.
- java.lang.String : 해당 배열이 어떤 타입의 배열인지를 보여준다.
- @1540e19d : 해당 배열의 고유 번호다.

그렇다면 기본 자료형의 배열을 그냥 출력할 경우에는 어떻게 될까?

```java
byteArray = [B@14ae5a5
shrotArray = [S@7f31245a
intArray = [I@6d6f6e28
longArray = [J@135fbaa4
floatArray = [F@45ee12a7
doubleArray = [D@330bedb4
charArray = [C@2503dbd3
booleanArray = [Z@4b67cf4d booleanArray=[Z@7ea987ac
```

long과 boolean의 대문자가 다르긴하지만 각 타입을 대표하는 대문자가 출력되는 것을 확인할 수 있다.

## 배열의 선언 방법?

배열을 선언할 때는 <code>new</code> 예약어를 이용한 방법과 중괄호를 이용한 방법이 있다. 단, 중괄호를 이용한 방법의 경우 선언과 동시에 초기화해주어야 하며 보통 절대 변경되지 않는 값을 지정할 때 사용한다.

```java
int[] num = {
    1, 2, 3, 4, 5
};
```

또한 얼마나 자주 사용하는지, 어디에서 사용하는지를 고려하여 메소드에서 선언해서 사용할지, 클래스의 인스턴스 변수로 선언하여 사용할지를 고려해주어야 한다.

특히 <code>static</code> 을 이용할 경우, 클래스 변수가 되기 때문에 심각한 문제를 야기시킬 수 있어 주의해서 사용해야한다.

## 2차원 배열?

2차원 배열에서는 주의해야할 점은 반드시 배열의 크기를 선언해주어야 한다는 점이다. 1차원의 크기만 지정하고 2차원의 크기를 지정하지 않을 수는 있지만, 1차원의 크기를 지정하지 않고 2차원의 크기를 지정하거나 1차원 및 2차원의 크기 모두 지정하지 않을 경우에는 문제가 발생한다.

1차원의 크기만 지정하고 2차원의 크기를 지정하지 않을 경우에는 선언은 가능하지만 반드시 2차원의 크기도 정해주어야 한다.

```java
int[][] twoDim;
twoDim = new int[2][];
twoDim[0] = new int[2];
twoDim[1] = new int[3];
```

## 배열의 길이?

배열의 길이는 <code>.length</code>만을 붙여주면 int 타입으로된 배열의 크기를 반환해준다.

많은 사람들이 <code>.length</code>를 for문에 바로 넣어서 사용하는 경우가 있다. 하지만 책에서는 성능적 측면에서는 좋지 않기 때문에 별도의 크기를 알아내는 변수를 할당하여 사용하는 것이 가장 좋다고 한다. 배열의 값을 for문의 조건에 직접 입력하는 하드 코딩은 반드시 피해주어야 한다고 한다.

```java
int oneLoopLength = twoDim.length;
for(int i = 0; i < oneLoopLength; i++) {
    int twoLoopLength = twoDim[i].length;
    for(int j = 0; j < twoLoopLength; j++) {
        // 생략
    }
}
```