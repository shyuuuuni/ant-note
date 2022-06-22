# Scala 튜토리얼 (2)

- [Scala 튜토리얼 (2)](#scala-튜토리얼-2)
  - [표현식](#표현식)
    - [값](#값)
    - [변수](#변수)
  - [블록](#블록)
  - [함수](#함수)
    - [익명 함수](#익명-함수)
    - [함수](#함수-1)
  - [메소드](#메소드)
  - [클래스](#클래스)
  - [케이스 클래스](#케이스-클래스)
  - [객체](#객체)
  - [트레이트 (Trait)](#트레이트-trait)
  - [메인 메소드](#메인-메소드)
  - [래퍼런스](#래퍼런스)

## 표현식

`1 + 1`이나 `"Hello," + "World!"`와 같은 연산이 가능한 명령문을 표현식이라고 한다.

아래는 `println`을 이용하여 표현식의 결과를 출력하는 예시이다.

```Scala
println(1) // 1
println(1 + 1) // 2
println("Hello!") // Hello!
println("Hello," + " world!") // Hello, world!
```

### 값

값(value)는 **이름이 붙여진 표현식의 결과**이다.

`val` 키워드와 함께 값의 이름을 작성하고, 값에 표현식을 할당할 수 있다.

```Scala
val x = 1 + 1 // 타입 추론을 통해 타입을 자동으로 결정
val x: Int = 1 + 1 // 명시적 타입 결정
```

### 변수

값과 다르게 변수는 **재할당이 가능**하다.

마찬가지로 `var` 키워드와 함께 변수의 이름을 작성하고 할당한다.

값과 동일하게 타입을 추론하거나 명시적으로 결정할 수 있다.

```Scala
var x = 1 + 1 // 타입 추론을 통해 타입을 자동으로 결정
var x: Int = 1 + 1 // 명시적 타입 결정
```

## 블록

`중괄호 {}`로 이루어진 표현식(들)을 블록이라고 한다.

블록에서, 블록 내의 마지막 표현식의 결과를 블록의 결과로 계산한다.

```Scala
println({
  val x = 1 + 1
  x + 1
}) // 3
```

## 함수

**매개변수를 가진 표현식**을 함수라고 한다.

### 익명 함수

말 그대로 이름이 없는 함수를 익명 함수라고 한다.

```Scala
(x: Int) => x + 1
```

위의 예시는 좌측 괄호 안에 있는 `x`를 매개변수를 하여 `=>` 매개변수를 사용한 오른쪽의 표현식을 가지는 익명 함수이다.

### 함수

`val` 키워드를 통해 함수에 이름을 지정할 수 있다.

또한 함수의 매개변수는 없을수도 있고, 1개, 2개, 그 이상 가질 수 있다.

```scala
val getTheAnswer = () => 42 // 매개변수 0개
val addOne = (x: Int) => x + 1 // 매개변수 1개
val add = (x: Int, y: Int) => x + y // 매개변수 2개
```

## 메소드

메소드는 `def` 키워드로 시작하여 메소드 명, 매개변수와 매개변수의 타입, 그리고 반환 타입과 표현식으로 이루어져있다.

```Scala
def add(x: Int, y: Int): Int = x + y
```

위 예시는 `add`라는 메소드가 `Int`형 매개변수 `x`, `y`를 입력받아서 `Int`형을 반환하는 `x + y`라는 표현식을 가진 메소드이다.

메소드는 블록을 사용하여 여러 표현식을 함께 사용할 수 있다.

```Scala
def getSquareString(input: Double): String = {
  val square = input * input
  square.toString
}
```

블록에서 설명한 것 처럼, 블록의 반환값은 블록에 포함된 마지막 표현식의 결과 값이기 때문에 위 메소드는 입력을 제곱한 뒤 이를 `String` 타입으로 변환하여 반환한다.

- 스칼라의 메소드의 매개변수는 `val` 형식이므로, 내부적으로 값을 재할당 할 수 없다.
- 프로시저 형태로 작성할 수 있다. 즉,
  ```Scala
  def add () { "test string" }  // Unit 반환
  def add () = { "test string" } // "test string" 반환
  ```

스칼라에서는 `return` 키워드가 있지만 대부분 키워드를 사용하지 않고 본문 블록의 마지막 표현식을 반환 값으로 사용한다.

## 클래스

클래스는 `class` 키워드로 정의할 수 있다.

클래스는 클래스 명과 함께 매개변수와 같은 형태로 **생성자 매개변수**를 함께 정의한다.

```Scala
class Greeter(prefix: String, suffix: String) {
  def greet(name: String): Unit =
    println(prefix + name + suffix)
}
```

위 예시는 `Greeter` 라는 이름의 클래스를 정의하였고, 생성자 파라미터로 `String` 타입의 `prefix`와 `suffix`를 제공한다.

클래스는 메소드를 보유할 수 있는데, 위의 예시처럼 `greet` 메소드를 정의할 수 있고, 그 메소드에서는 클래스의 생성자 파라미터 등을 참조하여 사용할 수 있다.

실제 사용은 클래스의 인스턴스를 만들어서 사용한다.

인스턴스는 `new` 키워드를 사용하여 만들 수 있고, 이때 클래스 명과 함께 생성자 파라미터를 입력하여 만들 수 있다.

```Scala
val greeter = new Greeter("Hello, ", "!")
greeter.greet("Scala developer") // Hello, Scala developer!
```

## 케이스 클래스

케이스 클래스는 `case class` 키워드로 정의하며, 클래스의 특별한 타입이다.

- 기본적으로 불변이다.
- 패턴 매칭을 통해 분해가 가능하다.
- 참조 대신 값을 비교한다.
- 초기화와 운영이 간결하다. (`new` 키워드 없이 인스턴스화 할 수 있다.)

예시를 통해 살펴보자.

추상 클래스와 케이스 클래스를 아래와 같이 정의한다.

```Scala
abstract class Notification
case class Email(sourceEmail: String, title: String, body: String) extends Notification
case class SMS(sourceNumber: String, message: String) extends Notification
case class VoiceRecording(contactName: String, link: String) extends Notification
```

케이스 클래스를 인스턴스화 할 수 있다.

```Scala
val emailFromJohn = Email("john.doe@mail.com", "Greetings From John!", "Hello World!") // new 키워드 없이 가능
```

위에서 인스턴스화하며 입력한 생성자 파라미터는 `public` 접근 권한으로 제공되며, 기본적으로 불변이다.

```Scala
val title = emailFromJohn.title // public 접근 가능
emailFromJohn.title = "Goodbye From John!" // 컴파일 에러 (기본적으로 불변)
```

생성자 파라미터 값을 변경하는 대신 `copy`를 통해 몇몇 값들을 변경하며 복사할 수 있다.

```Scala
val editedEmail = emailFromJohn.copy(title = "I am learning Scala!", body = "It's so cool!") // title과 body 값 변경하며 복사
```

**값을 통해 비교할 수 있다.** 스칼라에서 케이스 클래스는 컴파일러가 `equals`와 `toString` 메소드를 지원하여 비교할 수 있다.

아래 코드에서 `firstSms`와 `secondSms`는 구조적으로 동일하기 때문에 if문의 조건을 만족하여 `"They are equal!"`을 출력한다.

```Scala
val firstSms = SMS("12345", "Hello!")
val secondSms = SMS("12345", "Hello!")

if (firstSms == secondSms) {
    println("They are equal!")
}
```

마지막으로 케이스 클래스는 **패턴 매칭 적용이 가능**하다.

위에서 정의한 `Notification` 추상 클래스 내에서 패턴 매칭을 통해 특정 케이스별 로직을 설정할 수 있다.

```Scala
def showNotification(notification: Notification): String = {
  notification match {
    case Email(email, title, _) =>
      "You got an email from " + email + " with title: " + title
    case SMS(number, message) =>
      "You got an SMS from " + number + "! Message: " + message
    case VoiceRecording(name, link) =>
      "you received a Voice Recording from " + name + "! Click the link to hear it: " + link
  }
}
```

위 코드와 같이 패턴 매칭을 통해 `Email`, `SMS`, `VoiceRecording` 케이스 별 처리 로직을 따로 설정할 수 있다.

테스트 케이스를 사용하면:

- 불변성을 통해 값의 변경에서 자유로워진다.
- 값을 통한 비교를 통해 원시 타입 비교처럼 사용할 수 있다.
- 패턴매칭은 로직을 간단하게 만들어주며, 버그를 줄이고 코드의 가독성을 높일 수 있다.

## 객체

객체는 `object` 키워드로 정의된다.

```Scala
object IdFactory { // 객체 정의
  private var counter = 0
  def create(): Int = {
    counter += 1
    counter
  }
}

val newId: Int = IdFactory.create() // 객체 인스턴스화
```

객체 이름을 통해 객체를 인스턴스화 할 수 있고, 그 이름에 직접 접근하여 객체에 접근할 수 있다.

## 트레이트 (Trait)

트레이트는 **특정 필드와 메소드를 가지는 타입**이다.

- `trait` 키워드로 정의 할 수 있다.
- 다른 트레이트와 결합할 수 있다.

아래 예시처럼 메소드의 인터페이스만 제공하거나, 구체적인 정의도 함께 제공할 수 있다.

```Scala
trait Greeter { // 인터페이스만 제공
  def greet(name: String): Unit
}

trait Greeter { // 구체적 정의도 함께 제공
  def greet(name: String): Unit =
    println("Hello, " + name + "!")
}
```

`extends` 키워드를 통해 트레이트를 상속받을 수 있고, `override` 키워드를 통해 상속받은 메소드를 수정할 수 있다.

```Scala
class DefaultGreeter extends Greeter // 상속

class CustomizableGreeter(prefix: String, postfix: String) extends Greeter { // 상속 및 확장
  override def greet(name: String): Unit = {
    println(prefix + name + postfix)
  }
}
```

또한 다중 상속과 같이 사용할 수 있다.

## 메인 메소드

메인 메소드는 프로그램의 시작 지점을 알린다.

`object` 키워드를 사용하며, 내부에 `main` 메소드를 정의하고, 생성자 파라미터로 문자열 배열(Array[String]) 을 입력받도록 구현한다.

```Scala
object Main {
  def main(args: Array[String]): Unit =
    println("Hello, Scala developer!")
}
```

## 래퍼런스

https://docs.scala-lang.org/ko/tour/basics.html

https://okky.kr/article/339484
