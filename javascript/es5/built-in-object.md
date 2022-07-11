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
  - [String 오브젝트](#string-오브젝트)
    - [string type 기본](#string-type-기본)
    - [String()](#string)
    - [new String()](#new-string)
    - [valueOf()](#valueof-1)
    - [length](#length)
    - [trim()](#trim)
    - [toString()](#tostring-1)
    - [charAt()](#charat)
    - [indexOf()](#indexof)
    - [lastIndexOf()](#lastindexof)
    - [concat()](#concat)
    - [toUpperCase(), toLowerCase()](#touppercase-tolowercase)
    - [substring()](#substring)
    - [substr()](#substr)
    - [slice()](#slice)
    - [charCodeAt()](#charcodeat)
    - [fromCharCode()](#fromcharcode)
    - [localeCompare()](#localecompare)
    - [match()](#match)
    - [replace()](#replace)
    - [search()](#search)
    - [split()](#split)
  - [Object 오브젝트](#object-오브젝트)
    - [ES3기준 프로퍼티 리스트](#es3기준-프로퍼티-리스트)
    - [ES5에 추가된 기능](#es5에-추가된-기능)
    - [Object()](#object)
  - [Boolean 오브젝트](#boolean-오브젝트)
    - [프로퍼티](#프로퍼티)
    - [new Boolean()](#new-boolean)
    - [Boolean()](#boolean)
  - [JSON Object](#json-object)
    - [stringify()](#stringify)
    - [parse()](#parse)
  - [Date 오브젝트](#date-오브젝트)
    - [시간값 기준](#시간값-기준)
    - [프로퍼티 리스트](#프로퍼티-리스트)
  - [Math 오브젝트](#math-오브젝트)
    - [프로퍼티 리스트](#프로퍼티-리스트-1)
  - [래퍼런스](#래퍼런스)

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

**함수**

- `Number()`: 숫자 값으로 변환하여 반환

**프로토타입(Number.prototype)**

- `constructor`: 프로토타입 생성자
- `toString()`: 숫자를 문자 값으로 변환하여 반환
- `toLocaleString()`: 숫자를 지역화된 문자 갑승로 변환하여 반환
- `valueOf()`: 오브젝트의 원시(Primitive) 값 반환
- `toExponential()`: 지수 표현 방식으로 반환
- `toFixed()`: 고정 소숫점 표현 방식으로 반환
- `toPrecision()`: 고정 소숫점이나 지수 표현 방식으로 반환

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

## String 오브젝트

String 오브젝트는 문자 처리를 위한 오브젝트이다.

### string type 기본

- 문자열 연결: `+` 혹은 역슬래시(`\`)를 이용해서 연결한다.

  ```javascript
  var s1 = "abc" + "def";
  console.log(s1); // "abcdef"

  var s2 =
    "abc\
    def";
  console.log(s2); // abc   def
  ```

이처럼 기본적인 연산 말고도 String 오브젝트에서 제공하는 프로퍼티로 문자를 처리할 수 있다.

- `new String()`: String 인스턴스 생성

**함수**

- `String()`: 문자열로 변환하여 반환
- `fromCharCode()`: 유니코드를 문자열로 변환하여 반환

**프로퍼티**

- `length`: 문자열의 문자 수 반환

**프로토타입(String.prototype)**

- `constructor`: 생성자
- `valueOf()`: 원시 값 반환
- `toString()`: 문자열로 변환하여 반환
- `charAt()`: 해당 인덱스의 문자를 반환
- `indexOf()`: 일치하는 문자열 중에서 가장 앞의 인덱스 반환
- `lastIndexOf()`: 뒤에서부터 탐색했을 때 일치하는 문자열 중에서 가장 앞의 인덱스 반환
- `String.prototype.concat()`: 문자열 연결
- `toLowerCase()`: 영문 소문자로 변환
- `toUpperCase()`: 영문 대문자로 변환
- `trim()`: 문자열 앞 뒤의 공백 문자를 제거하여 반환
- `substring()`: 시작 인덱스에서 끝 인덱스 직전까지의 값을 반환
- `substr()`: 시작 인덱스에서 지정한 길이만큼의 문자 반환
- `slice()`: `substring()`과 비슷한 역할
- `match()`: 매치 결과를 반환
- `replace()`: 매치 결과를 지정값으로 대체
- `search()`: 검색된 첫 번째 인덱스를 반환
- `split()`: 구분자로 분리하여 반환
- `charCodeAt()`: 인덱스의 문자를 유니코드로 반환
- `localeCompare()`: 값 비교를 통해 비교 결과를 반환

### String()

- 변환 대상을 string type으로 변환하여 반환한다.
- 값을 작성하지 않으면 빈 문자열(`""`)을 반환한다.

**예시 코드**

- 아래 코드처럼 빈 문자열에 더하여 만들 수도 있지만, 가독성을 위하여 추천하지 않는다.

```javascript
var value = String(100);
console.log(typeof value); // string

console.log(value); // "100"
console.log("" + 100); // "100", 같은 결과
```

### new String()

- String 인스턴스를 생성하여 반환한다.
- 파라미터로 값을 입력받는다. 값을 String 타입으로 변환하여 원시 값으로 저장한다.
- 생성한 인스턴스의 `typeof` 결과는 `object`이다.

**예시 코드**

```javascript
var obj = new String(100);
console.log(typeof obj); // object
```

### valueOf()

- String 인스턴스의 원시 값을 반환한다.
- 파라미터를 입력받지 않는다.

```javascript
var obj = new String(100);
console.log(obj); // String {'100'}
console.log(obj.valueOf()); // "100"
```

### length

- 문자열의 문자 수를 반환한다.
- `for` 문을 활용하여 문자열의 문자 각각에 반복하여 접근할 수 있다.
- String 인스턴스가 아닌 문자열 값에도 사용할 수 있다. (자바스크립트 엔진이 내부적으로 인스턴스를 생성하여 `length` 프로퍼티를 호출한다.)

**예시 코드**

```javascript
var value = "ABC"; // 문자 값 (인스턴스X)
for (var i = 0; i < value.length; i++) {
  console.log(i, value[i]);
}
// 실행 결과
// 0 A
// 1 B
// 2 C
```

### trim()

- 대상 문자열의 앞 뒤의 화이트 스페이스를 삭제한다.
- 반환 결과도 문자열이므로 메소드 체인과 같은 방식을 사용할 수 있다.

**예시 코드**

- 원본 문자열은 변하지 않는 것을 주의하자.

```javascript
var value = "  ABCD  ";

console.log(value); // "  ABCD  "
console.log(value.trim()); // "ABCD"

console.log(value.length); // 8
console.log(value.trim().length); // 4
```

### toString()

- 데이터를 `string type` 으로 반환한다.
- `string type`을 `string type`으로 변환하는 이유?
  - String 오브젝트는 Object 오브젝트를 `__proto__`로 가진다.
  - Object 오브젝트에서도 `toString()`이 정의되어 있다.
  - 만약 String 오브젝트에서 `toString()`이 정의되어 있지 않다면 Object 오브젝트에서 찾는다. (`valueOf()`도 마찬가지이다.)

### charAt()

- 파라미터로 입력한 인덱스의 문자를 반환한다.
- 만약 인덱스 범위를 초과하면 빈 문자열을 반환한다.
- `charAt()`이 아니라 일반적으로 존재하지 않는 인덱스를 참조하면 `undefined`를 반환한다.

**예시 코드**

- 참고로 ES5 이상에서 대괄호를 이용하여 접근할 수도 있다.
- 대괄호로 없는 인덱스를 참조할 경우 `undefined`를 반환하는 것을 유의하자.

```javascript
var value = "ABCDE";
console.log(value.charAt(-1)); // ""
console.log(value.charAt(0)); // A
console.log(value.charAt(1)); // B
console.log(value.charAt(2)); // C
console.log(value.charAt(3)); // D
console.log(value.charAt(4)); // E
console.log(value.charAt(5)); // ""

console.log(value[0]); // A
console.log(value[5]); // undefined
```

### indexOf()

- 검색 대상에서 파라미터의 문자와 같은 첫번째 인덱스를 반환한다.
- 파라미터로 비교할 문자열과 검색의 시작 위치를 입력한다.
- 검색의 시작 위치는 기본값이 0이다.

**예시 코드**

- 왼쪽에서 오른쪽으로 검사한다.
- 파라미터가 하나이면 0번째 인덱스부터 검색한다.
- 여러개가 있더라도 가장 먼저 검색된 인덱스를 반환한다.

```javascript
var value = "ABCDABCD";
console.log(value.indexOf("A")); // 0
console.log(value.indexOf("B")); // 1
console.log(value.indexOf("AB")); // 0
console.log(value.indexOf("DA")); // 3

console.log(value.indexOf("A", 1)); // 4
```

**주의 사항**

- 파라미터로 입력한 시작 인덱스가 0보다 작거나 같으면 인덱스 0부터 검색한다.
- 시작 인덱스가 문자열의 길이보다 길다면 `-1`을 반환한다.
- 시작 인덱스로 들어온 값이 `NaN` 이라면 인덱스 0부터 검색한다.

### lastIndexOf()

- `indexOf()`를 오른쪽에서 왼쪽으로 검색한다.
- 특징이 같기 때문에 설명을 생략하겠다.

**예시 코드**

```javascript
var value = "ABCDABCD";
console.log(value.lastIndexOf("A")); // 4
console.log(value.lastIndexOf("A", 3)); // 0
```

### concat()

- 데이터에 파라미터로 입력한 문자열을 연결한다.
- 파라미터의 입력 순서대로 연결한다.
- String 인스턴스와 계산 할 경우 원시 값을 기준으로 연결한다.

**예시 코드**

```javascript
var value = "Hello".concat("world", "!");
console.log(value); // "Helloworld!"
```

### toUpperCase(), toLowerCase()

- 영문 대문자를 소문자로, 소문자를 대문자로 변환한다.

**예시 코드**

```javascript
var value = "abCD";
console.log(value.toUpperCase()); // ABCD
console.log(value.toLowerCase()); // abcd
```

### substring()

- 파라미터로 입력받은 시작 인덱스부터 끝 인덱스의 전까지 반환한다.
- 만약 두번째 파라미터(끝 인덱스)를 입력하지 않으면 문자열의 끝까지 반환한다.
- 파라미터를 모두 작성하지 않으면 전체 문자열을 반환한다.

**예시 코드**

```javascript
var value = "0123456789";
console.log(value.substring()); // "0123456789"
console.log(value.substring(5)); // "56789"
console.log(value.substring(0, 3)); // "012"
```

**주의 사항**

- 두번째 파라미터가 문자열 길이보다 크다면 문자열 끝까지 반환한다.
- 파라미터의 값이 음수 또는 `NaN` 이면 0으로 간주한다.

```javascript
console.log(value.substring(0, 100)); // "0123456789"
console.log(value.substring(-1, 3)); // "012"
console.log(value.substring("A", 3)); // "012"
```

### substr()

- 파라미터의 시작 인덱스부터 지정 문자 수 만큼을 반환한다.
- 만약 시작 인덱스가 음수이면 문자열의 `length` 만큼 더해서 사용한다.
- 두번째 파라미터를 작성하지 않으면 `infinity`로 사용한다. (끝까지 반환한다는 의미)

**예시 코드**

```javascript
var value = "ABCDEFG";
console.log(value.substr()); // "ABCDEFG"
console.log(value.substr(4)); // "EFG"
```

### slice()

- 파라미터로 입력받은 시작 인덱스부터 끝 인덱스의 전까지 반환한다.
- 첫번째 파라미터가 없거나 `NaN`일 경우 0으로 사용한다.
- 두번째 파라미터가 없다면 `length` 값을, 음수이면 `length` 값만큼 더해서 사용한다.

**예시 코드**

```javascript
var value = "ABCDEFG";
console.log(value.slice(1, 3)); // "BC"
console.log(value.slice(false, 3)); // "ABC"

console.log(value.slice(4, -2)); // "E" (4, 5)
console.log(value.slice(-5, -2)); // "CDE" (2, 5)
```

### charCodeAt()

- 파라미터로 입력한 인덱스의 문자의 유니코드 코드 포인트 값으로 반환한다.
- 만약 인덱스가 문자열의 `length` 값보다 크면 `NaN`을 반환한다.

**예시 코드**

```javascript
var value = "가나다라";
for (var i = 0; i < value.length + 1; i++) {
  console.log(i, value.charCodeAt(i));
}
// 실행 결과:
// 0 44032
// 4 1 45208
// 4 2 45796
// 4 3 46972
// 4 4 NaN
```

### fromCharCode()

- 파라미터의 유니코드 코드 포인트를 문자열로 변환하고 연결하여 반환한다.
- 파라미터로 여러개의 유니코드를 입력할 수 있다.
- `String.fromCharCode(...)`로 사용한다.

**예시 코드**

```javascript
console.log(String.fromCharCode(49, 65, 97, 44032)); // "1Aa가"
```

### localeCompare()

- 값을 비교하여 비교 결과를 반환한다.
  - 1: 앞이 더 크다.
  - 0: 같다.
  - -1: 뒤가 더 크다.
- 유니코드 사전 순으로 비교한다.

**예시 코드**

```javascript
var value = "B";
console.log(value.localeCompare("A")); // 1
console.log(value.localeCompare("B")); // 0
console.log(value.localeCompare("C")); // -1
```

> 아래는 정규 표현식을 활용한 프로퍼티인데, 정규 표현식 내용이 어려워 간단히 서술함.

### match()

- 정규 표현식 혹은 문자열에 매치된 결과를 리스트로 반환한다.
- 문자열을 파라미터로 전달할 경우 자바스크립트 엔진에서 정규 표현식으로 변환한다.

### replace()

- 정규 표현식 혹은 문자열에 매치된 결과를 대체할 값이나 함수 반환 값으로 대체한다.
- 치환 결과를 반환한다.

### search()

- 정규 표현식 혹은 문자열에 맞게 검색된 첫 번째 인덱스를 반환한다.
- 만약 매치되지 않으면 -1을 반환한다.

### split()

- 분리 대상을 분리자(정규 표현식, 문자열)로 분리하여 배열로 반환한다.
- 분리자는 배열에 포함되지 않는다.
- 만약 분리자가 없다면 배열에 원본 문자열을 담아서 반환한다.

## Object 오브젝트

파라미터 데이터 타입을 가지는 오브젝트 객체를 빌트인 Object 라고 한다.

- 모든 빌트인 오브젝트의 `__proto__`에 `Object.prototype`의 6개 메소드가 설정된다.

### ES3기준 프로퍼티 리스트

- new Object(): 파라미터 데이터 타입의 인스턴스를 생성한다.
- Object(): Object 인스턴스를 생성한다.

**프로토타입(Object.prototype)**

- `constructor`: 생성자
- `valueOf()`: 원시 값을 반환한다.
- `hasOwnProperty()`: 프로퍼티 소유 여부를 반환한다.
- `propertyIsEnumerable()`: 프로퍼티 열거 가능 여부를 반환한다.
- `isPrototypeOf()`: 프로토타입의 존재 여부를 반환한다.
- `toString()`: 문자열로 변환하여 반환한다.
- `toLocaleString()`: 지역화된 문자열로 반환한다.

### ES5에 추가된 기능

- 여러 기능의 함수(메소드X)가 추가되었다.
- 메소드가 아닌 함수가 추가되어서 다른 오브젝트들에게 추가적인 부담을 주지 않는다.

**함수**

- `defineProperty()`: 프로퍼티 추가 혹은 변경
- `defineProperties()`: 다수의 프로퍼티 추가 혹은 변경
- `getPrototypeOf()`: 프로토타입에 연결된 프로퍼티를 반환
- `getOwnPropertyNames()`: 프로퍼티 이름을 배열로 모두 반환
- `keys()`: 열거 가능한 프로퍼티 이름들을 반환
- `getOwnPropertyDescriptor()`: 디스크립터 속성 반환
- `preventExtensions()`: 프로퍼티 추가(확장)를 금지
- `isExtensible()`: 프로퍼티 추가 금지 상태인지 반환
- `seal()`: 프로퍼티 추가,삭제를 금지
- `isSealeD()`: 프로퍼티 추가,삭제 금지 상태인지 반환
- `freeze()`: 프로퍼티 추가,삭제,변경 금지
- `isFrozen()`: 프로퍼티 추가,삭제,변경 금지 상태인지 반환

**프로퍼티 디스크립터**

- `value`: `[[Value]]`, 설정된 값
- `writable`: `[[Writable]]`, 값 변경 가능 여부
- `get`: `[[Get]]`, getter, 값 반환 프로퍼티 함수
- `set`: `[[Set]]`, setter, 값 설정 프로퍼티 함수
- `enumerable`: `[[Enumerable]]`, 프로퍼티 열거 가능 여부
- `configurable`: `[[Configurable]]`, 프로퍼티 삭제 가능 여부

### Object()

- Object 인스턴스를 생성한다.
- `{name: value}` 형태의 파라미터를 입력받는다.
- 오브젝트 리터럴: `var obj = {};` 와 같은 방법으로도 인스턴스를 생성할 수 있다.

**예시 코드**

```javascript
var obj = Object({ name: "shyuuuuni" });
console.log(obj); // {name: 'shyuuuuni'}

var emptyObj = Object();
console.log(emptyObj); // {}
```

## Boolean 오브젝트

- Built-in Boolean Object
- true, false를 처리한다.
- 값이 있으면 true로 처리한다.
- undefined, null, NaN, 빈 문자열, 숫자타입 0 은 false로 처리한다.
- true를 1로, false를 0으로 변환한다.

### 프로퍼티

- `new Boolean()`: 인스턴스 생성
- `Boolean()`: `Boolean` 타입으로 변환

**프로토타입(Boolean.prototype)**

- `constructor`: 생성자
- `toString()`: `true`/`false` 문자열로 반환
- `valueOf()`: 원시 값 반환

### new Boolean()

- Boolean 인스턴스를 생성한다.
- 입력한 파라미터 값을 기준으로 true, false로 변환하여 원시 값으로 설정한다.
- 값이 있는 문자열이면 true로 설정한다.

**예시 코드**

- `false`가 저장되는 케이스
- `valueOf()`로 오브젝트의 원시 값을 볼 수 있다.

```javascript
var value = [undefined, null, NaN, 0, ""];
for (var i = 0; i < value.length; i++) {
  var obj = new Boolean(value[i]);
  console.log(i, obj.valueOf());
}
// 출력 결과
// 0 false
// 1 false
// 2 false
// 3 false
// 4 false
```

### Boolean()

- Boolean 값으로 변환한다.
- 인스턴스가 아닌 `true`, `false`로 변환한다.

**예시 코드**

```javascript
var value = [12, "1", "0", "false"];
for (var i = 0; i < value.length; i++) {
  console.log(i, Boolean(value[i]));
}
// 출력 결과
// 0 true
// 1 true
// 2 true
// 3 true
```

## JSON Object

- JSON: JavaScript Object Notation
- 데이터 송수신을 위한 텍스트 타입, json, txt 확장자를 가진다.

### stringify()

- `JSON.stringify()`
- 파라미터로 변환 대상 자바스크립트 타입을 입력받는다.
- 두번째 파라미터로 함수/배열을 입력받을 수 있다.
- 마지막 파라미터로 구분자를 입력받을 수 있다.

**예시 코드**

```javascript
var value = {
  book: "책",
  one: 1,
};
var result = JSON.stringify(value);
console.log(result); // {"book":"책","one":1}
```

- 아래 예시처럼 파라미터를 추가하여 함수를 적용할 수 있다.
- 문자열을 value로 가진 프로퍼티는 `undefined`를 리턴한다.
- `undefined`는 중괄호 내에서 `key-value` 모두 표시되지 않는다.

```javascript
function replacer(key, value) {
  if (typeof value === "string") {
    return undefined;
  }
  return value;
}

var foo = {
  foundation: "Mozilla",
  model: "box",
  week: 45,
  transport: "car",
  month: 7,
};
var result = JSON.stringify(foo, replacer);
console.log(result); // {"week":45,"month":7}
```

**주의 사항**

- `undefined` 사용 시 유의해야 한다.
- 아래 예시처럼 케이스마다 다른 결과를 가져올 수 있다.

```javascript
console.log(JSON.stringify(undefined)); // undefined
console.log(JSON.stringify([undefined])); // [null]
console.log(JSON.stringify({ value: undefined })); // {}
```

### parse()

- JSON 타입을 자바스크립트 타입으로 변환한다.
- 첫번째 파라미터로 변환 대상을, 두번째 파라미터로 파싱 데이터로 실행할 함수를 입력한다.

**예시 코드**

```javascript
var value = "123"; // JSON
try {
  var result = JSON.parse(value);
} catch (e) {
  console.log(e, "파싱 에러");
}
console.log(result); // 123
console.log(typeof result); // Number
```

- 아래처럼 함수를 사용 할 경우 key-value를 파라미터로 하는 함수를 실행한다.

```javascript
var value = '{"book": "책", "one": 1, "two": 2}';
var checkNumber = function (key, value) {
  if (typeof value === "string") {
    return undefined;
  }
  return value;
};
var result = JSON.parse(value, checkNumber);
console.log(result); // {one: 1, two: 2}
```

## Date 오브젝트

- 시간(년-월-일-시-분-초, 밀리초까지)을 관리할 수 있는 오브젝트
- 시간값(Time-value) 라고도 한다.
- UTC 기준 1970년 1월 1일 기준으로 밀리초를 제공한다. (최대 1억일을 지원한다.)

### 시간값 기준

- 월은 0부터 1월부터 시작한다.
  - 0: 1월, 1: 2월, ..., 11: 12월
- 일을 1부터 시작한다.
- 요일은 0부터 일요일부터 시작한다.
  - 0: 일요일, 1: 월요일, ..., 6: 토요일

**예시 코드**

```javascript
var obj = new Date(1970, 1, 1, 1, 1, 1, 1);
console.log(obj.toLocaleString()); // 1970. 2. 1. 오전 1:01:01
```

### 프로퍼티 리스트

**Date 함수**

- `Date()`: 현재 시각 반환
- `parse()`: 문자열 값을 밀리초로 변환
- `UTC()`: UTC 기준 밀리초로 변환
- `now()`: 현재 시각을 밀리초로 반환

**프로토타입(Date.prototype)**

- `constructor`: 생성자
- `toString()`: 일자와 시간을 변환하여 문자열로 반환
- `toUTCString()`: UTC 기준 일자와 시간을 반환
- `toISOString()`: ISO 8601 확장 형식의 간소 버전으로 일자와 시간 반환
- `toDateString()`: 연원일+요일을 읽기 쉬운 형태로 반환
- `toTimeString()`: 시분초+타임존을 읽기 쉬운 형태로 반환
- `toLocaleDateString()`: 연원일을 지역 언어로 반환
- `toLocaleTimeString()`: 시분초+오전/오후를 지역 언어로 반환
- `toJSON()`: JSON 형태의 일자/시간을 반환
- `vallueOF()`: 원시 값 반환
- `getTime()`: 시간값 반환
- `getYear()`: 세기 구분 + 연도 2자리 반환
- `getFullYear()`: 연도 반환
- `getDate()`: 일 반환
- `getMonth()`: 월 반환
- `getDay()`: 요일 반환
- `getHours()`: 시 반환
- `getMinutes()`: 분 반환
- `getSeconds()`: 초 반환
- `getMiliseconds()`: 밀리초 반환
- `getTimezoneOffset()`: UTC 시간차이를 분으로 반환
- `get + UTC + ...`: UTC기준 연도/일/시/초/ ... 반환

## Math 오브젝트

- 수학 계산용 오브젝트
- new 연산자로 인스턴스 생성 불가능하다. (Math, JSON, 글로벌 오브젝트)
- 함수 형태(Math.function())로 사용
- ES6에서 더 많이 기능이 추가되었다.

### 프로퍼티 리스트

**상수**

- `E`: 자연로그
- `LN10`: 자연로그 10
- `LN2`: 자연로그 2
- `LOG2E`: 밑이 2인 로그 e
- `LOG10E`: 밑이 10인 로그 e
- `PI`: 파이값
- `SQRT1_2`: 0.5의 제곱근
- `SQRT2`: 2의 제곱근

**함수**

- `abs()`: 절댓값
- `floor()`: 소수 이하를 버린 정수 반환
- `ceil()`: 소수 이하를 올린 정수 반환
- `round()`: 소수 이하를 반올림한 정수 반환
- `max()`: 최대값
- `min()`: 최소값
- `random()`: 0~1 사이의 난수 반환
- `pow()`: x의 y제곱값 반환

> 추가로 cos(), sin() 및 여러 다른 함수가 있지만 특수한 경우를 제외하고 잘 사용하지 않아서 따로 소개하지 않았다. ES6에서 Math 오브젝트에 더 많은 기능이 추가되어 딥러닝 등에서 많이 사용할 수 있게 되었다.

## 래퍼런스

https://www.inflearn.com/course/자바스크립트-비기너/
