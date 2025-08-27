---
title: 웹 해킹 블로그
published: 2023-09-09
author: hosung
description: 웹해커가 되고 싶은 김호성입니다.
tags: [Hacking Blog , Web, TRUST]
category: Tekanuf
draft: false
---
# 이번 주 웹해킹 공부: XSS와 CSRF
이번 주에는 웹 해킹의 대표적인 공격 기법 중 XSS(Cross-Site Scripting)와 CSRF(Cross-Site Request Forgery)를 배웠습니다.

## 1. XSS(Cross-Site Scripting)
XSS는 공격자가 웹 페이지에 악성 스크립트를 삽입해 사용자의 브라우저에서 실행되도록 만드는 공격입니다. 이를 통해 쿠키 탈취, 세션 하이재킹, 피싱 페이지 생성 등 다양한 피해가 발생할 수 있습니다.

### 종류
Stored XSS: 공격 코드가 서버에 저장되어 모든 방문자에게 노출
Reflected XSS: 공격 코드가 URL이나 요청에 포함되어 즉시 반영

# 2. CSRF(Cross-Site Request Forgery)
CSRF는 사용자가 로그인한 상태를 이용해 의도치 않은 요청을 서버에 보내게 하는 공격입니다. 공격자는 사용자의 권한으로 행동을 수행하게 만들 수 있어 위험합니다.

## 원리
사용자가 특정 사이트에 로그인된 상태에서, 공격자가 만든 악성 링크나 스크립트를 클릭하게 함
서버는 사용자가 보낸 정상 요청으로 판단하고 처리

한줄 요약: 이번주 웹해킹의 주요 공격기법들인 css와 csrf의 개념을 익히고 관련 문제를 4문제 풀어봄.
