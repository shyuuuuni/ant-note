# Statement 정리

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

## 래퍼런스

https://www.inflearn.com/course/자바스크립트-비기너/
