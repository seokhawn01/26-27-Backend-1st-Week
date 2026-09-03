# 데이터베이스 [1] - DB와 SQL 기본 문법

## 목차

- [[1] 데이터베이스와 DBMS](#1-데이터베이스와-dbms)
  - [데이터베이스의 정의](#데이터베이스는-데이터-그-자체입니다)
  - [데이터베이스를 관리하는 DBMS](#데이터베이스를-관리하는-dbms)
- [[2] DBMS의 종류](#2-dbms의-종류)
  - [표로 저장하는 RDBMS](#표로-저장하는-rdbms)
  - [MySQL과 PostgreSQL](#mysql과-postgresql)
  - [NoSQL](#nosql)
- [[3] 테이블의 구성](#3-테이블의-구성)
  - [행(Row) / 레코드(Record)](#행row--레코드record)
  - [열(Column) / 속성(Attribute)](#열column--속성attribute)
- [[4] SQL 명령어의 분류](#4-sql-명령어의-분류)
  - [DDL, DML, DCL](#ddl-dml-dcl)
- [[5] 데이터를 조작하는 DML](#5-데이터를-조작하는-dml)
  - [INSERT](#insert)
  - [UPDATE](#update)
  - [DELETE](#delete)
  - [한눈에 보기](#한눈에-보기)
- [[6] SQL 기본 문법](#6-sql-기본-문법)
  - [SELECT 와 FROM](#select-와-from)
  - [WHERE](#where)
- [[7] 묶어서 보고, 정렬해서 보기](#7-묶어서-보고-정렬해서-보기)
  - [GROUP BY](#group-by)
  - [HAVING](#having)
  - [ORDER BY](#order-by)
  - [작성 순서와 실행 순서](#작성-순서와-실행-순서)
- [[8] JOIN](#8-join)
  - [테이블을 나누는 이유](#테이블을-나누는-이유)
  - [INNER JOIN](#inner-join)
  - [나머지 조인은 과제입니다](#나머지-조인은-과제입니다)
- [[9] 전체 정리](#9-전체-정리)
  - [명령어 한눈에 보기](#명령어-한눈에-보기)

---



# [1] 데이터베이스와 DBMS

데이터베이스에 대한 정의부터 알아보겠습니다

## 데이터베이스는 데이터 그 자체입니다

먼저 데이터베이스(DB)는 정리된 상태로 보관된 데이터 그 자체를 말합니다

여기서 짚고갈 점은 데이터베이스가 프로그램이 아니라 데이터 그 자체라는 점입니다

## 데이터베이스를 관리하는 DBMS

그리고 이런 데이터베이스를 생성,관리,제어하는 소프트웨어가 DBMS(DataBase Management System) 입니다

이 DBMS를 통해서 사용자는 데이터를 검색,삽입,수정,삭제를 할 수 있다고 아시면 됩니다

우리가 흔히 "MySQL 깔았어" 라고 말할때의 그 MySQL이 바로 이 DBMS입니다

**정리하면 데이터는 데이터베이스에 들어있고, 그 데이터를 대신 관리해주는 프로그램이 DBMS입니다**

---



# [2] DBMS의 종류

이런 DBMS의 종류는 RDBMS, NoSQL이 있습니다

## 표로 저장하는 RDBMS

RDBMS는 데이터를 행과 열로 이루어진 테이블로 저장합니다

![member 테이블 구조](media/테이블-구조.png)

## MySQL과 PostgreSQL

이런 형태를 우리가 가장 흔히 보는 MySQL,PostgreSQL에서 볼 수 있습니다

요즘은 ai 서비스가 늘면서 구조가 고정되지 않은 JSON 데이터를 많이 다루는데, PostgreSQL은 JSON 데이터까지 강력하게 다룰 수 있어서 수 있다고 합니다

## NoSQL

NoSQL은 이름 그대로 테이블 형태를 고집하지 않는 DBMS입니다

MongoDB처럼 JSON 비슷한 문서를 통째로 저장하거나, Redis처럼 key-value로 저장하는것들이 여기에 속합니다

여기서 key-value가 눈에 익으실텐데, 1주차에서 봤던 `Map`과 똑같은 구조입니다

열을 미리 정해두지 않아도 되니까 자유롭지만, 대신 데이터 구조가 제각각이어도 아무도 막아주지 않습니다

**정리하면 구조가 정해져 있으면 RDBMS, 구조가 계속 바뀌면 NoSQL이 편하다고 보시면 됩니다**

스터디에서는 계속 RDBMS 기준으로 진행하겠습니다

---



# [3] 테이블의 구성

앞에서 본 테이블 그림을 조금만 더 뜯어보겠습니다

## 행(Row) / 레코드(Record)

테이블에서 가로 방향으로 저장된 데이터 단위입니다

데이터가 출력될 때, 행단위로 나옵니다

그림에서 파랗게 칠해진 `2, 이우빈, 16, 184` 이 한 줄이 행 하나라고 보시면 됩니다

## 열(Column) / 속성(Attribute)

세로 방향으로, 어떤 데이터를 담을지 미리 정해둔 자리입니다

그림에서 점선으로 표시한 `name`이 열 하나이고, 여기에는 이름만 들어가게 됩니다

열은 타입이 정해져 있어서 `age` 열에 `"스물넷"` 같은 문자를 넣으려고 하면 오류가 납니다

1주차에서 봤던 타입안정성이 여기서도 그대로 적용된다고 보시면 됩니다

---



# [4] SQL 명령어의 분류

이 테이블을 다루는 언어가 SQL이고, SQL은 하는 일에 따라 세가지로 나뉩니다

## DDL, DML, DCL

**DDL(Data Definition Language)**

테이블 자체를 만들고 바꾸는 명령어입니다 (`CREATE`, `ALTER`, `DROP`)

**DML(Data Manipulation Language)**

저장된 데이터에 대한 조작을 하는 명령어이고, 가장 많이 사용하게 될 명령어입니다 (`INSERT`, `UPDATE`, `DELETE`, `SELECT`)

**DCL(Data Control Language)**

누가 이 데이터를 건드릴 수 있는지 권한을 주고 뺏는 명령어입니다 (`GRANT`, `REVOKE`)

---



# [5] 데이터를 조작하는 DML

앞에서 본 `member` 테이블을 그대로 가지고 예시를 들어보겠습니다

## INSERT

테이블에 행을 삽입할 때, 사용하는 명령어입니다

```sql
INSERT INTO member (id, name, age, height)
VALUES (5, '김민수', 21, 175);
```

`INTO` 뒤에 어느 테이블인지, 괄호 안에 어느 열에 넣을지, `VALUES` 뒤에 실제 값을 적어주면 됩니다

여기서 문자열은 `'김민수'`처럼 작은따옴표로 감싸야 하고, 숫자는 그냥 적어주시면 됩니다

## UPDATE

테이블에 저장된 데이터를 수정할 때 사용하는 명령어입니다

방금 넣은 김민수의 키를 178로 고쳐보겠습니다

```sql
UPDATE member SET height = 178 WHERE id = 5;
```

`SET` 뒤에 무엇을 바꿀지, `WHERE` 뒤에 어느 행을 바꿀지 적어줍니다

만약 여기서 `WHERE`를 빼먹으면 모든 행의 키가 178로 바뀌어버립니다

## DELETE

테이블에 저장된 데이터를 행 단위로 삭제할 때 사용하는 명령어입니다

```sql
DELETE FROM member WHERE id = 5;
```

행 단위라서, 열 하나만 골라서 지우는건 불가능합니다

값 하나만 비우고 싶으시면 `DELETE`가 아니라 `UPDATE`로 그 자리에 `NULL`을 넣어주면 됩니다

**여기서도** `WHERE`**를 빼먹으면 테이블의 모든 행이 지워지기 때문에,** `UPDATE`**와** `DELETE`**는** `WHERE`**를 붙였는지 꼭 확인하고 실행하셔야 합니다**

## 한눈에 보기

지금까지 본 DML을 한번에 모아보겠습니다

```sql
-- 넣고
INSERT INTO member (id, name, age, height) VALUES (5, '김민수', 21, 175);

-- 고치고
UPDATE member SET height = 178 WHERE id = 5;

-- 지우고
DELETE FROM member WHERE id = 5;
```

셋 다 `member`라는 테이블 이름을 적어주는 자리가 있고, `UPDATE`와 `DELETE`는 어느 행인지 `WHERE`로 골라준다는 점이 똑같은걸 확인할 수 있습니다

---



# [6] SQL 기본 문법

이제 데이터를 꺼내보는 `SELECT`를 보겠습니다

## SELECT 와 FROM

`SELECT`는 데이터 조회를 하는 명령어이고, `FROM`은 어느 테이블에서 꺼낼지 적어주는 자리입니다

```sql
SELECT name, age FROM member;
```

`SELECT` 뒤에는 보고싶은 열을 적어주고, 전부 다 보고 싶으면 `*`를 적어주면 됩니다

```sql
SELECT * FROM member;
```


| id  | name | age | height |
| --- | ---- | --- | ------ |
| 1   | 김석환  | 24  | 188    |
| 2   | 이우빈  | 16  | 184    |
| 3   | 박연지  | 34  | 180    |
| 4   | 전천우  | 5   | 120    |


보다시피 테이블에 있는 4개의 행이 전부 나온걸 확인할 수 있습니다

## WHERE

조건에 맞는 행만 골라내는 자리입니다

```sql
SELECT name, height FROM member WHERE height >= 184;
```


| name | height |
| ---- | ------ |
| 김석환  | 188    |
| 이우빈  | 184    |


키가 184 이상인 행만 남은걸 볼 수 있습니다

조건에는 아래와 같은 것들을 쓸 수 있습니다


| 연산자                      | 설명                   |
| ------------------------ | -------------------- |
| `=`                      | 같은 값을 찾습니다           |
| `!=` 또는 `<>`             | 다른 값을 찾습니다           |
| `>`, `<`, `>=`, `<=`     | 크거나 작은 값을 찾습니다       |
| `BETWEEN a AND b`        | a 이상 b 이하인 값을 찾습니다   |
| `IN (a, b, c)`           | 나열한 값들 중 하나인 값을 찾습니다 |
| `LIKE '김%'`              | `김`으로 시작하는 값을 찾습니다   |
| `IS NULL`, `IS NOT NULL` | 값이 비어있는지 여부로 찾습니다    |
| `AND`, `OR`, `NOT`       | 조건을 여러개 묶어줍니다        |


여기서 `NULL`은 값이 아직 없다는 뜻인데, `= NULL`이 아니라 `IS NULL`로 비교해야 한다는 점만 알아두시면 좋습니다

---



# [7] 묶어서 보고, 정렬해서 보기



## GROUP BY

같은 값을 가진 행들을 하나로 묶어주는 자리입니다

그런데 지금 `member` 테이블은 나이도 키도 전부 달라서 묶을게 없으니, 회원이 쓴 글을 저장하는 `post` 테이블을 하나 가져오겠습니다


| member_id | title  |
| --------- | ------ |
| 2         | 자바 정리  |
| 2         | SQL 정리 |
| 3         | DB 정리  |


`member_id`는 이 글을 누가 썼는지를 나타내고, `2`번인 이우빈이 글을 두개 쓴걸 확인할 수 있습니다

이 테이블로 회원별 글 개수를 세보겠습니다

```sql
SELECT member_id, COUNT(*) FROM post GROUP BY member_id;
```


| member_id | `COUNT(*)` |
| --------- | ---------- |
| 2         | 2          |
| 3         | 1          |


3개였던 행이 회원별로 묶여서 2개가 된걸 확인할 수 있습니다

이렇게 묶은 그룹에 대해서 `COUNT`(개수), `SUM`(합계), `AVG`(평균), `MAX`(최댓값), `MIN`(최솟값) 같은 집계함수를 쓸 수 있습니다

## HAVING

묶고 난 결과에다가 조건을 거는 자리입니다. group by와 세트라고 생각하시면 편합니다

```sql
SELECT member_id, COUNT(*) FROM post GROUP BY member_id HAVING COUNT(*) >= 2;
```


| member_id | `COUNT(*)` |
| --------- | ---------- |
| 2         | 2          |


글을 2개 이상 쓴 회원만 남기라고 했더니 `2`번인 이우빈만 남은걸 확인할 수 있습니다

`WHERE`랑 뭐가 다른지 헷갈리실텐데, `WHERE`는 묶기 전의 행에 거는 조건이고 `HAVING`은 group by로 묶은 다음의 그룹에 거는 조건입니다

## ORDER BY

결과를 정렬하는 자리입니다

```sql
SELECT name, age FROM member ORDER BY age DESC;
```


| name | age |
| ---- | --- |
| 박연지  | 34  |
| 김석환  | 24  |
| 이우빈  | 16  |
| 전천우  | 5   |


넣은 순서와 상관없이 나이가 큰 순서대로 다시 줄세워진걸 확인할 수 있습니다

`ASC`는 오름차순, `DESC`는 내림차순이고 아무것도 안 적으면 오름차순이 기본값입니다

## 작성 순서와 실행 순서

지금까지 본 자리들을 순서대로 적으면 이렇게 됩니다

```sql
SELECT   member_id, COUNT(*)
FROM     post
WHERE    title LIKE '%정리%'
GROUP BY member_id
HAVING   COUNT(*) >= 2
ORDER BY COUNT(*) DESC;
```

**실행 순서는** `FROM` **→** `WHERE` **→** `GROUP BY` **→** `HAVING` **→** `SELECT` **→** `ORDER BY` **입니다**

---



# [8] JOIN



## 테이블을 나누는 이유

회원 정보와 회원이 쓴 글을 한 테이블에 다 넣는다고 생각해보겠습니다

그러면 이우빈이 글을 10개 쓸때마다 이름과 나이가 10번 중복해서 저장되겠죠?

그래서 회원은 `member`, 글은 `post`로 나누고, `post`에는 누가 썼는지 알 수 있게 `member_id`만 들고있게 만듭니다

아까 `GROUP BY`에서 봤던 그 `post` 테이블이 바로 이렇게 나눠둔 테이블입니다

이렇게 나눠둔 테이블을 다시 하나로 붙여서 보는게 JOIN입니다

## INNER JOIN

`INNER JOIN`은 양쪽 테이블에 모두 있는 데이터만 남기는 조인입니다

![INNER JOIN 동작](media/조인-inner.png)

그림에서 주황 점선으로 표시한 `id`와 `member_id`가 두 테이블을 이어주는 기준이 되는 열입니다

이 두 열의 값이 같은 것끼리 주황 선으로 이어진걸 확인할 수 있습니다

`2`번인 이우빈은 글이 두개라서 `자바 정리`,`SQL 정리` 두 줄과 이어졌고, `3`번인 박연지는 `DB 정리`와 이어졌습니다

**하지만 김석환은 쓴 글이 없어서 이어질 짝이 없고, 그래서 결과에서 아예 빠져버립니다**

이걸 SQL로 적으면 이렇게 됩니다

```sql
SELECT member.name, post.title
FROM member
INNER JOIN post ON member.id = post.member_id;
```


| name | title  |
| ---- | ------ |
| 이우빈  | 자바 정리  |
| 이우빈  | SQL 정리 |
| 박연지  | DB 정리  |


여기서 이우빈이 두 번 나오는건, 글이 두개라서 글마다 한 줄씩 만들어졌기 때문입니다

`ON` 뒤에는 두 테이블을 어떤 기준으로 이을지 적어주면 됩니다

그리고 테이블 이름을 매번 적기 귀찮으면 별칭을 붙여서 짧게 쓸 수 있습니다

```sql
SELECT m.name, p.title
FROM member m
INNER JOIN post p ON m.id = p.member_id;
```

참고로 `INNER`를 생략하고 `JOIN`만 적어도 똑같이 동작합니다

## 나머지 조인은 과제입니다

조인에는 `INNER JOIN` 말고도 `OUTER JOIN`, `NATURAL JOIN`, `USING` 같은게 더 있습니다

시간상 다 다루지는 못했으니 따로 공부해보시는걸 추천합니다!

---



# [9] 전체 정리



## 명령어 한눈에 보기

지금까지 본 명령어들을 표로 정리해봤습니다


| 명령어          | 하는 일               | 예시                                              |
| ------------ | ------------------ | ----------------------------------------------- |
| `INSERT`     | 행을 넣습니다            | `INSERT INTO member ... VALUES ...`             |
| `UPDATE`     | 저장된 값을 바꿉니다        | `UPDATE member SET height = 178 WHERE id = 5`   |
| `DELETE`     | 행을 지웁니다            | `DELETE FROM member WHERE id = 5`               |
| `SELECT`     | 어느 열을 볼지 고릅니다      | `SELECT name, age`                              |
| `FROM`       | 어느 테이블에서 꺼낼지 고릅니다  | `FROM member`                                   |
| `WHERE`      | 묶기 전, 행에 조건을 겁니다   | `WHERE height >= 184`                           |
| `GROUP BY`   | 같은 값끼리 묶습니다        | `GROUP BY member_id`                            |
| `HAVING`     | 묶은 다음, 그룹에 조건을 겁니다 | `HAVING COUNT(*) >= 2`                          |
| `ORDER BY`   | 결과를 정렬합니다          | `ORDER BY age DESC`                             |
| `INNER JOIN` | 양쪽에 다 있는 것만 붙입니다   | `INNER JOIN post ON member.id = post.member_id` |


한번에 다 외우실 필요는 전혀 없고, 필요하실 때마다 이 표를 다시 보시거나 구글링을 하시면 됩니다!

---

