# Java Type

## 원시(Primitive) 타입

자바에서 제공하는 8가지 기본형 타입을 원시 타입이라고 한다.

- 원시 타입 종류: `byte, short, int, long, float, double, boolean, char`
- 원시 타입은 종류에 따라 값의 범위와 기본값이 달라진다.

### 특징

- null 저장이 불가능하다.
- 실제 값을 저장하므로 스택에 저장된다.

### 원시 타입 종류

**정수형**

- byte: 8비트 부호있는 정수값
  - 기본값: 0
  - 범위: -128 ~ 127
- short: 16비트 부호 있는 정수값
  - 기본값: 0
  - 범위: -32,768 ~ 32,767
- int: 32비트 부호 있는 정수값
  - 기본값: 0
  - 범위: -2,147,483,648 ~ 2,147,483,647
- long: 64비트 부호 있는 정수값
  - 기본값: 0
  - 범위: -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807

**실수형**

- float: 단일 정밀도 32비트 IEEE 754 부동 소수점 값
  - 기본값: 0.0f
  - 범위: (3.4 X 10^(-38)) ~ (3.4 X 10^38) 의 근사값
- double: 이중 정밀도 64비트 IEEE 754 부동 소수점 값
  - 기본값: 0.0d
  - 범위: (1.7 X 10^(-308)) ~ (1.7 X 10^308) 의 근사값

**논리형**

- boolean: true, false의 부울 데이터 값
  - 기본값: false
  - 범위: true/false

**문자형**

- char: 단일 16비트 유니코드 문자 값
  - 기본값: '\u0000'
  - 범위: '\u0000'(0) ~ '\uffff'(65,535)

## 참조(Reference) 타입

8가지 원시 타입을 제외한 나머지 타입을 참조 타입이라고 한다.

### 특징

- 빈 곳을 참조한다는 의미의 null을 할당받을 수 있다.
- 스택에서는 참조할 데이터의 주소를 저장하고, 실제 데이터는 힙에 저장한다.

### 참조 타입 종류

- Array, Enum, Class 등

## 원시 타입 vs 참조 타입

### 접근 속도

![img](https://www.baeldung.com/wp-content/uploads/2018/08/plot-benchmark-primitive-wrapper-3.gif) \*출처: [[2]](https://www.baeldung.com/java-primitives-vs-objects)

원시 타입은 스택 메모리에 그대로 값을 저장한다.

반면 참조 타입은 스택 메모리에서는 주소를, 실제 데이터는 힙에 저장하므로 값에 접근할 때 마다 시간이 더 소요된다.

### 메모리 사용량

원시 타입은 그 타입에 맞는 데이터를 저장하므로 long이나 double 타입에서 최대 64bit를 사용한다.

그러나 참조 타입의 경우 1비트짜리 boolean을 저장하는 Boolean 타입이 128bit를 사용할 정도로 메모리 사용량이 크게 차이난다.

## 래퍼런스

[1] https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html

[2] https://www.baeldung.com/java-primitives-vs-objects

[3] https://gbsb.tistory.com/6
