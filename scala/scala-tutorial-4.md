# Scala 튜토리얼 (4)

- [Scala 튜토리얼 (4)](#scala-튜토리얼-4)
  - [트레잇 (Trait)](#트레잇-trait)
    - [믹스인 클래스 컴포지션](#믹스인-클래스-컴포지션)
  - [래퍼런스](#래퍼런스)

## 트레잇 (Trait)

`트레잇`은 클래스간 인터페이스 및 필드를 공유할 때 사용한다.

- `trait` 예약어를 통해 선언한다
- 블록으로 이루어진 body에 추상 멤버를 정의할 수 있다.
- `trait TraitName[T]`와 같이 제네릭과 함께 사용하면 유용하다.

트레잇의 예시를 살펴보자.

```Scala
trait Iterator[A] {
  def hasNext: Boolean
  def next(): A
}

class IntIterator(to: Int) extends Iterator[Int] {
  private var current = 0
  override def hasNext: Boolean = current < to
  override def next(): Int = {
    if (hasNext) {
      val t = current
      current += 1
      t
    } else 0
  }
}
```

Java의 인터페이스와 구현체처럼, 트레잇을 정의하고, 아래 클래스에서 이를 `extends`를 통해 상속받아서 해당 멤버 메소드를 `override`하여 구현한다.

### 믹스인 클래스 컴포지션

다중 상속과 같은 기능을 Scala에서 제공한다.

다음 추상 Iterator를 예시로 이해해보자.

```Scala
abstract class AbsIterator {
  type T
  def hasNext : Boolean
  def next : T
}
```

**1. 먼저 trait으로 정의한다.**

```Scala
trait RichIterator extends AbsIterator {
  def foreach(f: T => Unit) { while (hasNext) f(next()) }
}
```

클래스를 믹스인으로 사용하기 위해 `extends` 키워드로 상속받아서

**2. 다른 기능의 클래스를 정의한다.**

```Scala
class StringIterator (s : String) extends AbsIterator {
  override type T = Char

  private var i = 0

  override def next: T = {
    val ch = s.charAt(i)
    i += 1
    ch
  }

  override def hasNext: Boolean = i < s.length
}
```

여기서는 예시로 문자열을 Iteration 할 수 있는 클래스인 `StringIterator`를 정의했다.

**3. 믹스인 클래스 컴포지션**

1번과 2번에서 정의한 트레잇과 클래스는 각각 구현 메소드를 가지고 있기 때문에 단일 상속으로는 합칠 수 없다.

```Scala
object StringIteratorTest {
  def main(args: Array[String]) {
    class Iter extends StringIterator("Scala") with RichIterator
    val iter = new Iter
    iter foreach println
  }
}
```

위의 예시에서 `class Iter extends StringIterator("Scala") with RichIterator`가 믹스인 클래스 컴포지션이 적용된 부분이다.

`Iter` 클래스는 `extends`한 `StringIterator` 클래스를 상속받는데, 이때 `StringIterator` 위치의 클래스를 `슈퍼 클래스`라고 부른다.

이후 `with` 키워드를 통해 추가적인 부모를 상속받았는데, `RichIterator`와 같이 추가적인 부모를 **믹스인**이라고 한다.

## 래퍼런스

https://docs.scala-lang.org/ko/tour/traits.html

https://docs.scala-lang.org/ko/tour/mixin-class-composition.html
