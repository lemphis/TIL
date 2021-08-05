# Authentication

Spring Security에서 `Authentication`이 주로 담당하는 일은 다음과 같음

- `AuthenticationManager`의 입력으로 사용되어, 인증에 사용할 사용자의 크리덴셜을 제공함
- 이 상황에서는 `isAuthenticated()`는 `false`를 return함
- 현재 인증된 사용자를 나타냄. 현재 Authentication은 SecurityContext에서 가져올 수 있음

Authentication은 다음과 같은 정보를 가지고 있음

- `principal` - 사용자를 식별함. 사용자 이름, 비밀번호로 인증할 때 보통 `UserDetails` 인스턴스임
- `credentials` - 주로 비밀번호. 대부분은 유출되지 않도록 사용자를 인증한 다음 비움
- `authorities` - 사용자에게 부여한 권한은 `GrantedAuthority`로 추상화함. 예시로 role이나 scope가 있음
