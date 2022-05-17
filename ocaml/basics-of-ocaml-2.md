# OCaml 기초 (2)

> 함수형 프로그래밍을 공부하면서 배운 OCaml 언어의 기초를 알아보자.

- [OCaml 기초 (2)](#ocaml-기초-2)
  - [Pattern Matching](#pattern-matching)
  - [타입 추론 (Type Inference)](#타입-추론-type-inference)
  - [다형 타입 (Polymorphic Types)](#다형-타입-polymorphic-types)
  - [튜플 (Tuple)](#튜플-tuple)
  - [리스트 (List)](#리스트-list)
    - [주의사항](#주의사항)
    - [연산자](#연산자)
    - [리스트와 패턴 매칭](#리스트와-패턴-매칭)
  - [데이터 타입 (Data Type)](#데이터-타입-data-type)
  - [예외 (Exception)](#예외-exception)
    - [예외 처리](#예외-처리)
    - [사용자 정의 예외](#사용자-정의-예외)

## Pattern Matching

> 기존 조건문이나 Switch 문과 비슷한 기능을 할 수 있지만, 훨씬 더 강력한 기능을 제공하는 문법이다.

`match ... with ...` 형태로 사용한다.

Example:
```OCaml
# let rec factorial a =
    if a = 1 then 1 else a * factorial (a-1);;
...
# let rec factorial a =
    match a with
    |1 -> 1
    |_ -> a * factorial (a-1);;
...
```

위의 예시처럼 factorial 함수의 인자 a가 1이면 `1`을 반환하고 그렇지 않으면 재귀적으로 `a * factorial (a-1)` 을 반환하는데, 이를 패턴 매칭을 통해 더욱 편리하게 사용할 수 있다.

위의 `|_ -> ...` 는 조건문의 else 와 같은 역할로, 이전 패턴에 매칭되지 않았을 때 실행시킬 표현식을 나타낸다.

또한 여러가지 조건을 다음 예시처럼 한번에 처리할 수도 있다.

Example:
```OCaml
# let isabc c = if c = ’a’ then true
                else if c = ’b’ then true
                else if c = ’c’ then true
                else false;;
...
# let isabc c =
    match c with
    | 'a' | 'b' | 'c' -> true
    | _ -> false;;
...
```

## 타입 추론 (Type Inference)

basics-of-ocaml-1 에서 잠깐 소개한 것 처럼 OCaml 은 타입 표기가 필수적이지 않다.

Example in Java:
```Java
public static int f(int n) {
    int a = 2;
    return a * n;
}
```

Example in OCaml
```OCaml
# let f n =
    let a = 2 in
        a * n;;
var f : int -> int = <fun>
```

필요하다면 타입을 명시할 수 있다. 만약 표기한 타입이 추론한 타입과 틀리다면 OCaml 은 이를 에러로 받아들이고 이를 표시해준다. (디버깅을 위해서 사용할 수 있다.)

Example:
```OCaml
# let sum_if_true (test : int -> int) (x : int) (y : int) : int = 
     (if test x then x else 0)
   + (if test y then y else 0);;
Error: The expression (test x) has type int but an expression was expected of type bool
```

위의 예시에서 명시적으로 `test` 를 int 형 파라미터를 받아서 int 형 리턴값을 가지는 함수라고 표현했다.

그러나 `sum_if_true` 를 살펴보면, `if test x then x else 0` 이라는 표현식에서 `test x` 는 리턴값으로 boolean variable 을 반환해야 한다고 추론된다.

명시한 타입과 추론한 타입이 다르므로 위와 같이 에러를 발생시킨다.

## 다형 타입 (Polymorphic Types)

경우에 따라 어떤 타입을 가질지 알 수 없는 경우가 있다.

Example:
```OCaml
# let id x = x;;
val id : 'a -> 'a = <fun>
```

위의 예시처럼 `id` 함수는 파라미터로 `x` 를 받아서 `x` 를 리턴한다. 이때 `id` 함수의 타입을 추론하려면 애매해지는데, 입력하는 `x` 의 타입에 맞춰서 변화하기 때문이다.

이럴 경우 위 함수를 다형(Polymorphic) 이라고 하고, `'a` 를 타입 변수라고 한다.

한가지 예를 더 들어보자.

Example:
```OCaml
# let first_if_true test x y =
    if test x then x else y;;
val first_if_true : ('a -> bool) -> 'a -> 'a -> 'a = <fun>
```

1. `if be then e1 else e2` 문법에 의해 `test x` 는 boolean expression 이고, `test` 가 `x`라는 파라미터를 가지므로 함수임을 알 수 있다.
2. `if be then e1 else e2` 문법에 의해 `x`와 `y`는 무엇인지는 모르지만 같은 타입이여야 함을 알 수 있다.

위와 같은 추론을 통해 다음과 같은 타입을 추론할 수 있다.

* `test` : `'a -> bool`
* `x` : `'a`
* `y` : `'a`
* `first_if_true` : `('a -> bool) -> 'a -> 'a -> 'a = <fun>`

## 튜플 (Tuple)

> 다른 타입을 포함할 수 있는 여러 값들의 콜렉션

`([값1],[값2],...,[값])` 과 같은 형태로 표현한다. 원소의 개수는 2개 이상이여야 한다.

Example:
```OCaml
# let x = (1, "one");;
val x : int * string = (1, "one)
```

결과로 타입을 표시할 때 `,` 자리에 `*` 문자로 표시한다. (`int * string`)

튜플을 활용하기 좋은 방법은 패턴 매칭을 함께 사용하는 것이다.

Example:
```OCaml
# let fst tup = match tup with (x,_) -> x;;
val fst : 'a * 'b -> 'a = <fun>

# let snd tup = match tup with (_,x) -> x;;
val snd : 'a * 'b -> 'b = <fun>
```

위의 예시처럼 원소 두개를 가지는 튜플을 인자로 받아서 패턴 매칭을 통해 앞의 원소 또는 뒤의 원소에 접근할 수 있다.

또한 튜플과 `let` 을 함께 사용하여 할당할 수 있다.

Example:
```OCaml
# let tup = (1, true);;
val p : int * bool = (1, true)

# let (x,y) = tup;;
val x : int = 1
val y = bool = true
```

위의 예시처럼 튜플의 각 값들을 `let`을 이용하여 한번에 할당할 수 있다.

## 리스트 (List)

> 순서가 있는 같은 타입의 값들의 콜렉션

* 모든 원소는 같은 타입을 가져야 한다.
* 순서가 있으므로 리스트 `[1; 2; 3;]` 과 리스트 `[3; 2; 1;]` 는 다른 리스트다.
* 리스트는 `[]` 로 감싸고, 원소간에는 `;` 로 구분한다.
* 첫번째 원소를 $head$, 이를 제외한 나머지 원소를 $tail$ 이라고 부른다.

### 주의사항

`[]` (빈 리스트, $nil$) 은 `head`와 `tail`이 존재하지 않는다.
`[5]` 와 같이 원소가 하나인 리스트는 `head`와 `tail`이 동일하다. (즉 `head` = `tail` = 5)

### 연산자

* `::` : Cons, 리스트의 가장 앞에 원소를 추가한다. 연속해서 사용할 수 있다.
```OCaml
# 1 :: 2 :: [3; 4;];;
- : int list = [1; 2; 3; 4]
```
* `@` : Append, 리스트의 뒤에 다른 리스트를 추가한다.
```OCaml
# [1; 2;] @ [3; 4; 5;];;
- : int list = [1; 2; 3; 4; 5]
```

### 리스트와 패턴 매칭

리스트는 패턴 매칭과 사용하면 유용하다. 다음 예시를 통해 어떻게 적용되는지 알아보자.

Example:
```OCaml
let rec length l =
    match l with
    | [] -> 0
    | h::t -> 1 + length t;;
val length : 'a list -> int = <fun>
```

위의 예시는 리스트를 입력받아서 리스트의 길이를 반환하는 함수이다. 빈 리스트일 경우 0을 반환하면서 종료하고, 리스트가 `head`와 `tail` 로 나눠지는 패턴에 매칭될 경우 1 + 남은 리스트의 길이를 재귀적으로 반복하여 반환한다.

## 데이터 타입 (Data Type)

지금까지 알아본 `int, bool, char, string` 등의 타입 외에도 사용자가 임의로 새로운 타입을 정의할 수 있다.

새로운 타입 정의를 위해서 `type` 키워드를 사용한다.

Example: 요일(days) 타입 정의
```OCaml
type days = Mon | Tue | Wed | Thu | Fri | Sat | Sun;;
```

새로운 타입으로 요일을 나타내는 `days` 타입을 정의했다. 타입을 새로 선언한 이후 아래 예시처럼 일반 타입처럼 사용할 수 있다. 

Example: 다음 `days` 를 리턴하는 함수
```OCaml
# let netday d =
    | Mon -> Tue
    | Tue -> Wed
    | Wed -> Thu
    | Thu -> Fri
    | Fri -> Sat
    | Sat -> Sun
    | Sun -> Mon;;
val nextday : days -> days = <fun>
```

또한 **생성자**를 이용하여 선언할 수 있다.

Example: 도형(shape) 타입 정의
```OCaml
type shape = Rect of int * int | Circle of int;;
```

`shape` 타입은 `Rect` 인 int * int 튜플 또는 `Circle` 인 int로 정의되었다. 타입을 새로 선언한 이후 아래 예시처럼 사용할 수 있다.

* `Rect of int * int` : 직사각형(Rect) 의 가로, 세로
* `Circle of int` : 원(Circle) 의 반지름

Example: 생성자 사용
```OCaml
# Rect (2, 3);;
- : shape = Rect (2, 3)

# Circle 5;;
- : shape = Circle 5
```

또한 패턴 매칭도 생성자를 이용하여 적용할 수 있다.

Example: 도형의 넓이를 리턴하는 함수
```OCaml
# let area s =
    match s with
    | Rect (w, h) -> w * h
    | Circle r -> r * r * 3;;
val area : shape -> int = <fun>
```

마지막으로 귀납적(Inductive) 데이터 타입을 알아보자. 대표적인 예시가 바로 리스트이다.

리스트는 다음과 같은 Inference Rule 로 정의할 수 있다.

* 리스트는 빈 리스트이다. (Axiom)
* 리스트는 리스트에 새로운 원소를 추가한 리스트이다.

Example: 리스트 타입 정의
```OCaml
# type mylist = Nil | List of int * mylist;;
```

위처럼 빈 리스트 $Nil$ 을 axiom 으로 해서 귀납적으로 리스트를 정의할 수도 있다.

## 예외 (Exception)

> Runtime-error

### 예외 처리

먼저 대표적인 `divide-by-zero` 와 같은 런타임 에러를 OCaml 에서 어떻게 처리하는지 알아보자.

`try ... with ...` 문을 사용하면 예외를 처리할 수 있다.

Example: Division_by_zero 발생
```OCaml
# let div a b = a / b;;
val div : int -> int -> int = <fun>

# div 10 0;;
Exception: Division_by_zero.
```

Example: 예외 처리한 div 함수
```OCaml
# let div a b =
    try
        a / b
    with Division_by_zero -> 0;;
val div : int -> int -> int = <fun>

# div 10 0;;
- : int = 0
```

`try` 다음에 나오는 표현식을 실행시켰을 때 `with` 의 예외가 발생하면 처리할 표현식을 작성하는 방식으로 실행된다.

### 사용자 정의 예외

사용자 정의 데이터 타입처럼 새로운 예외를 정의할 수 있다. `exception` 키워드를 이용하여 예외를 정의해보자.

Example: 예외 정의
```OCaml
# exception Problem;;
```

위와 같이 예외를 정의하고, 표현식으로 원하는 위치에서 예외를 발생시킬 수 있다. 예외 발생은 `raise` 키워드를 이용한다.

Example: 예외 발생
```OCaml
# let div a b =
    if b = 0 then raise Problem
    else a / b;;
val div : int -> int -> int = <fun>

# div 10 0;;
Exception: Problem
```

위와 같이 정의하고, `b` 값이 0일 때 `Problem` 예외가 발생하는 것을 볼 수 있다.

만약 예외가 발생했을 때 메세지를 보여주기 위해서는 다음과 같은 방법을 사용할 수 있다.

Example: 예외 메세지
```OCaml
# exception Problem of string
exception Problem of string

# let div a b =
    if b = 0 then raise (Problem "divide by zero")
    else a / b
val div : int -> int -> int = <fun>

# div 10 0;;
Exception: Problem "divide by zero".
```