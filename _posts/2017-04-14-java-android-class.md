---
layout: post
title: 안드로이드 예제를 통해 Java 클래스, 상속 알아보기
category: Java, Android
tags:
- Java
- Android
---

### 안드로이드 예제 프로그램을 통해 클래스에 대해 알아본다.

* UI
  * 이름을 입력할 EditText가 있고, Radio Button에서 생성(객체화)할 사람의 종류(클래스)를 선택한다.
  * WALK, RUN Button은 Person(사람)과 Baseball(야구 선수, Peron 클래스 상속)가 공통으로 가지고 있는 메소드를 호출하고,
  * HIT Button은 Baseball 클래스 만이 가지고 있는 메소드를 호출한다.
  * PITCH Button은 Person 클래스가 기본으로 가지고 있게하고, Baseball 클래스는 이 메소드를 오버라이드한다.
  * 메소드 호출 버튼을 누를때마다 이미지가 바뀐다.

  ![andoird_class]({{ site.url }}/public/img/android_class.png)

* MainActivity.java
  * 기본적인 클래스의 사용법과 패키지의 개념
  * NullPointerException의 개념 등을 파악할 수 있다.
  * 변수에 대한 접근 권한 키워드를 파악한다.
    * private: 같은 클래스 안에서만 접근하여 사용할 수 있다.
    * public: 아무 클래스에서나 접근하여 사용할 수 있다.
    * protected: 이 클래스에서 상속받은 자식 클래스에서만 접근하여 사용 가능하다.

{% highlight java %}
public class MainActivity extends AppCompatActivity {
    EditText editText;
    ImageView imageView;

    // 한 개발자가 만든 클래스와 다른 개발자가 만든 클래스를 구분하기 위해 패키지 단위로 import한다.
    // Person 클래스는 이 파일과 같은 패키지안에 위치
    Person person01;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editText = (EditText) findViewById(R.id.editText);
        imageView = (ImageView) findViewById(R.id.imageView);

        Button button1 = (Button) findViewById(R.id.button1);
        Button button2 = (Button) findViewById(R.id.button2);
        Button button3 = (Button) findViewById(R.id.button3);
        Button button4 = (Button) findViewById(R.id.button4);
        Button button5 = (Button) findViewById(R.id.button5);

        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String name = editText.getText().toString();
                RadioButton radio1 = (RadioButton) findViewById(R.id.radioButton1);
                boolean personChecked = radio1.isChecked();

                if (personChecked) {
                    createPerson(name);
                } else {
                    createBaseball(name);
                }

                imageView.setVisibility(View.VISIBLE);

                TextView textview3 = (TextView) findViewById(R.id.textView3);
                textview3.setText(Person.total + "명");
            }
        });

        button2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // Person 클래스를 인스턴스화하면 메모리에 Person 클래스가 인스턴스화 되어 올라갑니다.
                // person01 변수는 이 클래스를 포인터로 가르킵니다.
                // 그런데 person01 변수가 가리키는 객체가 아직 메모리에 올라와 있지 않다면 이 값은 Null값이 되어 NullPointerException이 발생합니다.
                if (person01 != null) {
                    person01.walk(10);
                } else {
                    Toast.makeText(getApplicationContext(), "먼저 사람을 만들어주세요.", Toast.LENGTH_LONG).show();
                }
            }
        });

        button3.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (person01 != null) {
                    person01.run(10);
                } else {
                    Toast.makeText(getApplicationContext(), "먼저 사람을 만들어주세요.", Toast.LENGTH_LONG).show();
                }
            }
        });

        button4.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (person01 != null) {
                    if (person01 instanceof Baseball) {
                        Baseball baseball01 = (Baseball) person01;
                        baseball01.hit();
                    } else {
                        Toast.makeText(getApplicationContext(), "Baseball 객체가 아니어서 안타를 칠수 없습니다.", Toast.LENGTH_LONG).show();
                    }
                } else {
                    Toast.makeText(getApplicationContext(), "먼저 사람을 만들어주세요.", Toast.LENGTH_LONG).show();
                }
            }
        });

        button5.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (person01 != null) {
                    person01.pitch();
                } else {
                    Toast.makeText(getApplicationContext(), "먼저 사람을 만들어주세요.", Toast.LENGTH_LONG).show();
                }
            }
        });
    }

    public void createPerson(String name) {
        Toast.makeText(getApplicationContext(), name + "이(가) 생성되었습니다. ", Toast.LENGTH_LONG).show();
        person01 = new Person(name, this);
        imageView.setImageResource(R.drawable.person);

        person01.age = 20;
        Person.total += 1;
    }

    public void createBaseball(String name) {
        Toast.makeText(getApplicationContext(), name + "이(가) 생성되었습니다. ", Toast.LENGTH_LONG).show();
        person01 = new Baseball(name, this);
        imageView.setImageResource(R.drawable.baseball);

        person01.age = 25;
        Person.total += 1;
    }
}
{% endhighlight %}

