---
layout: post
title: Java의 자료형
category: Java
tags:
- Java
- Primitive Type
---

### Java의 자료형
  * Java의 자료형에는 기본형(Primitive Type)과 참조형(Reference Type)이 있다.
  * Primitive Type
    * byte/short/int/long, float/double, char, boolean
    * Java의 기본 자료형은 반드시 사용하기 전에 선언되어야 한다, 비객체 타입이므로 null값을 가질 수 없다.
    * Runtime Data Areas의 스택 영역에 값을 직접 가진다.

  * Reference Type
    * 기본적으로 java.lang.Object를 상속받으면 참조형이 된다.
    * 실제 보유하고 있는 데이터는 null or 메모리에 생성된 객체의 주소값이다.
    * 이 데이터는 Runtime Data Areas의 힙 or 메소드 영역에 존재한다.
    * 생성자 호출 없이도 사용 가능한 실제 객체로 생성되는 타입 두가지
      * String ""
      * 배열 {값1, 값2, ...}

  * 예제
  {% highlight java %}
  public class Test {
    // 두 변수 모두 객체가 생성되는 시점에 스택영역 메모리에 올라간다.
  	String name; // 참조 자료형 변수
  	int age; // 기본 자료형 변수

  	String getName() {
  		return this.name;
  	}

  	void setName(String name) {
      /*
      * 1. 참조 변수(String형) 메모리 확보(스택 영역)
      * 2. 실제 객체 생성(힙 영역)
      * 3. 값 저장(=연산)
      */
  		this.name = name;
  	}

  	int getAge() {
  		return age;
  	}

  	void setAge(int age) {
      /*
      * 1. 기본 변수(int형) 메모리 확보(스택 영역)
      * 2. 값 저장(=연산)
      */
  		this.age = age;
  	}

  	public static void main(String[] args) {
            Test t = new Test();
            /*
            * 1. 멤버 변수(Test형) 메모리 확보(스택 영역)
            * 2. 실제 객체 생성(힙 영역)
            * 3. 값 저장(=연산)
            */
            t.setName("김장원");
            t.setAge(25);
            System.out.println(t.getName() + " " + t.getAge());
  	}

  }
  {% endhighlight %}
