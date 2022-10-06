# OAuth 2.0

Oauth 2.0에서는 일반적으로 다음 개념이 사용됨

- Resource Owner
    - 보호 자원에 대한 액세스 권한을 부여할 수 있는 엔티티
    - Resource Owner가 개인인 경우에는 `사용자`
- Oauth Client
    - Resource Owner의 개인용 자원에 액세스하려는 써드파티 애플리케이션
    - Resource Owner로부터 권한을 부여받은 후에는 Resource Owner 대신 보호 자원 요청 작성 가능
- Oauth Server
    - Oauth 2.0에서는 Resource Server라고 함
    - Resource Owner를 대신하여 Oauth Client에 보호 자원에 대한 범위 지정된 액세스 권한 부여
    - 아래 조치를 수행한 후 Oauth Clientdp 액세스 토큰 발급
        - Resource Owner 인증
        - 요청 또는 권한 부여 유효성 검증
        - Resource Owner 권한 획득
