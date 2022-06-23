# 싱글톤 객체

- [싱글톤 객체](#싱글톤-객체)
  - [싱글톤 객체](#싱글톤-객체-1)
  - [동반자 (Companions)](#동반자-companions)
  - [래퍼런스](#래퍼런스)

## 싱글톤 객체

`class` 키워드 대신 `object` 키워드를 사용하여 사용할 수 있다.

```Scala
package test

object Blah {
  def sum(l: List[Int]): Int = l.sum
}
```

위 예시에서 `sum`메소드는 `test.Blah.sum`로 사용될 수 있다.

- 싱글톤 객체는 직접 인스턴스화 할 수 없다.
- 트레잇이나 클래스의 멤버로 사용될 수 있다.
- 스칼라에 없는 `static`키워드 대신 비슷한 역할을 수행할 수 있다.

## 동반자 (Companions)

싱글톤 객체가 같은 소스파일 내의 동일한 이름의 클래스와 함께 존재할 때, 그 클래스를 동반자라고 한다.

```Scala
class IntPair(val x: Int, val y: Int)

object IntPair {
  import math.Ordering

  implicit def ipord: Ordering[IntPair] =
    Ordering.by(ip => (ip.x, ip.y))
}
```

위의 `IntPair` 싱글톤 객체는 동일 소스코드 내에 같은 이름의 클래스를 보유하고 있다.

이 경우 싱글톤 객체에서 동반자 클래스에 접근하여 사용할 수 있다.

또한 싱글톤 객체에서 `new` 키워드 등으로 동반자 클래스의 인스턴스를 생성하는 메소드를 구현하면, 이를 호출하는 코드에서는 `new` 키워드 없이 새로운 인스턴스를 생성하여 사용할 수 있다.

## 래퍼런스

https://docs.scala-lang.org/ko/tour/singleton-objects.html
