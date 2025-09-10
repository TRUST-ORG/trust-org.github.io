---
title: C언어 괴랄하게 작성하는 법
published: 2025-09-10
author: suhodnkla
description: 'C언어 괴랄하게'
tags: ["C"]
category: 'Code'
draft: false
---

# C언어 괴랄하게 작성하는 법

## 1 . 개요

단순히 재미를 위한 방법으로 따라하는 것을 권장하지 않는다.

만일 이렇게 코드를 작성하고 남에게 넘기면, 역시나 욕을 먹을 것이다.

단순히 따라하는 것이 아니라 아래의 문법을 바탕으로 여러 프로그래밍 지식을 얻었으면 한다.

~~필자는 이러한 방법이 몸에 익어서 매번 스파게티 코드와 씨름을 한다~~

여러분은 그러지 말자.

---

## 2. goto문과 스파게티 코드

### 2.1. goto문이란

goto문은 어셈블리의 jmp와 대응하는 명령문이다.

그러나 현재는 사장된 문법인데 goto문은 현대의 반복문에 비교할 수 없는 유지관리의 복잡성 때문이다.

그리하여 현대의 언어에서는 goto문이 없다. 이를테면 JAVA나 C#은 C언어의 영향을 받았지만 goto문은 없다. 

다음 두 코드를 보자.

```c
#include <stdio.h>

int main(){
    int n;
    scanf("%d",&n);
    for(int i = 0;i < n;i++){
        printf("%d ",i);
    }
    return 0;
}
```

```c
#include <stdio.h>

int main(){
    int n;
    scanf("%d",&n);
    int i = 0;
L:
    if(i<n)
        goto O;
    printf("%d ",i);
    goto L;
O:
    return 0;
}
```

두 코드 모두 0~n-1의 수를 출력하는 코드이다. 그리고 컴파일 후에는 똑같이 작동한다. 그러나 이 두 코드 중 위의 코드는 단순하나 아래의 코드는 보기에 상당히 불편하다. 

### 2.2. 스파게티화

goto문의 해로움은 단순히 이해의 어려움에 있진 않다. 우리는 goto를 활용하여 for, while로는 불가능한 로직을 세울 수 있다.

이를테면 다음과 같은 코드를 생각해 볼 수 있다.

```c
#include <stdio.h>

int main(){
    int n;
    scanf("%d",&n);
    for(int i = 0;i <= n;i++){
        for(int j = 0;j <= n;j++){
            if(i*j==n){
                printf("%d*%d=%d",i,j,n);
                goto O;
            }
        }
    }
O:
    return 0;
}

```

이처럼 변수없이는 불가능한 이중 반복문 탈출을 간단하게 적을 수 있다. 

이는 가장 희망적인 사용법이고 이제 이를 활용하여 로직을 꼬아 보자.

다음과 같은 코드를 보자

```c
#include <stdio.h>

int main(){
    int n,i=1;
    scanf("%d",&n);
L1:
    if(i%2==0)
        goto O1;
L2:
    i++;
    goto L1;
O1:
    if(i>n)
        goto O2;
    printf("%d ",i);
    goto L2;
O2:
    return 0;
}
```

위 코드는 1부터 n까지의 수 중 짝수를 출력하는 코드이다. 

그러나 코드의 흐름은 일반적인 for문, while 문으로는 구현할 수 없다. 

뿐만 아니라 이해하는데에도 엄청난 시간이 들게 되기 때문에 복잡하게 코드를 짜는데에 goto는 필수적이다. 

---

## 3. 포인터와 메모리

### 3.1. 포인터의 활용

포인터를 활용해 보았다고 하는 학생들은, 백이면 백 배열을 접근하는데 사용해보았을 것이다.

그러나 포인터로 이상한 것을 할 수 있다.

이를테면 다음과 같은 것을 할 수 있다.
```c
int main(){
    long long a;
    char*b = &a;
    
    strcpy(a , "hello");
	
    puts(a);
}
```

long long은 8바이트 이고 char은 1바이트이다.

