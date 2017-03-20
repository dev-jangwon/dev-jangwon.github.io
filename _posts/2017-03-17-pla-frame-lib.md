---
layout: post
title: Framework & Library & API
category: 기타
tags:
- Framework
- Library
- API
---

### 플랫폼: 특정 장치나 시스템, 서비스 등에서 이를 구성하는 기반이 되는 하드웨어나 소프트웨어 환경
  * 컴퓨터: Windows, Mac OS, Linux
  * 모바일: iOS, Android
  * Java로 만든 시스템의 플랫폼: Java

### 프레임워크
  * 소프트웨어의 구체적인 부분에 해당하는 설계와 구현을 재사용이 가능하게끔 일련의 협업화된 형태로 클래스들을 제공하는 것
    * (좀 더 효율적인 개발을 위해 프레임워크 설계자들이 미리 어플리케이션의 기본 구조를 정해준 것)
  * 프레임워크는 구체적이며 확장 가능한 기반 코드를 가지고 있으며, 설계자가 의도하는 여러 디자인 패턴의 집합으로 구성되어 있다.
  * 프레임워크는 라이브러리와 달리 어플리케이션의 틀과 구조를 결정할 뿐 아니라, 그 위에 개발된 개발자의 코드를 제어한다.
  * 라이브러리는 개발자가 필요한 것들을 빌려와 쓰는 대상이고, 프레임워크는 개발자가 어떻게 개발할 것인지를 결정해주는 툴이다.
    * 라이브러리와 달리 완성된 도구가 아니다. 개발자가 구현하고자하는 것에 대한 방법론이나 설계만 제공.
  * Java의 Spring 프레임워크, Microsoft의 .NET 프레임워크

### 라이브러리
  * 미리 만든 함수들을 어딘가에 저장해 놓고, 개발자들은 필요시 가져와 편리하게 사용할 수 있는 것.
  * 개발을 하면서 필요한 기능들을 라이브러리에서 가져와 사용할 수 있다.

### API(Application Programming Interface)
  * 다른 프로그램 / 라이브러리의 특정 기능을 호출하기 위한 일종의 약속 / 사양
  * 그래픽 카드나 디스크 드라이브 등의 하드웨어 또는 데이터베이스를 조작할 때, API는 작업을 편리하게 해준다. 대개 실제로는 밑바닥에서 매우 저수준으로 이러한 작업이 수행된다. API는 이러한 작업들에 대한 기능을 대상이 되는 언어에 맞게 추상화하고 프로그래머가 사용하기 편리하게 설계된 인터페이스 사양이다.
  * https://namu.wiki/w/API

### SDK(Software Development Kit)  
  * API가 실제 기능 구현체인 라이브러리와 함께 제공되는 경우도 있으며, 이 경우를 보통 Software Development Kit(SDK)라고 한다. SDK는 보통 API, 라이브러리와 함께 프로그램을 개발하는데 필요한 여러 보조 프로그램이 같이 배포된다.

### 프레임워크 vs 라이브러리 vs API
  * 공장(프레임워크) 에서 상품(어플리케이션)을 만들고,

  * 상품(어플리케이션)를 만들기 위한 부품(라이브러리)이 필요하고,

  * 부품(라이브러리) 및 상품(어플리케이션)를 만들기위해 서류(API)가 필요하다.

출처: [재춘이이뻐염](http://jechue.tistory.com/11) /
     [hashcode](http://hashcode.co.kr/questions/1838/%ED%94%8C%EB%9E%AB%ED%8F%BC-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-api%EC%97%90-%EB%8C%80%ED%95%9C-%EC%9D%B4%ED%95%B4) / [쏭이리](https://opentutorials.org/module/1896/11023)