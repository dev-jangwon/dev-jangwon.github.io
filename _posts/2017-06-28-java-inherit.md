---
layout: post
title: Java 상속과 다형성
category: Java
tags:
- Inherit
- Polymorphism
- Overriding
- Overloading
---

### 상속(Inherit)
  * 하위 클래스에서 상위 클래스의 멤버를 물려받는 것.
  * 객체 생성 순서
  > java.lang.Object -> 부모 -> 자식 (상위 -> 하위)

  * extends 키워드 사용(상속은 단일 상속만 가능)
  * 상속받는 요소는 멤버, 메소드 2가지 뿐
  * 메소드 오버로딩(Overriding) - 재정의
    * 상속한 클래스에 동일한 메소드가 존재하며 인자의 수와 데이터 타입이 다른 경우
  * 메소드 오버라이딩(Overriding) - 다중정의
    * 동일한 클래스에서 동일한 이름의 생성자 또는 메소드를 여러개 만드는 것. parameter가 다를 수 있다.

### 다형성(Polymorphism)
  * 여러가지 형태를 가질 수 있는 능력 -> 코드의 재사용성 증대
  * 하나의 타입이 여러개의 형태를 가질 수 있는 것(조상클래스 타입의 참조변수로 자손클래스의 인스턴스를 참조할 수 있도록 하는 것)
  * 같은 모양의 코드가 다른 능력을 하는 것(핸드폰에 있는 키패드로 다이얼을 누르기도 하고, 문자를 보내기도 함)
  * 예제
{% highlight java %}

public class PolyTest {

	static Object m() { // Object 타입 return
		return "data";
	}

	// 다형성이 적용된 배열
	static Object[] m2() {
		Object[] v = new Object[3];
		v[0] = "data";
		v[1] = new Integer(3);
		v[2] = new Byte((byte) 2);
		return v;
	}

	static void m3(Object[] obj) {
		for (Object v : obj) {
			System.out.println(v.toString());
		}
	}

	static void m5(Object o) {
		if (o instanceof Book) {
			System.out.println(((Book) o).getTitle());
		} else if (o instanceof Person) {
			System.out.println(((Person) o).getId());
		}
	}

	public static void main(String[] args) {
		System.out.println("----1. 형변환----");
		String v = (String)m();
		System.out.println(v.length());
		System.out.println("----2. 다형성 적용 배열 및 toString override 메소드----");
		m3(m2());
		System.out.println("----3. 객체 타입 비교 연산자 : instanceof----");
		System.out.println(v instanceof Object);

		Book book = new Book("책1", "siba");
		Person person = new Person("김장원", "1234");

		System.out.println("----4. 객체 타입 비교 연산자2 : instanceof----");
		m5(book);
		m5(person);
	}

}
{% endhighlight %}
