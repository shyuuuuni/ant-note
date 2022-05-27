# JAVA 8 변경 사항

> Modern Java 라고 불리는 Java 8의 변경사항들에 대해 간단히 알아보자.

- [JAVA 8 변경 사항](#java-8-변경-사항)
  - [1. interface](#1-interface)
    - [변경 전](#변경-전)
    - [변경 후](#변경-후)
  - [2. Functional interface & Lambda](#2-functional-interface--lambda)
    - [변경 전](#변경-전-1)
    - [변경 후](#변경-후-1)
  - [3. Stream](#3-stream)
  - [4. java.time](#4-javatime)
    - [변경 전](#변경-전-2)
    - [변경 후](#변경-후-2)
  - [5. 나즈혼 (Nashorn)](#5-나즈혼-nashorn)

## 1. interface

### 변경 전

Java 8 이전까지는 interface에서 public abstract methods만 허용했다.

### 변경 후

Java 8 부터는 interface에서 static과 default 메서드를 사용할 수 있다.

```java
public interface MyInterface {
    static String hi() {
        return "Hi";
    }
    default String hello() {
        return "Hello";
    }
}
```

## 2. Functional interface & Lambda

### 변경 전

Java 8 이전에서는 함수형 프로그래밍의 조건인 함수가 First-class가 아니였다. 자세히 말하면,

- 값을 할당 할 수 있어야 한다.
- 함수의 파라미터로 넘겨줄 수 있어야 한다.
- 함수의 반환값이 될 수 있어야 한다.

라는 조건을 모두 만족하지 않았다. 따라서 이전까지는 함수형 프로그래밍을 지원하지 않았다.

### 변경 후

Java 8 이후에 달라진 점으로 람다식 문법을 제공하는 것과, 함수형 인터페이스를 제공하는 부분이 있다.

먼저 함수형 인터페이스를 알아보자.

함수형 인터페이스는 `@FunctionalInterface`라는 어노테이션으로 선언되어 있는 하나의 추상 메소드만 가지고 있는 인터페이스를 의미한다.

```java
@FunctionalInterface
interface Calculation {
  int calculate(final int num1, final int num2);
}
```

다음으로 람다식을 알아보자.

람다식은 함수형 인터페이스를 간단하게 표현할 수 있는 방법을 제공한다. 기본적인 형태는 다음과 같다

```
(파라미터1, 파라미터2, ...) -> {
    함수 body
}
```

이렇게 작성한 람다식 자체가 함수형 인터페이스와 같은 역할을 할 수 있다.

람다식과 함수형 인터페이스에 대해서는 추후 자세히 포스팅 할 예정이다.

## 3. Stream

Java 8부터는 ArrayList와 같은 여러 데이터가 있는 객체에 대해서 각 데이터에 연속적으로 처리를 할 수 있도록 스트림을 제공한다.

Stream 기능을 제공하는 기능을 Stream API 라고 하며, 앞서 설명한 함수형 인터페이스를 적용하여 사용할 수 있다.

예를 들어 이전까지 리스트 값 하나하나에 접근하여 조건을 만족하면 로직을 실행시키는 구현을 다음과 같은 형태로 진행했다.

```java
// intList : Integer 리스트
for (Integer element : intList) {
    if (/* condition */) {
        /* login */
    }
}
...
```

Java의 스트림을 사용하면 더 간단하고 가독성있는 코드를 작성할 수 있다.

```java
intList.stream()
       .filter(/* condition */)
       .map(/* login */)
       ...
```

이러한 Stream API 는 시작연산(stream), 중간연산(filter), 최종연산(map)와 같은 세가지 연산이 존재한다.

## 4. java.time

### 변경 전

이전까지는 `Date, Calendar, SimpleDateFormatter` 등을 이용해 시간을 처리했지만, 많은 단점들을 가지고 있어서 현재는 대부분 `Deprecated` 상태이다.

### 변경 후

위의 단점을 해결하기 위해 Java 8 이후부터는 날짜 및 시간을 처리하기 위해 `java.time` 패키지에서 여러 기능을 제공한다.

- `java.time.chrono` : ISO-8601에 정의된 표준 달력 이외의 달력 시스템을 사용할 때 필요한 클래스들

* `java.time.format` : 날짜와 시간에 대한 데이터를 구문분석하고 형식화하는 데 사용되는 클래스들

- `java.time.temporal` : 날짜와 시간에 대한 데이터를 연산하는 데 사용되는 보조 클래스들

- `java.time.zone` : 타임 존(time-zone)과 관련된 클래스들

## 5. 나즈혼 (Nashorn)

기존 자바스크립트 엔진이였던 리노(Rinho)를 대체하는 새로운 자바스크립트 엔진 나즈혼(Nashorn)을 적용했다.

기존 엔진에 비해 성능 및 메모리 관리 측면에서 발전이 있었고, 자바 객체를 호출할 수 있도록 하는 특징이 있다.
