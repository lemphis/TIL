# OAuth2ClientAutoConfiguration

Spring boot 2.x에서 OAuth client의 자동 설정을 지원하는 class는 `OAuth2ClientAutoConfiguration`

이 class는 다음과 같은 일을 한다:

- `OAuth2ClientRegistrationRepositoryConfiguration`: 설정한 OAuth client property로 `ClientRegistration`을 가지고 있는(여러 개
  가능) `ClientRegistrationRepository` `@Bean`을 등록함
- `OAuth2WebSecurityConfiguration`: `WebSecurityConfigurerAdapter` `@Configuration`을 제공하고 `httpSecurity.oauth2Login()`으로
  OAuth 2.0 login을 활성화함
