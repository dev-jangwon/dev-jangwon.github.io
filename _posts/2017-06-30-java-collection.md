---
layout: post
title: Java Collection과 Generic
category: Java
tags:
- Java
- Collection
- Generic
---

### Java 컬렉션 프레임워크
  * 여러 객체 원소의 삽입과 삭제가 편리한 자료구조를 지원하는 인터페이스
  * 인터페이스를 구현한 여러 클래스로 컬렉션 프레임워크를 구성
  * 인터페이스 분류
    * List 계열 -> ArrayList, Vector, Linked List
    * Set 계열 -> HashSet, TreeSet
    * Map 계열 -> HashMap, Properties, HashTable, TreeMap
  * Iterator객체를 멤버로 가지고 있는 컬렉션은 그를 통해 자료구조 내부의 요소를 순회할 수 있다.  

### 제네릭
  * 제네릭은 다양한 타입의 객체들을 다루는 메서드나 컬렉션 클래스에 컴파일 시의 타입 체크를 해주는 기능이다.
  * 클래스 내부에서 사용할 데이터 타입을 나중에 인스턴스를 생성할 때 확정하는 것을 제네릭이라 한다.
  * 객체의 타입을 컴파일 시에 체크하기 때문에 객체의 타입 안정성을 높이고 형변환의 번거로움이 줄어든다. (매번 꺼내서 형변환하고 이런 부분을 방지)
  * JDK 문서의 ArrayList, 제네릭 타입으로 선언되어 있다.
  ![java_generic]({{ site.url }}/public/img/generic.png)
