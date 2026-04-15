## Spring MVC
Spring 프레임워크에서 웹 애플리케이션을 구축하기 위해 제공하는 핵심 모듈로, 애플리케이션을 **Model(모델)**,  **View(뷰)**, **Controller(컨트롤러)** 세 가지 역할로 명확히 분리하여 개발하는 디자인 패턴이다. <br>
이 패턴의 핵심은 사용자 인터페이스와 비즈니스 로직을 분리하여 서로 영향 없이 독립적으로 개발, 테스트, 유지보수할 수 있게 만드는 것이다.

Spring MVC는 Front Controller 패턴을 기반으로 한다.<br>
모든 요청이 하나의 DispatcherServlet응ㄹ 통해 들어오고, 이를 각 전문 컴포넌트가 나누어 처리하는 구조이다.
- **DispatcherServlet:** 서블릿 컨테이너에서 들어오는 모든 HTTP 요청을 가장 먼저 받는 진입점으로 전체적인 흐름을 제어하며 각 단계에서 필요한 컴포넌트를 호출한다.
- **HandlerMapping:** 요청 URL과 HTTP 메서드에 매핑된 컨트롤러를 찾아주는 전략 인터페이스이다. <br>주로 ```@RequestMapping``` 어노테이션 정보를 기반으로 탐색한다.
- **HandlerAdapter:** 찾아낸 컨트롤러를 실제로 실행할 수 있게 해주는 인터페이스이다.<br> 다양한 형태의 컨트롤러를 실행할 수 있도록 유연성을 제공한다.
- **Controller:** 실제 비즈니스 로직이 시작되는 곳이다. <br> 사용자 요청을 해석하고 서비스 계층을 호출한 후, 그 결과를 모델에 담거나 응답 데이터를 생성한다.
- **ModelAndView:** 컨트롤러가 처리한 데이터와 화면을 그릴 뷰 이름을 함께 전달하는 객체이다.
- **ViewResolver:** 컨트롤러가 반환한 논리적인 뷰 이름에 실제 물리적인 경로로 변환해준다.

사용자의 요청이 들어와서 응답이 나갈 때까지의 내부 메커니즘은 다음과 같다.
- **Request 수신:** 클라이언트의 HTTP 요청이 DispatcherServlet에 도착한다.
- **Handler 조회:** DispatcherServlet은 HandlerMapping을 통해 해당 요청을 처리할 컨트롤러를 조회한다.<br> 이때 컨트롤러를 감싼 `HandlerExecutionChain`이 반환된다.
- **Adapter 조회:** 해당 컨트롤러를 실행할 수 있는 HandlerAdapter를 결정한다.
- **Handler 실행:** Adapter가 컨트롤러의 메서드를 호출하여 비즈니스 로직을 수행한다.
- **Return ModelAndView:** 컨트롤러가 비즈니스 결과를 담은 `ModelAndView` 객체를 Adapter를 통해 DispatcherServlet에 반환한다.<br>
  (현대적인 REST API 경우 `@ResponseBody`를 통해 객체를 직접 반환하기도 한다.)
<br>

<br>

**Controller**<br>
사용자의 HTTP요청을 가장 먼저 받는 진입점이다.<br>
요청에 필요한 파라미터를 검증하고, 해당 요청을 처리할 수 있는 Service를 호출, 이후 처리 결과를 클라이언트에게 어떤 형식으로 보낼지 결정하는 역할이다.

**Service**<br>
실질적인 비즈니스 로직이 구현되는 곳이다.<br>
여러개의 데이터 수정 작업이 일어날 때 모두 성공하거나 모두 실패하도록 관리하는 트랜잭션의 단위가 되기도 한다.

**Repository**<br>
데이터베이스와 통신하는 인터페이스이다.<br>
실제 데이터베이스에 접근하여 데이터를 저장, 조회, 수정, 삭제하는 SQL 작업을 수행한다.<br>
(JPA 등을 사용할 때 DAO의 현대적인 이름으로 불리기도 한다.)

**Entity**<br>
실제 데이터베이스의 테이블과 1:1로 매핑되는 객체이다.<br>
데이터베이스의 스키마와 직접 연결되어 있으므로, 비즈니스 로직 외의 화면 표시용 데이터 등을 담는 용도로 사용해서는 안된다.<br>
시스템의 가장 핵심적인 모델이다.

**DTO**<br>
계층 간 데이터 교환을 위해 사용되는 객체이다.<br>
Controller가 Service로 데이터를 보낼 때 혹은 Service가 화면에 필요한 데이터만 뽑아서 Controller에게 줄 때 사용한다.<br>
보안상의 이유와 효율성 때문에 반드시 Entity와 분리하여 사용한다.
<br>

<br>

*데이터 흐름*
1. 클라이언트가 요청을 보낸다.
2. Controller가 요청을 받고, 데이터를 DTO에 담아 Service로 넘긴다.
3. Service는 비즈니스 로직을 수행하며 필요한 경우 Repository를 통해 데이터베이스에서 데이터를 가져온다.<br> 이 때 데이터베이스 데이터는 Entity 형태이다.
4. Service는 처리 결과물인 Entity를 다시 DTO로 변환하여 Controller에게 반환한다.
5. Controller는 최종 결과(DTO)를 클라이언트에게 응답한다.