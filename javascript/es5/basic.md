# 자바스크립트 기초

> ES5 자바스크립트의 기초 문법을 알아보자.

- [자바스크립트 기초](#자바스크립트-기초)
  - [자바스크립트 사용하기](#자바스크립트-사용하기)
    - [직접 정의](#직접-정의)
    - [불러오기](#불러오기)
  - [문장 (Statement)](#문장-statement)
  - [변수 (Variable)](#변수-variable)
  - [주석](#주석)
    - [한 줄 주석](#한-줄-주석)
    - [두 줄 주석](#두-줄-주석)
  - [console.log()](#consolelog)
  - [정수/실수](#정수실수)
  - [상수](#상수)
  - [진수](#진수)
  - [자료형](#자료형)
    - [Number](#number)
    - [string](#string)
    - [Undefined](#undefined)
    - [Null](#null)
    - [Boolean](#boolean)
    - [Object](#object)
  - [래퍼런스](#래퍼런스)

## 자바스크립트 사용하기

일반적으로 자바스크립트는 html 파일 내에서 사용된다.

일반적으로 `head` 또는 `body` 태그 내부의 `script` 태그를 통해 자바스크립트를 사용한다.

### 직접 정의

자바스크립트를 사용하는 첫번째 방식은 html 파일의 `script` 태그 내부에 자바스크립트 코드를 작성하는 방식이다.

**예시 코드**

```html
<!-- basic-1.html -->
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="utf-8" />
    <title>자바스크립트</title>
    <script>
      var hello = "Hello, World!";
      console.log(hello);
    </script>
  </head>
  <body></body>
</html>
```

**실행 결과**

```console
Hello, World!
```

### 불러오기

하지만 위와 같은 방법으로 자바스크립트 코드를 작성하면, 큰 프로그램을 개발 할 경우 하나의 html 파일 내부에 너무 많은 코드가 사용될 수 있고, 재사용성이 떨어진다.

따라서 두번째 방법은 자바스크립트와 html 파일을 분리하는 방식이다.

**예시 코드**

```html
<!-- basic-2.html -->
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="utf-8" />
    <title>자바스크립트</title>
    <script src="hello.js" defer></script>
  </head>
  <body></body>
</html>
```

```javascript
// hello.js
var hello = "Hello, World!";
console.log(hello);
```

**실행결과**

```console
Hello, World!
```

위와 같이 `basic-2.html`과 `hello.js` 두가지 파일로 html 코드와 자바스크립트 코드를 분리할 수 있다.

> 참고: `script` 태그의 `defer` 옵션은 html 파일의 모든 코드를 읽은 뒤 해당 자바스크립트 코드를 실행한다는 의미이다.

## 문장 (Statement)

자바스크립트는 문장 단위로 실행된다.

자바스크립트는 `세미콜론(;)` 단위를 하나의 문장으로 판단하여 처리한다.

따라서 파이썬과 같은 특정 언어처럼 주석이나 문장의 실행 위치 등의 제약이 없다. (그러나 가독성을 위해 들여쓰기를 추가한다.)

**예시 코드**

```javascript
var x = 1; // 문장

if (true) {
  // if문 내의 문장
  var y = 2;
  var z = 3;
} // if문 또한 문장이다.
```

## 변수 (Variable)

> 최근 자바스크립트를 공부하면 `let` 키워드를 많이 사용하는데, 추후 ES6를 공부하면서 배워보자.

ES5 자바스크립트의 변수는 `var` 키워드를 통해 정의한다. (Variable의 약자)

아래 여러가지 예시를 통해 변수 선언을 알아보자.

**예시 코드**

```javascript
var variable; // 선언
variable = "변수"; // 할당

var x = 1; // x라는 변수에 1을 할당한다.

var y = 2,
  z = 3; // 여러개를 동시에 할당한다.

var book = "책",
  flower = "꽃"; // 공백이나 개행을 추가한다.

var a = (b = 1); // a와 b 변수 모두에 1을 할당한다.

var num = 10,
  num = 100; // num 변수에 100을 할당한다.
```

## 주석

주석은 한 줄 주석과 여러 줄 주석이 있다.

### 한 줄 주석

`//` 키워드를 사용해 주석을 처리한다.

**예시 코드**

```javascript
// 책 변수를 선언한다.
var book = "책";
```

### 두 줄 주석

`/* (코드) */` 형태로 주석을 처리한다.

**예시 코드**

```javascript
/*
여러 줄을 주석 처리한다.
var book = "책",
  flower = "꽃";
*/
```

이 방식을 응용하여 `/** (코드) */` 형태의 주석도 존재한다. **(권장)**

**예시 코드**

```javascript
/**
 * @function getName
 * @param people, 사람 객체를 입력한다.
 */
function getName(people) {
  // ...
}
```

위 예시 코드처럼 여러 줄 주석을 이용해 함수와 같이 긴 설명을 추가할 때 사용할 수 있다.

공식 기능은 아니지만, IDE의 지원으로 해당 주석이 있다면 자동으로 가독성 있는 인터페이스를 제공하는 등 관례적으로 많이 사용하는 방식이다.

또한 특정 툴을 사용한다면 위와 같이 주석 처리가 된 함수들을 자동으로 문서화하는 프로그램을 사용할 수도 있다.

## console.log()

[Console API](https://console.spec.whatwg.org)에서 제공하는 `console.log(..data)` 함수이다.

- 소괄호 내의 파라미터 값을 브라우저 콘솔에 출력한다.
- 쉼표를 통해 여러개의 파라미터 값들을 입력받을 수 있다. (각각 출력한다.)
- `log` 함수 이외에도 `clear`, `dir` 등 다양한 함수가 있다.

**예시 코드**

```javascript
console.log(1); // 1 출력

console.log(2, 3); // 2 3 출력

var x = 100;
console.log(x). // 100 출력
```

## 정수/실수

> ES6에서는 정수 타입과 실수 타입을 구분하지만 ES5에서는 구분하지 않는다.

- ES5는 정수와 실수를 구분하지 않는다.
- [IEEE 754](https://ko.wikipedia.org/wiki/IEEE_754) 표준의 64비트 부동 소숫점 처리를 따른다.
- 두 타입을 구분하지 않기 때문에 정수와 실수간 연산시 문제 없이 처리할 수 있다.

**예시 코드**

```javascript
console.log(1); // 1 출력
console.log(1); // 1 출력
console.log(1.0); // 1 출력

console.log(1 + 5.1); // 6.1 출력
```

## 상수

> ES6에서는 const 키워드를 도입하여 상수를 정식으로 제공한다.

- ES5에서는 변수값을 변경할 수 있어서 공식적으로 상수를 제공하지 않는다.
- 그러나 관례적으로 선언 시 영문 대문자로 선언하면 상수를 선언한다고 가정한다.
- `Number.MAX_VALUE` 등 선언되어 있는 자바스크립트 상수값은 변경할 수 없다.

**예시 코드**

```javascript
var ONE = 1; // 상수 변수 ONE 선언

ONE = 2; // 그러나 변경할 수 있다.
```

## 진수

- 10진수: 일반적으로 사용하는 숫자 표현 방식이다.
- 16진수: 앞에 `0x`를 붙인 후 뒤에 16진수를 사용하는 숫자 표현 방식이다.

```javascript
// 10진수 표현법
console.log(1); // 1 출력

// 16진수 표현법
console.log(0x01); // 1 출력
console.log(0xff); // 255 출력
```

**이외 진수**

- 2진수: ES6에서 제공한다.
- 8진수: ES3에서 폐지하고, ES6에서 제공한다.

## 자료형

- 자료형은 데이터가 가지고 있는 타입이다.
- 데이터는 항상 타입을 가진다. **데이터를 기준으로 타입을 결정한다.**
- `typeof` 키워드를 통해 타입을 반환할 수 있다.

**예시 코드**

```javascript
typeof 1; // number

typeof "hello"; // string
```

자료형은 크게 두 가지로 분류할 수 있다.

- `언어 타입`: 자바스크립트에서 사용할 수 있는 타입이다.
  - Undefined, Null, Boolean, String, Number, Object 등
- `스펙 타입`: 언어 알고리즘을 위한 타입이다. (자바스크립트에서 사용 불가능)
  - Reference, List, Completion, Property Descriptor, Data Block, Lexical Environment, Lexical Record 등

### Number

부호를 가진 숫자들의 자료형이다.

- 숫자: `-27, 0, 1, 100, 2.53` 등
- 숫자X: `NaN`
- 무한대: `Infinity`, `-Infinity`

**예시 코드**

```javascript
console.log(-27, 0, 1, 100, 2.53); // 숫자

console.log(1 * "A"); // NaN
```

### string

큰 따옴표("") 혹은 작은 따옴표('') 사이에 작성된 데이터 자료형이다.

- 따옴표를 문자열 내에 작성하고 싶다면 다른 따옴표 타입으로 묶으면 된다.

**예시 코드**

```javascript
console.log("hello world"); // hello world 출력

console.log("hello 'world'"); // hello 'world' 출력

console.log('hello "world"'); // hello "world" 출력
```

### Undefined

- `Undefined`: 변수가 선언되었을 때 기본 값(`undefined`)의 타입이다.
- 변수가 선언만 되고 할당되지 않으면 그 값으로 `undefined`가 할당된다.

**예시 코드**

```javascript
var x;
console.log(x); // undefined 출력
```

### Null

- 변수를 선언했는데, 아직 값을 채우지 않은 것인지, 의도적으로 임시값으로 채운것인지 구분되지 않는다.
- 이때 사용하는 값이 `Null` 타입 값인 `null` 이다.

**예시 코드**

```javascript
var x;
console.log(x); // undefined 출력

var y = null;
console.log(y); // null 출력
```

**주의**

- ES5에서는 `null`값을 `typeof` 키워드를 통해 검사하면 `object`가 반환된다.
- ES6에서는 이를 해결하였다.

```javascript
typeof null; // object
```

### Boolean

- `true`, `false` 로 구성된다.
- 추후 공부할 논리 연산자를 적용할 수 있다.

**예시 코드**

```javascript
console.log(true); // true
console.log(false); // false
```

### Object

- `속성(property)`: `name: value` 형태의 `name-value` 쌍 한개를 의미한다.
- `Object`: 중괄호 안에 0개 이상의 속성을 작성한 형태를 의미한다. `{name1: value1, name2: value2, ...}`
- 즉 `Object`는 속성의 집합이다.
- 속성의 `name`은 `key` 라고 불린다
- 앞서 설명한 것 처럼 ES5에서는 `Object`와 `Null` 타입을 구분할 수 없다.

## 래퍼런스

https://www.inflearn.com/course/자바스크립트-비기너/
