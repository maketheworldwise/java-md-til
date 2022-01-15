## DTO 패턴 🤔

VO는 데이터를 담아두기 위한 용도로, DTO는 데이터를 다른 서버로 전달하는 용도로 사용한다는 점이 다르다. DTO가 VO를 포함한다고 볼 수 있기 때문에 대부분 DTO라는 명칭을 선호한다고 한다.

왜 사용할까? 메소드는 하나의 타입만 반환할 수 있도록 선언할 수 있다. 하지만 반환해야하는 값이 하나가 아닌 각각 다른 자료형을 가진 여러 개의 데이터라면 곤란해지는 상황이 발생한다. 이 때 사용하는 것이 DTO다.

## Overloading

오버로딩은 동일한 메소드명을 가지지만 매개 변수의 종류와 개수, 순서가 다르면 다른 메소드로 인식되어 지는 것을 의미한다.

대표적으로 <code>System.out.println()</code> 메소드 처럼 어떤 자료형을 넘겨주어도 결과를 반환해주는데, 이것이 바로 오버로딩의 장점이다.