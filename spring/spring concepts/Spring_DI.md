# DI (Dependency Injection), 의존성 주입
의존성 주입은 제어의 역전 방법 중 하나로, **사용할 객체를 직접 생성하지 않고 외부 컨테이너가 생선한 객체를 주입받아 사용**하는 방식을 말한다.
<br>
IoC(제어의 역전)에서, 일반적으로 자바에서는

```java
@RestController
public class NoneDIController {
    private MyService = new MyServiceImpl();
}
```
이렇게 객체를 생성한다고 했었는데, <br>

스프링에서는 의존성 주입으로 직접 객체를 생성하지 않고 제어권을 스프링 컨테이너로 넘긴다.

#### 의존성 주입 방법 
의존법 주입 방법에서는 총 3개가 있다.
- 생성자를 통한 의존성 주입
- 필드 객체 선언을 통한 의존성 주입
- Setter를 통한 의존성 주입
 
 <br>

생성자를 통한 의존성 주입

```java
@RestController
public class DIConainer {
    MyService myService;

    @Autowired
    public DIController(MyService myService);
        this.myServoce = ;
}
```
생성자 이후 버전은 ```@Autowired``` 를 생략시킬 수 있다.
이 점을 이용하여 **롬북(Lombok)** 을 이용하여 아래와 같이 의존성 주입이 가능하다.

<br>

생성자주입
```java
@RestController
@RequiredArgsConstructor
public class DIController {
    private final MyService = MyService
}
```
결과적으로 위와 같은 방법이 가장 좋은 의존성 주입이라고 볼 수 있다.<br>

Lombok의 ```@RequiredArgsConstructor``` 어노테이션은 ```final```이 붙은 필드의 생성자를 자동으로 생성해 준다.