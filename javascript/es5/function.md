# 함수

- [함수](#함수)
  - [함수 정의](#함수-정의)
  - [함수의 구성 요소](#함수의-구성-요소)
  - [함수 이름 규칙](#함수-이름-규칙)
  - [함수의 호출과 반환](#함수의-호출과-반환)
  - [Function Object](#function-object)
    - [new Function()](#new-function)
    - [Function.length](#functionlength)
    - [Function.prototype.call()](#functionprototypecall)
    - [Function.prototype.apply()](#functionprototypeapply)
    - [Function.prototype.toString()](#functionprototypetostring)
  - [함수의 형태](#함수의-형태)
    - [1. 함수 선언문](#1-함수-선언문)
    - [2. 함수 표현식](#2-함수-표현식)
  - [Argument](#argument)
  - [래퍼런스](#래퍼런스)

## 함수 정의

자바스크립트에서도 다른 언어와 마찬가지로 함수(`function`)을 정의할 수 있다.

함수를 정의해서 호출하여 사용하거나, 함수 자체를 변수에 할당하여 사용할 수 있다.

**예시 코드**

```javascript
function book() {
  return "어린왕자";
}

var getBook = function () {
  return "어린왕자";
};
```

## 함수의 구성 요소

함수는 다음과 같은 구성 요소들로 정의된다.

- `function` 키워드
- 함수 이름
- 파라미터
- 함수 body

예시를 통해 자세히 알아보자.

**예시 코드**

- `function` 키워드를 통해 함수라고 명시한다.
- `add` 라는 이름의 함수이다.
- 파라미터로 `a`와 `b`를 입력받는다.
- `{}` 안에 함수 body를 작성한다.
- 함수의 결과로 `a + b` 를 반환(`return`) 한다.

```javascript
function add(a, b) {
  var result = a + b;
  return result;
}
```

## 함수 이름 규칙

- 첫 문자 규칙
  - `숫자, &, *, @, +`: 사용 불가
  - `영문자, $, _(언더바)`: 사용 가능
- 관례적으로 함수 이름과 파라미터로 기능을 유추할 수 있도록 명확히 작성한다.
- `CamelCase` 방식으로 작성을 추천한다.
  - 첫 단어(동사)는 소문자로 시작하고, 이후 단어는 맨 앞 단어를 대문자로 시작하는 방법이다.
  - `addTwo(a, b)`, `getName(book)` 등

## 함수의 호출과 반환

- 정의된 함수는 이후 함수 이름에 파라미터를 전달하여 호출할 수 있다.
- 함수 내부에 `return` 키워드로 반환하는 값을 설정하여 결과 값을 반환할 수 있다.
- 만약 `return` 키워드가 없다면 `undefined`가 반환된다.

**예시 코드**

```javascript
function addTwo(a, b) {
  return a + b;
}

var result = addTwo(1, 2);
console.log(result); // 3 출력
```

**주의 사항**

- `return`문에 표현식은 한 줄로 작성해야 한다.
- 아래 예시 코드처럼 `return` 키워드 뒤에 자바스크립트 엔진이 자동으로 `;`를 붙인다.

```javascript
function addTwo(a, b) {
  return;
  a + b;
}

var result = addTwo(1, 2);
console.log(result); // undefined 출력
```

## Function Object

- Built-in Function Object
  - `new Function()`: 인스턴스 생성
  - `Function()`: 인스턴스 생성
- 아래와 같은 프로퍼티를 가진다.
  - `length`: 함수의 파라미터 수
- 아래와 같은 `prototype` 프로퍼티를 가진다.
  - `constructor`: 생성자
  - `call()`: 함수를 호출한다.
  - `apply()`: 배열을 파라미터로 함수를 호출한다.
  - `toString()`: 함수를 문자열로 반환한다.
  - `bind()`: 새로운 오브젝트를 생성하여 함수를 실행한다.

### new Function()

- 파라미터와 실행 가능한 자바스크립트 코드 문자열을 입력받는다.
- 입력 내용을 이용하여 함수 인스턴스를 반환한다.
- `Function()` 과 같은 방식으로 처리한다.

**예시 코드**

- ES5 기준 (ES6에서는 `let`을 사용한다.)
- 그러나 아래와 같은 선언은 실행 가능한 자바스크립트 코드를 삽입할 수 있으므로 공격에 취약할 수 있다.
- 몇몇 브라우저에서는 보안 정책으로 실행되지 않을 수 있다.

```javascript
var functionObject = new Function("x", "console.log(x)");

functionObject("hello, world!"); // "hello, world!" 출력
```

**주의 사항**

파라미터 수에 따라 전달 방식이 조금 다르다.

- 파라미터의 개수가 **2개 이상**: 위의 예시와 같은 경우이다. 마지막 파라미터가 함수의 body, 나머지가 함수의 파라미터로 전달된다.
- 파라미터가 **1개**: 함수의 파라미터가 없는 경우이다. 즉 함수의 body만 작성한다.
- 파라미터가 **0개**: 함수의 코드가 없는 `Function` 인스턴스를 생성한다.

### Function.length

- 함수의 파라미터 수를 반환한다.
- 생성된 `Function` 인스턴스를 기준으로 한다. (함수 호출시의 파라미터 기준이 아님에 주의하자.)
- 자바스크립트 엔진에서 값을 설정한다.

**예시 코드**

```javascript
function add(a, b) {
  return a + b;
}

console.log(add.length); // 2 출력
```

### Function.prototype.call()

- 함수를 호출한다.
- 첫번째 파라미터: 함수 내부에서 `this`로 참조할 객체 (일반적으로 `this` 작성)
- 이후 파라미터: 함수로 전달할 파라미터

**예시 코드**

- 일반적인 방식

```javascript
function add(a, b) {
  return a + b;
}

var result = add.call(this, 1, 2);
console.log(result); // 3 출력
```

- `this`를 활용하는 방식

```javascript
function add() {
  return this.a + this.b;
}

var value = { a: 10, b: 20 };
var result = add.call(value); // this로 오브젝트 전달
console.log(result); // 30 출력
```

### Function.prototype.apply()

- 함수를 배열을 파라미터로 호출한다.
- 첫번째 파라미터: 함수 내부에서 `this`로 참조할 객체 (일반적으로 `this` 작성)
- 이후 파라미터: 함수로 전달할 파라미터를 배열로 제공한다. (배열의 0번째 인덱스의 원소부터 파라미터에 전달된다.)

**예시 코드**

```javascript
function add(a, b) {
  return a + b;
}

var result = add.apply(this, [1, 2]); // a = 1, b = 2
console.log(result); // 3 출력
```

### Function.prototype.toString()

- 함수를 문자열로 반환한다.

**예시 코드**

```javascript
var myFunction = function () {
  return "hello";
};

console.log(myFunction.toString()); // function () { return "hello"; } 반환
```

## 함수의 형태

함수는 `함수 선언문, 함수 표현식`의 두 가지 방식이 있다.

### 1. 함수 선언문

- Function Declaration
- `function myFunction(param) { ... }` 형태이다.
- `function` 키워드, 함수 이름, 함수 body 작성이 필수이다.
- 함수 이름을 `Function` 인스턴스의 이름으로 사용한다.

**예시 코드**

```javascript
function getBook(book) {
  return book;
}

console.log(getBook("어린 왕자")); // "어린 왕자" 출력
```

### 2. 함수 표현식

- Function Expression
- `var myFunction = function(param) { ... }` 형태이다.
- `Function` 인스턴스를 생성하고 변수에 할당한다. (즉 변수가 함수의 이름이 된다.)
- 식별자 위치의 함수 이름은 **생략이 가능하다.**

**예시 코드**

```javascript
var getBook = function (book) {
  return book;
};

console.log(getBook("어린 왕자")); // "어린 왕자" 출력
```

**주의 사항**

- 식별자 위치의 함수 이름을 사용할 수 있다.
- 함수 body에서 호출하기 위한 용도이다.

```javascript
var factorial = function fact(n) {
  if (n == 1) {
    return 1;
  } else {
    return n * fact(n - 1);
  }
};

console.log(factorial(5)); // 120 출력
console.log(fact(5)); // 에러, 정의되지 않음.
```

## Argument

- 함수가 호출되었을 때 함수도 전달되는 값을 보관하는 객체를 `Argument Object`라고 한다.
- 함수에 파라미터가 있을 경우 파라미터에 값을 설정하고 `Argument` 에도 값을 설정한다.
- `arguments` 키워드를 이용하여 접근할 수 있다.

**예시 코드**

- 파라미터 값으로 `a = 1, b = 2, c = 3` 이 전달된다.
- 그러나 동시에 `argument` 객체의 0번째, 1번째, 2번째 인덱스에 같은 값이 순서대로 전달된다.

```javascript
function addThree(a, b, c) {
  return arguments[0] + arguments[1] + arguments[2];
}

var result = addThree(1, 2, 3);
console.log(result); // 6 출력
```

## 래퍼런스

https://www.inflearn.com/course/자바스크립트-비기너/
