---
layout: post
title:  "[Spring] 2. 단축키"
subtitle:   "단축키"
categories: Spring
tags: Spring
comments: true
date: 2021-12-29 00:14:20
---

'IntelliJ' 에서 사용하는 단축키들을 알아보겠습니다. (Window 기준)

<br><br>

# 1. [Shift + F6] : 한번에 동일한 변수이름들 바꾸기 

***

```
Member member1 = new Member();
member1.setName("spring1");
repository.save(member1);

Member member2 = new Member();
member2.setName("spring1");
repository.save(member2);
```

위 코드에서 위의 3줄을 복사하여 아래 붙여넣기 하였습니다. 그리고 `member1`을 전부 `member2`로 바꿔야 합니다. <br>
하나씩 변경하면 귀찮기 때문에 `Shift` + `F6`을 누르면 한꺼번에 바꿀 수 있습니다.


<br><br>

# 2. [Ctrl + Alt + v] : Optional<> 추가

```
memberRepository.findByName(member.getName());
```

```
Optional<Member> byName = memberRepository.findByName(member.getName());
```
`Ctrl + Alt + v` 를 누르면 위의 코드에서 아래와 같이 자동으로 입력이 됩니다.<br>
`byName`만 자신이 원하는 이름으로 변경하시면 됩니다.

<br><br>

# 3. [Ctrl + Alt + M] : Refactor Extract Method

```
memberRepository.findByName(member.getName())
    .ifPresent(m -> {
        throw new IllegalStateException("이미 존재하는 회원입니다");
        });
```
이러한 기능을 하나의 함수로 빼고 싶다면 `Ctrl + Alt + M`을 누르면 함수로 만들 수 있습니다. <br>

```
validateDuplicateMember(member);

private void validateDuplicateMember(Member member) {
    memberRepository.findByName(member.getName())
        .ifPresent(m -> {
            throw new IllegalStateException("이미 존재하는 회원입니다");
        });
}
```

<br><br>

# 4. [Ctrl + Shift + T] : 테스트클래스 만들기

```
package hello.hellospring.service;

import org.junit.jupiter.api.Test;

import static org.junit.jupiter.api.Assertions.*;

class MemberServiceTest {

    @Test
    void join() {
    }

    @Test
    void findMembers() {
    }

    @Test
    void findOne() {
    }
}
```

자동으로 테스트 클래스를 만들어 줍니다

<br><br>

# 5. [Shift + F10] 방금 전에 실행한 것을 실행합니다.

<br><br>

# 6. [Alt + Insert] Generate 

Constructor, Getter 등을 생성해줍니다.

<br><br>

# 7. [Alt + Enter] Show Context Action

관련된 기능들을 보여줍니다. <br>
-> 람다함수로 변환 등

<br><br>

# 8. [F2] 오류난 곳으로 이동

# 9. 'iter' + [Tab]

```
String[] Name = {"n", "a", "m", "e"};
iter
```

```
String[] Name = {"n", "a", "m", "e"};
for (String s : Name) {
            
}
```
무언가 배열이 있는 곳에서 입력하면, 반복문을 자동으로 생성해줍니다
<br><br>

# 10. 'sout' + [Tab]

```
void method() {
    String name = "name";
    sout
    soutm
    soutv
}
```

```
void method() {
    String name = "name";
    System.out.println();
    System.out.println("ApplicationContextInfoTest.method");
    System.out.println("name = " + name);
}
```
sout
> System.out.println(); <br>

soutm
> sout 에 메소드 이름을 입력합니다 <br>

soutv
> sout 에 변수 이름을 입력합니다 <br>

<br><br>

# 11. [Ctrl + D]

선택한 내용을 복제합니다

<br><br>

# 12. [Ctrl + E]
recent File 로 이동할 수 있습니다.<br>
(이전 코드로 바로 이동 가능)<br><br>

# 13. [Ctrl + Alt + B]
해당 인터페이스를 선택하고 커맨드를 누르면 구현체로 이동이 가능합니다. <br><br>



