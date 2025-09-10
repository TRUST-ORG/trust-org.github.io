---
title: 리눅스 기본 명령어
published: 2025-08-26
author: Lanzarote
description: '리눅스의 기본적인 터미널 명령어를 알아봅니다.'
image: 'https://prd-cyberhub.oss-me-central-1.aliyuncs.com/uploads/t1_g-RJG0CyqV5RtldU0U_ANPu8B5Q'
tags: ["Linux", "Tools"]
category: 'Linux'
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
| 옵션 | 축약 | 설명 |
|-|-|-|
| `-l` | `long format` | 권한, 크기, 날짜를 포함하여 출력한다. |
| `-h` | `human readable` | `-l`과 같이 쓰여 파일의 크기를 인간이 읽을 수 있는 형식으로 출력한다. |
| `-a` | `all` | `.`으로 시작하는 숨겨진 파일과 디렉토리를 포함하여 출력한다. |
| `-t` | `time` | 마지막 수정 시간에 따라 정렬한다. |
| `-r` | `reverse order` | 반대 순서로 정렬하여 출력한다. | 
| `-R` | `recursive` | 하위 디렉토리의 내용까지 출력한다. |
| `-d` | `directory` | 하위 디렉토리의 내용을 출력하지 않고, 디렉토리 자체만 출력한다. |
| `-i` | `inode` | 각 파일과 디렉토리의 inode 번호를 출력한다. |

### Change Directory
```sh
cd [directory]
```
만약 Documents 폴더에 가고 싶으면, `cd Documents`로 입력한다. 
**[directory]** 자리를 비우면, home directory가 기본값으로 들어간다. 

이름 대신 `-`(하이픈)을 입력하면 이전 디렉토리로 이동한다. 다음 예시를 통해 알아보자.
```sh
lanzarote@lanzarotelinux /etc $ cd /home/lanzarote
lanzarote@lanzarotelinux lanzarote $ pwd
/home/lanzarote
lanzarote@lanzarotelinux lanzarote $ cd -
/etc
lanzarote@lanzarotelinux /etc $ cd -
/home/lanzarote
lanzarote@lanzarotelinux lanzarote $
```
디렉토리로 이동하기 전에 이동할 디렉토리명을 출력하는 것을 알 수 있다.

### Make File
```sh
touch [option] filename
```
새로운 파일을 생성하거나 이미 있는 파일의 [타임스탬프](/posts/linux_101/timestamp/)를 변경한다. ~~하지만 타임스탬프는 바꾸는 일이 거의 없다.~~

touch 명령어를 사용하는 이유는 한 파일의 권한을 미리 설정해 둠으로써 공격자가 미리 획득한 권한을 사용하는 것을 방지하기 위함이다.
또한 파일을 만들 때 파일의 권한도 확실히 해 두는 편이 보안적인 측면에서 더 낫다고 볼 수 있다.

#### 또 다른 명령어
```sh
>> filename
```
`>`가 아니라 `>>`을 쓰면 이미 있는 파일을 실수로 입력하였을 때 내용이 덮어씌워지는 참사가 발생하지 않는다.

### Make Directory
```sh
mkdir [option] directory_name
```
| 옵션 | 축약 | 설명 |
|-|-|-|
| `-p` | `parents` | 여러 개의 하위 디렉토리를 한 번에 만든다. |
```sh
lanzarote@lanzarotelinux Project $ mkdir src/helpers/mysql/  
mkdir: src/helpers: No such file or directory
lanzarote@lanzarotelinux Project $ mkdir -p src/helpers/mysql/
lanzarote@lanzarotelinux Project $ cd src/helpers/mysql
lanzarote@lanzarotelinux mysql $ pwd
/home/lanzarote/Project/src/helpers/mysql
lanzarote@lanzarotelinux mysql $
```

### Remove
```sh
rm [option] filename
```
| 옵션 | 축약 | 설명 |
|-|-|-|
| `-r` | `Recursive` | 하위 디렉토리까지 전부 지운다. |
| `-f` | `Force` | 쓰기 보호가 되어있는 파일을 유저에게 확인시키지 않고 바로 지운다. |
```sh
lanzarote@lanzarotelinux Project $ git init
Initialized empty Git repository in /home/lanzarote/Project/.git/
lanzarote@lanzarotelinux Project $ ls -al
total 0
drwxr-xr-x   3 lanzarote lanzarote   96 Aug 21 08:24 .
drwxr-xr-x  12 lanzarote lanzarote  384 Aug 21 08:24 ..
drwxr-xr-x   9 lanzarote lanzarote  288 Aug 21 08:24 .git
lanzarote@lanzarotelinux Project $ rm .git
rm: .git: is a directory
lanzarote@lanzarotelinux Project $ rm -r .git
override r--r--r-- lanzarote/lanzarote for .git/objects/32/73f2766cc63d64ce5fc148db6d34ce5d2a1561? ^C
lanzarote@lanzarotelinux Project $ rm -rf .git
lanzarote@lanzarotelinux Project $ ls -al
total 0
drwxr-xr-x   3 lanzarote lanzarote   64 Aug 21 08:25 .
drwxr-xr-x  12 lanzarote lanzarote  384 Aug 21 08:24 ..
lanzarote@lanzarotelinux Project $ 
```

### Move
```sh
mv [options] [source file/directory_name(s)] [destination file/directory_name]
```
| 옵션 | 축약 | 설명 |
|-|-|-|
| `-i` | `interactive` | 파일을 덮어쓰기 전에 사용자의 확인을 거친다. |
| `-f` | `force` | 쓰기 보호가 되어있는 파일도 overwrite한다. |
| `-v` | `verbose` | Move 동작이 실행되고 있는 진행률을 알 수 있다.

mv는 용도가 많다.
파일의 이름을 바꿀 수도 있고, 파일 또는 디렉토리를 옮길 수도 있으며, 원하는 파일을 덮어쓸 수도 있다. 

### Copy
```sh
cp [options] [source file/directory_name(s)] [destination file/directory_name]
```
cp 또한 mv와 같은 옵션을 사용할 수 있다. 

> 출처
>
> https://www.geeksforgeeks.org/linux-unix/basic-shell-commands-in-linux/
