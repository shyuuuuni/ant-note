# 빌트인 오브젝트 정리

- [빌트인 오브젝트 정리](#빌트인-오브젝트-정리)
  - [빌트인(Built-in) 오브젝트란?](#빌트인built-in-오브젝트란)
  - [Number 오브젝트](#number-오브젝트)
    - [Number 상수](#number-상수)
    - [Number()](#number)
    - [new Number()](#new-number)
    - [valueOf()](#valueof)
    - [toString()](#tostring)
    - [toLocaleString()](#tolocalestring)
    - [toExponential()](#toexponential)
    - [toFixed()](#tofixed)

## 빌트인(Built-in) 오브젝트란?

- 빌트인(Built-in): 자바스크립트 언어에 미리 포함된 값, 타입, 오브젝트 등을 의미한다.
- 빌트인 타입: `Undefined, Null, Boolean, Number, String, Object`
- 빌트인 연산자: `+ - * / % ++ --` 등
- 빌트인 오브젝트: `오브젝트.프로퍼티` 와 같은 형태로 접근하여 사용할 수 있도록 제공한다.

**예시 코드**

```javascript
console.log(Number.isNaN(100)); // false 출력
```

## Number 오브젝트

Number 오브젝트는 수를 처리하기 위한 오브젝트이다.

**프로퍼티 리스트**

- `new Number()`: 인스턴스 생성
- `Number()`: 숫자 값으로 변환하여 반환
- `Number.prototype.constructor`: 프로토타입 생성자
- `Number.prototype.toString()`: 숫자를 문자 값으로 변환하여 반환
- `Number.prototype.toLocaleString()`: 숫자를 지역화된 문자 갑승로 변환하여 반환
- `Number.prototype.valueOf()`: 오브젝트의 원시(Primitive) 값 반환
- `Number.prototype.toExponential()`: 지수 표현 방식으로 반환
- `Number.prototype.toFixed()`: 고정 소숫점 표현 방식으로 반환
- `Number.prototype.toPrecision()`: 고정 소숫점이나 지수 표현 방식으로 반환

### Number 상수

Number 오브젝트에서 제공하는 **변경과 삭제할 수 없는** 상수를 의미한다.

- `Number.MAX_VALUE`: 숫자로 표현할 수 있는 최대 값
- `Number.MIN_VALUE`: 숫자로 표현할 수 있는 최소 값
- `Number.NaN`:` Not-a-Number` 를 의미한다. (숫자로 표현할 수 없음.)
- `Number.POSITIVE_INFINITY`: `infinity` 값
- `Number.NEGATIVE_INFINITY`: `-infinity` 값

### Number()

- 파라미터 값을 숫자 타입으로 변환한다.
- 파라미터 값을 숫자로 변환시킬 수 있으면 숫자로 변환한다. (예를 들어 문자열 `"123"`을 숫자 `123`으로 변환하여 계산한다.)
- 파라미터 값이 없다면 0을 반환한다.

**예시 코드**

- 숫자로 변환할 수 없다면 `NaN` 을 반환하는 것을 주의해야 한다.

```javascript
console.log(Number(1)); // 1
console.log(Number("2")); // 2
console.log(Number("A")); // NaN

console.log(Number(0x20)); // 32
console.log(Number(true)); // 1
console.log(Number(false)); // 0
console.log(Number(null)); // 0
console.log(Number(undefined)); // NaN
```

### new Number()

- Number 오브젝트의 인스턴스를 생성하여 반환한다.
- `typeof` 의 값은 `object` 를 반환한다.
- 파라미터로 값을 입력받을 수 있다.
- 만약 숫자가 아닌 값을 입력받을 경우 숫자로 변환하여 입력한다. (변환이 불가능 한 경우 `NaN` 값을 가진다.)

**예시 코드**

```javascript
var obj = new Number(100);
console.log(obj.valueOf()); // 100 출력
```

**작동**

- Number 인스턴스의 `__proto__`(혹은 `[[prototype]]`) 내부에 `[[PrimitiveValue]]` 값에 생성 시 입력한 값을 저장한다.
- `[[PrimitiveValue]]`: 원시(Primitive) 값을 저장한다. 더이상 분해할 수 없는 가장 낮은 단계의 값을 의미한다.
- 숫자 연산자를 사용할 경우 Number 인스턴스의 원시 값과 계산한다.

> 참고) 원시 값을 가지는 오브젝트는 `Boolean, Date, Number, String`이 있다.

### valueOf()

- Number 오브젝트의 원시 값을 반환한다.
- 파라미터를 입력받지 않는다.

### toString()

- 데이터를 문자열 타입을 변환한다.
- 파라미터로 변환할 진수(2진수~36진수)를 입력한다. 입력하지 않으면 기본적으로 10진수 기준으로 변환한다.

**예시 코드**

- 주의 사항으로 아래 코드처럼 `20.toString()`과 같은 방식은 에러가 발생한다.
- `20`이 아닌 `20.` 을 값으로 인식하기 때문이다. 따라서 점을 두개 사용하여 변환한다.

```javascript
var value = 20;
console.log(value.toString()); // 20 출력

console.log(20.toString()); // 오류 발생
console.log(20..toString()); // 20 출력
```

### toLocaleString()

- 숫자를 브라우저가 지원하는 지역화된 문자로 변환한다.
- 변환 형태가 브라우저의 역할임에 주의한다.
- ES5에서는 파라미터를 사용할 수 없지만, ES6부터는 파라미터에 변환할 언어 타입을 선택할 수 있다.
- 지역화를 지원하지 않을 경우 `toString()` 을 호출한다.

**예시 코드**

```javascript
var value = 1234.56;
console.log(value.toLocaleString()); // 1.234,56 출력
console.log(value.toLocaleString("de-DE")); // 1.234,56(독일) 출력
console.log(value.toLocaleString("zh-Hans-CN-u-nu-hanidec")); // 一,二三四.五六(중국) 출력
```

### toExponential()

- 숫자를 지수 표기한 문자열로 변환하여 반환한다.
- 파라미터에 소수점 이하 자릿수를 입력한다.(0~20) 만약 소수가 잘리면 해당 자리에서 반올림한다.
- `변환 대상의 첫 자리`.`나머지 자릿수` `e+n` 형태 (지수 표현)

**예시 코드**

```javascript
var value = 1234;
console.log(value.toExponential()); // 1.234e+3 출력
console.log(value.toExponential(2)); // 1.23e+2 출력
```

### toFixed()

- 고정 소숫점 표기로 변환하여 문자열로 반환한다.
- 파라미터로 반환할 소수 이하 자릿수를 입력한다.
- 파라미터의 값(소수 이하 자릿수)보다 소수의 자릿수가 길면 나머지 소수 자릿수에서 반올림한다.
- 파라미터의 값이 더 크면 나머지 자리를 0으로 채워서 반환한다.

**예시 코드**

```javascript
var value = 1234.56789;
console.log(value.toFixed()); // 1235 (5에서 반올림)
console.log(value.toFixed(3)); // 1234.568 (8에서 반올림)
console.log(value.toFixed(10)); // 1234.5678900000 0으로 채운다.
```
