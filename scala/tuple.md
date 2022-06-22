# 튜플

- [튜플](#튜플)
  - [튜플](#튜플-1)
    - [튜플과 패턴 매칭](#튜플과-패턴-매칭)
  - [래퍼런스](#래퍼런스)

## 튜플

튜플은 `(요소1, 요소2, ...)`와 같은 형태로 정의하는 요소들의 집합이다.

- 각 요소는 고유한 타입을 가질 수 있다.
- 튜플은 **불변**이다.
- 메소드의 반환값으로 여러개를 반환하고 싶을 때 유용하다.

예시: "Sugar"와 25를 요소로 가지는 튜플

```Scala
val ingredient = ("Sugar" , 25)
```

위 예시 튜플의 타입은 `Tuple2[String, Int]`로, 줄여서 `(String, Int)`로 표현한다.

> cf) 스칼라에는 Tuple2는 2개의 파라미터를 가진 튜플, Tuple3은 3개의 파라미터를 가진 튜플, ... 과 같은 튜플 타입이 있다.

튜플의 요소는 `_(번호)` 형태로 접근할 수 있다. (가장 앞이 1번이다.)

```Scala
println(ingredient._1) // Sugar
println(ingredient._2) // 25
```

### 튜플과 패턴 매칭

튜플은 패턴 매칭과 사용했을 때 유용하게 사용할 수 있다.

아래와 같이 패턴 매칭을 통해 값을 할당할 수 있다.

```Scala
val (name, quantity) = ingredient
println(name) // Sugar
println(quantity) // 25
```

또는 아래와 같이 튜플의 요소들에 대해서도 패턴 매칭이 가능하다.

```Scala
val planets =
  List(("Mercury", 57.9), ("Venus", 108.2), ("Earth", 149.6),
       ("Mars", 227.9), ("Jupiter", 778.3))

planets.foreach{ // 요소에 대한 패턴 매칭
  case ("Earth", distance) =>
    println(s"Our planet is $distance million kilometers from the sun")
  case _ =>
}
```

## 래퍼런스

https://docs.scala-lang.org/ko/tour/tuples.html
