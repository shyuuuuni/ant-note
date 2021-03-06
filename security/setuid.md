# Set-UID

> Linux 운영체제에서 공격에 사용될 수 있는 Set-UID에 대해 간단히 소개한다.

- [Set-UID](#set-uid)
  - [리눅스의 접근 제어](#리눅스의-접근-제어)
  - [패스워드 딜레마](#패스워드-딜레마)
  - [Set-UID](#set-uid-1)
  - [Set-UID 설정](#set-uid-설정)
  - [예시](#예시)

## 리눅스의 접근 제어

리눅스에서 어떤 자원에 접근할 때 사용자 혹은 그룹의 권한을 확인한다. 리눅스에서 설정되어있는 이러한 정책을 **Access Control List**이라고 한다.

사용자와 그룹은 각각 UID, GID 라고 하는 ID로 구분되며, 그 중 최상위 사용자 **root의 UID 값은 0이다.**

리눅스는 파일 혹은 디렉토리별로 읽기, 쓰기, 실행권한을 설정할 수 있다. 파일의 경우 위와 같지만 폴더의 경우 다음과 같이 약간 다른점이 있다.

- r: 폴더의 내용을 읽을(list) 수 있는 권한
- w: 폴더 내에서 파일이나 폴더를 생성할 수 있는 권한
- x: 폴더에 입장할 수 있는 권한

이러한 rwx 권한을 소유자(owner), 그룹(group), 기타(other) 각각 설정할 수 있다.

> 참고 : 하지만 rwx 권한을 일일히 설정하기 힘드므로 리눅스에서 사용자가 생성한 파일 혹은 폴더에 적용하는 권한을 **umask** 라고 한다.

## 패스워드 딜레마

Set-UID 를 알아보기 전에, 간단한 딜레마 상황을 생각해보자.

리눅스 운영체제를 사용한다면 사용자별로 패스워드가 걸려있다. `/etc/shadow` 파일은 이러한 패스워드를 관리하는 파일이다. 해당 파일의 권한은 `-rw-------` 이고, 즉 소유자(Owner)인 root만 읽고 쓸 수 있는 파일이다.

하지만 종종 보안을 위해 사용자가 주기적으로 패스워드를 변경해야 한다. 이를 위해 `passwd` 라는 명령어로 비밀번호를 변경할 수 있다.

`shadow` 파일은 root만 변경할 수 있는데 어떻게 일반 사용자가 `shadow` 파일을 변경하여 비밀번호를 변경할 수 있을지 알아보자.

## Set-UID

> 다른 사용자가 프로그램을 실행할 때 그 프로그램의 소유자가 실행한 것과 같은 권한으로 실행할 수 있도록 하는 것

앞서 설명한 `passwd` 라는 파일과 같은 경우가 Set-UID 가 적용된 프로그램이다. (소유자인 root의 권한으로 실행되므로 `passwd` 명령어를 통해 `shadow`파일을 수정할 수 있다.)

어떻게 이런 일이 가능할까?

모든 프로세스는 다음과 같은 두개의 UID를 가진다.

- RUID (Real UID) : 프로세스의 소유자의 ID
- EUID (Effective UID) : 프로세스의 권한 ID, **리눅스의 접근 제어는 EUID를 기준으로 작동한다.**

일반적인 프로그램은 RUID와 EUID가 같은 상태로 실행된다. 그러나 **Set-UID가 적용된 프로그램은 RUID와 EUID가 다른 상태로 실행**된다. 프로그램을 실행하는 동안 EUID가 해당 프로그램의 소유자의 ID로 설정되기 때문이다. (만약 소유자가 root라면 프로그램 내에서 root권한을 가진다.)

## Set-UID 설정

Root Set-UID 프로그램을 만들어보자.

1. `chown` 명령어로 소유자를 root로 변경한다.

```bash
sudo chown root myfile
ls -l myfile
-rwxr-xr-x 1 root seed ...
```

2. `chmod` 명령어로 권한을 변경하여 Set-UID 권한을 설정한다.

```bash
sudo chmod 4755 myfile
```

위와 같은 과정을 거치면 Set-UID 프로그램을 만들 수 있다.

2번의 `chmod` 시 4755 권한을 설정하는 것을 조금 더 자세히 알아보자.

리눅스의 권한은 맨 앞의 권한을 제외하고 소유자, 그룹, 기타 각각을 3비트로 표현한다. 즉 소유자, 그룹, 기타 각각의 rwx 권한이 있다면 1, 없다면 0으로 표현한다.

예를 들어 0755의 경우를 살펴보자

```
7 : 111 - 소유자는 r, w, x 권한을 가지고 있다.
5 : 101 - 그룹은 r, x 권한을 가지고 있다.
5 : 101 - 기타는 r, x 권한을 가지고 있다.
```

그리고

즉 r w x 별로 비트를 가지고 있고, 그 비트를 `4755`와 같은 십진수로 표현할 수 있다.

그럼 다시 돌아와서 `4755` 권한을 살펴보면, 뒤의 `755` 는 위의 예시처럼 나타나고 있고, 맨 앞의 `4` 같은 특수 권한을 알아보자.

맨 앞의 3개의 비트는 일반적인 r, w, x 권한과는 조금 다르다.

각 비트별로 **set-uid**, set-gid, stciky-bit 로 사용된다. 우리가 알아보고 있는 set-uid 비트가 특수권한 비트의 가장 앞이므로 앞에서 실행했던

```bash
sudo chmod 4755 myfile
```

명령어를 통해 3개의 특수권한 비트 중 가장 앞의 set-uid 비트를 킨 것이다.

## 예시

`cat` 명령어를 복사한 `mycat` 파일로 set-uid가 잘 적용되는지 알아보자.

```bash
cp /bin/cat ./mycat
sudo chown root mycat
```

1. set-uid 적용 전

```bash
./mycat /etc/shadow
./mycat: /etc/shadow: Permission denied
```

2. set-uid 적용 후

```bash
sudo chmod 4755 mycat
./mycat /etc/shadow
root: ...
daemon: ...
```

기존에 권한이 없어서 볼 수 없었던 파일을 열어볼 수 있다.

이렇게 set-uid 는 앞서 설명한 패스워드 딜레마와 같은 문제를 해결하기 위해 제공되지만, 권한을 상승시킬 수 있다는 점에서 다른 공격들의 표적이 된다. 따라서 프로그램의 권한을 설정할 때 set-uid 설정은 보안을 신경써서 적용해야 한다.
