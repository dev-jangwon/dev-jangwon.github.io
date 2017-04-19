---
layout: post
title: 안드로이드 예제를 통해 리스트뷰와 인플레이션 알아보기
category: Java, Android
tags:
- Java
- Android
---

### 안드로이드 예제 프로그램을 통해 리스트뷰와 인플레이션의 사용법에 대해 알아봅니다

* 리스트뷰(listView)
  * 지금까지의 예제에서는 ArrayList와 같은 타입의 리스트 객체를 사용할 때, 그 안에 들어 있는 각 객체를 텍스트뷰로 만들어 스크롤뷰 안에 보여주는 방법을 사용했었습니다.
  * 이렇게 스크롤뷰를 직접 만드는 방법을 사용하지 않고 하나의 위젯으로 이미 만들어둔 기능을 이용해 여러 뷰를 한꺼번에 화면에 보여줄 수 있는 것이 리스트뷰입니다.

* 선택 위젯(Selection Widget)
  * 리스트뷰와 같이 여러 데이터를 보여주고 그 중 하나를 선택할 때 원하는 기능을 실행할 수 있는 위젯을 선택 위젯이라고 부릅니다.
  * 선택 위젯(껍떼기)에서 어댑터의 역할
    * 선택 위젯의 안에 보이는 여러 데이터를 어댑터에서 관리합니다.
    * 어댑터는 리스트뷰 안에 보이는 각 아이템이 어떻게 보일지를 결정합니다.
    * 선택 위젯에 보이는 각 아이템을 위한 뷰 객체(버튼, 텍스트뷰, 이미지뷰 등)도 위젯에서 직접 만들지 않고 어댑터에서 만듭니다

* UI
  * 하나의 리스트뷰안에 야구팀 아이템들을 표시합니다
  * 각 아이템은 하나의 이미지와 팀명, 순위 두개의 텍스트로 이루어져 있습니다.
  * 이 아이템의 레이아웃을 인플레이션하여 어댑터를 통해 리스트뷰에 삽입합니다.

  ![andoird_listview]({{ site.url }}/public/img/listview.png)

* MainActivity.java
  * 리스트뷰를 정의하고 어댑터 클래스를 만들어서 setAdapter 함수를 통해 어댑터를 설정합니다.

{% highlight java %}
package com.example.jangwon.androidlistview;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.ListView;

public class MainActivity extends AppCompatActivity {

    public String[] teams = {"넥센", "삼성", "두산", "LG", "롯데", "한화", "SK", "NC", "KT", "KIA"};
    public String[] rank = {"1", "2", "3", "4", "5", "6", "7", "8", "9", "10"};
    public int[] images = {R.drawable.nexen, R.drawable.samsung, R.drawable.dusan, R.drawable.lg, R.drawable.lotte, R.drawable.hanhwa,
            R.drawable.sk, R.drawable.nc, R.drawable.kt, R.drawable.kia};

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        ListView listView = (ListView) findViewById(R.id.listview);

        MyAdapter adapter = new MyAdapter(this);

        // 만들어진 어댑터 객체를 통해 데이터를 어댑터에 추가한다
        for (int i = 0; i < 10; i++) {
            BaseballItem item = new BaseballItem(teams[i], rank[i], images[i]);
            adapter.addItem(item);
        }
        listView.setAdapter(adapter); // listview에 setAdapter함수를 통하여 어댑터를 설정한다.
    }
}
{% endhighlight %}

* MyAdapter.java
  * 안드로이드에서 기본으로 제공하는 BaseAdapter 클래스를 상속함으로써 어댑터의 기능을 구체적으로 구현합니다.
  * getView 메소드
    * 어댑터 안에 들어 있는 getView 메소드가 리스트뷰 위젯에 의해 자동으로 호출됩니다.
    * 내부적으로 getCount 함수를 호출하며 getView 메소드에서 리턴하는 뷰 객체가 리스트뷰의 한 아이템으로 보이게 됩니다.
    * getView에서 직접 java코드로 뷰 객체를 생성할 하여 리턴할 수도 있지만, 따로 레이아웃을 정의하여 이를 inflation 합니다.

  * 인플레이션
    * 일부 영역을 위한 레이아웃을 만드는 과정
      1. 일부 영역을 위한 XML 레이아웃 만들기
      2. 레이아웃 클래스를 상속하는 새로운 클래스 만들기
      3. 레이아웃 클래스에 XML 레이아웃 인플레이션으로 설정하기

  * 각 아이템에 필요한 데이터들을 어댑터에서 관리하는데, 이 데이터는 따로 클래스(BaseballItem)를 정의해놓고, 이를 ArrayList에 넣어둡니다.    

{% highlight java %}
package com.example.jangwon.androidlistview;

import android.content.Context;
import android.util.TypedValue;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseAdapter;
import android.widget.LinearLayout;
import android.widget.TextView;

