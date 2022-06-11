# OCaml 기초 (1)

> 함수형 프로그래밍을 공부하면서 배운 OCaml 언어의 기초를 알아보자.

- [OCaml 기초 (1)](#ocaml-기초-1)
  - [OCaml 은 Expression 이다.](#ocaml-은-expression-이다)
  - [산술(Arithmetic) 표현식](#산술arithmetic-표현식)
  - [부울(Boolean) 표현식](#부울boolean-표현식)
  - [형변환 (Type Conversion)](#형변환-type-conversion)
    - [실수(Float) 타입 표현식](#실수float-타입-표현식)
  - [다른 원시 값 (Primitive Values)](#다른-원시-값-primitive-values)
    - [Character](#character)
    - [String](#string)
    - [Unit](#unit)
  - [조건문](#조건문)
  - [변수](#변수)
  - [함수](#함수)
    - [함수의 선언](#함수의-선언)
    - [함수와 First-class](#함수와-first-class)

## OCaml 은 Expression 이다.

> **Statement** does something
> **Expression** evaluates to a value

먼저 C, Java, Python, Javascript 등 대부분의 사람들이 알고 있는 명령형(inperative) 언어를 생각해보자. 

명령형 언어에서는 Statement 를 기본 단위로 사용하는데, 이를 통해 메모리나 디스플레이와 같은 **상태(Machine-state)를 변경**시킨다. 예를 들어 C에서 printf() 를 실행시키면 모니터에 값을 출력하면서 모니터의 상태를 변화시키는 것을 볼 수 있다.

그래서 대부분의 명령형 언어들을 **Statement-Oriented Programming Language** 라고 한다.

반면 ML, Haskell, Scala 와 같은 언어를 생각해보자. 이러한 언어들은 프로그램이 상태를 바꾸는 것이 아니라 수학적인 수식을 바꾸는 것이라는 관점으로 동작한다.

따라서 이러한 언어들을 **Expression-Oriented Programming Language** 혹은 **Functional Programming Language** 라고 한다.

## 산술(Arithmetic) 표현식

정수 연산에 관련된 산술 연산자를 살펴보자.

* 피연산자 : integer

```
a + b   : 덧셈
a - b   : 뺄셈
a * b   : 곱셈
a / b   : a를 b로 나눈 몫
a mod b : a를 b로 나눈 나머지
```

위 연산들의 결과는 정수이고, REPL 이 가능하다.

> REPL : Read-Eval-Print-Loop, 표현을 읽고 판단하여 출력하는것을 반복하는 것. 아래 예시처럼 연속적으로 문법에 맞춘 연산이 가능함.

```OCaml
# 1+2*3;;
- : int = 7
```

## 부울(Boolean) 표현식

부울 연산에 관련된 연산자를 살펴보자.

* 피연산자 : integer

```
a = b   : a와 b가 같다면 true
a <> b  : a와 b가 다르다면 true
a < b   : a가 b보다 작다면 true
a <= b  : a가 b보다 작거나 같다면 true
a > b   : a가 b보다 크다면 true
a >= b  : a가 b보다 크거나 같다면 true
```

위 연산들의 결과는 boolean variable 이다.

* 피연산자 : boolean variable (true, false)

```
a && b  : a AND b
a || b  : a OR b
```

## 형변환 (Type Conversion)

> OCaml 은 정적 타입(Static Type) 언어다. 즉, 컴파일시 타입을 체크하고, 다른 타입간의 연산 시 에러를 발생시킨다.

> 또한 OCaml 은 Type-Safe 언어다. 즉, 컴파일된 프로그램은 런타임동안 타입 에러를 발생시키지 않는 것을 보장한다.

위의 특징으로 OCaml 에서는 변수를 선언하면 자동으로 형이 지정된다. 따라서 C언어와 같이 변수형을 선언할 필요가 없다. (`let x = ...` 와 같은 형태로 선언하면 컴파일 시 타입이 지정된다.)

반대로 타입에 맞춰서 작성하지 않으면 에러가 발생하기 때문에 잘 신경써야 하는 부분도 존재한다.

### 실수(Float) 타입 표현식

* 피연산자 : float variable

위에서 살펴본 정수 연산자 뒤에 '.' 을 추가하여 사용한다.

Example: 
```OCaml
# 1.2 +. 2.3;;
- : float = 3.5
```

만약 정수와 실수를 연산하고 싶다면 `float_of_int` 함수를 사용한다. 위 함수는 정수형 변수를 실수형 변수로 변환시켜준다.

Example:
```OCaml
# float_of_int 1 +. 2.2;;
- : float = 3.2
```

## 다른 원시 값 (Primitive Values)

그 외 다른 형태의 원시 값들을 예시와 함께 살펴보자.

### Character

문자 타입

```OCaml
# 'c';;
- : char = 'c'
```

### String

문자열 타입

```OCaml
# "string";;
- : string = "string"
```

### Unit

임의의 타입

```OCaml
# ();;
- : unit = ()
```

## 조건문

```OCaml
if be then e1 else e2
```

* be : boolean expression
* be 가 true 면 e1 을, 아니면 e2 값을 나타낸다.
* be 값이 항상 boolean expression 임에 유의한다. (C언어처럼 `if (1)` 과 같은 방식은 불가능하다.)
* e1과 e2는 동일 타입이여야 한다.

## 변수

지금까지 배운 값(정수, 실수, 부울 등) 을 저장하는 변수이다.

* 전역변수 : `let` 키워드로 선언한다.
```OCaml
# let x = 3 + 4;;
val x : int = 7
```

* 지역변수 : `let ... in ...` 구조로 선언한다.
```OCaml
# let d =
    let a = 1 in
    let b = a + a in
    let c = b + b in
        c + c;;
val d : int = 8
```
위의 예시처럼 `let ... in ...` 구조로 다음 expression 의 지역변수로 앞의 변수가 사용된다.

## 함수

`OCaml 은 함수형 프로그래밍 언어기 때문에, OCaml의 함수는 First-Class 이다. `

> **First-Class 란? : 어떤 값이 first-class라면 그 값은 변수에 저장될 수 있고, 함수의 인자로 넘길 수 있고, 다른 함수의 리턴값으로 사용될 수 있다.**

즉 1, 2, 'c', true/false 와 같은 일반 변수와 함수가 동일하게 사용될 수 있다는 의미이다.

### 함수의 선언

`let [함수명] [파라미터] = [로직]` 형태로 선언한다.

Example:
```OCaml
# let square x = x * x;;
val square : int -> int = <fun>
```

위 예시처럼 선언할 경우 아래 결과로 `int -> int = <fun>` 이라는 문구가 발생한다.

이 의미는 `int` 를 파라미터로 받아서 `int` 를 리턴하는 `<fun>` (함수) 라는 의미이다.

사용시에는 아래와 같이 파라미터를 넘겨서 사용할 수 있다.
```OCaml
# square 2;;
- : int = 4
```

**재귀 함수**의 경우 함수명 앞에 `rec` 키워드를 붙여서 사용한다.

즉, `let rec [함수명] [파라미터] = [로직]` 형태로 선언해야 한다.

Example:
```OCaml
# let rec factorial a =
    if a = 1 then 1 else a * factorial (a-1);;
val factorial : int -> int = <fun>
```

**Nameless-function**도 가능하다.

`fun [파라미터] -> [로직]` 으로 선언한 뒤 뒤에 파라미터를 넘겨서 실행시킬 수 있다.

Example:
```OCaml
# (fun x -> x * x) 2;;
- : int = 4
```

### 함수와 First-class

예를 들어 다음과 같이 주어진 조건이 참일 경우 파라미터의 두 값을 더해서 리턴하는 함수인 `sum_if_true` 함수와, 주어진 값이 짝수일때 true를 반환하는 함수인 `even` 이라는 함수를 선언하자.

```OCaml
# let sum_if_true = test first second =
    (if test first then first else 0)
  + (if test second then second else 0);;
val sum_if_true : (int -> bool) -> int -> int -> int = <fun>

# let even x = x mod 2 = 0;;
val even : int -> bool = <fun>
```

OCaml에서 함수는 First-class기 때문에 함수의 인자로 넘겨줄 수 있다. 예를 들어 `sum_if_true` 함수의 `test` 라는 인자로 `even` 함수를 넘길 수 있다.

Example:
```OCaml
# sum_if_true even 3 4;;
- : int = 4
```

3이라는 값은 홀수기 때문에 0을, 4라는 값은 짝수기 때문에 4를 if문에서 반환하고, 두 값을 더한 4가 결과로 리턴되었다.

위의 sum_if_true 함수처럼, **함수를 입력받거나 리턴하는 함수를 Higher-Order Function 이라고 한다.**