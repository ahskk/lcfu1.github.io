---
layout: post
title: Bottom Navigation底部导航栏
author: lcfu1
original: 原创
---

## 一、Bottom Navigation

- 这里我就不介绍[Material Design](https://material.io/guidelines/material-design/introduction.html)了,想了解更多就去看看官网，来看看他们自己的Introduction：(温馨提示：由于本人英语水平有限，以下引用均用有道翻译来翻译)

>We challenged ourselves to create a visual language for our users that synthesizes the classic principles of good design with the innovation and possibility of technology and science. This is material design. This spec is a living document that will be updated as we continue to develop the tenets and specifics of material design.
我们挑战自己，为我们的用户创造一种视觉语言，它综合了优秀设计的经典原则和技术和科学的可能性。这是材料设计。这个规范是一个活的文件，将会更新，因为我们继续发展的原则和材料设计的细节。

- [Bottom Navigation](https://material.io/guidelines/components/bottom-navigation.html#)，想要使用Bottom Navigation，个人建议先看一下Bottom Navigation的设计，再来学习怎么用它。

>Bottom navigation bars make it easy to explore and switch between top-level views in a single tap.
底部导航条使得在单个点击中探索和切换顶级视图变得很容易。

>Tapping on a bottom navigation icon takes you directly to the associated view or refreshes the currently active view.
点击底部导航图标将直接带您到相关视图或刷新当前活动视图。

>Bottom navigation is primarily for use on mobile. To achieve a similar effect for desktop, use side navigation.
底部导航主要用于移动设备。为了达到类似的效果，桌面，使用边导航。

>**Usage**
Three to five top-level destinations
Destinations requiring direct access
3到5个顶级目的地
目的地需要直接访问

>**Color**
Tint the active icon with the app’s primary color. Use black or white if the bottom navigation bar is already colored.
用app的主色来着色活动图标。如果底部导航栏已经着色，请使用黑色或白色。

>**Specs**
Width of each action: The width of the view divided by the number of actions (with a max of 168dp and a minimum of 80dp)
Height: 56dp
Icon: 24 x 24dp
每个动作的宽度:视图的宽度除以操作数(最大值为168dp，最小为80dp)
高度:56 dp
图标:24×24 dp

## 二、使用

- 最快的方法就是在android studio中直接新建一个Bottom Navigation Activity。当然也可以新建一个Empty Activity。
- 首先添加以下依赖

```
implementation 'com.android.support.constraint:constraint-layout:1.0.2'
```

1、MainActivity.java

```
package com.example.lcf.myapplication;

import android.os.Bundle;
import android.support.annotation.NonNull;
import android.support.design.widget.BottomNavigationView;
import android.support.v7.app.AppCompatActivity;
import android.view.MenuItem;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {
    private TextView mTextMessage;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        mTextMessage = (TextView) findViewById(R.id.message);

        BottomNavigationView navigation = (BottomNavigationView) findViewById(R.id.navigation);
        navigation.setOnNavigationItemSelectedListener(new BottomNavigationView.OnNavigationItemSelectedListener() {
            @Override
            public boolean onNavigationItemSelected(@NonNull MenuItem item) {
                switch (item.getItemId()) {
                    case R.id.navigation_home:
                        mTextMessage.setText(R.string.title_home);
                        return true;
                    case R.id.navigation_edit:
                        mTextMessage.setText(R.string.title_edit);
                        return true;
                    case R.id.navigation_dashboard:
                        mTextMessage.setText(R.string.title_dashboard);
                        return true;
                    case R.id.navigation_notifications:
                        mTextMessage.setText(R.string.title_notifications);
                        return true;
                }
                return false;
            }
        });
    }
}
```

2、activity_main.xml

```
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/container"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.example.lcf.myapplication.MainActivity">

    <TextView
        android:id="@+id/message"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginLeft="@dimen/activity_horizontal_margin"
        android:layout_marginStart="@dimen/activity_horizontal_margin"
        android:layout_marginTop="@dimen/activity_vertical_margin"
        android:text="@string/title_home"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <android.support.design.widget.BottomNavigationView
        android:id="@+id/navigation"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginEnd="0dp"
        android:layout_marginStart="0dp"
        android:background="?android:attr/windowBackground"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:menu="@menu/navigation" />

</android.support.constraint.ConstraintLayout>
```

3、navigation.xml，右击menu文件夹新建一个Menu resource file，name为navigation，由于我在这里使用了vector drawable，所以还要添加以下依赖`implementation 'com.android.support:support-vector-drawable:26.1.0'`。navigation.xml的代码如下：

```
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:id="@+id/navigation_home"
        android:icon="@drawable/ic_home_black_24dp"
        android:title="@string/title_home" />
    <item
        android:id="@+id/navigation_edit"
        android:icon="@drawable/ic_edit_black_24dp"
        android:title="@string/title_edit" />
    <item
        android:id="@+id/navigation_dashboard"
        android:icon="@drawable/ic_dashboard_black_24dp"
        android:title="@string/title_dashboard" />

    <item
        android:id="@+id/navigation_notifications"
        android:icon="@drawable/ic_notifications_black_24dp"
        android:title="@string/title_notifications" />

</menu>
```

## 三、上图来看看

- 运行截图如下：

![image.png](http://upload-images.jianshu.io/upload_images/6025530-f926d09e07dc52ce.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 上面是四个top-level destinations的，来看看3个的
![image.png](http://upload-images.jianshu.io/upload_images/6025530-cd953b9326932733.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 对比一下，如果只有三个动作，则始终显示图标和文本标签
如果有四个或五个操作，则仅将非活动视图显示为图标。
