# DI 프레임워크 구현

## 페어 규칙
1. 미리 요구사항을 정해놓고 각자 학습/생각하는 시간을 가지기.
2. 일일 요구사항 명세를 정하고 실천하기.
3. 드라이버는 30분 간격으로 교체한다.
4. TDD로 할 수 있다면 최대한 적용한다.

## Step 1 구현
- `@Controller`, `@Service`, `@Repository` 클래스 스캔
    - 빈 주입시 Service가 다른 Service를 주입하는 경우 고려
    - `@Inject`가 없는 경우 기본생성자를 이용하여 빈으로 등록
    - 그 외 경우는 `initializeInjectedBeans()`로 빈 등록
- `@Inject`에 필요한 객체를 찾아서 주입 / 생성
- 기존의 `@Controller`를 스캔하는 ControllerScanner 클래스를 확장된 BeanScanner와 통합


## Step 2 구현
- `@Configuration` 어노테이션으로 빈 설정
    - `@ComponentScan`으로 패키지 스캔
    - `@Bena` 어노테이션이 선언된 메서드의 반환값을 빈으로 생성
- 빈 생성 과정
    - `@Configuration`을 찾고 `@ComponentScan`의 값을 `BeanScanner`에 전달하여 빈 생성
    - `@Configuration`도 빈으로 등록하여 내부의 `@Bean` 메서드 결과를 빈으로 등록한다.