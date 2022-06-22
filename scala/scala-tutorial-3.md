# Scala 튜토리얼 (3)

- [Scala 튜토리얼 (3)](#scala-튜토리얼-3)
  - [통합된 타입](#통합된-타입)
    - [AnyRef](#anyref)
    - [AnyVal](#anyval)
    - [타입 캐스팅](#타입-캐스팅)
    - [Nothing, Null](#nothing-null)
  - [클래스](#클래스)
    - [기본 파라미터 값](#기본-파라미터-값)
    - [이름을 지정한 파라미터](#이름을-지정한-파라미터)
  - [래퍼런스](#래퍼런스)

## 통합된 타입

![type](https://docs.scala-lang.org/resources/images/tour/unified-types-diagram.svg)

스칼라에서는 숫자 값과 함수 등 모든 값이 타입을 가지고 있으며, 모든 타입은 `Any` 라는 슈퍼 타입 아래 계층 구조로 구성된다.

이렇게 구성된 모든 타입들을 가진 값들은 모두 객체로 취급된다. (Scala가 객체지향인 이유이다.)

`Any`는 `AnyVal` 타입과 `AnyRef` 타입으로 구성된다.

### AnyRef

`AnyRef`는 이름에 `Ref`가 들어간 것 처럼, 참조 타입을 포함한다.

참조 타입에는 값 타입이 아닌 모든 타입이 포함되며, Java와 함께 사용 될 경우 `AnyRef`는 `java.lang.Object`에 매핑된다.

### AnyVal

`AnyVal`은 이름에 `Val`이 들어간 것 처럼, 값 타입을 포함한다.

`Double, Float, Long, Int, Short, Byte, Char, Unit, Boolean` 의 기본 타입들이 여기에 포함되며, 이러한 타입들은 `Null`을 가질 수 없다.

### 타입 캐스팅

![cast](https://docs.scala-lang.org/resources/images/tour/type-casting-diagram.svg)

값 타입은 위와 같이 타입을 변환할 수 있다.

- 캐스팅은 단방향이다.
- 잘못된 캐스팅은 컴파일 오류를 발생시킨다.

### Nothing, Null

계층 구조 이미지에서, 가장 아랫쪽에 있는 `Nothing`과 `Null`을 살펴보자.

**Nothing**

- `Nothing`은 모든 타입의 서브타입이며, 바텀 타입으로 불린다.
- `Nothing`은 값이 없음을 의미한다.
- 일반적으로 예외 발생, 프로그램 종료 또는 무한 루프와 같은 비정상 종료 신호를 보낼 때 사용한다.

**Null**

- `Null`은 모든 참조 타입(`AnyRef`)의 서브 타입이다.
- `null` 예약어를 통해 사용할 수 있다.
- 주로 Java의 `null`을 위해 사용한다.

## 클래스

클래스는 `class` 키워드를 통해 정의하고, `new` 키워드를 통해 인스턴스를 생성하여 접근할 수 있다.

```Scala
class User // 클래스 정의

val user1 = new User // 인스턴스화
```

다음 예시를 통해 클래스 정의에 대해 더 자세히 알아볼 수 있다.

```Scala
class Point(var x: Int, var y: Int) {

  def move(dx: Int, dy: Int): Unit = {
    x = x + dx
    y = y + dy
  }

  override def toString: String =
    s"($x, $y)"
}
```

위의 `Point` 클래스는 `x`, `y`라는 파라미터를 받는 클래스 생성자를 가진다.

또한 `move`, `toString`과 같은 메소드를 멤버로 가진다. (총 4개의 멤버를 가지는 클래스이다.)

> cf) `toString`은 `class`가 `AnyRef`에 포함되어 있는데, `AnyRef`에서 기본적으로 제공하는 메소드기 때문에 `override` 키워드로 수정된 메소드를 정의했다.

또한 파이썬처럼 생성자의 기본값을 정의할 수 있다.

```Scala
class Point(var x: Int = 0, var y: Int = 0)
```

위 `Point` 클래스에서 매개변수를 정의하지 않으면 기본값으로 적용되고, `val point2 = new Point(y=2)`와 같이 특정 멤버만 초기화 할 수 있다.

마지막으로 클래스의 멤버는 기본적으로 `public` 권한을 가진다. 외부 접근을 차단하기 위해 `private` 키워드를 사용할 수 있다.

직접 접근 대신 Getter와 Setter를 이용한 접근을 허용할 수 있다.

```Scala
class Point {
  // private 접근 권한으로 선언
  private var _x = 0
  private var _y = 0
  private val bound = 100

  def x = _x // getter
  def x_= (newValue: Int): Unit = { // setter
    if (newValue < bound) _x = newValue else printWarning
  }

  def y = _y // getter
  def y_= (newValue: Int): Unit = { // setter
    if (newValue < bound) _y = newValue else printWarning
  }

  private def printWarning = println("WARNING: Out of bounds")
}

val point1 = new Point
point1.x = 99
point1.y = 101 // 경고 출력
```

getter는 `public` 멤버에 `private` 멤버 값을 참조할 수 있도록 제공하면 된다.

setter는 getter 메소드 명 뒤에 `_` 키워드를 사용한 뒤 설정할 값을 받을 수 있도록 매개변수를 제공한다.

> cf) setter의 경우 변수(var)만 가능하며, 값(val)의 경우 변경하려고 하면 컴파일 에러가 발생한다.

### 기본 파라미터 값

Java의 메소드 오버로딩과 같은 기능을 Scala에서 마찬가지로 지원한다.

```Scala
class HashMap[K,V](initialCapacity:Int = 16, loadFactor:Float = 0.75) {
}

// 기본 값을 사용
val m1 = new HashMap[String,Int]

// 초기 크기는 20, 로드 팩터는 기본 값
val m2= new HashMap[String,Int](20)

// 둘 모드를 오버라이드
val m3 = new HashMap[String,Int](20,0.8)

// 이름을 지정한 인수를 통해 로드 팩터만을 오버라이드
val m4 = new HashMap[String,Int](loadFactor = 0.8)
```

`HashMap` 클래스를 인스턴스화 할 때, 기본 파라미터 값을 정의해두면, 위와 같이 파라미터를 특정 파라미터만 사용할 수 있는 등 메소드 오버로딩과 같은 기능을 사용할 수 있다.

### 이름을 지정한 파라미터

```Scala
def printName(first:String, last:String) = {
  println(first + " " + last)
}

printName("John","Smith") // "John Smith"를 출력
printName(first = "John",last = "Smith") // "John Smith"를 출력
printName(last = "Smith",first = "John") // "John Smith"를 출력
```

위 세가지 표현식은 같은 결과를 낸다.

기본적으로 파라미터의 이름을 지정하지 않으면 정의된 순서대로 입력된다.

두번째와 세번째 표현식처럼 특정 파라미터 이름을 정하면 그 순서를 변경할 수 있다.

앞서 설명한 **기본 파라미터 값**과 함께 사용하면, 변경하고 싶은 특정 파라미터만 이름을 이용해 설정하고, 나머지 값은 기본 파라미터 값을 이용해 채울 수 있다.

## 래퍼런스

https://docs.scala-lang.org/ko/tour/unified-types.html
