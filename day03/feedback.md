1. string.length 글자 수?? 어떻게 구현되어있을까? 문자열의 특정 길이를 의미하는 것도 아니다! 대표적으로 이모지별로 length가 다름.. 그래서 실제로 이모지를 넣었다고 글자수를 넘어가는 경우도 있었음 (https://engineering.linecorp.com/ko/blog/the-7-ways-of-counting-characters/)

2. 롬복이 무엇인지, 어떤 이유로 사용되는지, 어노테이션에 대한 retention과 target 범위 인지? 어떤 기능을 제공할 수 있는지, 왜 도입을 했는지

## 인터페이스를 사용해야할까? 추상화를 사용해야할까?

- https://kingofbackend.tistory.com/128

## 자바 문서는 어떤걸 기준으로 봐야하는가?

버전과는 관계없이 같이 보는 편이 좋다고 한다. 하지만 굳이 선택을 한다면 자바 8, 11, 17 기준으로 문서를 보는게 좋다는 의견이 있다. 이 중에서도 현재 내 수전에 맞게 꼭 하나만 선택을 한다면 라이선스 이슈로 인해 8에서 11로 넘어가는 추세이기에 11 문서를 추천한다고 한다.

## String의 더하기 연산에 대한 비밀

String은 연산을 수행할 때마다 새로운 객체를 생성해낸다고 공부해왔다. 하지만 실제로는 컴파일러가 자동으로 <code>StringBuilder</code>로 최적화해주기 때문에 더하기 연산을 해도 새로운 객체가 생성하지 않는다. 단, <code>for</code>문 내부에서 일어나는 더하기 연산의 경우에는 컴파일러가 판단할 수 없다.

<code>StringBuilder, StringBuffer</code>의 <code>toString()</code> 메소드는 새로운 객체를 만들어준다.

## 내부 클래스의 메모리 누수?

- https://jade314.tistory.com/entry/%EB%82%B4%EB%B6%80innter%ED%81%B4%EB%9E%98%EC%8A%A4-%EC%A4%91%EC%B2%A9nested%ED%81%B4%EB%9E%98%EC%8A%A4-%EA%B7%B8%EB%A6%AC%EA%B3%A0-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%88%84%EC%88%98

이너클래스를 많이 사용하는 패턴이 데이터 전달하는 용도로 많이 사용함
외부에 어떤 노출을 해주는데 외부 클래스에 대한 참조를 유지하고 있어서 GC의 대상이 안딤 여기서 메모리의 누수가 발생할 수 있음
그래서 IDE에서 Static 워닝을 띄워주는 이유가 있음! 가능하면 안쓰는 것을 추천함


