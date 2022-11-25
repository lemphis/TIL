# HashMap

HashMap 자체의 source code는 Oracle JDK, OpenJDK 둘 다 같다.  
HaspMap은 Java Collection Framework에 속한 구현체 클래스이다.  
Java Collection Framework는 1998년 12월에 발표한 Java 2에서 정식으로 선보였다.  
Map interface 자체는 Java 5에서 Generic이 적용된 것 외에 처음 선보인 이후 변화가 없지만 HashMap 구현체는 성능을 향상시키기 위해 지속적으로 변화해 왔다.

해시 충돌이 발생하더라도 key-value 데이터를 잘 저장하고 조회할 수 있게 하는 방식에는 대표적으로 `Open Addressing`,`Separate Chaining`이다.  
이 둘 외에도 해시 충돌을 해결하기 위한 다양한 자료 구조가 있지만 거의 모두 이 둘을 응용한 방식이다.
Java HashMap에서 사용하는 방식은 Separate Chaining이다.

Java 8부터는 데이터의 개수가 많아지면 Separate Chaining에서 LinkedList 대신 Tree를 사용한다.