## 프로세스와 스레드?

프로세스는 운영체제로부터 자원을 할당받은 작업의 단위이며, 스레드는 프로세스가 할당받은 자원을 이용하는 실행 흐름의 단위를 의미한다.

- [프로세스와 스레드](https://velog.io/@maketheworldwise/%EC%9E%90%EB%B0%94%EC%9D%98-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4%EC%99%80-%EC%8A%A4%EB%A0%88%EB%93%9C)
- [멀티 프로세싱, 멀티 스레드, 멀티*](https://velog.io/@maketheworldwise/%EB%A9%80%ED%8B%B0-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8B%B1-%EB%A9%80%ED%8B%B0-%EC%8A%A4%EB%A0%88%EB%93%9C-%EB%A9%80%ED%8B%B0)

## 레이스 컨디션? 

레이스 컨디션은 두 개 이상의 프로세스 혹은 스레드가 공유 자원을 서로 사용하려고 경합(Race)하는 현상을 의미한다. 

- [레이스 컨디션 그게 뭐야?](https://velog.io/@maketheworldwise/%EB%A0%88%EC%9D%B4%EC%8A%A4-%EC%BB%A8%EB%94%94%EC%85%98-%EA%B7%B8%EA%B2%8C-%EB%AD%90%EC%95%BC)

## String 선언 방식의 차이 (+ .equals와 ==의 차이)

String을 선언하는 방식은 <code>new</code> 예약어를 이용한 선언 방식과 ""를 이용한 선언 방식이 있다. 

**"String은 변하지 않는다"** 는 특징을 가지고 있기에 <code>new</code> 예약어를 이용한 방식의 경우 새로운 객체를 만들어 메모리 관리가 비효율적이라면, 리터럴을 이용한 방식은 String Pool을 이용하기 때문에 메모리 관리 측면에서 효율적으로 운영할 수 있다는 점에서 차이가 있다.

- [String에 대해 알아보자!](https://velog.io/@maketheworldwise/String%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90)

## Float, Double, 부동소수점

실수를 표현하는 방법은 고정 소수점 방식과 부동 소수점 방식이 있다. 정확도는 고정 소수점 방식이 높지만 대부분의 컴퓨터는 부동 소수점 방식을 이용한다.

따라서 금융 계산과 같은 정확한 결과를 원할경우 <code>BigDecimal, int long</code>을 사용하는 편이 좋다.

- [float, double, 부동 소수점](https://velog.io/@maketheworldwise/float-double-%EB%B6%80%EB%8F%99%EC%86%8C%EC%88%98%EC%A0%90)

## 상태와 행동의 관계?

## 상태의 단점?



