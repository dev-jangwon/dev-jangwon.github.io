---
layout: post
title: 안드로이드 예제를 통해 액티비티와 인텐트 알아보기
category: Java, Android
tags:
- Java
- Android
---

### 안드로이드 예제 프로그램을 통해 액티비티와 인텐트에 대해 알아봅니다.

* UI
  * 메인 액티비티에서 Hello 버튼을 통해 다른 액티비티로 인텐트를 통해 데이터를 전달하면서 전환합니다.
  * Blog 버튼을 누르면 브라우저를 열고 블로그를 띄웁니다.
  * Phone 버튼을 누르면 다이얼 화면을 띄웁니다

  ![andoird_activity1]({{ site.url }}/public/img/activity1.png)
  ![andoird_activity2]({{ site.url }}/public/img/activity2.png)
  ![andoird_activity3]({{ site.url }}/public/img/activity3.png)

* MainActivity.java
  * 안드로이드에서는 일반적으로 한 화면을 액티비티라고 부릅니다.
  * 인텐트(Intent)는 데이터를 전달하기 위해 만들어준 안드로이드의 객체 타입입니다. 화면을 띄울 때 사용하는 startActivity라는 함수 상자로 넘겨주면 안드로이드 시스템으로 전달됩니다.
  * 부가 데이터(Extra Data)는 인텐트 객체에 넣어둘 수 있는 데이터입니다.
  * onActivityResult 메소드에서 받는 파라미터
    * 요청 코드: 액티비티를 띄울 때 사용한 숫자 값을 그대로 돌려받습니다.
    * 응답 코드: 다른 액티비티에서 응답 상태를 알려주기 위해 보내온 숫자 값을 받습니다.
    * 인텐트 객체: 다른 액티비티에서 setResult 메소드를 이용해 보내온 인텐트 객체입니다.

  * 컨텍스트(Context)
    * 컨텍스트란 어떤 객체의 주변 환경에 대한 정보를 가지고 있는 객체입니다.
    * 액티비티 안에 들어 있는 버튼이 화면의 어디에 위치하고 있는지 등에 대한 정보는 액티비티에서 관리해야하므로 일반적으로 액티비티가 버튼의 컨텍스트 역할을 합니다.

  * 수명 주기(Life Cyle)
    * 앱이 원하는 상황이 아니라 시스템이 강제로 지시하는 상황이 생길 수 있으므로, 그때마다 앱에 상황을 알려주어 필요한 일들을 할 수 있도록 만들어 놓은 것을 '생명주기'라고 합니다
    * 메인 액티비티에서는 onCreate 메소드가 시작점 역할을 합니다
    * onResume 메소드는 액티비티가 화면에 보이기 전에 호출되고
    * onPause 메소드는 액티비티가 화면에서 사라지기 전에 호출됩니다.


{% highlight java %}
package com.example.jangwon.androidintentactivity;

import android.content.Intent;
import android.net.Uri;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        Toast.makeText(getApplicationContext(), "onCreate() 호출됨", Toast.LENGTH_LONG).show();
        // 화면이 메모리에 만들어짐
        setContentView(R.layout.activity_main);

        Button button1 = (Button) findViewById(R.id.newbutton1);
        Button button2 = (Button) findViewById(R.id.button2);
        Button button3 = (Button) findViewById(R.id.button3);

        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // 안드로이드 뷰와 컨텍스트
//                Intent myintent = new Intent(getApplicationContext(), NewActivity.class);
                // 이 클래스 변수는 새로운 클래스를 만들 때마다 자바에서 자동으로 만들어주는 변수이며 클래스 객체를 나타낸다.
                // 클래스라는 틀을 하나의 객체처럼 전달할 수 있게 해준다
//                myintent.putExtra("loginName", "dev.jangwon");
//                startActivityForResult(myintent, 1);

                User.loginName = "dev.jangwon";
                Intent myintent2 = new Intent(getApplicationContext(), NewActivity.class);
                startActivityForResult(myintent2, User.REQ_CODE_PHONEBOOK);
            }
        });

        button2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse("https://dev-jangwon.github.io/"));
                startActivity(intent);
            }
        });

        button3.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse("tel:01094729601"));
                startActivity(intent);
            }
        });
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        // protected : 상속한 클래스에서만 수정할 수 있음
        super.onActivityResult(requestCode, resultCode, data);

