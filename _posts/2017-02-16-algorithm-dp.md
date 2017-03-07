---
layout: post
title: 동적 계획법
category: 알고리즘
tags:
- 알고리즘
- Dynamic Programming
---

### 동적 계획법(Dynamic Programming)
* 일반적으로 주어진 문제를 풀기 위해서, 문제를 여러 개의 하위 문제(subproblem)로 나누어 푼 다음, 그것을 결합하여 최종적인 목적에 도달하는 것이다. 각 하위 문제의 해결을 계산한 뒤, 그 해결책을 저장하여 후에 같은 하위 문제가 나왔을 경우 그것을 간단하게 해결할 수 있다. 이러한 방법으로 동적 계획법은 계산 횟수를 줄일 수 있다. 특히 이 방법은 하위 문제의 수가 기하급수적으로 증가할 때 유용하다.
* 부분 문제들이 곂치지 않는 분할정복 알고리즘과는 다르다.
* 다음 두 가지 속성을 만족해야 동적 계획법으로 문제를 풀 수 있다.
  * 곂치는 부분문제 (Overlapping Subproblem)
    * 큰 문제와 작은 문제를 같은 방법으로 쪼갤 수 있다.
    * 문제를 작은 문제로 쪼갤 수 있다.
    * 같은 재귀함수 호출 반복.
  * 최적 부분구조 (Optimal Substructure)
    * 문제의 정답을 작은 문제의 정답에서 구할 수 있다.
    * Optimal Substructure를 만족한다면, 문제의 크기와 상관없이 어떤 한 문제의 정답은 일정하다.
    * 부분 문제의 최적해로부터 전체 문제의 최적해가 만들어지는 구조.
    * 최적 부분구조를 만족하는 동적 계획법 문제에서 각 문제는 한번만 풀어야 한다.
* Memoization
  * 중복된 계산을 막기 위해 저장된 결과를 배열에 저장한 뒤, 다음에 계산이 필요할 때는 저장된 값을 불러오는 기법.

### 동적 계획법을 푸는 두 가지 방법
* Top-Down
  * 문제를 작은 문제로 나누고, 해결된 작은 문제들을 이용해 전체 문제를 해결한다.
  * 재귀함수 + 메모이제이션
  {% highlight cpp %}
  int memo[100];
  int fibonacci(int n) {
    if (n <= 1) {
      return n;
    } else {
      if (memo[n] > 0) {
        return memo[n];
      }
      memo[n] = fibonacci(n - 1) + fibonacci(n - 2);
      return memo[n];
    }
  }
  {% endhighlight %}
* Bottom-Up
  * 문제를 크기가 작은 문제부터 차례대로 푼다.
  * 문제의 크기를 조금씩 크게 만들면서 문제를 점진적으로 풀어나간다.
  * 반복문 + 배열
  {% highlight cpp %}
  int memo[100];
  int fibonacci(int n) {
    d[0] = 0;
    d[1] = 1;
    for (int i = 2; i <= n; i++) {
      d[i] = d[i - 1] + d[i - 2];
    }
    return d[n];
  }
  {% endhighlight %}

  * 동적 계획법으로 해결한 피보나치 수
  ![fibonacci]({{ site.url }}/public/img/fibonacci.png)

### 동적 계획법 문제 풀이 전략
* 문제를 작은 문제로 나누고, 수식을 이용하여 문제를 표현해야 한다.
  1. 함수의 정의를 세운다.
  2. 점화식을 세운다.
  3. 기저조건을 세운다.
  4. 메모이제이션 변수의 차원 수를 정한다. (Top-Down의 경우에는 재귀 호출의 인자의 개수)

* 1463 [1로 만들기](https://www.acmicpc.net/problem/1463) / [소스코드](https://github.com/dev-jangwon/algorithm/blob/master/201701/20170125/1463.cpp)

* 9465 [스티커](https://www.acmicpc.net/problem/9465) / [소스코드](https://github.com/dev-jangwon/algorithm/blob/master/201701/20170126/9465.cpp)
