# CommonOAuth2Provider

`CommonOauth2Provider`는 유명한 provider인 Google, Github, Facebook, Okta 전용 default client property가 미리 정의되어 있는 enum class
예를 들어 provider의 authorization-uri, token-uri, user-info-uri는 자주 변경되는 값이 아님  
따라서 default 값을 제공하여 필요한 설정을 줄이는 게 바람직함

다음은 Google client 설정 예시임

```yml
spring:
  security:
    oauth2:
      client:
        registration:
          google:
            client-id: google-client-id
            client-secret: google-client-secret
```

여기서는 client property가 자동으로 default 값으로 들어가는데, `registrationId(google)`가 `CommonOAuth2Provider`에 있는 `GOOGLE enum`과 일치하기 때문임(대소문자 구분 X)

`google-login`등 다른 registrationId를 지정할 때에도 provider property를 설정하면 해당하는 default 값이 자동으로 들어가게 할 수 있음

예를 들어

```yml
spring:
  security:
    oauth2:
      client:
        registration:
          google-login:  # (1)
            provider: google  # (2)
            client-id: google-client-id
            client-secret: google-client-secret
```

(1) `registrationId를` `google-login`으로 설정함  
(2) `provider` property를 `google`로 설정하면 `CommonOAuth2Provider.GOOGLE.getBuilder()`에 있는 default client property가 자동으로 설정됨