//        String outName = data.getStringExtra("name");
//        Toast.makeText(getApplicationContext(), "전달받은 name 속성의 값: " + outName, Toast.LENGTH_LONG).show();

        if (requestCode == User.REQ_CODE_PHONEBOOK) {
            if (resultCode == User.REQ_CODE_SUCCESS) {
                String outName2 = data.getStringExtra("name");
                Toast.makeText(getApplicationContext(), "전달받은 name 속성의 값: " + outName2, Toast.LENGTH_LONG).show();
            } else {
                Toast.makeText(getApplicationContext(), "실패하였습니다.", Toast.LENGTH_LONG).show();
            }
        }
    }

    @Override
    protected void onStart() {
        super.onStart();
        // 화면 기능을 실행할 준비를 함ㅁ
        Toast.makeText(getApplicationContext(), "onStart() 호출됨", Toast.LENGTH_LONG).show();
    }

    @Override
    protected void onStop() {
        super.onStop();
        // 화면의 기능을 중지시키는 과정
        Toast.makeText(getApplicationContext(), "onStop() 호출됨", Toast.LENGTH_LONG).show();
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        // 화면을 메모리에서 없애버른 과정
        Toast.makeText(getApplicationContext(), "onDestroy() 호출됨", Toast.LENGTH_LONG).show();
    }

    @Override
    protected void onPause() {
        super.onPause();
        // 화면에서 보이지 않도록 하는 과정
        // 화면의 상태를 임시 저장
        Toast.makeText(getApplicationContext(), "onPause() 호출됨", Toast.LENGTH_LONG).show();
    }

    @Override
    protected void onResume() {
        super.onResume();
        // 화면에 보여주기 전에 준비를 끝냄
        // 임시로 저장된 화면의 상태를 불러온다
        Toast.makeText(getApplicationContext(), "onResume() 호출됨", Toast.LENGTH_LONG).show();
    }

    @Override
    protected void onRestart() {
        super.onRestart();

        Toast.makeText(getApplicationContext(), "onRestart() 호출됨", Toast.LENGTH_LONG).show();
    }
}
{% endhighlight %}

* NewActivity.java
  * 매니패스트
    * 안드로이드에서는 어떤 화면을 추가했는 지 확실하게 하기 위해서 매니페스트에 화면에 대한 정보를 등록한다.
    * 이는 AndroidManifest.xml 파일에 등록되어 있으며, 이 안에는 어떤 화면이 만들어져 있는지에 대한 정보 외에도 다양한 정보가 들어있다.
    * activity_new.xml 액티비티를 생성후, Activity 클래스를 상속한 NewActivity 클래스를 만들고 <activity android:name=".NewActivity"/>를 매니패스트에 추가한다.
  * 액티비티를 없애고 싶을 때는 finish 메소드를 이용합니다.
  * 원래 액티비티로 응답을 보내고 싶을 때는 setResult 메소드를 사용합니다

{% highlight java %}
package com.example.jangwon.androidintentactivity;

import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

public class NewActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_new);

        Button newbutton1 = (Button) findViewById(R.id.newbutton1);

       newbutton1.setOnClickListener(new View.OnClickListener() {
           @Override
           public void onClick(View v) {
//               Intent passedIntent = getIntent();
//               String loginName = passedIntent.getStringExtra("loginName");
//               Toast.makeText(getApplicationContext(), "화면에서 받은 loginName." + loginName, Toast.LENGTH_LONG).show();

               String loginName2 = User.loginName;
               Toast.makeText(getApplicationContext(), "화면에서 받은 loginName." + loginName2, Toast.LENGTH_LONG).show();

               Intent intent = new Intent();
               intent.putExtra("name", "jangwon");
//               setResult(RESULT_OK, intent);

               setResult(User.REQ_CODE_SUCCESS);

               finish(); // 화면에 보이는 액티비티를 없애준다.
           }
       });
    }
}
{% endhighlight %}

* User.java
  * 화면 간에 데이터를 전달할 때 인텐트를 통하여 데이터를 전송할 수도 있지만 새로운 클래스를 하나 만들고 그 안에 static 키워드를 사용한 "클래스 변수"를 만들어 사용할 수도 있습니다.

{% highlight java %}
package com.example.jangwon.androidintentactivity;

/**
 ** Created by jangwon on 2017. 4. 17.
 ** /

public class User {
    public static String loginName;

    public static final int REQ_CODE_PHONEBOOK = 1;

    public static final int REQ_CODE_SUCCESS = 200;
    public static final int REQ_CODE_FAILURE = 400;
}

{% endhighlight %}

* 참고: \[자바 + 안드로이드를 다루는 기술](정재곤 저)