import org.w3c.dom.Text;

import java.util.ArrayList;

/**
 ** Created by jangwon on 2017. 4. 18..
 ** /

public class MyAdapter extends BaseAdapter {

    ArrayList<BaseballItem> items = new ArrayList<BaseballItem>();

    Context mContext;

    public MyAdapter(Context context) {
        mContext = context;
    }

    @Override
    public int getCount() {
        return items.size();
    }

    @Override
    public Object getItem(int position) {
        return items.get(position);
    }

    @Override
    public long getItemId(int position) {
        return position;
    }

    public void addItem(BaseballItem item) {
        items.add(item);
    }

    public void clear() {
        items.clear();
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        // 화면에 보일 뷰 객체를 리턴해주는 메소드
//        LinearLayout layout = new LinearLayout(mContext);
        // 세로 방향으로 뷰를 추가한다
//        layout.setOrientation(LinearLayout.VERTICAL);
        // layout_width, layout_height 속성에 값을 넣어준다
//        LinearLayout.LayoutParams params = new LinearLayout.LayoutParams(
//                LinearLayout.LayoutParams.MATCH_PARENT,
//                LinearLayout.LayoutParams.WRAP_CONTENT);
//
//        TextView nameView = new TextView(mContext);
//        nameView.setText(teams[position]);
//        nameView.setTextSize(TypedValue.COMPLEX_UNIT_DIP, 30);
//
//        layout.addView(nameView, params);
//
//        TextView rankView = new TextView(mContext);
//        rankView.setText(rank[position]);
//        rankView.setTextSize(TypedValue.COMPLEX_UNIT_DIP, 24);
//
//        layout.addView(rankView, params);

        BaseballTeamLayout layout = new BaseballTeamLayout(mContext);

        BaseballItem item = items.get(position);

        layout.setImage(item.getResId());
        layout.setNameText(item.getName());
        layout.setRankText(item.getRank());

        return layout;
    }
}
{% endhighlight %}

* BaseballTeamLayout.java
  * LayoutInflater 객체를 통해 XML파일을 inflate합니다.
  * 생성자를 통해 상위 레이아웃으로부터 레이아웃 컨텍스트를 받아 옵니다.
  * getSystenService 메소드는 안드로이드 시스템에서 제공하는 서비스 객체들을 참조할 수 있도록 도와줍니다.
    * 시스템 서비스 객체란 OS가 시작되면 자동으로 만들어지는 서비스 객체로, 앱을 만들 때 필요한 기능을 항상 대기하면서 사용할 수 있도록 합니다.

{% highlight java %}
package com.example.jangwon.androidlistview;

import android.app.Activity;
import android.content.Context;
import android.support.annotation.Nullable;
import android.util.AttributeSet;
import android.view.LayoutInflater;
import android.widget.ImageView;
import android.widget.LinearLayout;
import android.widget.TextView;

/**
 ** Created by jangwon on 2017. 4. 18..
 ** /

public class BaseballTeamLayout extends LinearLayout {

    Context mContext;

    ImageView imageView;
    TextView textView1;
    TextView textView2;

    public BaseballTeamLayout(Context context) {
        super(context);
        mContext = context;
        init();
    }

    public BaseballTeamLayout(Context context, @Nullable AttributeSet attrs) {
        super(context, attrs);
        mContext = context;
        init();
    }

    private void init() {
        // baseballteam_item.xml 파일에 만들어둔 위젯의 배치를 이 레이아웃 클래스에 설정
        // 액티비티 클래스인 경우에는 setContentView에서 알아서 인플레이션 과정을 실행
        // 여기서는 xml 파일을 불러와서 직접 인프레이션 과정을 실행해본다
        LayoutInflater inflater = (LayoutInflater) mContext.getSystemService(Activity.LAYOUT_INFLATER_SERVICE);
        // 인플레이션 과정을 도와주는 시스템 서비스 객체를 찾는다
        // getSystenService 메소드는 안드로이드 시스템에서 제공하는 서비스 객체들을 참조할 수 있도록 도와준다
        inflater.inflate(R.layout.baseballteam_item, this, true);
        // inflate 메소드를 통해 레이아웃에 만들어진 정보를 이용해 메모리에 실제 레이아웃과 뷰 객체를 만든 후 레이아웃 클래스에 설정할 수 있도록 한다

        imageView = (ImageView) findViewById(R.id.imageView);
        textView1 = (TextView) findViewById(R.id.textView1);
        textView2 = (TextView) findViewById(R.id.textView2);
    }

    public void setNameText(String name) {
        textView1.setText(name);
    }

    public void setRankText(String rank) {
        textView2.setText(rank);
    }

    public void setImage(int resId) {
        imageView.setImageResource(resId);
    }
}

{% endhighlight %}

* 참고: \[자바 + 안드로이드를 다루는 기술](정재곤 저)
