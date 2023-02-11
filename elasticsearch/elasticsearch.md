# Elasticsearch

일래스틱서치(Elasticsearch)는 루씬 기반의 검색 엔진이다.
Elasticsearch는 모든 데이터를 색인하여 저장하고 검색, 집계 등을 수행하며 결과를 클라이언트 또는 다른 프로그램으로 전달하여 동작하게 한다.

Elasticsearch의 가장 큰 특징 중 하나는 실시간(real-time) 분석 시스템이다.  
Elasticsearch는 하둡 시스템과 달리 Elasticsearch 클러스터가 실행되고 있는 동안에는 계속해서 데이터가 입력되고, 그와 동시에 실시간에 가까운 속도로 색인된 데이터의 검색, 집계가 가능하다.

현재 대규모 시스템들은 대부분 MSA를 기본으로 설계된다.  
이러한 구조에 빠질 수 없는 것이 REST API와 같은 표준 인터페이스이다.  
Elasticsearch는 REST API를 기본으로 지원하며 모든 데이터 조회, 입력, 삭제를 HTTP 프로토콜을 통해 REST API로 처리한다.

Elasticsearch의 데이터들은 인덱스라는 논리적인 집합 단위로 구성되며 서로 다른 저장소에 분산되어 저장된다.  
서로 다른 인덱스들을 별도의 커넥션 없이 하나의 질의로 묶어서 검색하고, 검색 결과들을 하나의 출력으로 도출할 수 있다.  
Elasticsearch의 이러한 특징을 멀티테넌시(multi-tenancy)라고 한다.