---
layout: post
title: 그래프
category: 알고리즘
tags:
- 알고리즘
- 그래프
---

### 그래프
* 정점과 간선으로 이루어진 자료구조의 일종
  * G = (V, E)
* 정점(Vertex)
* 간선(Edge): 정점간의 관계를 나타낸다.

* 경로: 정점 사이의 길
* 사이클: 시작과 끝이 같은 경로

* 단순 경로 / 단순 사이클
  * 경로 / 사이클에서 같은 정점을 두 번 이상 방문하지 않는 경로 / 사이클

* 방향 있는 그래프 / 방향 없는 그래프(양방향 그래프)

* 루프: 간선의 양 끝 점이 같은 경우

* 가중치: A에서 B로 이동하는 거리, 필요한 시간, 비용 등 / 가중치가 없는 경우에는 모든 가중치가 1이라고 생각하고 풀면 된다.

* 차수: 정점과 연결되어 있는 간선의 개수

### 그래프의 표현 방법
![graph]({{ site.url }}/public/img/graph.png)
* 정점: 변수 하나로 개수를 저장하면 된다.
* 간선: 무엇과 무엇을 연결하였는지 저장해야 한다.

* 인접 행렬
  * 정점의 개수를 V라고 했을 때, (V X V) 행렬로 그래프를 표현한다.
  * 없는 간선도 저장하기 때문에 자주 사용하지 않는다.
  * 공간 복잡도: O(V^2)

* 인접 리스트
  * 링크드 리스트를 이용해서 구현한다.
  * 링크드 리스트는 구현하는데 시간이 오래걸리기 때문에, 주로 vector와 같이 길이를 변경할 수 있는 배열을 이용해서 구현한다.
  * 공간 복잡도: O(E)

### 그래프의 탐색
  * 목적: 모든 정점을 1번씩 방문한다.
  * DFS(깊이 우선 탐색)
    * 최대한 깊숙히, 스택을 사용한다.
    * 갈 수 있는 만큼 최대한 많이 가고, 갈 수 없으면 이전 정점으로 돌아가서 탐색을 진행한다.
    * 재귀 호출을 이용해서 구현할 수 있다.
    {% highlight cpp %}
    int V, E; // 정점, 간선
    int adj[SIZE][SIZE]; // 인접 행렬
    int visited[SIZE] // 방분 여부 표시

    void DFS(int now) {
      int next;
      visited[now] = 1; // 현재 정점 방문했음 표시
      for(next = 0; next < V; next++) { // 정점 개수만큼 반복
        // 현재 정점과 다음 정점이 인접하고,
        // 다음 정점을 방문한 적이 없다면
        if (adj[now][next] == 1 && !visited[next]) {
          DFS(next);
        }
      }
    }
    {% endhighlight %}

  * BFS(너비 우선 탐색)
    * 최대한 넓게, 큐를 사용한다.
    * 모든 가중치가 1이라고 했을 때, 최단 거리를 찾는 알고리즘이 된다.
    {% highlight cpp %}
    int V, E; // 정점, 간선
    vector<vector<int> > adj; // 인접 리스트
    bool visited[SIZE]; // 방문 여부 표시

    void BFS(int root) { // root: 맨 처음 시작 정점
      visited[root] = true; // 시작 정점 방문했음 표시
      queue<int> q;
      q.push(root); // 맨 처음 시작 정점 push
      while(!q.empty()) { // queue가 빌 때까지 탐색
        int now = q.front();
        q.pop();
        int size = adj[now].size();
        for (int i = 0; i < size; i++) {
          int next = adj[now][i];
          if (!visited[next]) { // 다음 정점에 방문한 적이 없다면
            visited[next] = true; // 다음 정점 방문했음 표시
            q.push(next); // 다음 정점 queue에 push
          }
        }
      }
    }
    {% endhighlight %}

  * 1260 [DFS와 BFS](https://www.acmicpc.net/problem/1260) / [소스코드](https://github.com/dev-jangwon/algorithm/blob/master/201702/20170215/1260.cpp)

  * 11724 [연결 요소의 개수](https://www.acmicpc.net/problem/11724) / [소스코드](https://github.com/dev-jangwon/algorithm/blob/master/201702/20170221/11724.cpp)
