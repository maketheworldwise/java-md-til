## String 🤔

### 현재 문자열을 byte 배열로 변환하는 메소드

```java
getBytes()
getBytes(Charset charset)
getBytes(String charsetName)
```

- 한글을 처리하기 위해서 자바에서 많이 사용하는 캐릭터 셋은 UTF-16임을 기억해두자. 
- 만약 잘못된 캐릭터 셋으로 변환을 하면 우리들이 알아볼 수 없는 문자로 표현된다. 이를 방지하기 위해서 byte 배열로 생성할 때 사용한 캐릭터 셋을 문자열로 다시 전환할 때에도 동일하게 사용해야만한다.

```java
try {
    String korean = "한글";
    byte[] array = korean.getBytes("UTF-16"); // UTF-16 이니
    String ko = new String(array, "UTF-16");  // 되돌릴 때도 UTF-16
} catch (Exception e) {
    e.printStackTrace();
}
```

- 한글을 byte 배열로 만들 때 어떤 캐릭터 셋을 사용했는지에 따라 배열의 크기는 달라진다. (EUC-KR은 "한글" 두 글자를 표현하기 위해서 4 바이트를 사용하지만, UTF-16은 6 바이트를 사용한다.)
- 한글이 몇 바이트를 점유하는지 알아 두는 것은 개발할 때 매우 중요하다.
- 존재하지 않는 캐릭터 셋을 이용할 경우에는 <code>UnsupportedEncodingException</code> 예외가 발생한다.
- 메소드의 매개 변수로 넘어오는 객체가 null이 될 확률이 조금이라도 있다면 반드시 한 번씩 확인하는 습관을 가지고 있어야 한다. null 체크는 반드시 수행해야하는 작업이다.

### 문자열 길이를 확인하는 메소드

```java
length()
```

- 배열도 객체이지만 메소드는 없는 특수한 객체다. 그래서 배열의 크기를 확인할 때에는 괄호가 없는 <code>length</code>를 사용한다. 하지만 그 이외의 모든 클래스는 메소드를 호출해야하며, String 객체의 길이를 확인하기 위해서는 <code>length()</code> 메소드를 사용해야만 한다. 
- 문자열의 길이에는 공백도 포함되어 있다.

### 문자열이 비어 있는지 확인하는 메소드

```java
isEmpty()
```

- 문자열에 공백이 들어가 있더라도 비어있지 않다고 판단한다.

### 문자열이 같은지 비교하는 메소드

```java
equals(Object anObject)
equalsIgnoreCase(String anotherStr)
compareTo(String anotherStr)
compareToIgnoreCase(String str)
contentEquals(CharSequence cs)
contentEquals(StringBuffer sb)
```

<code>compareTo()</code>는 보통 정렬을 할 때 사용한다. 따라서 비교하려는 매개 변수로 넘겨준 String 객체가 알파벳 순으로 앞에 있으면 양수를, 뒤에 있으면 음수를 반환한다. 또한 알파벳 순서만큼 그 숫자값은 커진다.

### 특정 조건에 맞는 문자열이 있는지를 확인하는 메소드

```java
startsWith(String prefix)
startsWith(String prefix, int toOffset)
endsWith(String suffix)
contains(CharSequenece s)
matches(String regex) // 정규 표현식
regionMatches(boolean ignoreCase, int toffset, String other, int offset, int len) // 영역 문자열 확인
regionMatches(int toffset, String other, int ooffset, int len)
```

### 위치를 찾아내는 방법

```java
indexOf(int ch)
indexOf(int ch, int fromIndex)
indexOf(String str)
indexOf(String str, int fromIndex)
lastIndexOf(int ch)
lastIndexOf(int ch, int fromIndex)
lastIndexOf(String str)
lastIndexOf(String str, int fromIndex)
```

- char는 정수형이기에 매개 변수에 넣으면 자동으로 형 변환이 일어나기 때문에 큰 걱정을 할 필요없다.
- <code>indexOf()</code>와 <code>lastIndexOf()</code>의 차이는 검색의 시작 위치만 다른 것에만 차이가 있다.

### 값의 일부를 추출하기위한 메소드

```java
charAt(int index)
getChars(int srcBegin, int srcEnd, char[] dst, int dstBegin)
codePointBefore(int index)
codePointCount(int beginIndex, int endIndex).
offsetByCodePoints(int index, int codePointOffset)
```

### char 배열의 값을 String으로 변환하는 메소드

```java
copyValueOf(char[] data)
copyValueOf(char[] data, int offset, int count)
```

### String의 값을 char 배열로 변환하는 메소드

```java
toCharArray()
```

### 문자열의 일부 값을 잘라내는 메소드

```java
substring(int beginIndex)
substring(int beginIndex, int endIndex)
subSequence(int beginIndex, int endIndex)
```

### 문자열 여러 개의 String 배열로 나누는 split 메소드

```java
split(String regex)
split(String regex, int limit)
```

정규 표현식을 사용하여 문자열을 나눈다면 <code>split()</code> 메소드를, 그저 String으로 문자열을 나눈다면 <code>StringTokenizer</code>를 사용하는 편이 좋다.

### String 값을 바꾼는 메소드

```java
concat(String str)
trim()
```

<code>concat()</code> 메소드로 문자열을 계속 더하는 것보다는 <code>StringBuilder, StringBuffer</code> 클래스를 사용하는 것이 좋다.

### 내용을 교체하는 메소드

```java
replace(char oldChar, char newChar)
replace(CharSequenece target CharSequenece replacement)
replaceAll(String reges, String replacement)
replaceFirst(String rex, String replacement)
```

