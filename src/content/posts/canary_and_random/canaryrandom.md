---
title: 'canary 재배치'
published: 2025-08-24
author: 'onLeaf'
description: '카나리의 함수 재배치!?'
image: ''
tags: ['canary']
category: 'PWN'
draft: false
---

# 스택 카나리와 변수 배치 실험 기록

## 문제 배경

최근 여러 행사에서 **랜덤값을 덮어 비밀번호를 뚫는 문제**와 유사한,
**랜덤값 릭(leak)** 문제를 접했다.저 문제가 굉장히 흥미로워 핵심만 살린 간단한
코드를 직접 작성해 보았다.

## 실험 과정

1.  **코드 작성**
    -   `name`, `apt`, `num` 변수를 선언.
    -   랜덤값(`apt`)과 입력값(`num`)이 같으면 `win()` 호출 구조.
    -   보안 기법을 끄면 BOF가 가능함.
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
void win(){
    printf("H0W yoU! D1D tH1s!!!\n");
    system("/bin/sh");
}

int main(){
    srand(time(NULL));
    char name[16];
    int apt = 0;
    int num = 0;

    apt = rand();
    
    puts("what is your name?");
    printf("> ");
    gets(name);
    
    puts("");
    
    puts("what is your favorite number?");
    printf("> ");
    scanf("%d",&num);

    if (apt == num){
        win();
    }
    else{
        printf("Hello! %s, your favorite number is %d!!",name,num);
    }
    
    return 0;
}
```
2.  **보안 기법 활성화 후 컴파일**
    -   gcc에서 **모든 보안 기법을 활성화**하고 컴파일을 진행.
    -   코드에서는 `name`을 먼저 선언했으나,
    -   컴파일된 실행 파일에서는 `apt`가 `name` 위에 배치됨.
    -   결과적으로 BOF가 불가능해짐.
3.  **보안 기법 비활성화 후 재컴파일**
    -   모든 보안 기법을 끄고 다시 컴파일.
    -   선언 순서가 원래 의도대로 유지됨.
    -   이를 통해 **카나리가 변수 배치 순서를 바꾼다는 사실**을 확인.

## 학습한 내용

-   기존 지식:
    -   카나리는 **스택 덮어쓰기를 방지하기 위한 랜덤 값**으로 이해하고
        있었음.
-   새롭게 알게 된 점:
    -   카나리에는 **강도의 차이**가 있음.
    -   **약한 카나리**: 취약할 가능성이 있는 함수 뒤에 단순히 위치.\
    -   **Strong 카나리**: 위험한 버퍼를 **카나리 앞쪽으로 재배치**하여
        보호 강도를 높임.
-   결론:
    -   단순히 "랜덤 값"만이 아니라, **스택 배치 구조에도 영향을 미치는
        보안 기법**임을 알게됨.