* Person.Java
  * MainActivity.java와 같은 패키지에 Person.java 클래스를 생성했다.
  * 클래스의 생성자의 개념에 대해 알 수 있었다.
  * static 키워드를 통해 인스턴스 변수와 클래스 변수의 차이점에 대해 알 수 있었다. static 메소드는 다음에 살펴보기로 함
  * Leg 클래스는 편의상 포스팅하지 않았다.
  * pitch 메소드는 하위 상속 클래스에서 오버라이드를 한다. 무조건 오버라이드하는 인터페이스 같은 것을 배웠던 것 같은데 나중에 살펴보기로 함
{% highlight java %}
package com.example.jangwon.androidclassstudy3;

import android.widget.Toast;

/**
 ** Created by jangwon on 2017. 4. 14..
 ** /

public class Person {
    // class에 접근 권한을 주지 않고 그대로 class Person으로 썻었던 이유는
    // MainActivity.java 파일안에 Person 클래스가 있어 그 필요성이 없었기 때문이다.
    protected String name;
    MainActivity activity;
    Leg leg = new Leg();

    // static 키워드를 붙이면 변수는 '클래스 변수'가 됩니다
    // 클래스 변수란 실제 객체들이 가지는 변수가 아니라 클래스라는 틀에 들어 잇는 변수 <-> '인스턴스 변수'
    // 세개의 객체를 만들었다고 해도 변수는 한 개가 그대로 유지됩니다 -> 모든 객체가 그 값을 사용하거나 바꿀 수 있습니다
    public static int total = 0;
    // static으로 선언된 클래스 변수는 객체 안에 들어있는 인스턴스 메소드에 의해 마음대로 접근 가능하지만
    // static으로 선언된 메소드는 객체 안에 들어 있는 인스턴트 변수를 마음대로 접근할 수 없습니다.
    public int age = 0;

    public Person() {

    }

    public Person(String inName, MainActivity inActivity) {
        name = inName;
        activity = inActivity;
    }

    public void walk(int speed) {
        // getApplicationContext 메서드는 Activity 클래스를 상속한 MainActiviy 클래스 안에 들어 있기 때문에 그 안에는 바로 호출이 가능하지만
        // 이 클래스에서는 바로 호출할 수 없기 때문에 생성자를 통해 Person 클래스로 MainActivity 객체를 전달한다.
        Toast.makeText(activity.getApplicationContext(), name + "이(가) " + speed + "km 속도로 걸어갑니다.", Toast.LENGTH_LONG).show();

        activity.imageView.setImageResource(com.example.jangwon.androidclassstudy3.R.drawable.person_walk);

        System.out.println(name + "이(가) " + speed + "km 속도로 걸어갑니다.");
    }
    public void run(int speed) {
        Toast.makeText(activity.getApplicationContext(), name + "이(가) " + speed + "km 속도로 뛰어갑니다.", Toast.LENGTH_LONG).show();
        activity.imageView.setImageResource(com.example.jangwon.androidclassstudy3.R.drawable.person_run);
        System.out.println(name + "이(가) " + speed + "km 속도로 뛰어갑니다.");
    }

    public void pitch() {
        Toast.makeText(activity.getApplicationContext(), name + "이(가) 아직 던지는 방법을 모릅니다.", Toast.LENGTH_LONG).show();
    }
}

{% endhighlight %}

* Baseball.Java
  * Person 클래스를 상속한다. Person 클래스의 멤버 변수와 생성자를 포함한 메소드를 그대로 사용가능하다.
  * hit 메소드는 Baseball 클래스에만 있는 메소드이다. Person 객체는 이 메소드를 사용할 수 없다.
  * pitch 메소드는 Person 클래스의 메소드를 Override 했다. super 키워드로 상위 클래스의 동일 메소드를 호출할 수 있지만 주석처리 했다.

{% highlight java %}
package com.example.jangwon.androidclassstudy3;

import android.widget.Toast;

/**
 ** Created by jangwon on 2017. 4. 14..
 ** /

class Baseball extends Person {

    public Baseball(String inName, MainActivity inActivity) {
        // 부모 클래스의 생성자의 파라미터로 받은 이름과 액티비티를 그대로 사용할 수 있다.
        name = inName;
        activity = inActivity;
    }

    public void hit() {
        Toast.makeText(activity.getApplicationContext(), name + "이(가) 안타를 칩니다.", Toast.LENGTH_LONG).show();
        activity.imageView.setImageResource(R.drawable.baseball_hit);
    }

    @Override
    public void pitch() {
//        super.pitch();
        Toast.makeText(activity.getApplicationContext(), name + "이(가) 투구합니다.", Toast.LENGTH_LONG).show();
        activity.imageView.setImageResource(R.drawable.baseball_pitch);
    }
}
{% endhighlight %}

* 참고: \[자바 + 안드로이드를 다루는 기술](정재곤 저)