이 메소드들은 대소문자를 구분하기 때문에 주의해야한다. 반환하려고  생각하지 않은 값이 변환되어 버릴 수 있다.

### 특정 형식에 맞춰 값을 치환하는 메소드

```java
format(String format, Object ...object)
format(Locale 1, String format, Object ...args)
```

오직 출력만을 사용한다면, <code>System.out.format()</code> 메소드도 있다.

### 대소문자를 바꾸는 메소드

```java
toLowerCase()
toLowerCase(Locale locale)
toUpperCase()
toUpperCase(Locale locale)
```

### 기본 자료형을 문자열로 변환하는 메소드

```java
valueOf(boolean b)
valueOf(char c)
valueOf(char[] data)
valueOf(char[] data, int offset, int count)
valueOf(double d)
valueOf(float f)
valueOf(int i)
valueOf(long l)
valueOf(Object obj)
```

대부분 기본 자료형을 String 타입으로 변환할 필요가 있을 때는 String과 합치는 과정을 이용한다. 이 경우에는 <code>valueOf()</code> 메소드를 사용할 필요는 없지만, String으로 변환만하고 별도의 문자열과 합치는 과정이 없을 경우에는 이 메소드를 사용하는 것을 권장한다.

매개 변수로 객체가 넘어가는 경우에는 <code>toString()</code> 메소드의 결과를 반환해주는데, null인 객체의 경우 <code>toString()</code> 메소드를 사용할 수 없기 때문에 <code>NullPointerException</code>이 발생한다. 이를 방지하고자 객체를 출력할 때는 <code>valueOf()</code> 메소드를 사용하면 좋다. (객체가 null일 경우 "null"이라는 문자열을 넘겨준다.)

### String Constant Pool

자바에는 Constant Pool이 존재하는데, 객체들을 재사용하기 위해서 만들어졌다. String의 경우 동일한 값을 갖는 객체가 있다면, 이미 만든 객체를 재사용한다.

### 절대로 사용하면 안되는 메소드

```java
intern()
```

이 메소드는 Native C로 구현되어있는 메소드로, 시스템의 심각한 성능 저하를 발생시킬 수 있기 때문에 사용해서는 안된다. 확실히 풀에 있는 값으로 <code>equals()</code> 메소드가 아닌 "=="으로 비교하는 것이 훨씬 빠르지만, 강제로 문자열 풀에 값을 할당하도록 한다면, 저장되는 영역에 한계가 있기 때문에 그 영역에 대해서 별도로 메모리를 청소하는 단계를 거치게된다. 따라서 작은 연산 하나를 빠르게 하기 위해서 전체 자바 시스템의 성능에 악영향을 주게 된다.

### StringBuilder, StringBuffer

두 개의 공통점은 String의 더하기 연산처럼 새로운 객체가 생성되는 것이 아니라는 점이다. 반대로 차이점은 Thread safe의 차이가 존재한다.

JDK 5 이상에서는 String의 더하기 연산에서는 컴파일할 때 자동으로 해당 연산을 <code>StringBuilder</code>로 변환해준다. 따라서 더하는 작업을 변환해줄 필요는 없으나 포문과 같이 반복 연산을 할 때는 자동으로 변환해주지 않기때문에 주의해서 사용해야한다.

---

## 질문에 답해보자 💁‍♂️

**Q1. String 클래스는 final 클래스인가요? 만약 그렇다면 그 이유는 무엇인가요?**

<code>final</code> 클래스이며 더 이상 이 클래스를 확장할 수 없기 때문이다.

**Q2. String 클래스가 구현한 인터페이스에는 어떤 것들이 있나요?**

<code>Serializable, Comparable, CharSequence</code>

**Q3. String 클래스의 생성자 중에서 가장 의미없는 (사용할 필요가 없는) 생성자는 무엇인가요?**

기본 생성자

**Q4. String 문자열을 byte 배열로 만드는 메소드의 이름은 무엇인가요?**

```java
getBytes()
```
**Q5. String 문자열의 메소드를 호출하기 전에 반드시 점검해야 하는 사항은 무엇인가요?**

null

**Q6. String 문자열의 길이를 알아내는 메소드는 무엇인가요?**

```java
length()
```

**Q7. String 클래스의 equals() 메소드와 compareTo() 메소드의 공통점과 차이점이 무엇인가요?**

객체의 주소값이 아닌 값만으로 비교한다는 점에서 공통점을 가지고 있찌만, 리턴값이 다르다.

**Q8. 문자열이 "서울시"로 시작하는지를 확인하려면 String의 어떤 메소드를 사용해야 하나요?**

```java
startsWith()
```

**Q9. 문자열에 "한국"이라는 단어의 위치를 찾아내려고 할 때에는 String의 어떤 메소드를 사용해야 하나요?**

```java
indexOf()
```

**Q10. 9번 문제의 답에서 "한국"이 문자열에 없을 때 결과 값은 무엇인가요?**

-1

**Q11. 문자열의 1번째부터 10번째 위치까지의 내용을 String으로 추출하려고 합니다. 어떤 메소드를 사용해야 하나요?**

```java
substring();
```

**Q12. 문자열의 모든 공백을 * 표시로 변환하려고 합니다. 어떤 메소드를 사용하는 것이 좋을까요?**

```java
replaceAll()
```

**Q13. String의 단점을 보완하기 위한 두 개의 클래스는 무엇인가요?**

<code>StringBuilder, StringBuffer</code>

**Q14. 13번의 답에서 문자열을 더하기 위한 메소드의 이름은 무엇인가요?**

```java
append()
```