즉 char포인터로 보기에 long long과 char[8]은 다른 것이 없다.

그리하여 변수 a속에 "hello"가 들어가도 문제가 없는 것이다.

### 3.2. union, 공용체

struct가 메모리 구조를 만들어 방을 배분했다면,
union은 디미고 기숙사같이 한곳에 몰아 방을 배정한다.

이를테면 다음과 같다.

```c
union DIMI{
	long long stu1;
	int stu2;
} A;

int main(){
	A.stu1 = 1;
	A.stu2 = 2;
	
	printf("%d %d", A.stu1, A.stu2);
	// result : 2 2 
}
```

위는 stu1과 stu2가 같은 메모리를 차지하기 때문에 결과가 "2 2"가 나온 것이다.

이를 활용하여 메모리를 절약 할 수 있다.

---

## 4. 숏코딩 (CodeGolf)

### 4.0. 기초

숏코딩을 들어본 사람도 있을 것이고 들어본적이 없는 사람도 있을 것이다.

먼저 모르는 사람을 위해 약간의 개요를 적어본다.

숏코딩이란? 코드를 최대한 짧게 적는 것이다. 

이를테면 a값에 4를 더하고 1을 더하는 코드를 생각해보자

```c
a = a + 4 + 1
```

이와 같이 작성하는 것이 일반적이지만

```c
a+=5
```

처럼 압축할 수 있다. 이와 같이 더 짧게 쓰는 것이다.

BOJ나 CodeUp과 같은 온라인 저지 사이트에서는 재미의 일환으로 숏코딩 순위를 보여준다. 

### 4.1. 대괄호 줄이기

대괄호는 코드블럭을 만드는 문법이다. 그리하여 C언어에서 필수적인 문자이지만, 숏코딩으로 본다면 무려 2 Byte나 차지하는 문법이다. 

그러니 숏코딩을 한다면 대괄호를 없애는 것을 생각해보아야 한다.

이를테면 다음 코드를 보자

```c
#include <stdio.h>

int main(){
    int n;
    scanf("%d",&n);
    while(n!=0){
        printf("%d ",n);
        n--;
    }
    return 0;
}
```

이 코드를 대괄호를 없이 짠다고 하면 for를 이용하는 방법을 떠올릴 수 있다.
    
```c
#include <stdio.h>
    
int main(){
    int n;
    scanf("%d",&n);
    for(;n!=0;n--)
        printf("%d ",n);
    return 0;
}
```
    

그러면 적어도 2Byte나 압축할 수 있다.

그러나 연산이 세 개 이상이 되면 이 방법은 영 쓰기 힘들다. 

그리하여 꼼수가 있는데, 쉼표를 활용하는 것이다.

이를테면 f1(), f2(), f3() 함수를 n번 실행한는 코드라면

```c
int main(){
    int n;
    scanf("%d",&n);
    for(int i = 0;i < n;i++)
        f1(),f2(),f3();
    return 0;
}
```

이와 같이 작성할 수 있다. 
원리는 쉼표는 **우선순위가 낮은 연산자**이므로 세 함수를 묶어서 하나의 묶음으로 컴파일되는 것이다. 
이를 이용하여 함수, 연산 등을 대괄호 없이 반복문, 조건문 안에 넣을 수 있다.

### 4.2. 삼항연산자의 활용

다음 코드를 보자.

```c
int main(){
    int n;
    scanf("%d",&n);
    if(n==1)      f1();
    else if(n==2) f2();
    else if(n==3) f3();
    else          f4();
    return 0;
}
```
위 코드는 매우 복잡하다.

만일 switch 문을 안다면 이로 바꾸어 볼 것이다.

```c
int main(){
    int n;
    scanf("%d",&n);
    switch(n){
    case 1:  f1(); break;
    case 2:  f2(); break;
    case 3:  f3(); break;
    default: f4();
    }
    return 0;
}
```
그러나 이도 복잡하다!

삼항연산자를 이용하면 간단하게 작성할 수 있다!

