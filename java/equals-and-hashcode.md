# equals & hashCode

- equals
    - 두 객체의 내용이 같은지 확인하는 method
    - Value Object의 비교를 하려면 equals() override 필요
- hashCode
    - 두 객체가 같은 객체인지 확인하는 method
    - override하지 않으면 native method call하여 주솟값을 가지고 hash 값을 만듬
    - 즉 두 객체의 reference가 다르고 hashCode가 override 되어 있지 않다면 절대 같은 값이 나오지 않음
- 요점
    - Hash function을 사용하는 Collection(HashMap, HashTable, HashSet, LinkedHashSet, ...)은 key를 결정할 때 hashCode() 사용
    - HashMap 등의 Collection에서 equals() 결과가 true인 객체 간 key duplicate issue가 있음 (hashCode()의 결과가 다르기 때문)
- 결론
    - equals()를 override한다면 side effect를 줄이기 위해 hashCode()도 override하는 게 좋음