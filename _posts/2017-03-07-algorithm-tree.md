---
layout: post
title: 트리
category: 알고리즘
tags:
- 알고리즘
- 트리
---

### 트리
* 트리
  * 수학(그래프)에서 트리는 회로(cycle)가 없는 무방향 연결 그래프.
  * 자료구조에서 트리는 부모-자식 관계로 정의. 부모에서 자식으로 간선이 부속되어 있는 방향 그래프.

* 트리의 종류
  * 순서 트리(ordered tree)
    * 각 자식 노드에 순서가 부여되어 저장 위치가 고정되는 트리
  * 이진 트리(binary tree)
    * 각 노드의 차수 / 자식이 2 이하인 순서 트리
  * [이진 탐색 트리](https://ko.wikipedia.org/wiki/%EC%9D%B4%EC%A7%84_%ED%83%90%EC%83%89_%ED%8A%B8%EB%A6%AC)(binary search tree, BST)
  * 균형 트리(balanced tree, B-Tree)
    * 이진 트리에서 하위 노드 구조가 좌우 대칭이 되도록 한 것.
    * 이진 탐색 트리를 일반화시킨 트리 자료구조를 말함. 데이터베이스 및 파일 시스템에 널리 쓰이는 자료구조.
    * 성능 및 공간 활용을 위해 이진 탐색 트리에 제약 조건을 부가시켜 확장.
      * 트리가 항상 균형을 유지
      * 삭제로 인한 공간 낭비 최소화
    * DBMS에서의 B-Tree  

* 트리 용어
  ![tree]({{ site.url }}/public/img/tree.png)
  * 노드, 마디
    * 트리를 구성하는 기본 원소
    * A, B, C ...
  * 차수
    * 자식 노드 들 중 최대 개수
    * B가 가장 많은 자식 3을 가지므로 차수: 3
  * 깊이, 높이, 레벨
    * 깊이: 루트 노드에서 어떤 노드까지의 경로 길이
      * D의 깊이: 2
    * 높이: 가장 긴 깊이
      * 가장 긴 깊이: 4
    * 레벨: 같은 깊이
      * A의 레벨: 1
      * B, C의 레벨: 2
      * D, E, F, G, H의 레벨: 3

* 트리 순회
  * 일정 순서로 트리 내 모든 노드를 방문하는 것.
  * ![tree_traversal]({{ site.url }}/public/img/tree_traversal.png)
  * 전위 순회한 결과 : ABDCEFG // (루트) (왼쪽 자식) (오른쪽 자식)
  * 중위 순회한 결과 : DBAECFG // (왼쪽 자식) (루트) (오른쪽 자식)
  * 후위 순회한 결과 : DBEGFCA // (왼쪽 자식) (오른쪽 자식) (루트)
  * 1991 [트리 순회](https://www.acmicpc.net/problem/1991) / [소스코드](https://github.com/dev-jangwon/algorithm/blob/master/201703/20170307/1991.cpp)

* 트리를 저장하는 방법
  * N링크 표현법(N-link)
    * 장점: 직관적으로 이용 가능. 시간 복잡도 비교적 우수
    * 단점: 구현이 복잡함. 자식의 개수는 최대 N개.
  * 왼쪽 자식 / 오른쪽 형제 표현법(LCRS)
    * 장점: 구현이 비교적 쉬움. 데이터가 늘어나도 효과적으로 만들 수 있음.
    * 단점: 부모노드에서 자식노드를 한번에 방문할 방법이 없음. 내 자식이 몇 명인지 모름.

* 트리의 부모, 지름
  * 11725 [트리의 부모 찾기](https://www.acmicpc.net/problem/11725) / [소스코드](https://github.com/dev-jangwon/algorithm/blob/master/201703/20170307/11725.cpp)
  * 1967 [트리의 지름](https://www.acmicpc.net/problem/1967) / [소스코드](https://github.com/dev-jangwon/algorithm/blob/master/201703/20170307/1967.cpp)
