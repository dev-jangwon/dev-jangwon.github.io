---
layout: post
title: 안드로이드 예제를 통해 인터페이스와 어댑터 알아보기
category: Android
tags:
- Java
- Android
---

### 안드로이드 예제 프로그램을 통해 캡슐화, 인터페이스와 어댑터에 대해 알아봅니다

* 캡슐화(Encapsulation)
  * 하나의 객체가 그 안에서 모든 기능을 수행하도록 하는 것
  * 캡슐이나 풍선처럼 막에 싸여 있다면 모든 기능을 다른 객체가 건드릴 수 없으며 명령만 내릴 수 있습니다.

* UI
  * 두 숫자를 입력하고 사칙연산을 통한 결과를 출력합니다.
  * 결과란 아래에는 연산할때마다 연산과정의 히스토리를 출력합니다.
  * clear 버튼을 누르면 히스토리가 초기화 됩니다.

  ![andoird_calculator]({{ site.url }}/public/img/calculator.png)

* MainActivity.java
  * 인터페이스(interface)
    * 인터페이스란 클래스에 접근할 수 있는 방법이 무엇인지를 정의한 것입니다.
    * 구현한다(implement)의 의미: 인터페이스에서는 껍떼기만 있고 실행될 코드가 없던 것에 직접 실행 가능한 기능을 넣어준다는 의미입니다

  * Exception 키워드 사용하기
    * 이 앱에서는 계산기의 메소드가 Calculator라는 인터페이스로 제공이 되는데, 이를 구현하는 클래스에서 메소드를 구현하지 않았을 때 Exception을 던져주는 것을 위해 다음 예외 클래스를 만들었습니다.

