# IoC (Inversion of Control), 제어의 역전
Ioc는 사용할 객체를 **직접 생성하지 않고**, 객체의 생명주기 관리를 **외부(스프링 컨테이너)에 위임**하는 것이다.

일반적으로 자바에서 객체는 아래와 같이 생성한다. <br>
```java
@RestController
public class NoneDIController {
    private MyService service = new MyServiceImpl();
}
```
위와 같이 객체를 직접 생선한 뒤 그 객체에서 제공하는 기능을 사용한다. <br>
즉, 객체를 생성하고 작업을 개발자가 직접 제어하는 것이다.

그러나 스프링은 기본적으로 제어 역전(IoC)을 이용하여 **개발자가 직접 객체를 생성하고 않고**, 객체의 생명주기 관리를 **외부에 위임**한다.<br>
여기서 **외부**란 스프링에서 관리하는 Spring Container 또는 IoC Container 라고 한다. <br>
이렇게 객체의 관리를 컨테이너에 맡겨 제어권이 넘어간 것을 **제어의 역전**이라고 부른다. <br>

제어의 역전을 통해 **의존성 주입(DI: Dependency Injection), 관점 지향 프로그래밍(AOP: Aspect-Oriented-Programming)**이 가능해진다. <br>
이에 따라 개발자는 객체의 제어권을 컨테이너로 넘기고 객체의 생명 주기 관리 등의 복잡한 요소들을 신경쓰지 않고 비즈니스 로직에만 집중할 수 있다.