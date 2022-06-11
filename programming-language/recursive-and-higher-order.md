# Recursive and Higher-order 프로그래밍

> OCaml 의 강력한 특징인 Recursive와 Higher-order Programming에 대해 살펴보자.

- [Recursive and Higher-order 프로그래밍](#recursive-and-higher-order-프로그래밍)
  - [Recursive](#recursive)
    - [재귀적 해결법](#재귀적-해결법)
    - [명령형 언어 vs 함수형 언어](#명령형-언어-vs-함수형-언어)
    - [Tail-call 최적화](#tail-call-최적화)
  - [고차 함수 (Higher-order Function)](#고차-함수-higher-order-function)
    - [예시 : map](#예시--map)

## Recursive

### 재귀적 해결법

1. 주어진 문제가 충분히 작다면 바로 해결한다.
2. 충분히 작지 않다면 다음을 반복한다.
    * 문제를 충분히 작은 문제로 나눈다.
    * 각각의 작은 문제를 해결한다.
    * 해결한 결과를 하나의 결과로 합친다.

### 명령형 언어 vs 함수형 언어

* 명령형 언어는 **수행 방법(How to accomplish)** 을 중요하게 여긴다.
* 다음과 같이 조건문과 반복문을 사용하여 문제를 해결한다.
  
```c
 int factorial (int n) {
      int i; int r = 1;
      for (i = 0; i < n; i++)
        r = r * i;
      return r;
}
```

* 그러나 함수형 언어는 프로그램이 해야 할 것을 중요하게 여긴다.
* 다음과 같이 표현식과 재귀를 사용하여 문제를 해결한다.

```OCaml
let rec factorial n =
    if n = 0 then 1 else n * factorial (n-1)
```

### Tail-call 최적화

> Tail-recursion 이란? : 함수의 반환으로 함수만 반환하면 이를 Tail-recursion 이라고 부른다.

ML 에서 Tail-recursion은 추가적인 메모리를 소모하지 않는다. 그리고 언어에서 Non Tail-recursion 인 재귀 함수들을 자체적으로 Tail-recursion 로의 최적화를 제공한다.

따라서 Recursion이 ML에서는 비싸지 않다.

Example: Non Tail-recurison
```OCaml
let rec factorial a =
  if a = 1 then 1
  else a * factorial (a - 1)
```

위 코드는 반환값으로 a * factorial 과 같이 함수만 반환하지 않으므로 Tail-recursion이 아니다.

Example: Optimazation to Tail-recursion
```OCaml
let rec fact product counter maxcounter =
  if counter > maxcounter then product
  else fact (product * counter) (counter + 1) maxcounter
```

위와 같은 Tail-recursion 형태로 최적화하기 때문에 재귀를 사용하여 문제를 해결하는 것은 큰 비용이 들지 않는다.

## 고차 함수 (Higher-order Function)

> 고차 함수(Higher-order Function)은 함수를 입력받거나 함수를 결과값으로 사용하는 함수이다.

고차 함수는 강력한 추상화를 제공한다. 추상화를 통해 작은 아이디어를 결합하여 큰 아이디어를 만들거나, 코드 재사용을 할 수 있도록 제공한다.

변수(Variable)은 값을 저장하는 이름이고, 함수(Function)은 기능을 저장하는 이름이다. 고차 함수를 통해 함수 사이로 함수를 넘길 수 있으므로 추상화를 위한 강력한 매커니즘을 제공한다.

다음 예시를 통해 추상화의 강력함을 알아보자

### 예시 : map

```OCaml
let rec inc_all l =
  match l with
  | [] -> []
  | hd::tl -> (hd+1)::(inc_all tl)

let rec square_all l =
  match l with
  | [] -> []
  | hd::tl -> (hd*hd)::(square_all tl)

let rec cube_all l =
  match l with
  | [] -> []
  | hd::tl -> (hd*hd*hd)::(cube_all tl)
```

위 함수는 리스트 l의 각 원소들에 대해서

1. 각 원소의 값을 1 증가시킨다.
2. 각 원소를 제곱한다.
3. 각 원소를 세제곱한다.

의 기능을 수행하는 세 가지 함수이다.

보이는 것과 같이 비슷한 모양이지만 각각은 다른 기능을 한다. 하지만 공통적으로 리스트의 모든 원소에 접근하여 각각의 로직을 처리한다는 공통점이 있다.

위 함수들을 추상화를 이용하여 생각해보자.

```OCaml
let rec map f l =
  match l with
  | [] -> []
  | hd::tl -> (f hd)::(map f tl)
```

`map` 함수는 위에서 말했던 공통 기능인 리스트의 각 원소에 함수 `f` 를 적용하도록 추상화 한 함수이다.

ML은 고차 함수를 지원하기 때문에 위와 같이 `map` 함수의 인자로 함수인 `f` 를 넣을 수 있다.

이제 위에서 추상화를 사용하지 않을 때의 세 가지 함수를 추상화를 이용하여 조금 더 확장성있게 접근해보자.

```OCaml
let inc x = x + 1
let inc_all l = map inc l

let square x = x * x
let square_all l = map square l

let cube x = x * x * x
let cube_all l = map cube l
```

1씩 더하거나 제곱, 세제곱을 하는 기능들을 제공하는 함수를 `inc, square, cube` 와 같은 함수로 선언했다.

이후 map 함수의 위 함수를 활용하여 확장성 있게 함수를 작성할 수 있다.