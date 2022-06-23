# 함수

- [함수](#함수)
  - [고차 함수](#고차-함수)
  - [중첩 함수](#중첩-함수)
  - [커링](#커링)
  - [래퍼런스](#래퍼런스)

## 고차 함수

**고차 함수란?**

- 함수가 파라미터로 함수를 입력받을 수 있다.
- 함수의 수행 결과로 함수를 반환한다.

```Scala
class Decorator(left: String, right: String) {
  def layout[A](x: A) = left + x.toString() + right
}

object FunTest extends App {
  def apply(f: Int => String, v: Int) = f(v)
  val decorator = new Decorator("[", "]")
  println(apply(decorator.layout, 7))
}
```

위의 `apply` 메소드는 `Int` 타입의 파라미터를 받아서 `String` 타입으로 반환하는 함수 `f`를 파라미터로 받는다.

이후 `Int` 타입의 파라미터 `v`를 받아서 `f(v)`를 실행시킨다.

마지막 줄은 `apply` 함수에 `Decorator` 클래스의 `layout` 메소드와 7이라는 숫자를 입력한다.

이는 스칼라에서 함수가 고차 함수로 취급할 수 있음을 보여준다.

## 중첩 함수

스칼라에서 함수 내부에서 함수를 중첩해서 선언하는 중첩 함수를 지원한다.

```Scala
object FilterTest extends App {
  def filter(xs: List[Int], threshold: Int) = {
    def process(ys: List[Int]): List[Int] =
      if (ys.isEmpty) ys
      else if (ys.head < threshold) ys.head :: process(ys.tail)
      else process(ys.tail)
    process(xs)
  }
  println(filter(List(1, 9, 2, 8, 3, 7, 4), 5))
}
```

`filter` 메소드는 정수 리스트에서 `threshold`보다 작은 값들만 필터링하여 반환하는 메소드이다.

`filter` 메소드 내부에 실제 로직을 담은 `process` 메소드를 정의하고, `process(xs)` 표현식으로 메소드를 실행시켜 그 결과를 반환한다.

스칼라에서는 이와 같이 중첩 함수를 지원한다.

## 커링

- 메소드는 여러개의 파라미터를 받을 수 있다.
- 만약 일부 파라미터만 입력하여 호출한 경우, 입력하지 않은 파라미터로 호출할 수 있는 함수를 반환한다.

```Scala
object CurryTest extends App {

  def filter(xs: List[Int], p: Int => Boolean): List[Int] =
    if (xs.isEmpty) xs
    else if (p(xs.head)) xs.head :: filter(xs.tail, p)
    else filter(xs.tail, p)

  def modN(n: Int)(x: Int) = ((x % n) == 0)

  val nums = List(1, 2, 3, 4, 5, 6, 7, 8)
  println(filter(nums, modN(2)))
  println(filter(nums, modN(3)))
}
```

위의 예시로 살펴보면, `filter` 메소드는 `xs`라는 정수 리스트의 각 요소에 대해서, `p` 라는 조건을 만족하는 요소들을 반환하는 메소드이다.

`p`는 `Int` 타입의 파라미터를 입력받아 `Boolean` 타입의 반환을 가지는 함수인데, 해당 함수의 파라미터에 정수 리스트의 각 요소를 입력하여 `True`일 경우에만 반환한다.

`modN` 메소드는 정수 `n, x`를 입력받아 `x`를 `n`으로 나눈 나머지가 0인지 확인하는 메소드이다.

마지막 두개의 `println` 표현식을 보면, `modN(2)`와 `modN(3)`을 사용한다.

각 표현식은

- `modN(2)`: `(x: Int) => ((x % 2) == 0)`
- `modN(3)`: `(x: Int) => ((x % 3) == 0)`

과 같이 남은 파라미터를 기준으로 새로운 함수를 반환한다.

이를 커링이라고 한다.

## 래퍼런스

https://docs.scala-lang.org/ko/tour/higher-order-functions.html

https://docs.scala-lang.org/ko/tour/nested-functions.html

https://docs.scala-lang.org/ko/tour/multiple-parameter-lists.html
