---
title: SQL SELECT문 기본 문법
published: 2025-08-26
author: junham
description: 'database'
tags: ["Blogging", "Customization"]
category: 'junham'
draft: false
---

<h2>데이터 분석의 기초, SQL 기본문법에 대하여 알아보자</h2>

```SQL title="SELECT문 기본 문법"
SELECT     [DISTINCT] 열이름 [of 별칭] 
FROM       테이블 이름
[WHERE          조건식]
[ORDER BY       열이름 [ASC or DESC]];
```

<h5>

- SELECT, FROM, 열이름, 예약어는 필수 입력항목이다
- SELECT, FROM은 시스템에서 명령문을 실행하기 위해 미리 정해놓은 <b>예약어</b>이다.
- 대괄호 안에 들어간 항목은 선택사항으로 생략할 수 있다
- 문장을 모두 작성했다면 문장이 끝났다는 의미로 _세미콜론(;)_을 입력한다
단, SQL문장이 하나라면 세미콜론을 입력하지 않아도 SQL문이 실행된다

</h5>
<h2>이제 SQL문 작성 규칙에 대하여 알아보자</h2>
<h5>

1. SQL문은 대문자와 소문자를 구별하지 않는다<br>
예를 들어 SELECT와 select를 동일하게 인식한다<br>
2. SQL문은 한 줄 또는 여러 줄로 작성할 수 있다<br>
- 가독성과 편집의 용이성을 위해 내용이 달라지면 줄을 나눈다<br>
- 명령어는 여러 줄로 나눌 수 없다. 예를 들어 SEL LET라고 쓸 수 없다<br>
3. 코드 수준에 따른 들여쓰기는 SQL 문장을 좀 더 읽기 쉽게 한다<br>
4. 명령어를 대문자로 작성하고 나머지를 소문자로 작성하면 가독성이 좋아진다
</h5>

```SQL title="SQL문 작성규칙"
SELECT *
FROM employees A,
    (
    select *
    FROM departments
    WHERE department_id = 20
    ) B
WHERE A.department_id = B.department_id;
```
<h5>

>명령어는 대문자로, 줄바꿈 적용, 명령어 외에는 소문자로 입력, 들여쓰기 적용<br>
위와 같이 SQL문 작성 규칙이 모두 적용되어 있는 코드다<br>
이러한 형태로 SQL문을 작성한다고 생각하면 된다
</h5>