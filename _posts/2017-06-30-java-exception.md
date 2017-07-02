---
layout: post
title: Java 예외처리
category: Java
tags:
- Java
- Exception
---

### 예외 처리
  * 예외(Exception): Java 프로그램에서 실행중에 발생할 수 있는 경미한 오류 -> 적절한 처리 모듈을 추가하여 발생한 문제를 복구 가능
  * try ~ catch ~ finally 문법으로 예외처리
  * 에러(Error): 메모리나 내부의 심각한 문제, 복구 불가한 오류
  * 사용자 정의 예외 클래스
  {% highlight java %}
    public class IdDoubleException extends Exception { // 최상위 Exception 클래스 상속
      IdDoubleException() {}

      public IdDoubleException(String msg) {
        super(msg);
      }
    }
  {% endhighlight %}
  * 예외 클래스 사용 -> throws, throw new ~, try ~ catch
  {% highlight java %}
    public class ExceptionTest3 {
      static void idCheckWithException(String id) throws IdDoubleException {
        if (!id.equals("master")) {
          throw new IdDoubleException("id 중복 불허 " + id);
        }
      }

      public static void main(String[] args) {
        try {
          idCheckWithException("master");
          idCheckWithException("nono");
        } catch(IdDoubleException e) {
          e.printStackTrace();
        }
      }
    }
  {% endhighlight %}
