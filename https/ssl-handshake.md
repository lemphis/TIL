# SSL Handshake 과정

1. Client가 Server에 접속
   - 이 단계를 Client Hello라고 함
   - Client Hello 단계에서 주고 받는 정보
     1. Client 측에서 생성한 random data
     2. Client가 지원하는 암호화 방식
     3. Session ID
          - 이미 SSL Handshaking을 했다면 비용과 시간을 절약하기 위해 기존의 Session 재활용
          - 이 때 사용할 식별자를 Server 측으로 전송함
2. Server는 Client Hello에 대한 응답으로 Server Hello를 함
    - Server Hello 단계에서 주고 받는 정보
      1. Server 측에서 생성한 random data
      2. Server가 선택한 Client의 암호화 방식
          - Client가 전달한 암호화 방식 중에서 Server 쪽에서도 사용할 수 있는 암호화 방식을 선택하여 Client로 전달
          - 이로써 암호화 방식에 대한 협상이 종료
          - Server와 Client는 이 암호화 방식을 이용하여 정보를 교환하게 됨
      3. 인증서
3. Client는 Server가 보낸 인증서가 CA에 의해서 발급된 것인지를 확인하기 위해 Client에 내장된 CA list를 확인함
    - CA list에 인증서가 없다면 사용자에게 경고 메시지 출력
    - 인증서가 CA에 의해서 발급된 것인지를 확인하기 위해 Client에 내장된 CA의 공개키를 이용해서 인증서를 복호화
    - 복호화에 성공했다면 인증서는 CA의 개인키로 암호화된 문서임이 암시적으로 보증된 것
4. Client는 Client가 생성한 random data와 Server가 생성한 random data를 조합하여 pre master secret이라는 key를 생성
5. Client는 Server가 보낸 인증서에 포함된 공개키로 pre master secret값을 암호화해서 Server로 전송
6. Server는 Client가 전송한 pre master secret 값을 자신의 비공개키로 복호화
7. Client와 Server는 모두 일련의 과정을 거쳐서 pre master secret 값을 master secret 값으로 만듬
    - master secret은 session key를 생성
    - 생성한 session key 값을 이용하여 Server와 Client는 데이터를 대칭키 방식으로 암호화한 후 주고 받음
8. Client와 Server는 Handshake 단계의 종료를 서로에게 알림