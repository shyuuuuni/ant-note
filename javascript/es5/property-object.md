# 프로퍼티와 오브젝트

- [프로퍼티와 오브젝트](#프로퍼티와-오브젝트)
  - [프로퍼티란? 오브젝트란?](#프로퍼티란-오브젝트란)
    - [특징](#특징)
  - [프로퍼티 추가](#프로퍼티-추가)
  - [프로퍼티 접근](#프로퍼티-접근)
    - [for ~ in 문법](#for--in-문법)

## 프로퍼티란? 오브젝트란?

객체지향에서의 객체가 아니라 자바스크립트에서의 `Object`는 `Property` 들의 집합으로 구성된다.

- `Property` 란 `name: value` 형식의 쌍을 의미한다.
- `Object` 는 `{ name: value }` 형식을 의미한다. (중괄호 내부에 `Property` 집합)

### 특징

- `name` 에는 해당 프로퍼티의 이름을 작성한다. (`key` 라고도 불린다.)
- `value` 에는 자바스크립트에서 제공하는 타입을 작성한다.
- 숫자, 문자, 함수, `Boolean`, `Object` 등 대부분의 타입 값이 가능하다.

**예시 코드**

```javascript
var book = {
  name: "어린 왕자",
  price: 13000,
};
```

## 프로퍼티 추가

예시와 함께 접근 방법을 알아보자.

**예시 코드**

```javascript
var obj = {}; // 비어있는 object 생성
```

1. 점(`.`) 이용: `obj.name = "어린 왕자"`
2. 대괄호(`[]`) 이용: `obj["name"] = "어린 왕자"`
3. 대괄호와 변수 이용
   ```javascript
   var x = "name";
   obj[x] = "어린 왕자"; // obj["name"] = "어린 왕자"
   ```

**특징**

`Object` 내부에 해당 `name` 의 프로퍼티가 있다면 `value`를 갱신한다.

만약 없다면 새로운 프로퍼티를 추가한다.

## 프로퍼티 접근

마찬가지로 점(`.`)과 대괄호(`[]`) 를 이용하여 프로퍼티에 접근할 수 있다.

**예시 코드**

```javascript
var book = {
  name: "어린 왕자",
  price: 10000,
};

var bookName = book.name;
var price = book["price"];
console.log(bookName, price); // 어린 왕자 10000 출력
```

만약 존재하지 않는 프로퍼티에 접근하면 `undefinded`를 반환한다.

### for ~ in 문법

**형태:**

```javascript
for (var 변수 in object) {
  // statements
}
```

- `object`의 각 프로퍼티 `name`을 변수에 할당한다.
- `for` 문 내부에서 `object[변수]` 형식으로 `name: value` 프로퍼티에 접근할 수 있다.
- 주의점으로 프로퍼티가 작성된 순서대로의 접근을 보장하지 않는다.

**예시 코드**

```javascript
var sports = {
  soccer: "축구",
  baseball: "야구",
};

for (var name in sports) {
  console.log(name, sports[name]);
}
// 출력 결과:
// soccer 축구
// baseball 야구
```
