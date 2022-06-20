# 싱글톤 컨테이너

- [싱글톤 컨테이너](#싱글톤-컨테이너)
  - [문제상황](#문제상황)
  - [싱글톤 패턴](#싱글톤-패턴)
  - [싱글톤 컨테이너](#싱글톤-컨테이너-1)
    - [동시성 문제](#동시성-문제)
  - [`@Configuration` 과 싱글톤](#configuration-과-싱글톤)
    - [CGLIB](#cglib)
  - [래퍼런스](#래퍼런스)

## 문제상황

스프링 MVC에서 DI(Dependency Injection) 컨테이너(설정 파일)은 요청을 보내면 그에 맞는 객체 인스턴스를 반환해준다.

즉 요청에 맞는 스프링 빈을 반환한다.

하지만 스프링 MVC는 기본적으로 웹 애플리케이션을 위한 프레임워크이므로 **여러개의 요청이 동시에 입력**될 수 있다.

추가적인 처리가 되지 않는다면 위와 같이 여러 요청이 들어올 경우 각 요청마다 스프링 빈을 생성하여 반환할 것이다.

이럴 경우 **메모리 누수가 발생하고 성능이 저하**될 수 있다.

## 싱글톤 패턴

디자인 패턴 중, **클래스의 인스턴스가 하나만 존재하도록 보장**하는 디자인 패턴을 싱글톤 패턴이라고 한다.

싱글톤 패턴이 적용된 경우 임의로 추가적인 인스턴스 생성이 불가능하므로 위에서 설명한 여러개의 인스턴스를 생성하는 문제를 막을 수 있다.

그러나 싱글톤 패턴은 아래와 같은 단점이 존재한다.

- 싱글톤 패턴 구현을 위한 긴 코드가 요구된다.
- 의존관계상 클라이언트가 구현체 클래스에 의존한다. (DIP 위반, OCP 위반 가능성)
- 테스트가 어려워진다.
- 생성자를 이용한 내부 속성 초기화 등이 어려워진다.
- private 생성자를 이용한 자식 클래스 생성이 어려워진다.
- 클래스의 유연성이 떨어진다.

## 싱글톤 컨테이너

스프링에서 싱글톤 패턴을 적용하면서 앞서 설명한 싱글톤 패턴의 문제점을 해결하였다.

- **싱글톤 레지스트리**: 스프링 빈 객체를 싱글톤으로 생성하고 관리하는 역할을 하는 스프링의 기능.
- 어떤 요청이 들어와도 스프링 컨테이너는 싱글톤으로 관리하고 있는 스프링 빈 객체를 반환할 수 있다.

그러나 싱글톤 패턴이 항상 유효한 것은 아니다.

### 동시성 문제

싱글톤 패턴은 결국 하나의 인스턴스를 사용하는 것이기 때문에 여러 스레드에서 사용할 때 문제가 발생할 수 있다.

싱글톤 인스턴스는 전역으로 관리되므로 멀티 스레드 환경에서 동시성 문제가 발생할 수 있다.

그래서 동시성 문제를 예방하도록 코드를 작성해야 한다.

또는 코드를 무상태성(Stateless) 으로 작성해야 한다.

- 즉, 특정 클라이언트에 의존하여 인스턴스 내부의 값을 변경하지 않도록 한다.
- 가급적 읽기만 가능하도록 구현한다.
- 만약 데이터가 필요하면 자바에서 공유되지 않는 지역변수, 파라미터, ThreadLocal 등을 사용한다.

## `@Configuration` 과 싱글톤

일반적으로 `@Configuration` 어노테이션을 붙인 스프링 설정 파일에서 의존관계를 주입할 때 `new myService()` 등 생성자를 사용하여 다른 스프링 빈의 생성자의 파라미터로 넘겨준다.

그러나 아래와 같은 코드를 살펴보자.

```java
@Configuration
public class AppConfig {
  @Bean
  public MyRepository myRepository {
      return new MyRepository(new CommonService());
  }

  @Bean
  public YourRepository yourRepository {
      return new YourRepository(new CommonService());
  }
}
```

위 스프링 설정 파일에서 `MyRepository`와 `YourRepository`를 스프링 빈에 등록하고 있다.

두 스프링 빈 모두 `new CommonService()`라는 생성자를 이용하여 의존관계를 주입받고 있는데, 이러면 서로 다른 인스턴스가 생성되어 입력되지 않을까 라는 의문이 생긴다.

**결과적으로는 동일한 `CommonService` 인스턴스가 주입된다.**

### CGLIB

`CGLIB`는 바이트코드를 조작해서 동적으로 클래스를 생성하는 기술을 제공하는 라이브러리이다.

`@Configuration` 어노테이션이 붙은 클래스가 실제로는 `CGLIB` 라이브러리가 작동하여 싱글톤 패턴이 적용되는 클래스로 변경시킨다.

- 만약 호출한 메소드(`new CommonService()`)가 스프링 빈으로 등록되어 있다면 스프링 컨테이너에서 가져와서 대신 주입한다.
- 그렇지 않다면 기존 로직대로 주입한다.

따라서 스프링 설정파일에서 제공하는 의존관계 주입 또한 싱글톤 패턴을 유지할 수 있다.

**참고**

만약 `@Configuration` 대신 `@Bean` 어노테이션만을 이용하여 스프링 빈에 등록한다면?

`@Configuration` 어노테이션에서만 `CGLIB` 라이브러리가 작동하므로 싱글톤을 보장하지 못할 것이다.

## 래퍼런스

https://www.inflearn.com/course/스프링-핵심-원리-기본편