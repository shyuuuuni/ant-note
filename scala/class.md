# 클래스

- [클래스](#클래스)
  - [제네릭 클래스](#제네릭-클래스)
  - [가변성](#가변성)
    - [상위 타입 경계](#상위-타입-경계)
    - [하위 타입 경계](#하위-타입-경계)
  - [내부 클래스](#내부-클래스)
  - [래퍼런스](#래퍼런스)

## 제네릭 클래스

스칼라도 자바와 같은 다른 언어처럼 제네릭 타입을 제공한다.

```
class Stack[T] {
  var elems: List[T] = Nil
  def push(x: T): Unit =
    elems = x :: elems
  def top: T = elems.head
  def pop() { elems = elems.tail }
}
```

위의 예시는 C++ 언어의 `Stack<T>`와 같이 타입을 입력받을 수 있는 스택 클래스를 나타내는 예시이다.

위 클래스를 인스턴스하며 입력한 임의의 타입에 대해서 해당 타입만 담는 스택을 정의할 수 있다.

## 가변성

제네릭 클래스에 대한 가변성 어노테이션을 지원한다.

즉 일반 제네릭 클래스는 지정한 타입 이외에는 사용할 수 없는 제약이 있었다.

가변성이 추가된 스택 예시를 살펴보자.

```Scala
class Stack[+T] {
  def push[S >: T](elem: S): Stack[S] = new Stack[S] {
    override def top: S = elem
    override def pop: Stack[S] = Stack.this
    override def toString: String =
      elem.toString + " " + Stack.this.toString
  }
  def top: T = sys.error("no element on stack")
  def pop: Stack[T] = sys.error("no element on stack")
  override def toString: String = ""
}

object VariancesTest extends App {
  var s: Stack[Any] = new Stack().push("hello")
  s = s.push(new Object())
  s = s.push(7)
  println(s)
}
```

가변성에는 두가지 종류를 사용할 수 있다.

- `Stack[+T]`: 순가변자(Covariant), `[+T]`를 사용하는 순가변자는 타입 `T`가 주어졌을 때, 해당 타입 하위 타입을 호환할 수 있도록 한다.
- `Stack[-T]`: 역가변자(Contravariant), `[-T]`를 사용하는 역가변자는 타입 `T`가 주어졌을 때, 해당 타입 상위 타입을 호환할 수 있도록 한다.

위의 예시에서 `Stack`이 `Any` 타입이므로, 해당 타입 하위 타입인 `String, Object, Int` 모두 입력할 수 있다.

또한 타입의 경계를 설정할 수 있다. 위의 예시에서 `push` 메소드를 살펴보자.

### 상위 타입 경계

`T <: A`와 같은 형태로 경계를 설정할 수 있다.

상위 타입 경계는 타입 변수 T를 선언하면서 A 서브타입을 참조한다.

### 하위 타입 경계

특정 타입의 서브타입을 참조하는 상위 타입과 반대로, 하위 타입 경계는 슈퍼타입을 참조한다.

`T >: A`와 같은 형태로 경계를 설정하며, 위의 스택 예시에서 이렇게 사용했다.

## 내부 클래스

스칼라의 클래스는 해당 클래스 내에 새로운 클래스를 가질 수 있다. 이를 내부 클래스라고 한다.

아래 예시는 그래프와 노드를 표현하기 위한 클래스이다.

```Scala
class Graph {
  class Node {
    var connectedNodes: List[Node] = Nil
    def connectTo(node: Node) {
      if (!connectedNodes.exists(node.equals)) {
        connectedNodes = node :: connectedNodes
      }
    }
  }
  var nodes: List[Node] = Nil
  def newNode: Node = {
    val res = new Node
    nodes = res :: nodes
    res
  }
}
```

먼저 그래프의 인스턴스를 생성하고, `newNode` 메소드를 통해 새로운 노드를 생성하여 반환할 수 있다.

```Scala
object GraphTest extends App {
  val g = new Graph
  val n1 = g.newNode
  val n2 = g.newNode
  val n3 = g.newNode
  n1.connectTo(n2)
  n3.connectTo(n1)
}
```

주의해야 할 점은 자바와 다르게 동일 클래스의 다른 인스턴스에서 내부 클래스를 인스턴스화할 경우 다른 타입으로 인식한다.

```Scala
object IllegalGraphTest extends App {
  val g: Graph = new Graph
  val n1: g.Node = g.newNode
  val n2: g.Node = g.newNode
  n1.connectTo(n2)      // legal
  val h: Graph = new Graph
  val n3: h.Node = h.newNode
  n1.connectTo(n3)      // illegal!
}
```

두 그래프 `g, h`를 선언하고, `g`에서 `n1, n2`노드를, `h`에서 `n3`노드를 만들었다.

자바에서는 `n1, n2, n3`가 모두 `Graph`의 `Node` 타입으로 인식하여 같은 타입이라고 생각하지만, 스칼라는 다른 타입으로 생각하여 마지막 줄에서 에러가 발생한다.

이를 해결하기 위해서는 `connectTo` 메소드의 파라미터 타입 정의를 변경하면 된다.

```Scala
def connectTo(node: Graph#Node)
```

위와 같이 `Graph#Node`를 사용하면 해결할 수 있다.

## 래퍼런스

https://docs.scala-lang.org/ko/tour/generic-classes.html

https://docs.scala-lang.org/ko/tour/variances.html

https://docs.scala-lang.org/ko/tour/inner-classes.html
