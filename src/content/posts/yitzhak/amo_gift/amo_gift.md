---
title: Amo's gift를 해결하기 위해 crt에 대해 알아보자
published: 2025-09-10
author: yitzhak
description: 'CRT에 대해 간략히 알아봅니다.'
image: ''
tags: ["crypto"]
category: 'YITZHAK'
draft: false
---


#Dreamhack Amo's gift
---

아모가 우리를 위해 선물을 준비했다고 한다. 그런데 오다가 다 섞여 버렸다니 참으로 슬픈일이 아닐 수 없다. 

#prob.py
---
```from Crypto.Util.number import *

FLAG = b"DH{FAKE_FLAG}"
FLAG = bytes_to_long(FLAG)

while True:
    p = getPrime(1024)
    q = getPrime(1024)
    N = p * q
    e = 0x10001
    if GCD(e, (p - 1) * (q - 1)) == 1:
        break

# Here is amo's gift for you!
gifts = []
for i in range(800):
    if isPrime(i):
        gift = [p % i, q % i]
        gift = sorted(gift) # What's wrong with you, AMO?
        gifts.append(gift)

FLAG_enc = pow(FLAG, e, N)

print(f"{N = }")
print(f"{e = }")
print(f"{FLAG_enc = }")
print(f"{gifts = }") 
``` 

prob.py의 전문은 위와 같다.  

p와 q 설정, N 생성, 암호화 복호화 과정은 기존 RSA와 동일하다. 
그러나 이 코드에는 기존 RSA에서 추가된 부분이 있다. 

```gifts = []
for i in range(800):
    if isPrime(i):
        gift = [p % i, q % i]
        gift = sorted(gift) # What's wrong with you, AMO?
        gifts.append(gift)
```
위 코드는 0부터 799 사이의 소수 $i$를 사용해 $p \mod i$, $q \mod i$ 값을 [작은 값, 큰 값]으로 정렬해 제공해 주고 있다.  
이 때, $p \mod i$와 $q \mod i$ 중 어떤 것이 $p$와 $q$인지 알 수는 없지만 합 $(p+q) \mod i = (p \mod i + q \mod i) \mod i$는 항상 일정하다.  

따라서 이를 이용해 $p$와 $q$를 구할 수 있다.  

#crt
---
crt란 chinese remainder theorem의 약자로 '중국인의 나머지 정리'라고도 불린다. crt는 연립합동식의 유일한 해를 찾는 정리이다. 

$x\equiv a_1​ \pmod {n_{​1}} ,x≡a_2 \pmod {n{2}}​,…,x≡a_k​ \pmod {n{k}​}$이 있을 때 $n1​,n2​,…,nk$ 가 서로소라면 이 모든 조건을 동시에 만족하는 해는 $N \equiv n_1​×n_2​×⋯×n_k​$의 범위 내에서 유일하게 존재한다. 

따라서 $(p+q) \mod i = (p \mod i + q \mod i) \mod i$ 조건이 주어지므로 CRT를 통해 모든 $i$에 대한 나머지 정보를 합치면 $p+q$를 구할 수 있다. 

그 뒤에는 $φ(N)=(p−1)(q−1)=N−(p+q)+1$를 통해 $φ(N)$를 구하고, $d=e^{-1} \modφ(N)$을 통해 복호화 하면 된다. 



#삶의 지혜
---


무언가를 공짜로 주는 사람은 좋은 사람이다.  
이런 사람은 인생에서 소중한 사람이니 절대 놓치지 않아야 한다. 