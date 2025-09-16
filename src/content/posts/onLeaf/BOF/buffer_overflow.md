---
title: 'BOF가 뭘까요'
published: 2025-09-08
author: 'onLeaf'
description: 'BOF'
image: ''
tags: ['bof']
category: 'PWN'
draft: false
---
## BOF (Buffer OverFlow)란?

프로그래밍에서 발생하는 대표적 보안 취약점 중 하나이다.

```c
#include <stdio.h>
#include <stdlib.h>
void win(){
	system("/bin/sh");
}
int main(){
	char buf[10];
	printf("buf : ");
	gets(buf);
	return 0;
}

```
스택 프레임 구조:\
- 지역 배열/변수는 `buf`라는 공간에 저장된다.\
- Canary는 다음 글에서 다룬다 (이 글에서는 생략).

정수형 변수 `a`, 배열 `b[10]`, 실수형 변수 `c` 선언 시,\
스택에 푸시 방식(LIFO)으로 `a` → `b` → `c` 순서로 저장된다.

#### 요약

-   `buf`는 고정된 크기임에도 입력이 크면 넘친다.\
-   예: `"KoreaDigitalMediaHighSchool"` 입력 시 10자를 초과한 부분이 `c`
    변수로 흘러 들어감.
-   이를 통해 특정 변수나 리턴 주소를 조작할 수 있다.
------------------------------------------------------------------------

### 실제 코드 사례

`gets` 사용 위험:\
- `scanf`처럼 길이 제한이 없고, 오히려 더 위험하다.
- `win()` 함수는 관리자 권한의 셸을 실행하는 함수다.\
- 입력을 조작해 `win()` 실행이 가능하다.

스택 구성: `buf` → `SFP` → `RET` 순서.\
- `RET`를 `win()` 주소로 덮으면 셸 접근 가능.
- 필요한 입력 크기 = `buf` 크기 + `SFP` 크기 + `win()` 주소.

------------------------------------------------------------------------

## 예제: 게임 채팅 기능 모방 코드
```c
#include <stdio.h>
#include <stdlib.h>
void administrator() {
    int command = 0;
    printf("환영합니다 관리자님\n");
    printf("무엇을 하시겠습니까?\n");
    printf("1. 유저 밴\n");
    printf("2. 전체 공지\n");
    printf("3. 서버 종료\n");
    printf("4. 모든 유저 죽이기\n");
    printf("-> ");
    scanf("%d", &command);
}
int main() {
    char chatting[16];
    int admin = 0;       
    printf("message : ");
    gets(chatting);
    if (admin == 1) {
        administrator();
    }
    else{
        printf("%s\n", chatting);
    }
    return 0;
}   
    
```
-   `gets` 입력으로 BOF 취약점 발생.

-   `admin()` 함수는 `admin` 변수가 1인 경우만 실행된다. 기본값은 0.\
-   목표: `admin` 변수를 1로 변경.

스택 구성:

    [ chatting (16 bytes) ]  
    [ padding (12 bytes) ] ← 변수 정렬(alignment)  
    [ admin (4 bytes) ]
    ```

    이를 이용해 입력을 다음과 같이 구성:

"A"*16 + "B"*12 + p32(1) \`\`\`

-   `"A"*16"`는 `chatting` 덮기\
-   `"B"*12"`는 `padding` 덮기\
-   `p32(1)`은 `admin` 변수 위치에 `1` 쓰기

정상 실행 시: 입력 메시지 출력 후 종료.\
익스플로잇 성공 시: `administrator()` 함수 실행.

------------------------------------------------------------------------

### 마치며

Pwnable의 기초이며, 매우 강력한 BOF 취약점을 다뤘다.\

