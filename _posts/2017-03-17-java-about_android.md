---
layout: post
title: Android Platform
category: Android
tags:
- Java
- Android
---

### Android Platform Architecture

![Android]({{ site.url }}/public/img/Android_Platform.png)

* Linux Kernel
  * 가장 아랫단에, Linux 커널이 올라가 있다. 일반적인 Linux 커널과 크게 다르지는 않지만, 모바일 디바이스에 최적화된 전력 관리 기능이나 안드로이드에 최적화된 Binder IPC (프로세스간 커뮤니케이션) 부분등이 포함
  1. 프로세스 관리, 디바이스 관리, 메모리 관리를 Linux를 사용한다.
  2. C 언어로 작성되었다.

* Libraries: 안드로이드 시스템 컴포넌트가 사용하는 다양한 C/C++ Library를 제공한다.
  * Linux 커널위에는 C로 구현된 몇가지 네이티브 라이이브러리들이 올라가 있다. 3차원 그래픽을 위한, OPEN GL, 로컬 데이타 베이스를 제공하는 SQLLite 데이타 베이스, 웹 브라우징을 위한 WebKit, 멀티미디어 재생을 위한 Media Framework들이 올라가 있다.
  * 이러한 시스템 라이브러리들은 내부적으로 JNI 인터페이스를 통해서 자바 코드로부터 호출되게 된다.
    1. SQLite : 경량 데이터베이스 엔진
    2. Webkit : HTML 컨텐츠를 신속하게 디스플레이하기 위한 브라우저 엔진
    3. Surface Manager : 다양한 창화면의 그래픽 효과를 제공

* Android Runtime
  * Java Core Libraries와 Dalvik Virtual Machine으로 구성(안드로이드 런타임 위에는 기본 JVM과 자바 라이브러리가 올라감.)
  * 모바일 애플리케이션을 위해서 최적화된 JVM으로 안드로이드는 달빅(Dalvik)이라는 이름의 VM이 올라간다. 이 달빅 JVM이 실제로 안드로이드 애플리케이션을 시작하게 된다.
  * 그리고, 그 위에 코어 자바라이브러리들이 올라가게 된다. (java.*, javax.* ,org.* ...등)
    1. Java 가상머신을 직접 사용하지 않고 모바일 환경에 최적화된 Dalvik Virt을 사용한다.
    2. Dalvik Virtual Machine은 안드로이드 전용 가상머신이므로 자바 클래스를 바로 실행
    할 수는 없으며 클래스 파일을 dex 포맷으로 변환해야만 실행 가능합니다.
    3. Dalvik Virtual Machine : Application 마다 Object(객체) 1개를 생성합니다.

* Application Framwork
  * 마치 서버 개발에서 자바 위에, JEE 나 스프링,Hibernate와 같은 프레임웍이 있는 것 같이 애플리케이션 개발용 프레임웍이 올라가 있다.
    1. Framework API로 구성, 개발자를 위해 여러 Architecture를 제공한다.
    2. Application을 만들때 사용될 빌딩블럭을 제공한다.
    3. 응용 프로그램들은 하위 Kernel들을 직접 호출할 수 없으며 이 영역의 Framwork를 통해 기능을 요청 할 수 있습니다.
    4. Activity Manager : Activity 관리, Activity 생명주기를 관리
    5. Content Providers : DataBase를 관리하며 SQLite가 탑재되어 있다.
    6. View System : View를 관리
    7. Package Manager : Android는 패키지로 이루어졌는데 그 패키지를 관리한다.
    8. Resource Manager : 문자열, 그래픽, 레이아웃 파일과 같은 코드화되지 않은 자원에 대한 접근을 관리한다.
    9. Notification Manager : 통보 기능을 관리, 통지(Battery 부족하다는 경구 메시지 알림 기능 등)
    10. Location Manager : 위치관련 등을 관리, GPS 탑재