```c
int main(){
    int n;
    scanf("%d",&n);
    n==1 ? f1() :
    n==2 ? f2() :
    n==3 ? f3() : f4();
    return 0;
}
```

### 4.3. #define 의 활용

define 문을 사용해본 사람이라면 대개 상수를 정의하는데에 사용해보았을 것이다. 이를테면 pi나 e같은 상수를 #define으로 정의했을 것이다. 그러나 #define은 단순한 상수 외, 다른 쓰임도 있다. #define으로 코드의 일부를 적어 반복할 수 있고, 함수도 적을 수 있다. 

먼저 define과 함수를 보자. 

이를테면 다음과 같은것 이 가능하다.

```c
#deine max(a,b) (a>b?a:b)
```
이러한 경우 아래의 코드는 다음과 같이 치환된다.

```c

m = max(3,5)
-> m = (3>5?3:5)

```
즉 define문은 치환해주는 역할이다. 

다음과 같은 것도 가능하다.

```c
#define begin {
#define end }
#define times(A) for(int i = 0;i < A;i++)
#define ll long long
#define ret return 0;

int main()
begin
    ll a = 10;
    times(a)
    begin
        printf("%lld ",a);
    end
    ret
end
```

#### 4.3.1. define문에서 #문자
define 문에서 ```#```은 두가지로 쓰인다.

첫번째로 받은 구문을 문자열로 변환한다.

이를테면 다음과 같다.

```c
#define str(A) #A  
/*
 * str(10) -> "10"
 * str(a+b) "a+b"
 */
```

다음과 같이 응용할 수 있다.
```c
#define CalOut(A) printf(#A " = %d\n", A);
int main(){
    int a = 3,b = 2;
    CalOut(a+b);
    CalOut(a-b);
    CalOut(a*b);
    CalOut(a/b);
}

/* result
 * a+b = 5
 * a-b = 1
 * a*b = 6
 * a/b = 1
 */
```

다음으론 ```##```으로 붙여쓸 수 있도록 해 준다.

이를테면 다음과 같다.

```c
#define Int(a,b) int a##b;
int main(){
    Int(a,1)  // int a1;
    Int(a,2)  // int a2;
    Int(b,3)  // int b3;
}
```

이러한 문법을 어떻게 사용할지는 전적으로 여러분의 상상력에 달려있다.

---

## 5. 명제와 논리

### 5.1. 명제, 코드 늘여 쓰기

일반적으로 
"사과는 장미과 사과나무속 사과나무 식물의 열매로 중앙아시아에서 출발하여 전세계에 퍼지어 우리의 식문화에 깊숙히 들어왔디"
라고 하는 것은 너무나도 이해가 어렵다.

간단하고 명료하게  "우리는 사과를 즐겨먹는다." 라고 한다면 쉽게 이해할 수 있다.

코드도 같다. 코드는 간단하고 명료하게 작성하는 것이 좋다.

x=4+1 이라면 x = 5 라 적는것이 보기 좋다.

그러나 이 글에서는 괴랄하게 작성하는 것을 목표로 한다.

명제를 늘려 써 보자. 같은 기능도 번잡하게 작성해보자.

```c
TreeNode*SetTree(unsigned int idx){
    if(idx > size)
        return NULL;
    
    TreeNode*T=NewNode(tree[idx]);
	
    T->left = SetTree(idx*2);
    T->right = SetTree(idx*2+1);
    return T;
}

```
```
TreeNode* setTree(int idx){
    int leftIdx, rightIdx;
    
    TreeNode* T = malloc(sizeof(TreeNode));
    T->value = tree[idx];
    T->left = T->right = NULL;
    
    leftIdx = idx*2;
    rightIdx = leftIdx+1;
    
    if(leftIdx <= size) newNode->left = setTree(leftIdx)
    if(rightIdx<= size) newNode->right= setTree(rightIdx); 
    
    return NewNode;
}
```

위 두 코드는 자료구조 과제에서 위는 필자의 코드, 아래는 에제 코드이디.

어느쪽이 보기 좋은가?

