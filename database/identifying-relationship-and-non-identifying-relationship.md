# Identifying Relationship & Non-Identifying Relationship

1. Identifying Relationship
    - 부모 테이블의 기본키 또는 복합키가 자식 테이블의 기본키 또는 복합키의 구성원으로 전이 (관계 종속)
    - 데이터의 정합성 유지를 Database에서 한 번 더 할 수 있다
    - 요구사항이 변경되었을 경우 구조 변경이 어렵다

2. Non-Identifying Relationship
    - 부모 테이블의 기본키 또는 복합키가 자식 테이블의 일반 속성 그룹의 구성원으로 전이
    - 변경되는 요구사항을 유동적으로 수용할 수 있다
    - 부모 데이터와 독립적인 자식 데이터를 생성할 수 있다
    - 데이터 무결성을 보장하지 않는다
    - 데이터 정합성을 지키기 위해서는 별도의 비즈니스 로직이 필요하다