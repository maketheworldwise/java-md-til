## JVM 이란 뭘까?

JVM은 바이트 코드를 실행하는 환경이다. OS 위에 JVM이 있고, 그 위에 프로그램이 올라가기 때문에 메모리, 프로세스 등 모든 환경을 관리해준다는 특징을 가지고 있다.

- [자바의 동작 구조를 알아보자](https://velog.io/@maketheworldwise/%EC%9E%90%EB%B0%94%EC%9D%98-%EB%8F%99%EC%9E%91-%EA%B5%AC%EC%A1%B0%EB%A5%BC-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90)
- https://docs.oracle.com/javase/specs/index.html

## GC는 뭘까?

GC에 대한 알고리즘에 대한 내용은 이론적으로 어떤 형태로 동작하는지 알아야 한다. GC는 참조값이 있는지 없는지에 대한 여부로 판단해서 지워주게 되는데, 문제는 GC가 동작할 때 멈추게되는 단점이 있다.

왜 멈추게 될까? 그 이유는 알고리즘상에서 GC의 특정 포인트에서 멈추게 하기 때문이다. 

이 이유에 대한 유사한 개념으로는 디스크 조각 모음이 있다. 디스크 조각 모음과 마찬가지로 메모리도 객체를 계속 할당할 때 공간이 부족하면 쪼개서 넣거나 한번에 들어갈 수 있는 공간을 만들어주기 위한 조각 모음을 수행한다. 여기서 알아야하는 점은 쪼개서 넣는 방식으로 수행할 경우에는 여러 개의 참조값을 가르켜야하기 때문에 비효율적인 구조가 된다. 따라서 GC도 쪼개서 넣는 방식이 아닌 공간을 만들어주기 위한 조각 모음을 수행하는데, 그 시점에 객체를 사용하는 것을 바뀌면 안되기에 Stop-the-world를 발생시키게 된다.

자바 개발자라면 GC가 Stop-the-world를 왜 발생시키고 왜 발생해야하는지 알아야 하고 각 알고리즘의 차이점 정도로만 개념을 이해하고 넘어가는게 좋다. GC가 중요한 이유는, 실무에서 GC 튜닝을 통해 서버를 늘려 비용을 올리지 않고도 비용 절감의 효과와 트래픽상에서의 긍정적인 효과를 가지기 때문에 반드시 알아둬야 한다.

- [가비지 컬렉터는 뭘까?](https://velog.io/@maketheworldwise/%EA%B0%80%EB%B9%84%EC%A7%80-%EC%BB%AC%EB%A0%89%ED%84%B0%EB%8A%94-%EB%AD%98%EA%B9%8C)
- [가비지 컬렉터는 뭘까? (정리)](https://velog.io/@maketheworldwise/%EA%B0%80%EB%B9%84%EC%A7%80-%EC%BB%AC%EB%A0%89%ED%84%B0%EB%8A%94-%EB%AD%98%EA%B9%8C-%EC%A0%95%EB%A6%AC)
- [가비지 컬렉터 종류](https://velog.io/@maketheworldwise/%EA%B0%80%EB%B9%84%EC%A7%80-%EC%BB%AC%EB%A0%89%ED%84%B0-%EC%A2%85%EB%A5%98)

## 스레드 세이프는 뭘까?

하나의 function이 한 Thread로 부터 호출되어 실행 중일 때,
다른 Thread가 동일한 함수를 호출하여 동시에 실행되더라도
각 Thread에서 함수의 수행 결과가 바르게 나오는 것을 의미한다.

## 스레드의 상태값

- NEW: 스레드가 생성되었지만 아직 실행되지 않은 상태
- RUNNABLE: 현재 CPU를 점유하고 작업을 수행 중인 상태. 운영체제의 자원 분배로 인해 WAITING 상태가 될 수도 있다.
- BLOCKED: Monitor를 획득하기 위해 다른 스레드가 락을 해제하기를 기다리는 상태
- WAITING: <code>wait()</code> 메서드, <code>join()</code> 메서드, <code>park()</code> 메서드 등를 이용해 대기하고 있는 상태
- TIMED_WAITING: <code>sleep()</code> 메서드, <code>wait()</code> 메서드, <code>join()</code> 메서드, <code>park()</code> 메서드 등을 이용해 대기하고 있는 상태. WAITING 상태와의 차이점은 메서드의 인수로 최대 대기 시간을 명시할 수 있어 외부적인 변화뿐만 아니라 시간에 의해서도 WAITING 상태가 해제될 수 있다는 것이다.

## ConcurrentHashMap

- [ConcurrentHashMap?](https://velog.io/@maketheworldwise/ConcurrentHashMap)
