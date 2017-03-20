---
layout: post
title: JVM, JRE, JDK
category: Java, Android
tags:
- Java
- JDK, JRE, JVM
---

### Java 플랫폼
  * Java 프로그램을 구동시킬 수 있는 Hardware, Software 환경
  * Java를 구동시키는 환경에 따라 Java 플랫폼이 달라진다.
    * Java SE: 표준 Java 플랫폼. Java 가상머신 규격 및 API 집합을 포함.
    * Java EE: Java를 이용한 서버측 개발을 위한 플랫폼. SE기능을 모두 포함한다.
    * Java ME: 임베디드를 위한 Java 플랫폼
  * JVM / JRE는 운영체제와 같은 플랫폼에 의존적이지만 Java 언어는 독립적.
    * 자바 프로그램은 운영체제에 독립적이며, 자바 가상머신은 운영체제에 의존적이다.


### JDK(Java Development Kit)
* Java SE, EE, ME 중 하나를 구현한 것. Oracle사에 의해 바이너리로 배포된다.
* Java 컴파일러, Java 가상 머신, 각종 Java Library를 포함합니다.
* Java를 개발 할 수 있는 SDK == JDK
  * JVM:  하드웨어와 소프트웨어 플랫폼에서 Java 기술을 사용한 어플리케이션을 동작시키기 위한 프로그램
    *  사용자 .java -> JDK 컴파일, .class 생성 -> JVM 기계어 변환
  * JRE
    * jvm이 실행되도록 도와주는 역할
    * 컴파일된 Java 프로그램을 실행시킬 수 있는 Java 환경
  * Java API, Library
    * java, javac, jar...
