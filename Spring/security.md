### 1. Spring Security
Spring기반의 애플리케이션의 보안을 담당하는 스프링 하위 프레임워크.
인증과 권한에 대한 부분을 Filter흐름에 따라 처리함.
Filter는 Dispatcher Servlet으로 가기 전 적용되어 가장 먼저 URL요청을 받지만 Interceptor는 Dispatcher와 Controller사이에 위치한다는 점에서 적용시기의 차이가 있다.

### 2. 특징
- filter기반으로 동작.
- 기본적으로는 세션&쿠키 방식으로 인증된다.
- dispatcher servlet이전에 처리된다.

### 3. 용어
- 인증(Authenticate) : 현재 유저가 누구인지 확인
- 인가(Authorize) : 현재 유저가 요청한 자원에 접근 가능한지 확인
- 접근 주체(Principal) : 자원에 접근하는 유저
- 비밀번호(Credential) : 자원에 접근하는 대상의 비밀번호

### 4. 동작 과정
![spring_security동작과정](https://user-images.githubusercontent.com/90902468/199498138-7295f2b2-81df-4420-be74-cea82d3e5fcf.png)


1) HTTP요청 수신(Http Request) 및 AuthenticationFilter 통과
2) 사용자 자격 증명을 기반으로 Authentication Token 
3) AuthenticationManager를 위해 생성된 AuthenticationToken 위임
4) AuthenticationProvider 목록으로 인증 시도
5) UserDetailsService
6) UserDetails
7) User<br>
: 일부 AuthenticationProvider는 사용자 이름을 기반으로 사용자 세부 정보를 검색하기 위해 UserDetailsService를 사용할 수 있다.
그 안에는 DB에 저자된 회원의 비밀번호와 비교해 일치하면 UserDatails 인터페이스를 구현한 객체를 반환한다.
8) 인증 실패시 AuthenticationException 발생 -> 인증메커니즘을 지원하는 AuthenticationEntryPoint에 의해 처리
9) 인증 완료
10) SecurityContext에서 인증 개체 설정
