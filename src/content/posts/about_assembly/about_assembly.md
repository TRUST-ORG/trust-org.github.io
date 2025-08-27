---
title: 어셈블리어
published: 2025-08-26
author: 연골어류
description: '간단한 어셈블리어에 대해 알아보자'
image: 'https://lh5.googleusercontent.com/proxy/GoHmckCdrIJlFBlK1_fAv7Dhwx_15WaB9BaH78L8XaZPIN-PN35E9LxGAizpSuUmaMY2hLoDHkaltlvVtjDv2RLGqguapcR4EG9ErSZq'
tags: ["Blogging", "Customization"]
category: 'Moru_Anvil'
draft: false
---


# 어셈블리어란

CPU가 이해할 수 있는 가장 간단한 기계어

속도가 빠르고 고급 언어에서의 작업을 직접 표현

*CPU 레지스터와 메모리에 직접 명령을 내려서 연산과 제어를 수행하는 언어*라네요..

* * *

## 어셈블리어 기초 문법 구조와 명령어

```

ex) mov rax, rbx    ; rbx 값을 rax에 복사하기

```




### 1. 기본 명령어
| 명령어 | 의미 |
|--------|------|
| mov    | 값 복사 |
| add    | 더하기 |
| sub    | 빼기 |
| xor    | XOR 연산 / 0으로 초기화 |
| push   | 스택에 값 저장 |
| pop    | 스택에서 값 꺼내기 |
| call   | 함수 호출 |
| retn   | 함수 종료 |
| test   | 값 비교 / 플래그 설정 |
| jz     | 0이면 점프 |
| jnz    | 0이 아니면 점프 |
| rep stosb | 반복 저장 (버퍼 초기화) |

---

## 공부하다가 궁금해서 찾아본것들

### 어셈블리어는 cpu의 종류와 운영체제에 따라 조금씩 다르다.

    CPU 아키텍쳐와 종류에 따라 규약과 시스템 호출의 차이로 문법과 레지스터명이 다르다.


#### EX)

    x86 어셈블리 (Intel)
```
mov eax, 5
add eax, 3

```
    ARM CPU 어셈블리

```

mov r0, #5
add r0, r0, #3

```

### 레지스터별 일반적 사용처

| 레지스터 | 의미 |
|----------|------|
| eax      | 연산 결과 / 반환값 |
| ebx      | 일반 목적 |
| ecx      | 반복 카운터 / 인자 |
| edx      | 인자 / 연산용 |
| rdi      | 버퍼 주소 / 인자 |
| rsi      | 버퍼/문자열 주소 / 인자 |
| rbp      | 스택 기준점 |
| rsp      | 스택 포인터 |
| r8~r15   | 일반 목적 |

이것도 역시 호출규약 때문
    


