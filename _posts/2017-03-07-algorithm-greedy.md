---
layout: post
title: 그리디 알고리즘
category: 알고리즘
tags:
- 알고리즘
- Greedy Algorithm
---

### 그리디 알고리즘
* 욕심쟁이 알고리즘
  * 여러 경우 중 하나를 결정해야 할 때마다 그 순간에 최적이라고 생각되는 것을 선택해 나가는 방식
  * 그 순간마다 최적의 해를 구하기 때문에, 결과적으로 항상 최적해는 아니다.
  * '부분해 집합'

* 대표 알고리즘
  * kruskal algorithm
  * prim algorithm
  * dijkstra algorithm
  * task scheduling algorithm

* 예시
  * 11047 [동전 0](https://www.acmicpc.net/problem/11047) / [소스코드](https://github.com/dev-jangwon/algorithm/blob/master/201703/20170307/11047.cpp)
    1. 해 선택: 가장 가치가 높은 동전을 우선으로 거스름돈을 구성하면 동전의 개수가 줄어들 테니, 현재 고를 수 있는 가장 가치가 높은 동전을 골라서 부분해 집합에 추가한다.
    2. 적절성 검사: 부분해 집합이 거슬러 줄 금액을 초과하는지 검사한다. 초과한다면 가장 최근에 추가한 동전을 삭제하고, 1로 돌아가서 현재보다 한 단계 작은 동전을 추가한다.
    3. 해 검사: 부분해 집합이 거슬러 줄 금액과 일치하는 지 검사한다. 액수가 모자라면 다시 1로 돌아가서 부분해 집합에 추가한 동전을 고른다.
  * * 1931 [회의실 배정](https://www.acmicpc.net/problem/1931) / [소스코드](https://github.com/dev-jangwon/algorithm/blob/master/201703/20170308/1931.cpp)
