# Annotation

### Annotation 기본 개념
Java에서 어노테이션과 Spring Boot에서 사용하는 어노테이션은 기본 개념은 같지만 사용되는 목적과 방식에서의 차이가 있다.<br>

**Java에서 어노테이션**은 메타데이터(metadata)의 일종으로 클래스, 메서드, 변수 등에 부가적인 정보를 제공하는 역할을 한다.<br>
어노테이션 자체는 프로그램 로직에 영향을 주지 않지만 런타임이나 컴파일 타임에 특정 처리를 수행할 수 있도록 도와주는 역할을 한다.<br>

**Spring Boot의 어노테이션**은 Java 어노테이션을 활용하여 빈 관리, 의존성 주입, 트랜잭션 관리 등 다양한 기능을 자동으로 처리한다. <br>
Spring Boot에서는 어노테이션을 통해 설정을 최소화하고 자동화를 구현하는 것이 큰 특징이다.

<br>
<br>

**주요 어노테이션**<br>
- `@Component`, `@Service`, `@Repository`→ Spring이 객체를 자동으로 관리
- `@Autowired`, `@Qualifier` → 의존성 주입(DI)
- `@GetMapping`, `@PostMapping` → 요청 처리
- `@Transactional` → 트랜잭션 관리

<br>

### Annotation 역할
<br>

- 설정 역할 (Configuration): XML 설정 없이 어노테이션만으로 설정 가능
- 자동화 역할 (Auto-wiring): `@Autowired`를 사용해 의존성 자동 주입
- 행동 제어 역할 (Behavior): `@Transactional`, `@Cacheable` 같은 어노테이션으로 기능 추가
- 메타데이터 제공 역할: 코드가 어떤 의미를 가지는지 설명 <br>
(ex. `@Override`는 메서드 재정의 표시)

<br>
<br>

**Spring의 기본 어노테이션**<br>
`@Component`: Spring이 관리하는 일반적인 객체를 정의한다.<br>
`@Controller`: MVC에서 컨트롤러 역할을 하는 클래스 지정한다.<br>
`@Service`: 서비스 역할을 하는 클래스 지정(비즈니스 로직)한다.<br>
`@Repository`: 데이터베이스 관련 작업을 하는 클래스 지정한다. <br>

<br>

**의존성 주입 관련 어노테이션**<br>
`@Autowired`: 필요한 객체를 자동으로 주입(DI)한다.<br>
`@Qualifier`: 주입할 객체를 특정 이름으로 지정한다.<br>
`@Inject`: `@Autowired`와 같은 역할을 한다.<br>
`Value`: application.properties의 값을 주입한다.<br>

<br>

**요청 매핑 관련 어노테이션**<br>
`@RequestMapping`: 특정 URL과 메서드를 연결한다.<br>
`@GetMapping`: GET 요청을 처리한다.<br>
`@PostMapping`: POST 요청을 처리한다.<br>
`@PutMapping`: PUT 요청을 처리한다.<br>
`@DeleteMapping`: DELETE 요청을 처리한다.<br>

<br>

**트랜잭션 관련 어노테이션**<br>
`@Transactional`: 트랜잭션을 관리하여 오류 발생 시 자동 롤백한다.<br>

<br>

**기타 유용한 어노테이션**<br>
`@RestController`: `@Controller` + `@ResponseBody` (JSON 반환)<br>
`@ResponseBody`: 메서드의 반환값을 JSON으로 변환한다.<br>
`@PathVariable`: URL 경로 변수 값을 가져온다.<br>
`@RequestParam`: GET 또는 POST 요청의 파라미터 값을 가져온다.<br>
`@ExceptionHandler`: 예외가 발생했을 때 특정 메서드에서 처리한다. <br>