# Statement 정리

- [Statement 정리](#statement-정리)
  - [Statement](#statement)
    - [화이트 스페이스](#화이트-스페이스)
    - [세미콜론 자동 삽입](#세미콜론-자동-삽입)
  - [Block](#block)
  - [if](#if)
  - [debugger](#debugger)
  - [while](#while)
    - [do ~ while](#do--while)
  - [for](#for)
    - [break](#break)
    - [continue](#continue)
  - [switch](#switch)
  - [try ~ catch](#try--catch)
    - [throw](#throw)
  - [strict](#strict)
  - [래퍼런스](#래퍼런스)

## Statement

`세미콜론 (;)` 으로 끝나는 자바스크립트의 실행 단위

- 예시: `var book = "책;`

### 화이트 스페이스

가독성을 위해 사용하는 `보이지 않는` 문자를 화이트 스페이스라고 한다.

아래와 같이 여러 종류마다 기능을 가지고 있다.

_White Space_

- `\u0009`: Horizontal Tab
- `\u000B`: Vertical Tab
- `\u000C`: Form feed
- `\u00A0`: NBSP(No-break space)
- `\uFFF`: BOM(Byte Order Mark)

_Line Terminator_

- `\u000A`: LF(Line Feed)
- `\u000D`: CR(Carriage Return)
- `\u2028`: LS(Line Separator)
- `\u2029`: Paragraph Separator

### 세미콜론 자동 삽입

자바스크립트 엔진이 코드를 분석하고 문장(Statement) 끝에 세미콜론을 자동으로 붙여준다.

즉, 세미콜론으로 문장의 끝을 표시하지 않아도 자동으로 문장이 끝나게 된다.

**예시 코드**

- 아래 코드에서 첫번째 줄의 끝에 세미콜론을 붙이지 않아서 에러가 발생해야 한다.
- 하지만 자바스크립트 엔진에서 자동으로 `var x = 1;` 과 같이 설졍해줘서 오류 없이 선언된다.

```javascript
var x = 1;
var y = 2;
```

## Block

`{ Statements... }` 와 같은 형태를 블록(Block) 이라고 한다.

- 블록 내를 실행 그룹으로 취급한다.
- 블록 내부에는 문장들의 리스트를 작성한다. (Optional, 작성하지 않아도 된다.)
- 즉 블록 안의 모든 문장을 실행한다.

## if

`if ( [expression] ) [statement]` 또는 `if ( [expression] ) [statement] else [statement]` 형태를 if문이라고 한다.

- 먼저 `expression`을 평가하여 true/false를 반환한다.
- `true`이면 첫번째 문장을 실행한다.
- `false`이면 `else` 뒤의 문장을 실행한다.

**예시 코드**

```javascript
var x = 1,
  y = 1;

if (x === y) console.log("same"); // "same" 출력

if (x === y) {
  console.log("same"); // "same" 출력
}
```

블록을 사용하지 않으면 세미콜론까지 조건에 해당하는 문장들을 실행한다.

(그러나 일관성을 위해 블록으로 감싸는 것을 추천한다.)

**예시 코드**

```javascript
var x = 1,
  y = 1;

if (x === 1) console.log(1); // 1 출력
console.log(2); // 2 출력
```

false를 반환했을 경우 `else` 뒤의 문장을 실행한다.

**예시 코드**

```javascript
var x = 1,
  y = 2;

if (x === y) {
  console.log("same");
} else {
  console.log("diff");
} // diff 출력
```

## debugger

- ES5부터 지원하는 기능으로 이름 그대로 디버깅과 관련된 기능을 제공한다.
- `debugger` 가 표시된 위치에서 실행을 멈춘다.
- 개발자 도구가 열려 있을 때 작동한다.
- `Breaking point` 등과 연계하여 효율적으로 디버깅을 진행할 수 있다.

**예시 코드**

- 개발자 도구가 열려 있는 상태에서 아래 코드는 `debugger;` 라인에서 멈춘다.
- 개발자 도구의 기능을 이용하여 `Step into next function call` 등 버튼을 사용하여 다음 줄로 넘어갈 수 있다.

```javascript
var x = "hello, world!";

debugger; // 실행 정지

console.log(x); // "hello, world!" 출력
```

## while

`while ( [expression] ) [statement]` 형태를 while문이라고 한다.

- expression 의 평가 결과가 false를 반환할 때 까지 문장을 반복한다.
- 종료 조건을 정확히 설정하지 않으면 무한 루프에 빠질 수 있다.

**예시 코드**

```javascript
var k = 1;
while (k < 3) {
  console.log(k);
  k++;
} // 1 2 출력
```

### do ~ while

`do [statement] while ( [expression] ) [statement]` 형태를 do~while문 이라고 한다.

- `do [statement]` 부분을 먼저 실행한다.
- `while ( [expression] )` 부분의 조건을 만족하지 않으면 do 문의 문장을 다시 실행한다.
- 조건을 만족하면 while 문의 문장을 실행한다.

**예시 코드**

```javascript
var k = 0;
do {
  console.log("do:", k);
  k++;
} while (k < 3);
{
  console.log("while:", k);
}
// 출력 결과:
// do: 0
// do: 1
// do: 2
// while: 3
```

## for

`for ( [초기 설정] ; [비교 조건] ; [증가/감소] ) [expression]` 형태의 구문을 for문 이라고 한다.

- `[비교 조건]`의 평가 결과가 true를 반환하면 아래 문장을 반복하여 실행한다.
- `for` 내부의 세 가지 자리는 Optional이다. 즉 비워둔 상태로도 사용할 수 있다.

**예시 코드**

```javascript
for (var k = 0; k < 2; k++) {
  console.log(k);
}
// 실행 결과:
// 0
// 1
```

### break

- 반복문 내부에서 반복문을 중간에 종료하기 위해 사용하는 식별자이다.
- `break;` 로 사용한다.
- `for, for ~ in, while, do ~ while, switch` 등에서 사용한다.

**예시 코드**

```javascript
var k = 0;
while (k < 10) {
  if (k === 5) {
    break;
  }
  console.log(k);
  k++;
}
// 실행 결과:
// 0
// 1
// 2
// 3
// 4
```

### continue

- 반복문 내부에서 반복문의 처음(조건 검사) 단계로 분기하는 식별자이다.
- `continue;` 로 사용한다.
- `for, for ~ in, while, do ~ while` 등에서 사용한다.

**예시 코드**

- `i` 값이 0부터 9까지 입력되는데, 값이 짝수(`i % 2 === 0`) 일 경우 `continue` 문을 만난다.
- `continue;` 코드를 실행하면, `for`문의 `증가/감소` 부분에 따라서 `i++`이 실행된다.
- 이후 다시 조건 검사를 통해 10보다 작은지 확인한 후, 블록을 반복하여 실행한다.

```javascript
for (var i = 0; i < 10; i++) {
  if (i % 2 === 0) {
    continue;
  }
  console.log(i);
}
// 실행 결과:
// 1
// 3
// 5
// 7
// 9
```

## switch

- 형태:
  ```javascript
  switch ( [expression] ) {
    case [expression-1]: [statement]
    case [expression-2]: [statement]
    ...
    default: [statement]
  }`
  ```
- `switch` 이후의 표현식의 평가 값과 일치하는 `case` 문의 문장부터 실행한다.
- 즉, 해당 위치부터 아래의 문장을 계속 실행한다.
- 만약 특정 문장까지만 실행하기 위해서는 `break`를 활용한다.
- 일치하는 평가 값이 없다면 `default` 의 문장을 실행한다.

**예시 코드**

```javascript
var x = 1;
// 1. break X
switch (x) {
  case 1:
    console.log(1);
  case 2:
    console.log(2);
}
// 실행 결과:
// 1
// 2

// 2. break O
switch (x) {
  case 1:
    console.log(1);
    break;
  case 2:
    console.log(2);
    break;
}
// 실행 결과:
// 1
```

**예시 코드**

- 만족하는 평가 값이 없으면 `default` 위치의 문장을 실행한다.
- 만약 `default`에 `break` 가 없다면 그 아래 문장들도 실행한다.

```javascript
var x = 3;

switch (x) {
  case 1:
    console.log(1);
    break;
  case 2:
    console.log(2);
    break;
  default:
    console.log("no match");
    break;
} // "no match" 출력
```

**예시 코드**

- 혹은 여러 조건이 하나의 문장을 실행시킬 수 있다.

```javascript
var x = 3;

switch (x) {
  case 1:
  case 2:
  case 3:
    console.log("<= 3");
} // "<= 3" 출력
```

## try ~ catch

- 형태:
  - `try { [statement] } catch ( [식별자] ) { [statement] }`
  - `try { [statement] } finally { [statement] }`
  - `try { [statement] } catch ( [식별자] ) { [statement] } finally { [statement] }`
- `try` 내부의 문장에서 예외(Exception) 발생을 감지한다.
- 발생된 예외를 `catch` 문의 식별자로 설정한 후, 내부의 블록을 실행한다.
- `finally` 블록은 예외 발생과 관계 없이 항상 마지막에 실행되는 블록이다.

**예시 코드**

- 선언되지 않은 변수 `chicken`을 `value`에 할당하기 때문에 예외가 발생한다.
- 예외 발생을 감지하여 아래의 출력 코드가 실행된다.

```javascript
var value; // 할당되지 않음
try {
  value = chicken;
} catch (error) {
  console.log("error catch!");
} finally {
  console.log("finished.");
}
// 실행 결과
// "error catch!"
// "finished."
```

### throw

예외 처리마다 출력을 하는 것 보다는 명시적인 예외를 발생시키는 것이 좋다.

- `throw [epxression]`: 명시적으로 예외를 발생시킬 수 있다.
- 예외가 발생되면 해당 `try` 블록 아래의 코드는 실행되지 않는다.

**예시 코드**

```javascript
try {
  throw "예외";
} catch (error) {
  console.log(error); // "예외" 출력
}

try {
  throw new Error("예외 객체");
} catch (error) {
  console.log(error.message); // "예외 객체" 출력
}
```

## strict

- `"ust strict"` 문자열을 작성한다.
- 작성한 코드 이후 엄격하게 자바스크립트 문법을 사용하겠다는 선언을 의미한다.
- ES5 부터 지원한다.

**예시 코드**

- 첫번째 코드는 `var` 키워드가 없으므로 틀린 코드이다.
- 그러나 자바스클비트 엔진이 자동으로 변수를 선언하고 값을 할당해준다.

```javascript
book = "책";
console.log(book); // 책 출력
```

- 두번째 코드는 엄격한 자바스크립트 문법을 사용한다.
- 즉 예외를 발생시킨다.

```javascript
"use strict";
try {
  book = "책";
  console.log(book);
} catch (error) {
  console.log(error.message); // "book is not defined" 출력
}
```

가장 중요한 실수를 방지할 수 있으므로 가급적 `"use strict";` 를 사용하도록 하자.

## 래퍼런스

https://www.inflearn.com/course/자바스크립트-비기너/
