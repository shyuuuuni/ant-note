# 객체지향 생활체조 원칙

> "소트웍스 엔솔러지" 라는 책에서 다룬 객체지향 프로그래밍을 잘 하기 위한 9가지 기본 원칙이다.

- [객체지향 생활체조 원칙](#객체지향-생활체조-원칙)
  - [1. 메소드 하나당 하나의 들여쓰기를 사용한다.](#1-메소드-하나당-하나의-들여쓰기를-사용한다)
  - [2. ELSE 키워드를 사용하지 않는다.](#2-else-키워드를-사용하지-않는다)
  - [3. Primitive 값들과 문자열을 객체로 포장한다.](#3-primitive-값들과-문자열을-객체로-포장한다)
  - [4. First Collection 을 사용한다.](#4-first-collection-을-사용한다)
  - [5. 한 줄에 한 점만 사용한다.](#5-한-줄에-한-점만-사용한다)
  - [6. 축약을 하지 않는다.](#6-축약을-하지-않는다)
  - [7. 모든 엔티티를 작게 유지한다.](#7-모든-엔티티를-작게-유지한다)
  - [8. 2개 이상의 인스턴스 변수를 가진 클래스를 사용하지 않는다.](#8-2개-이상의-인스턴스-변수를-가진-클래스를-사용하지-않는다)
  - [9. getter/setter/properties 를 사용하지 않는다.](#9-gettersetterproperties-를-사용하지-않는다)
  - [참고 문서](#참고-문서)

## 1. 메소드 하나당 하나의 들여쓰기를 사용한다.

한 메소드에서 하나의 기능을 수행하는 것이 좋다.

따라서 한가지 기능만 담당하도록 들여쓰기를 1단계만 존재하도록 코드를 분리한다.

```java
// 적용 전
class Board {
    // ...
    String board() {
        StringBuffer buf = new StringBuffer();

        // indent(0)
        for (int i = 0; i < 10; i++) {
            // indent(1)
            for (int j = 0; j < 10; j++) {
                // indent(2)
                buf.append(data[i][j]);
            }
            buf.append("\n");
        }
        return buf.toString();
    }
}

// 적용 후
class Board {
   // ...
    String board() {
        StringBuffer buf = new StringBuffer();
        collectRows(buf);
        return buf.toString();
   }

    void collectRows(StringBuffer buf) {
        // indent(0)
        for (int i = 0; i < 10; i++) {
            // indent(1)
            collectRow(buf, i);
        }
    }

    void collectRow(StringBuffer buf, int row) {
        for (int i = 0; i < 10; i++) {
            buf.append(data[row][i]);
        }
        buf.append("\n");
   }
}
```

## 2. ELSE 키워드를 사용하지 않는다.

여러 겹으로 중첩된 조건문(IF-ELSE)은 코드의 품질을 떨어뜨리게 된다.

따라서 Early Return 이나 변수를 사용하여 복잡한 조건문을 처리하는 것이 좋다.

```java
// 적용 전
public void endMe() {
    if (status == DONE) {
        doSomethingIfDone();
    } else {
        doSomethingElse();
    }
    return;
}

// 적용 후 (Early return)
public void endMe() {
    if (status == DONE) {
        doSomething();
        return;
    }
    doSomethingElse();
    return;
}
```

## 3. Primitive 값들과 문자열을 객체로 포장한다.

원시(primitive) 데이터들은 의미를 가지고 있지 않다.

해당 데이터들을 클래스 단위로 묶어서 사용하면 그 데이터가 무엇인지, 왜 사용해야 하는지 명확해진다.

```java
public class KakaoBankMoney {

    private final int money;

    public KakaoBankMoney(int money) {
        validMoney(money <= 0, "현금은 0원 이상이여야 합니다.");
        this.money = money;
    }

    // 조건에 따라 유효성을 검사하고 예외를 처리한다.
    private void validMoney(boolean expression, String exceptionMessage) {
        if (expression) {
            throw new IllegalArgumentException(exceptionMessage);
        }
    }

    // 의미가 없던 primitive 값이 행위를 가지도록 할 수 있다.
    public int getMoney() {
        return money;
    }
}
```

## 4. First Collection 을 사용한다.

**컬렉션을 가진 클래스는 컬렉션 외 다른 멤버 변수를 가지면 안된다.**

사람 객체 안에 사람의 이름과 소유중인 차량들을 가지고 있다고 가정해보자.

즉 사람 객체는 차량들을 리스트(Collection) 형태의 `cars` 멤버 변수로 가지고 있다.

여기서 `List<Car> cars`를 유일한 멤버 변수로 가지는 새로운 객체 `Cars`를 정의하자. 이렇게 정의한 Cars는 **하나의 콜렉션 멤버변수만 가지는데, 이를 일급 컬렉션 (First Collection)이라고 한다.**

이를 통해 컬렉션 관련 코드의 중복을 막고, 상태와 로직을 따로 관리하며 역할과 책임을 분리할 수 있고, 데이터의 캡슐화를 얻을 수 있다.

```java
// 변경 전 (Person(name,cars))
public class Person {
    private String name;
    private List<Car> cars;
}
public class Car {
    private String name;
    private String oil;
}


// 변경 후 (Person(name,cars), Cars(cars))
public class Person {
    private String name;
    private Cars cars;
}
public class Cars {
    // 콜렉션 멤버 변수만 가지는 객체로 선언한다.
    private List<Car> cars;
}

public class Car {
    private String name;
    private String oil;
}
```

## 5. 한 줄에 한 점만 사용한다.

객체가 너무 멀리 있는 객체를 불러와서 사용하는 것을 지양한다.

즉, 책임에 따라서 현재 객체에서 .(점) 하나만 사용하여 요청하는 방식으로 호출한다.

```java
// 적용 전
class Board {
    class Piece {
        String representation;
    }

    class Location {
        Piece current;
    }

    // 현재 메소드는 모든 Location에 대해 representation의 substring 메소드를 실행하는 책임을 가진다.
    // 즉 한 메소드가 너무 많은 책임을 가지고 있다.
    String boardRepresentation() {
        StringBuffer buf = new StringBuffer();
        for (Location l : squares()) {
            buf.append(l.current.representation.substring(0, 1));
        }
        return buf.toString();
    }
}

// 적용 후
class Board {
    class Piece {
        String representation;

        String character() {
            return representation.substring(0, 1);
        }

        void addTo(StringBuffer buf) {
            buf.append(character());
        }
    }

    class Location {
        Piece current;

        void addTo(StringBuffer buf) {
            current.addTo(buf);
        }

    }

    // representation의 substring을 처리하는 책임은 Piece의 책임이다.
    // 따라서 Location에서는 addTo라는 메소드로 단순히 호출하고, 그 책임은 Piece가 지도록 구현한다.
    // 이렇게 구현하면 자연스럽게 점이 하나만 사용된다.
    String boardRepresentation() {
        StringBuffer buf = new StringBuffer();
        for (Location l : squares()) {
            l.addTo(buf);
        }
        return buf.toString();
    }
}
```

## 6. 축약을 하지 않는다.

클래스, 메소드, 변수 등의 이름을 축약하지 않는다.

만약 이름을 지었을 때 너무 길다면 애초에 클래스나 메소드의 책임이 너무 많기 때문이다.

즉, 단일 책임 원칙에 위배되었으므로 변수를 축약할 필요가 생겼다고 볼 수 있다. 이를 수정하고 이름을 짓자.

```java
// 변경 전 (EName, KName 이라는 단어가 모호하다.)
public class NamePrinter {

    void printMyName() {
        String EName = "Shyuuuuni";
        String KName = "승현";
        // 출력
    }
}

// 변경 후
public class NamePrinter {

    // 메소드명도 중복되어 필요없는 My를 제거한다.
    void printName() {
        String englishName = "Shyuuuuni";
        String koreanName = "승현";
        // 출력
    }
}
```

## 7. 모든 엔티티를 작게 유지한다.

엄청나게 많은 클래스나 파일을 가진 패키지가 없도록 한다.

패키지도 클래스처럼 응집력 있고 단일 목표를 가지도록 유지한다.

## 8. 2개 이상의 인스턴스 변수를 가진 클래스를 사용하지 않는다.

많은 인스턴스를 가진 클래스가 응집력 있는 단일 작업을 진행하기 어렵다.

따라서 3번이나 4번 원칙과 같이 자료구조형으로 묶어 계층 구조로 분해하면 더 효율적인 객체 모델로 사용할 수 있다.

```java
// 변경 전
public class Person {

    // 인스턴스(기본형/자료구조형 변수)
    private final String name;
    private final String job;
    private final int age;

    public Jamie(String name, String job, int age) {
        this.name = name;
        this.job = job;
        this.age = age;
    }
}

// 변경 후
public class Person {

    // Wrapper 객체로 변경
    private final Name name;
    private final Job job;
    private final Age age;

    public Jamie(Name name, Job job, Age age) {
        this.name = name;
        this.job = job;
        this.age = age;
    }
}
```

## 9. getter/setter/properties 를 사용하지 않는다.

객체 바깥에서 객체의 상태를 가져와서 객체애 대한 결정을 내리는 것은 좋지 않다.

객체의 상태에 대한 결정은 그 객체 안에서 이루어지는 것이 좋다.

객체에 대한 메소드가 한곳에서 관리되므로 변경이 용이하고 중복 오류가 줄어든다.

## 참고 문서

https://jamie95.tistory.com/99

https://velog.io/@mohai2618/객체지향-생활-체조를-하는-이유

https://tecoble.techcourse.co.kr/post/2020-05-08-First-Class-Collection/
