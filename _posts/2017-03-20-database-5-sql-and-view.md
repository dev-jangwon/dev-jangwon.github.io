---
layout: post
title: 관계 데이터베이스의 SQL과 View
category: 데이터베이스
tags:
- 관계 데이터베이스
- SQL
- View
---

### DDL(데이터 정의어)

* create, alter, drop

### DML(데이터 조작어)

* select, insert, delete, update

### DCL(데이터 제어어)

* commit, rollback, grant, revoke

### Embedded SQL(내장 SQL)

* 응용 프로그램이 실행될 때 함께 실행되도록 호스트 프로그램 언어로 만든 프로그램에 삽입된 SQL


### 뷰(View)

* 사용자에게 접근이 허용된 자료만을 제한적으로 보여주기 위해 하나 이상의 기본 테이블로부터 유도된 가상 테이블
* 저장장치 내에 물리적으로 존재하지 않음
* 뷰를 통해서만 데이터에 접근하게 하면 뷰에 나타나지 않는 데이터를 안전하게 보호할 수 있음
* 논리적 데이터 독립성 제공
