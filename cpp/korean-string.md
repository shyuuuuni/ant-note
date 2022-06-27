# 한글 문자열

- [한글 문자열](#한글-문자열)
  - [문제 상황](#문제-상황)
  - [원인](#원인)
  - [해결 방법](#해결-방법)
    - [결론](#결론)
  - [한계](#한계)
  - [래퍼런스](#래퍼런스)

## 문제 상황

아래 예시 코드를 살펴보자.

```c++
#include <iostream>
#include <string>

int main(void) {
    std::string korean_str = "안녕하세요";

    std::cout << korean_str << "\n"; // 안녕하세요

    return 0;
}
```

위 코드는 한글 문자열 `"안녕하세요"` 를 출력하는 간단한 c++코드다.

코드를 컴파일해서 실행하면 다음과 같이 예상했던 결과가 출력된다.

출력:

```bash
안녕하세요
```

이제부터 진짜 문제가 발생한다.

위처럼 한글 문자열 그 자체를 출력했을 때 문제 없는것을 보고, 다른 문자열을 사용하는 것 처럼 그대로 사용하면 아래와 같은 문제가 발생한다.

```c++
#include <iostream>
#include <string>

int main(void) {
    std::string korean_str = "안녕하세요";

    std::cout << korean_str << "\n"; // 안녕하세요

    std::cout << korean_str[0] << "\n"; // 1. 안
    std::cout << korean_str.substr(0, 1) << "\n"; // 2. 안

    return 0;
}
```

출력:

```bash
안녕하세요
?
?
```

우리의 코드는 `1번` 주석의 코드에서는 문자 `'안'`을, `2번` 주석의 코드에서는 문자열 `"안"`을 기대했을 것이다.

그러나 위와 같이 `?` 출력이 발생한다.

## 원인

그 이유는 바로 문자열 인코딩 방식의 차이 때문이다.

위의 예시에서 `korean_str[0]`와 `substr` 함수는 `char`형 변수를 기본으로 한다.

즉 `char` 자료형은 `ASCII`코드를 기반으로 `utf-8`(1바이트씩) 인코딩으로 저장한다.

그러나 우리가 사용하려는 한글은 조금 다른 특징을 가진다.

한글은 기존 `ASCII`코드에 존재하는 문자처럼 1바이트 안에 표현할 수 없어서 위와 같은 문제가 발생한다.

`utf-8`에서 한글은 총 3개의 바이트를 하나의 문자로 취급한다.

따라서 `utf-8`환경에서 한글을 사용하려면 3바이트씩 잘라서 사용하면 된다.

> 참고: `utf-8` 대신 `UNICODE`를 사용해도 된다. 한글의 유니코드는 44032~55199 사이의 번호를 가진다.

## 해결 방법

```c++
#include <iostream>
#include <string>

int main(void) {
    std::string korean_str = "안녕하세요";

    std::cout << korean_str << "\n"; // 안녕하세요
    std::cout << korean_str.size() << "\n"; // 15

    return 0;
}
```

출력:

```bash
안녕하세요
15
```

앞서 설명한 것 처럼 **한글 문자 하나는 3개의 문자로 취급**되기 때문에 `korean_str` 문자열에 포함된 원소의 개수를 출력했을 때 `5`가 아닌 `15`가 출력된다.

간단한 해결법은 바로 문자를 3개씩 끊어서 사용하는 방법이다.

```c++
#include <iostream>
#include <string>

int main(void) {
    std::string korean_str = "안녕하세요";

    std::cout << korean_str << "\n"; // 안녕하세요

    std::cout << korean_str.substr(0, 3) << "\n"; // 1. 안
    std::cout << korean_str[0] << korean_str[1] << korean_str[2] << "\n"; // 2. 안

    return 0;
}
```

출력:

```bash
안녕하세요
안
안
```

첫번째 방법은 `substr` 함수의 두번째 파라미터로 3을 넣는 방법이다.

`substr` 함수는 첫번째 파라미터로 부분 문자열을 시작할 인덱스와 두번째 파라미터로 부분 문자열의 길이를 입력받는다.

따라서 0번째 인덱스부터 문자열 길이 3만큼 잘라서 사용하므로 정상적으로 출력 가능하다.

두번째 방법은 `korean_str` 문자열의 원소를 연속적으로 3번 접근하는 방법이다.

`std::cout << korean_str[0] << korean_str[1] << korean_str[2] << "\n";` 코드처럼 0번째부터 3개의 문자를 연속으로 출력하면 `안` 이라는 하나의 한글 문자가 출력된다.

### 결론

```c++
#include <iostream>
#include <string>

int main(void) {
    std::string korean_str = "안녕하세요";

    std::cout << korean_str << "\n"; // 안녕하세요

    std::string s = korean_str.substr(0,6);
    std::cout << s << "\n"; // 안녕

    // 빈 문자열에 추가
    s = "";
    s.push_back(korean_str[0]);
    s.push_back(korean_str[1]);
    s.push_back(korean_str[2]);

    std::cout << s << "\n"; // 안

    return 0;
}
```

최종적으로 위와같이 문자열을 선언하고 `substr` 으로 부분적으로 잘라서 사용하거나, 빈 문자열 `""`을 선언한 뒤 `push_back` 함수를 이용해 문자를 순서대로 추가하는 방식으로 사용하면 된다.

## 한계

> 요약: 코딩 테스트를 C++로 해야하는데 한글 문자열이 등장하면 파이썬을 사용하도록 하자.

지금까지 설명한 간단한 방법은 `한글 문자열`에 대해서 적용된다.

즉, 중간에 `ASCII` 문자열이 섞여있는 등 예외 상황을 처리하지는 못한다.

더 자세한 방법을 공부하고 싶다면 https://modoocode.com/292 링크에서 굉장히 자세히 설명해주셔서 참고하면 좋겠다.

## 래퍼런스

https://modoocode.com/292

https://blog.makebyhand.co.kr/227

https://unluckyjung.github.io/cpp/2020/07/04/Use_Korean/
