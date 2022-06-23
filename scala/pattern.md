# 패턴

- [패턴](#패턴)
  - [패턴 매칭](#패턴-매칭)
    - [기본 사용법 (1)](#기본-사용법-1)
    - [기본 사용법 (2)](#기본-사용법-2)
  - [정규 표현식 패턴](#정규-표현식-패턴)
  - [추출자 오브젝트](#추출자-오브젝트)
  - [래퍼런스](#래퍼런스)

## 패턴 매칭

- 스칼라는 패턴을 검사할 수 있는 기능인 패턴 매칭을 지원한다.
- C언어의 switch문과 비슷한 역할로, OCaml 언어의 패턴 매칭과 같이 강력한 기능을 제공한다.
- tuple 포스팅에서 설명한 것 처럼, 자료구조에도 사용 가능하다.

### 기본 사용법 (1)

```Scala
object MatchTest1 extends App {
  def matchTest(x: Int): String = x match {
    case 1 => "one"
    case 2 => "two"
    case _ => "many"
  }
  println(matchTest(3))
}
```

기본적으로 패턴 매칭은 `(매칭할 변수) match { case (매칭 조건) => (매칭 시 반환값) ... }` 꼴로 사용한다.

위의 예시에서 정수 `x`에 대한 패턴 매칭으로 1일 경우 "one", 2일 경우 "two", 그 이외의 경우(\_) 에는 "many"를 반환한다.

### 기본 사용법 (2)

```Scala
object MatchTest2 extends App {
  def matchTest(x: Any): Any = x match {
    case 1 => "one"
    case "two" => 2
    case y: Int => "scala.Int"
  }
  println(matchTest("two"))
}
```

위의 예시는 `x`의 타입이 `Any` 타입으로, 여러 타입이 입력될 수 있다.

이러한 경우에도 패턴 매칭으로 처리할 수 있다.

## 정규 표현식 패턴

> cf) 현재 스칼라에서 `RegExp` 패턴이 일시적으로 제외되었다.

**우측 무시 시퀸스 패턴**

와일드카드와 별 키워드(`_*`)를 이용하여 임의의 긴 시퀀스를 대신할 수 있다.

```Scala
object RegExpTest1 extends App {
  def containsScala(x: String): Boolean = {
    val z: Seq[Char] = x
    z match {
      case Seq('s','c','a','l','a', rest @ _*) =>
        println("rest is "+rest)
        true
      case Seq(_*) =>
        false
    }
  }
}
```

위 예시에서 문자열 `x`를 문자 `Seq`인 `v`로 변환한 후, `v` 값에 대한 패턴 매칭을 진행한다.

패턴 매칭 시 맨 앞의 글자가 `s, c, a, l, a`를 포함하고, 나머지는 `rest` 변수에 저장할 수 있도록 표현할 수 있다.

## 추출자 오브젝트

`object`내부에 `unapply` 메소드를 정의한 것을 추출자 오브젝트라고 한다.

추출자 오브젝트가 선언되면, 패턴 매칭에서 해당 객체를 `case` 키워드에 매칭할 경우 추출자 메소드를 실행시킨다.

```Scala
object Twice {
  def apply(x: Int): Int = x * 2
  def unapply(z: Int): Option[Int] = if (z%2 == 0) Some(z/2) else None
}

object TwiceTest extends App {
  val x = Twice(21)
  x match { case Twice(n) => Console.println(n) } // prints 21
}
```

`Twice(21)` 코드는 생성자역할로 `Twice.apply(21)`을 의미한다.

그 `x`를 패턴 매칭할 때 `case Twice(n)`과 같은 표현식으로 나타냈다. 이는 `Twice.unapply`를 호출하고, 파라미터 `z`에 `Twice(21)`을 입력한다.

- `z = Twice(21) = 42`
- `z % 2 == 0` : True
- `Some(z/2)`가 가능하므로 그 값을 반환한다.
- 패턴 매칭이 성공했으므로(`None`이 반환되지 않음) 21을 출력한다.

따라서 결과적으로 21을 출력하게 된다.

**unapply**의 반환값은 다음 중 하나여야 한다.

- Boolean
- Option[T]
- Option[(T1,T2,...,Tn)] (Tn은 Seq[S]일 수 있다.)

## 래퍼런스

https://docs.scala-lang.org/ko/tour/pattern-matching.html

https://docs.scala-lang.org/ko/tour/regular-expression-patterns.html

https://docs.scala-lang.org/ko/tour/extractor-objects.html
