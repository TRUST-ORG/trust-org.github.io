---
title: Vim 사용법
published: 2025-09-16
author: Lanzarote
description: '리눅스에서 가장 많이 사용하는 텍스트 에디터인 Vim에 대해서 알아봅시다'
image: 'https://upload.wikimedia.org/wikipedia/commons/9/9f/Vimlogo.svg'
tags: ["Linux", "Tools", "Vim"]
category: 'Linux'
draft: false
---

# What is Vim?
Vim은 Unix의 역사적인 에디터인 Vi를 iMprove하여 커스터마이징이 아주 쉬운 에디터입니다. 
리눅스와 시스템 관리를 할 때 단연 가장 많이 쓰는 에디터입니다. 

마우스를 사용하지 않는 유닉스 환경 상 마우스에 손을 갖다 대지 않아도 되는 구조로 설계되어서 숙달되면 사용하기 아주 편하고 빠른 에디터입니다. 

`.vimrc` 파일을 사용하여 커스터마이징을 하기 아주 쉬우며 외부 플러그인을 include하기 쉬운 구조로 되어 있어서 커스터마이징의 재미를 느낄 수 있습니다. 

Register, Window, Mark/Jump, Regex Search, Macro 등 좋은 기능이 모여있어서 배우는 것이 재미있고 알면 알수록 기능을 효과적으로 쓸 수 있게 됩니다. 

# Modal Editing
Vim은 Mode가 있습니다. Normal mode, Insert mode, Visual mode, Command-line mode로 나뉘고, 각각의 mode가 하는 역할이 있습니다. 

## Normal Mode
Normal Mode에서는 화면 가장 아래에 `--INSERT--`라는 글자가 없습니다. 그냥 빈 줄로 있거나 가끔씩은 `--NORMAL--`이라고 쓰여 있기도 합니다. 

Normal Mode에서는 텍스트를 입력하지 않고 Vim을 조종합니다. 

- `h`, `l`, `j`, `k`는 키보드의 방향키와 같은 역할을 합니다. 손이 키보드 귀퉁이에 있는 방향키까지 가지 않아도 되어서 편합니다. 각각 왼쪽, 아래, 위, 오른쪽입니다. 
- `0`을 누르면 커서가 줄의 가장 앞으로 가고, `$`를 누르면 커서가 줄의 가장 뒤로 가게 됩니다. 
- `w`, `b`는 word 단위로 커서가 앞과 뒤로 가게 됩니다. 
- `gg`와 `G`는 각각 문서 가장 위쪽, 문서 가장 아래쪽으로 갈 수 있습니다. `(숫자)gg` 또는 `(숫자)G`를 입력하면 숫자번째 줄로 가게 됩니다. 
- `x`는 커서에 위치한 문자 1개를 지웁니다. 
- `r<문자>`는 커서에 위치한 문자를 replace합니다. 
- `dd`는 커서가 위치한 줄 전체를 지우고 커서를 그 아래 줄에 배치합니다.
- `dw`는 커서가 위치한 곳부터 word가 끝나는 지점까지를 지웁니다.
- `cc`는 커서가 위치한 줄 전체를 지우고 Insert mode로 전환합니다.
- `cw`는 커서가 위치한 곳부터 word가 끝나는 지점까지를 지우고 Insert mode로 전환합니다.
- `yy`는 커서가 위치한 줄 전체를 yank(복사)합니다.
- `yw`는 커서가 위치한 곳부터 word가 끝나는 지점까지를 yank합니다. 
- `p`는 yank한 내용을 커서 다음에 붙여넣습니다. 만약 `yy`를 사용하여 줄을 yank했다면 커서가 위치한 다음 줄에 paste하게 됩니다. 
- `u`는 되돌리기(undo)를 수행합니다. 
- `<C-r>`은 다시하기(redo)를 수행합니다. 
- `<C-e>`와 `<C-y>`는 화면을 위아래로 움직입니다.
- `<C-d>`와 `<C-u>`는 화면을 크게 위아래로 움직입니다.

> 출처
>
> My Brain
