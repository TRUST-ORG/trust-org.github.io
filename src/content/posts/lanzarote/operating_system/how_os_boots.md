---
title: 컴퓨터는 어떻게 부팅하는가?
published: 2025-09-10
author: Lanzarote
description: '컴퓨터가 부팅하는 과정에 대해 구체적으로 알아봅시다.'
image: 'https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2F3.bp.blogspot.com%2F-xigjplXLFH4%2FWckhYcHzGoI%2FAAAAAAAAI2M%2Fe2WOBOFNBSM02yA3D2SGSjwjU5MQ4dy1wCLcBGAs%2Fs1600%2FLinux-Booting-process.png&f=1&nofb=1&ipt=3c0313dd72dc2254aea4ab4df2ea6f1c25abbd80134f6f58eddfe61f9b7110b5'
tags: ["OS"]
category: 'Operating System'
draft: false
---

## Boot Sequence 이해하기
Boot Sequence는 BIOS 또는 UEFI에서 시작한다. 
BIOS와 UEFI는 메인보드에 저장되어 있는 firmware로, 컴퓨터 하드웨어와 OS가 소통하는 interface가 된다. 
요즘 시스템은 대부분 UEFI를 사용하고, BIOS는 일부 구형 기종에서만 사용된다. 
전원이 켜지면, 
- BIOS와 UEFI는 하드웨어를 초기화하고, 
- 자기 자신이 제대로 작동하는지 테스트한다 (Power On Self Test, POST)
- POST가 완료되면, BIOS나 UEFI는 HDD, SSD, Memory Stick 등을 확인하여 부팅을 할 수 있는 media를 찾게 된다. 
- 적절한 media를 찾게 되면 그 media의 부트로더 프로그램을 실행하게 된다.  

## First stage Bootloader
부트로더란, 컴퓨터의 OS를 부팅하는 데 필요한 프로그램이다. 
대부분의 시스템은 처음 부팅할 때 64비트로 부팅하지 않는다.
이것의 Instruction set을 64비트로 끌어올리고 보안 기법을 수행하는 등 OS를 부팅하는 데 필요한 일을 한다고 할 수 있다. 

컴퓨터가 꺼졌을 때, 모든 데이터는 보조기억장치에 저장된다. 
주기억장치에 저장된다면 전원이 꺼졌을 때 전부 날아가기 때문이다. 
그래서, 컴퓨터가 처음 부팅되었을 때 RAM에는 아무것도 없다.
컴퓨터는 켜졌을 때 boot ROM(Read Only Memory)에 저장되어 있는 프로그램을 실행하여 Boot Sequence를 수행할 수 있도록 한다. 

## Second stage Bootloader
이 부트로더는 이 자체로 OS는 아니지만, OS를 제대로 로드하기 위해 필요한 프로그램이다. 예를 들어 GRUB, rEFInd, BOOTMGR 등이 있다고 한다. 
유저 input을 받는 interface가 들어가 있을 수 있는데, interface로 부트 옵션을 설정하여 부팅할 수도 있다. 
이러한 부트로더를 boot manager이라고 한다. 


## Network booting
현대의 많은 컴퓨터들은 네트워크 부팅을 지원한다. 
많이 사용하지는 않지만, 모든 컴퓨터의 하드디스크를 일관적으로 관리할 수 있다는 점에서 기관에서 사용한다.
먼저 First stage Bootloader에서 부팅할 수 있는 디스크를 찾을 수 없다면 Second stage Bootloader에서 Network booting을 시도한다.
이 프로그램 또한 ROM에 저장되어있다. 


> 출처
> 
> https://networkencyclopedia.com/boot/
> https://en.wikipedia.org/wiki/Bootloader
