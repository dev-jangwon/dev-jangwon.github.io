---
layout: post
title: 관계 데이터베이스의 관계대수, 정규화
category: 데이터베이스
tags:
- 관계 데이터베이스
- 관계대수
- 릴레이션 정규화
---

### 관계대수

관계형 데이터베이스에서 원하는 정보와 그 정보를 어떻게 유도하는 가를 기술하는 절차적인 언어
* 피연산자: 릴레이션, 결과: 릴레이션
* 순수 관계 연산자
  * select, project, join, division
* 일반 집합 연산자
  * union, intersection, difference, cartesian product

### 정규화(Nomalization)

* 함수적 종속성 등의 종속성 이론을 이용하여 잘못 설계된 관계형 스키마를 더 작은 속성의 세트로 쪼개어 바람직한 스키마로 만들어 가는 과정
* 정규형의 차수가 높아질수록 만족시켜야 할 제약 조건이 늘어난다.
* 데이터베이스의 논리적 설계 단계에서 수행

### 정규화의 목적

* 데이터 구조의 안정성
* 중복을 배제하여 삽입, 삭제, 갱신 이상의 발생을 방지

### 이상( Anomaly)의 개념 및 종류
정규화를 거치지 않은 데이터베이스 내에 데이터들이 불필요하게 중복되어 릴레이션 조작 시 발생하는 예기치 못한 현상
* 삽입 이상
* 삭제 이상
* 갱신 이상

### 정규화 과정
[데이터 종속성과 정규화](http://beansberries.tistory.com/entry/%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A2%85%EC%86%8D%EC%84%B1%EA%B3%BC-%EC%A0%95%EA%B7%9C%ED%99%94)