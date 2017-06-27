---
layout: post
title: Java 정적(Static) 변수와 메소드
category: Java
tags:
- Java
- Static Variables
- Static Method
---

### Static 변수
  * 정적 변수는 하나의 클래스에 하나만 존재한다. (그 클래스의 모든 객체들에 의하여 공유된다.)
  * 메모리에 생성되는 시점: byte code가 메모리에 로딩되면서 문제없을 경우 메모리에 자동 생성된다.(메소드 영역)
  * 효과
    * 공유: lastname을 static 변수로 두면 이 변수는 클래스의 모든 객체에 의하여 공유된다. (같은 메모리 주소 값을 바라본다)
    * 메모리 절약: lastname을 static 변수로 두면 java는 메모리 할당을 한번만 하게 되어 메모리 사용에 이점을 볼 수 있다.
  {% highlight java %}
    public class Familly {
      static String lastname = "Kim";
      public static void main(String[] args) {
        Familly one = new Familly();
        Familly two = new Familly();
      }
    }
  {% endhighlight %}
  * final static
    * final 키워드는 한번 설정되면 그 값을 변경하지 못하게 하는 기능이 있다. 변경하려고 하면 예외가 발생한다.

### Static 메소드
  * 객체가 생성되지 않은 상태에서 호출되는 메소드. 객체안에서만 존재하는 인스턴스 변수 및 메소드들을 내부에서 사용할 수 없다.
  * 메소드 내부에서는 정적, 지역 변수만을 사용한다. (this 키워드도 인스턴스 변수이므로 사용 불가)
  * 인스턴스 변수에 따라 행동이 달라지지 않기 때문에 인스턴스나 객체가 필요하지 않고, 클래스명만 있어도 된다. (일반 메소드를 사용할 때는 레퍼런스 변수를 사용한다.)
  * static 메소드와 API: Util 클래스의 getCurrentDate메소드는 static 메소드.
  {% highlight java %}
    import java.text.SimpleDateFormat;
    import java.util.Date;

    public class Util {
      public static String getCurrentDate(String fmt) {
        SimpleDateFormat sdf = new SimpleDateFormat(fmt);
        return sdf.format(new Date());
      }

      public static void main(String[] args) {
        System.out.println(Util.getCurrentDate("yyyyMMdd"));
      }
    }
  {% endhighlight %}

  * static메소드와 일반 메소드
  {% highlight java %}
    // String의 length함수가 static이 왜 아닐까
    int length() {}
    static int length(String st) {}

    // 문자열을 구하는 함수는 문자열이 이미 메모리에 올라와 있는 상태이어야만 한다.
    // static 메소드로 이를 구현하면 메소드만 메모리에 올라와있는 상태로 구현이 가능하게 되야함..
  {% endhighlight %}

### Singleton 패턴
  * 싱글톤 패턴은 단 하나의 객체를 생성하게 강제하는 자바의 디자인 패턴이다.
  * static에 대한 개념이 생겼기 때문에 코드상으로 이 패턴을 구현하는 것이 가능하다.

  {% highlight java %}
    class Singleton {
      private static Singleton one;
      private Singleton() { } // private 클래스로 이 클래스의 생성자가 외부에서 호출되는 것을 막는다.
      public static Singleton getInstance() { // 이 클래스의 클래스 정적 변수를 반환하는 정적 메소드
         if (one == null) {
           one = new Singleton();
         }
         return one;
      }
    }
    public class SingletonTest {
      public static void main(String[] args) {
        Singleton singleton1 = Singleton.getInstance();
        Singleton singleton2 = Singleton.getInstance();
        System.out.println(singleton1 == singleton2); // true 출력된다.
      }
    }
  {% endhighlight %}
