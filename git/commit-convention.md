# Git Commit Convention

> Git 의 대표적인 장점 중 하나가 다른 사람과 협업을 할 수 있도록 제공하는 기능이다. 협업을 더 잘 하기 위해서 좋은 Commit Convention 을 따를 수 있도록 *Udacity Git Commit Message Style Guide* 를 소개한다.

## Udacity Git Commit Message Style Guide

[Udacity](https://www.udacity.com) 는 온라인 학습을 제공하는 사이트로, Computer Science 분야의 과목을 집중적으로 다루는 사이트이다.

한국의 [네이버 핵데이 Java 코딩 컨벤션](https://naver.github.io/hackday-conventions-java/) 처럼 해당 사이트에서 추천하는 컨벤션이 있는데, 그 중에서 [Udacity Git Commit Message Style Guide](https://udacity.github.io/git-styleguide/) 를 소개한다.

항상 이러한 컨벤션이 정답은 아니고 추천하는 사항이지만, 협업에 도움이 되고 자기 코드를 돌아볼 때에도 도움이 되므로 필요하다면 컨벤션을 적용하는 습관을 들이는 것을 추천한다.

## Commit Message Structure

```
type: Subject

body

footer
```

위와 같은 3개의 파트로 구성되어 있고, 각 파트는 빈 공백으로 구분한다.

각각에 대해 자세히 알아보자.

### Type

커밋의 의도를 설명한다. `Type` 의 종류는 다음과 같다.

```
feat: 새로운 기능 추가
fix: 버그 수정
docs: 문서 수정
style: 코드 포멧팅, 세미콜론(;) 추가 등 코드의 수정이 없는 변경
refactor: 코드 리팩토링
test: 테스트 추가, 테스트 리팩토링 등 일반 코드의 수정이 없는 변경
chore: 기타 설정 변경 (빌드 작업 업데이트, package manager 수정 등) 일반 코드의 수정이 없는 변경
```

### Subject

최대 50글자로 커밋의 내용을 요약하여 작성한다.

영문 작성 시 맨 앞글자를 대문자로 사용하고, 동사 원형을 사용한다.

마침표를 찍지 않는 것을 주의한다.

### body

최대 72자로 커밋에 대한 긴 설명(부연설명)이 필요할 때 작성한다.

`body` 는 제목 줄과 빈 공백으로 구분한 후에 작성한다. 필요하지 않을 경우 작성하지 않아도 된다.

### footer

Issue Tracker ID 등이 필요할 경우에 작성한다.

`footer` 또한 본문 줄과 빈 공백으로 구분한 후에 작성한다.

## Git 에 컨벤션 적용

위의 내용을 매번 찾아보기 힘들 수 있다. 따라서 `git commit` 명령어 시 컨벤션을 확인할 수 있도록 적용해보자.

먼저 아래와 같이 `.gitmessage.txt` 파일을 작성한다.

```
# type: Subject

# body

# footer

# --- git commit type ---
#   feat    : 새로운 기능 추가
#   fix     : 버그 수정
#   docs    : 문서 추가, 수정, 삭제
#   refactor: 코드 리팩토링
#   style   : 코드 포멧팅, 세미콜론(;) 추가 등 코드의 수정이 없는 변경
#   test    : 테스트 추가, 테스트 리팩토링 등 일반 코드의 수정이 없는 변경
#   chore   : 기타 설정 변경 (빌드 작업 업데이트, package manager 수정 등)
# --- git commit convention ---
#   제목은 최대 50글자로, 첫 글자를 대문자와 명령문으로 작성한다.
#   제목 줄의 끝은 마침표를 사용하지 않는다. 
#   각 줄의 사이는 빈 공백으로 분리한다.
#   여러줄의 메시지 작성 시 '-' 문자로 구분한다.
# ---
```

이후 아래 명령어로 git 커밋 설정을 변경한다.

```bash
git config --global commit.template [.gitmessage.txt 위치]
```

이후 `git commit` 명령어를 사용하면 위에서 커밋 시 위의 메세지가 함께 출력된다. '#' 문자는 무시되므로 편하게 커밋할 수 있다.

협업 뿐만 아니라 좋은 코드를 위해서라도 깃의 커밋 컨벤션을 지키는 것은 중요하다. 이제부터라도 커밋 컨벤션을 신경써서 작성하도록 하자.