{% highlight java %}
package com.example.jangwon.androidcalculator;
/**
 ** Created by jangwon on 2017. 4. 17..
 ** /

public class UnImplementedException extends Exception {
    public UnImplementedException() {
        super();
    }
    public UnImplementedException(String name) {
        super(name);
    }
}
{% endhighlight %}

  * 다음과 같이 예외 클래스를 하나 만들면 예외 상황이 발생할 때 그 클래스로 만든 예외 객체를 throw 키워드를 이용해 던져줄 수 있습니다
  * Exception
    1. Exception 클래스를 상속하는 새로운 객체 만들기
    2. 인터페이스에서 구현하지 못한 메소드에 사용하기 위해 throw 키워드와 함께 넣어주기
    3. 인터페이스를 구현한 클래스에서 throws 키워드 함께 넣어주기
    4. 예외 상황이 발생하는 코드에서 throw와 함께 예외 객체 던져주기
    5. 메소드를 호출하는 쪽에서는 try-catch 문으로 예외 처리하기

{% highlight java %}
package com.example.jangwon.androidcalculator;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        final EditText editText1 = (EditText) findViewById(R.id.editText1);
        final EditText editText2 = (EditText) findViewById(R.id.editText2);
        final EditText editText3 = (EditText) findViewById(R.id.editText3);

        final TextView textView = (TextView) findViewById(R.id.textView);

        Button button1 = (Button) findViewById(R.id.button1);
        Button button2 = (Button) findViewById(R.id.button2);
        Button button3 = (Button) findViewById(R.id.button3);
        Button button4 = (Button) findViewById(R.id.button4);
        Button button5 = (Button) findViewById(R.id.button5);

       final Calculator calculator = new MyCalculator();

        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String aStr = editText1.getText().toString();
                String bStr = editText2.getText().toString();

                int a = 0, b = 0;
                try {
                    a = Integer.parseInt(aStr);
                    b = Integer.parseInt(bStr);
                } catch (Exception e) {
                    e.printStackTrace();
                }

                int result = calculator.add(a, b);

//                Calculator calculator1 = new FriendCalculator(getApplicationContext());
//                result = calculator1.add(a, b);
                editText3.setText(String.valueOf(result));

                ArrayList<CalcData> history = calculator.getHistory();
                String outStr = "";
                for (int i = 0; i < history.size(); i++) {
                    CalcData curData = history.get(i);
                    outStr = "\n#" + i + " : " + curData.getA() + ", "
                             + curData.getB() + ", "
                             + curData.getType() + ", "
                             + curData.getResult() + ", ";
                }
                textView.setText(outStr);
            }
        });

        button2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String aStr = editText1.getText().toString();
                String bStr = editText2.getText().toString();

                int a = 0, b = 0;
                try {
                    a = Integer.parseInt(aStr);
                    b = Integer.parseInt(bStr);
                } catch (Exception e) {
                    e.printStackTrace();
                }

                Calculator calculator = new MyCalculator();
                int result = 0;
                try {
                    result = calculator.substract(a, b);
                } catch (UnImplementedException e) {
                    Toast.makeText(getApplicationContext(), "빼기는 안됩니다.", Toast.LENGTH_LONG).show();
                    e.printStackTrace();
                }

                editText3.setText(String.valueOf(result));
            }
        });

        button5.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                calculator.clearHistory();
                textView.setText("");
            }
        });
    }
}

{% endhighlight %}

* MyCalculator.java
  * MyCalculator.java는 객체화 될 수 없는 추상 클래스 CalculatorAdapter를 상속합니다
  * 추상 클래스
    * 아직 모든 메소드가 구현되지 않은 클래스입니다, 클래스 앞에 abstract를 붙이고, 구현되지 않는 메소드 앞에 abstract를 붙입니다.
    * 추상 클래스는 미완성된 클래스이므로 실제 객체로 만들 수 없습니다
    * abstract 키워드
      * 클래스 앞에 abstract 키워드가 붙으면 추상 클래스라고 부릅니다
      * 추상 클래스는 abstract 키워드가 붙어 있는 메소드를 하나 이상 포함하고 있는 클래스를 말합니다

  * 어댑터(Adapter)
    * 메소드들 중에서 필요한 것만 구현할 수 있도록 걸러주는 역하를 하는 클래스를 어댑터라는 이름으로 부르기도 합니다
    * 어댑터는 클래스가 만들어야 하는 기능 중 일부를 대신 만들어주는 역할을 합니다

{% highlight java %}
  package com.example.jangwon.androidcalculator;

  /**
   ** Created by jangwon on 2017. 4. 17..
   ** /

  public class MyCalculator extends CalculatorAdapter {
      @Override
      public int add(int a, int b) {
          int result = a + b;
          addHistory(a, b, CalcData.TYPE_ADD, result);

          return result;
      }

      @Override
      public int substract(int a, int b) throws UnImplementedException {
          throw new UnImplementedException("구현 안함");
  //        return 0;
      }

      @Override
      public int multiply(int a, int b) throws UnImplementedException {
          throw new UnImplementedException("구현 안함");
  //        return 0;
      }

      @Override
      public int divide(int a, int b) throws UnImplementedException {
          throw new UnImplementedException("구현 안함");
  //        return 0;
      }
  }

{% endhighlight %}

* CalculatorAdapter.java
  * 추상 클래스 CalculatorAdapter는 Calculator 인터페이스를 구현합니다.
{% highlight java %}
package com.example.jangwon.androidcalculator;

import java.util.ArrayList;

/**
 ** Created by jangwon on 2017. 4. 17..
 ** /

public abstract class CalculatorAdapter implements Calculator {

    private ArrayList<CalcData> history = new ArrayList<CalcData>();

    public abstract int add(int a, int b);

    @Override
    public int substract(int a, int b) throws UnImplementedException {
        throw new UnImplementedException("구현 안함");
    }

    @Override
    public int multiply(int a, int b) throws UnImplementedException {
        throw new UnImplementedException("구현 안함");
    }

    @Override
    public int divide(int a, int b) throws UnImplementedException {
        throw new UnImplementedException("구현 안함");
    }

    public void addHistory(int a, int b, int type, int result) {
        CalcData data = new CalcData(a, b, type, result);
        history.add(data); // ArrayList 내장 함수 add
    }

    public void clearHistory() {
        history.clear();
    }

    public ArrayList<CalcData> getHistory() {
        return history;
    }
}

{% endhighlight %}

* Calculator.java
  * 계산기 메소드를 제공하는 인터페이스입니다.
{% highlight java %}
package com.example.jangwon.androidcalculator;

import java.util.ArrayList;

/**
 ** Created by jangwon on 2017. 4. 17..
 ** /

public interface Calculator {
    public int add(int a, int b);
    public int substract(int a, int b) throws UnImplementedException;
    public int multiply(int a, int b) throws UnImplementedException;
    public int divide(int a, int b) throws UnImplementedException;

    public void clearHistory();
    public ArrayList<CalcData> getHistory();
}

{% endhighlight %}



* 참고: \[자바 + 안드로이드를 다루는 기술](정재곤 저)
