---
title: 리눅스 기본 문법
published: 2025-08-20
author: Lanzarote
description: '리눅스의 기본적인 터미널 명령어를 알아봅니다.'
image: 'https://upload.wikimedia.org/wikipedia/commons/3/35/Tux.svg'
tags: ["Linux", "Tools"]
category: 'Lanzarote'
draft: false
---

리눅스 명령어는 POSIX로 규정된 유닉스 공통 인터페이스를 기반으로 한다. 
따라서 POSIX 표준을 따르는 UNIX 기반 운영체제인 MacOS 또한 리눅스 명령어를 동일하게 사용할 수 있다. 
UNIX와 POSIX 등의 개념은 다른 entry에서 더 설명하도록 하겠다. 

## 디렉토리 관련 명령어

Windows의 File Explorer, MacOS의 Finder가 하는 역할이다. 

### Print Working Directory
`pwd`는 현재 절대경로를 출력한다. 

### List
```sh
ls [option] [file/directory]
```
현재 경로에 있는 파일과 디렉토리를 출력한다. 
내가 자주 쓰는 옵션은 다음과 같다. 
| 옵션 | 설명 |
|-|-|
| `-l` | 권한, 크기, 날짜를 포함한 **L**ong format이다. |
| `-a` | `.`으로 시작하는 숨겨진 파일과 디렉토리를 포함하여 출력한다. |
| `-h` | `-l`과 같이 쓰여 파일의 크기를 인간이 읽을 수 있는 형식으로 출력한다. |

### Change Directory
```sh
cd [directory]
```
만약 Documents 폴더에 가고 싶으면, `cd Documents`로 입력한다. 
**[directory]** 자리를 비우면, home directory가 기본값으로 들어간다. 

이름 대신 -(하이픈)을 입력하면 이전 디렉토리로 이동한다. 다음 예시를 통해 알아보자.
```sh
lanzarote@lanzarotelinux /etc # cd /home/lanzarote
lanzarote@lanzarotelinux /home/lanzarote # cd -
/etc
lanzarote@lanzarotelinux /etc # cd -
/home/lanzarote
lanzarote@lanzarotelinux /home/lanzarote #
```
디렉토리로 이동하기 전에 이동할 디렉토리명을 출력하는 것을 알 수 있다.

### Make file
```sh
touch [option] filename
```
새로운 파일을 생성하거나 이미 있는 파일의 [타임스탬프](/posts/linux_101/timestamp/)를 변경한다. 
TODOTODO

### Make Directory
```sh
mkdir [options...] directory_name
```
TODOTODO

### Remove
```sh
rm [OPTION]... FILE...
```




> 출처
> https://www.geeksforgeeks.org/linux-unix/

