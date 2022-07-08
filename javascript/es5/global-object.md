# 글로벌 오브젝트

- [글로벌 오브젝트](#글로벌-오브젝트)
  - [글로벌 오브젝트란?](#글로벌-오브젝트란)
    - [Global 함수/변수](#global-함수변수)
    - [프로퍼티 리스트](#프로퍼티-리스트)
    - [전역 프로퍼티(값)](#전역-프로퍼티값)
    - [parse 함수](#parse-함수)
    - [isNaN, isFinite](#isnan-isfinite)
    - [인코딩 관련 함수](#인코딩-관련-함수)
    - [eval()](#eval)
  - [래퍼런스](#래퍼런스)

## 글로벌 오브젝트란?

- 전역 객체(Global Object)
- <script> 태그에 하나만 존재하는 오브젝트이다.
- 모든 코드에서 공유가 가능하므로, `new` 키워드로 인스턴스를 생성할 필요가 없다.
- 오브젝트의 이름(Global)은 있지만 실체가 없기 때문에 작성할 수 없다.

### Global 함수/변수

- 전역 객체 내부의 함수와 변수를 전역 함수/변수라고 한다.
- 구분하여 함수 내분에 작성된 것을 지역(Local) 함수/변수라고 한다.

### 프로퍼티 리스트

**값**

- `NaN`: Not-a-Number
- `Infinity`: 무한대 값
- `undefined`: 정의되지 않음

**함수**

- `isNaN()`: 파라미터가 NaN인지 검사한다.
- `isFinite()`: 파라미터가 유한대인지 검사한다.
- `parseInt()`: 정수로 변환하여 반환한다.
- `parseFloat()`: 실수로 변환하여 반환한다.
- `eval()`: JS 코드 문자열을 실행한다.
- `encodeURI()`: URI로 인코딩하여 반환한다.
- `encodeURIComponent()`: 확장된 URI로 인코딩하여 반환한다.
- `decodeURI()`: encodeURI 함수의 인코딩 된 값을 디코딩한다.
- `decodeURIComponent()`: `encodeURIComponent` 함수의 인코딩 된 값을 디코딩한다.

### 전역 프로퍼티(값)

상수 개념으로 사용할 수 있다. (외부에서 프로퍼티의 값의 변경이 불가능하다.)

- delete 연산자로 삭제할 수 없다.

**예시 코드**

```javascript
console.log(NaN);
console.log(Infinity);
console.log(undefined);
```

### parse 함수

**ParseInt()**

- 값을 정수로 변환하여 반환한다.
- 0 또는 빈 문자열은 제외한다.
- 파라미터로 진수를 입력받아 변환할 수 있다.

```javascript
console.log(parseInt("-123.45")); // -123
console.log(parseInt("123xx")); // 123
console.log(parseInt("12AB34")); // 12

console.log(parseInt("0012")); // 00
console.log(parseInt("  12  ")); // 12
console.log(parseInt()); // NaN
```

**parseFloat()**

- 값을 실수로 변환하여 반환한다.
- 문자열의 실수 변환에 사용한다.
- 지수 표현도 변환할 수 있다.

```javascript
console.log(parseFloat("-123.45")); // -123/45
console.log(parseFloat("12.34AB56")); // 12.34
console.log(parseFloat("1.2e3")); // 1200
console.log(parseFloat()); // NaN
```

### isNaN, isFinite

- NaN, 유한대를 체크하는 함수

**isNaN()**

- 값의 NaN 여부를 true, false로 반환한다.
- `NaN === NaN` 표현식의 결과는 `false`이다. (**설계 실수**)
  - ES6에서는 `Object.is()` 함수가 제공된다.

```javascript
console.log(isNaN("aaa")); // true
console.log(isNaN()); // true

console.log(isNaN(100)); // false
console.log(isNaN("100")); // false
console.log(isNaN(null)); // false
```

**isFinite()**

- 값이 Infinity, NaN 일때 false를 반환한다.
- 값이 숫자로 변환되면 숫자로 인식된다.

```javascript
console.log(isFinite(0 / 0)); // false
console.log(isFinite(1 / 0)); // false
console.log(isFinite("ABC")); // false

console.log(isFinite(100)); // true
console.log(isFinite("100")); // true
```

### 인코딩 관련 함수

**encodeURI()**

- URI를 인코딩하여 변환한다.
- 인코딩 제외 문자: `영문자/숫자, # ; / ? : @ & = + $ , - _ . ! ~ * ( )`
- 인코딩 제외 문자를 제외하고 `%16진수...` 형태로 변환한다.

```javascript
var uri = "data?name=안";
console.log(encodeURI(uri)); // data?name=%EC%95%88
```

**encodeURIComponent()**

- encodeURI()의 확장된 버전이다.
- `; / ? : @ & = + $ ,` 문자도 인코딩한다.

**decodeURI()**

- 인코딩을 디코딩하여 반환한다.

```javascript
var uri = "data?name=%EC%95%88";
console.log(decodeURI(uri)); // data?name=안
```

**decodeURIComponent()**

- encodeURIComponent()로 인코딩 된 문자열을 디코딩한다.

### eval()

- 파라미터의 문자열을 자바스크립트 코드로 간주하여 실행한다.
- 실행 결과를 반환 값으로 사용한다.
- **그러나 코드를 직접 실행하므로 보안에 문제가 있어 사용을 권장하지 않는다.**

```javascript
var result = eval("parseInt('123.45')");
console.log(result); // 123
```

## 래퍼런스

https://www.inflearn.com/course/자바스크립트-비기너/
