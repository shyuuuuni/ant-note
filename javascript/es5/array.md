# 빌트인 배열 오브젝트

- [빌트인 배열 오브젝트](#빌트인-배열-오브젝트)
  - [Array Object](#array-object)
    - [특징](#특징)
  - [배열 사용](#배열-사용)
    - [배열 초기화](#배열-초기화)
  - [ES3 프로퍼티 리스트](#es3-프로퍼티-리스트)
  - [ES5 프로퍼티 리스트](#es5-프로퍼티-리스트)
    - [isArray()](#isarray)
    - [indexOf()](#indexof)
    - [lastIndexOf()](#lastindexof)
  - [래퍼런스](#래퍼런스)

## Array Object

- 빌트인 배열 오브젝트이다.
- 대괄호 `[]` 내에 콤마로 원소를 구분하여 값을 작성한다.
- 배열 원소(element): 배열 내의 값들을 원소/요소/엘리먼트 등으로 부른다.
- 인덱스: 왼쪽부터의 엘리먼트의 위치를 0번, 1번, ... 등으로 표기한다.

### 특징

- 원소가 순서(인덱스)를 가지고 있다.
- 배열 전체를 순서대로 읽을 수 있다.
- 인덱스를 이용하여 원소의 값을 추출할 수 있다.

## 배열 사용

- `new Array()` 혹은 `Array()`로 생성할 수 있다.
- 대괄호를 이용해서 사용할 수 있다. (가장 일반적)

**예시 코드**

```javascript
var book = new Array();

var book = Array();

var book = [];
```

### 배열 초기화

- 대괄호 내에 원소를 작성하여 초기화 할 수 있다.
- 만약 쉼표로만 구분하여 작성하면 `undefined`로 초기화된다.
- 배열 내에 배열을 작성하여 다차원 배열을 정의할 수 있다.

**예시 코드**

```javascript
var list1 = [1, 2, 3];
var list2 = [
  [1, 2],
  [3, 4],
];
var list3 = [
  [[1], [2]],
  [[3], [4]],
];
```

## ES3 프로퍼티 리스트

초기 배열 객체의 프로퍼티를 먼저 소개한다.

- `new Array()`: 인스턴스 생성
- `Array()`: 인스턴스 생성

**Array 프로퍼티**

- `length`: 배열의 원소 수 반환

**프로토타입(Array.prototype)**

- `constructor`: 생성자
- `unshift()`: 배열 맨 앞에 원소를 삽입한다.
- `push()`: 배열 끝에 원소를 추가한다.
- `concat()`: 배열 끝에 값을 연결한다.
- `slice()`: 인덱스 범위의 원소들을 복사한다.
- `join()`: 원소의 분리자를 결합하여 반환한다.
- `toString()`: 원소들의 문자열로 연결하여 반환한다.
- `toLocaleString()`: 원소를 지역화 문자로 변환한 후 문자열로 연결하여 반환한다.
- `shift()`: 첫번째 원소를 삭제하고 삭제한 원소를 반환한다.
- `pop()`: 마지막 원소를 삭제하고 삭제한 원소를 반환한다.
- `splice()`: 원소를 삭제하고 새로운 원소를 삽입한다. (삭제한 원소를 반환한다.)
- `sort()`: 원소 값을 유니코드 순서로 정렬하여 반환한다.
- `reverse()`: 원소 위치를 역순으로 바꾸어 반환한다.

## ES5 프로퍼티 리스트

ES5 이후 사용할 수 있는 프로퍼티를 소개한다.

- isArray(): 배열 여부를 true/false로 반환한다.

**프로토타입(Array.prototype)**

- indexOf(): 지정한 값과 일치하는 첫번째 원소의 인덱스를 반환한다.
- lastIndexOf(): 지정한 값과 일치하는 마지막 원소의 인덱스를 반환한다.
- forEach(): 배열을 반복하면서 콜백 함수를 실행한다.
- every(): 반환 값이 false일 때 까지 콜백 함수를 실행한다.
- some(): 반환 값이 true일 때 까지 콜백 함수를 실행한다.
- `filter()`: 콜백 함수에서 true를 반환한 원소들만 반환한다.
- `map()`: 콜백 함수에서 반환한 값을 새로운 배열로 반환한다.
- `reduce()`: 콜백 함수의 반환 값을 파라미터 값으로 사용한다.
- `reduceRight()`: `reduce()`와 같지만 배열의 끝에서 앞쪽으로 진행한다.

### isArray()

- 체크 대상이 배열이면 true, 아니면 false를 반환한다.
- `typeof arrayObject` 값이 `object`로 표기되기 때문에 필요하다.

**예시 코드**

```javascript
console.log(Array.isArray([1, 2])); // true
console.log(Array.isArray(12)); // false
```

### indexOf()

- 파라미터와 같은 값의 원소 인덱스를 반환한다.
- 왼쪽에서 오른쪽으로 검색하고, 같은 값의 원소가 있다면 종료한다.
- 데이터 값 뿐만 아니라 타입도 체크한다.
- 두번째 파라미터 값의 인덱스부터 검색한다. (기본은 0이다.)

**예시 코드**

- 찾을 수 없으면 -1을 반환한다.

```javascript
var value = [1, 2, 3, 2, 1];
console.log(value.indexOf(1)); // 0
console.log(value.indexOf(1, 1)); // 4
console.log(value.indexOf("1")); // -1
```

### lastIndexOf()

- `indexOf()`의 마지막 인덱스를 반환한다.

**예시 코드**

```javascript
var value = [1, 2, 3, 2, 1];
console.log(value.lastIndexOf(1)); // 4
```

## 래퍼런스

https://www.inflearn.com/course/자바스크립트-비기너/
