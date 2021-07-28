# Spring Security Architecture

- SecurityContextHolder
  - SecurityContext 제공
  - 기본적으로 ThreadLocal 사용
- SecurityContext
  - Authentication 제공
- Authentication
  - Principal과 GrantAuthority 제공
- Principal
  - `누구`에 해당하는 정보
  - UserDetailsService 구현체의 loadUserByUsername method에서 return한 객체
- GrantAuthority
  - ROLE_USER, ROLE_ADMIN 등 Principal이 가지고 있는 `권한`을 나타냄
  - 인증 이후 인가 및 권한 확인할 때 이 정보를 참조
- UserDetails
  - 애플리케이션이 가지고 있는 유저 정보와 Spring Security가 사용하는 Authentication 객체 사이의 Adapter
- UserDetailsService
  - 유저 정보를 UserDetails 타입으로 가져오는 DAO interface
