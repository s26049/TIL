## Spring Security
스프링 기반의 애플리케이션의 보안을 담당하는 프레임워크이다.

**필터**를 기반으로 동작하기 때문에 스프링 MVC와 분리되어 관리 및 동작한다.<br>
필터는 Dispatcher Servlet으로 가기 전에 적용되므로 가장 먼저 URL 요청을 받지만, Intercepter는 Dispatcher와 Controller 사이에 위치한다.<br>
그래서 이 둘은 적용 시기에 차이점이 있다.
<br>

**인증(Authentication)**<br>
사용자가 누구인지 확인(로그인)

**인가(Authorization)**<br>
인증된 사용자의 권한을 확인하여 특정 리소스에 대한 접근 제어