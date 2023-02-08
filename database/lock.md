# Lock

Lock이란 트랜잭션 처리의 순차성을 보장하기 위한 방법이다.  
Lock의 종류로는 `Shared Lock(Read Lock)`과 `Exclusive Lock(Write Lock)`이 있다.

- `Shared Lock`
    - 데이터를 읽을 때 사용되는 Lock
    - Shared Lock간 동시에 접근 가능
    - Shared Lock이 설정된 데이터에 Exclusive Lock을 사용할 수 없음
- `Exclusive Lock`
    - 데이터를 변경하고자 할 때 사용되는 Lock

## Lock의 설정 범위

- 데이터베이스
    - 전체 데이터베이스를 기준으로 lock
    - DB의 소프트웨어 버전을 올리는 등의 주요한 DB 업데이트 시 사용
- 파일
    - 데이터베이스 파일을 기준으로 lock
    - 잘 사용되지 않음
- 테이블
    - 테이블을 기준으로 lock
    - 테이블의 모든 행을 업데이트하는 등의 전체 테이블에 영향을 주는 변경을 수행할 때 사용
    - DDL 구문과 함께 사용되며 DDL Lock이라고도 함
- 페이지와 블록
    - 파일의 일부인 페이지와 블록을 기준으로 lock
    - 잘 사용되지 않음
- 컬럼
    - 컬럼을 기준으로 하는 lock
    - lock 설정 및 해제의 리소스가 많이 들어서 일반적으로 사용되지 않으며 지원하는 DBMS도 많지 않음
- 행(row)
    - 1개의 행(row)을 기준으로 lock
    - DML에 대해 가장 일반적으로 사용하는 lock