모두 전자를 보기 좋아할 것이다. 

노드 생성을 다른 함수로 빼고 size 확인을 재귀 호출 후 함으로서
코드가 더 깔끔해졌다.

그러나 후자는 장황하다.

두 코드는 모두 동치지만, 가독성 차이를 불러왔다.

괴랄하게 작성하고 싶다면 후자처럼 쓸데없이 꼼꼼하면 된다.

### 5.2. ||, && 연산의 최적화

만일 포인터 변수에 NULL이 들어있을 때, 값을 가져온다면 문제가 될 수 있다.

그리하여 다음과 같이 처리를 하지 않으면 안된다.

```c
if(p!=NULL){
    if(*p == 0)
        ...
}
```

그러나 다행히도 && 연산자는 **앞이 거짓이면 뒤를 계산하지 않는다**

그렇기에 다음과 같이 작성할 수 있다.

```c
if(p!=NULL && *p == 0)
    ...
```

이와 같이 && 과 || 는 뒤의 항을 볼 필요가 없으면, 
계산하지 않는다.

아래 두 코드는 똑같이 실행된다.

```c
int main(){
    int n;
    scanf("%d",&n);
    for(int i = 1;i <= n;i++)
        if(i%2==0)
            printf("%d ",i);
    return 0;
}
```

```c
int main(){
    int n;
    scanf("%d",&n);
    for(int i = 1;i <= n;i++)
        i%2 || printf("%d ",i);
    return 0;
}
```
## 6. 기타 문법

### 6.1. main 재귀 함수

main 함수도 재귀함수로 이용할 수 있다.

```c
#include <stdio.h>
int p=7,n;
int main(){
    p!=7||(puts("10진수 : ")+scanf("%d",&*&n)+printf("2진수 : "));
    printf("%d",n>>p&1);p--;
    return p<0||main()&0;    
}
```

위 코드는 과거 필자가 작성했던 것이다. 

위 코드는 10진법 수를 입력받고 이진법으로 변환하는 코드다.

위 코드의 흐름을 생각해 보아라. 이와 같이 main 재귀를 사용할 수 있다.

### 6.2. main함수의 인자

원래 main 함수의 원형은 아래와 같다.
```c 
int main(int argc, char*argv[]){
    ...
}
```

main 함수의 인자에는 본래 실행할 때 입력된 문자열을 받아오는 역할이다.

그러나 우리는 앞서 main 함수를 재귀함수로 호출하였다.

위의 의미는 무시하고, 일반적으로 사용되도록 해보자.

그러면 온가지 알고리즘을 main함수만을 이용하여 구현할 수 있다.

### 6.3. XOR의 활용

xor은 자기자신이 자신의 역연산이란 재밌는 특징을 가지고 있다.

이를 이용하면 재밌는 것을 할 수 있다.

```
a ^= a; // xor a, a
```

위 코드는 a를 0으로 만드는 코드다.

리버싱에서도 많이 보이기에 기억해두면 좋을 것이다.

```
a ^= b ^= a ^= b;
```

위 코드는 swap 연산이다.

못 믿겠다면 한번 손으로 해 보아라.

신기하게도 될 것이다.

증명은 해오면 칭찬을 해 줄 것이다.

### 6.4. static 변수

static 변수는 스택, 힙 메모리를 사용하는 것이 아니라, 고정된 부분을 사용하는 것이다.

쉽게 말하면, local에서만 사용할 수 있는 전역변수이다.

다음 예제를 보자.

```
int f(int a){
    static int sum = 0;
    sum+=a;
    return sum;
}

int main(){
    for(int i = 1;i <= 10;i++)
        f(i);
	printf("%d",f(0)); //result : 55
}
```

위 코드는 1부터 10까지 더하여 출력하는 코드이다.

그러나 함수 f는 매번 새로 호출된다. 

만일 static 키워드가 없었다면 결과는 0 였을 것이다.

이와 같이 새로 호출되어도 전역변수와 같이 변치 않게 해주는 게 static 키워드이다.
```