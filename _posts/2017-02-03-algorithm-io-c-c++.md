---
layout: post
title: 알고리즘과 입/출력
category: 알고리즘
tags:
- 알고리즘
- C / C++
---

## 알고리즘 문제에서 입력받는 방식

### 테스트 케이스가 주어지는 경우
* 테스트 케이스의 개수를 입력받은 뒤 그 갯수만큼 반복문을 순회
  * 10950 [A+B-3](https://www.acmicpc.net/problem/10950) / [소스코드](https://github.com/dev-jangwon/algorithm/blob/master/201702/20170203/10950.c)

### 테스트 케이스가 주어지지 않는 경우
* 입력을 EOF까지 받으면 된다.
{% highlight cpp %}
// C : scanf의 리턴 값은 성공적으로 입력받은 변수의 개수다.
while(scanf("%d %d", &a, &b) == 2)
// C++
while(cin >> a >> b)
{% endhighlight %}
  * 10951 [A+B-4](https://www.acmicpc.net/problem/10951) / [소스코드](https://github.com/dev-jangwon/algorithm/blob/master/201701/20170121/10951.c)

### 한 줄을 입력받아야 하는 경우
* 아래 두 방법은 한 줄을 입력받을 수 없다.
{% highlight cpp %}
// C
scanf("%s", s);
// C++
cin >> s;
{% endhighlight %}
* 아래 세 방법은 모두 한 줄을 전체로 입력받을 수 있다. fgets는 줄바꿈까지 입력되기 때문에, 조심해야한다.
{% highlight cpp %}
// C
fgets(s, 100, stdin);
scanf("%[^\n]\n", s);
// C++
getline(cin, s);
{% endhighlight %}
  * 11718 [그대로 출력하기](https://www.acmicpc.net/problem/11718) / [소스코드](https://github.com/dev-jangwon/algorithm/blob/master/201701/20170121/11718.c)
  * 11719 [그대로 출력하기2](https://www.acmicpc.net/problem/11719) / [소스코드](https://github.com/dev-jangwon/algorithm/blob/master/201701/20170121/11719.c)
