---
layout: post
title: SharedPreferences存储
---

## 一、百科一下

- SharedPreferences是Android平台上一个轻量级的存储类，用来保存应用的一些常用配置，比如Activity状态，Activity暂停时，将此activity的状态保存到SharedPereferences中;当Activity重载，系统回调方法onSaveInstanceState时，再从SharedPreferences中将值取出。

- SharedPreferences提供了java常规的Long、Int、String等类型数据的保存接口。 &nbsp;SharedPreferences类似过去Windows系统上的ini配置文件，但是它分为多种权限，可以全局共享访问。

- 提示最终是以xml方式来保存，整体效率来看不是特别的高，对于常规的轻量级而言比SQLite要好不少，如果真的存储量不大可以考虑自己定义文件格式。xml处理时Dalvik会通过自带底层的本地XML Parser解析，比如XMLpull方式，这样对于内存资源占用比较好。

## 二、SharedPreferences数据的四种操作模式

- Context.MODE_PRIVATE
- Context.MODE_APPEND
- Context.MODE_WORLD_READABLE
- Context.MODE_WORLD_WRITEABLE

1、Context.MODE_PRIVATE:为默认操作模式,代表该文件是私有数据,只能被应用本身访问,在该模式下,写入的内容会覆盖原文件的内容。

2、Context.MODE_APPEND:模式会检查文件是否存在,存在就往文件追加内容,否则就创建新文件。

3、Context.MODE_WORLD_READABLE和Context.MODE_WORLD_WRITEABLE用来控制其他应用是否有权限读写该文件。在android 4.2中已废用。

## 三、使用
- getSharedPreferences()方法中，第一个参数为SharedPreferences文件的名称，第二个为操作模式。
- PreferenceManager类中的getDefaultSharedPreferences()方法。自动使用包名作为前缀来命名SharedPreferences文件。它接受一个Context参数
- edit()方法获取一个SharedPreferences.Editor对象。
- apply()方法提交数据。
- SharedPreferences文件是xml格式的，可在File Explorer中导出。

MainActivity.java

```
package com.lcfu1.sharedpreferences;

import android.content.SharedPreferences;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;

public class MainActivity extends AppCompatActivity {
    private EditText mEditText;
    private Button mSave;
    private Button mShow;
    private SharedPreferences mSharedPreferences;
    private SharedPreferences.Editor mEditor;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        mEditText= (EditText) findViewById(R.id.ed);
        mSave= (Button) findViewById(R.id.save);
        mShow= (Button) findViewById(R.id.show);

        mSharedPreferences=getSharedPreferences("text",MODE_PRIVATE);
        mEditor=mSharedPreferences.edit();

        mSave.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                //添加数据
                mEditor.putString("String",mEditText.getText().toString());
                mEditor.putInt("Int",1);
                mEditor.putBoolean("Boolean",true);
                //apply()方法提交数据
                mEditor.apply();
            }
        });
        mShow.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Log.d("MainActivity", "---String---"+mSharedPreferences.getString("String",""));
                Log.d("MainActivity", "---Int---"+mSharedPreferences.getInt("Int",0));
                Log.d("MainActivity", "---Boolean---"+mSharedPreferences.getBoolean("Boolean",false));
            }
        });
    }
}
```

- activity_main.xml

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
   >
    <EditText
        android:id="@+id/ed"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>
    <Button
        android:id="@+id/save"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="save"/>
    <Button
        android:id="@+id/show"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="show"/>

</LinearLayout>
```

![1](http://upload-images.jianshu.io/upload_images/6025530-721a8505bf08fa60.PNG?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 打印的log信息如下图
![打印的log](http://upload-images.jianshu.io/upload_images/6025530-96eef750eaf2aae9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 保存的位置：/data/data//shared_prefs

![打开](http://upload-images.jianshu.io/upload_images/6025530-0f68680d20750f3b.PNG?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![保存的位置](http://upload-images.jianshu.io/upload_images/6025530-9c7783a00b110e90.PNG?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
