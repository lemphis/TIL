# SecurityContextHolder

SecurityContextHolder에는 Spring Security로 인증한 사용자의 상세 정보를 저장함
SecurityContextHolder에 어떻게 값을 넣는지는 상관하지 않음
값이 있다면 현재 인증한 사용자 정보로 저장함

Setting SecurityContextHolder Example

```java
SecurityContext context = SecurityContextHolder.createEmptyContext(); // (1)
Authentication authentication = new TestingAuthenticationToken("username", "password", "ROLE_USER"); // (2)
context.setAuthentication(authentication);

SecurityContextHolder.setContext(context); // (3)
```

(1) 비어 있는 `SecurityContext`를 만드는 것으로 시작함. thread race condition을 피하려면 SecurityContextHolder.getContext()
.setAuthentication(authentication)을 사용해선 안 되며, 새 SecurityContext 인스턴스를 생성해야 함
(2) 새 Authentication 객체 생성. Authentication 구현체라면 모두 SecurityContext에 담을 수 있음. 여기서는 간단하게 TestingAuthenticationToken 사용.
production 환경에서는 `UsernamePasswordAuthenticationToken`(userDetails, password, authorities)를 주로 사용
(3) SecurityContextHolder에 SecurityContext를 설정함. Spring Security는 이 정보를 사용하여 권한을 인가함
