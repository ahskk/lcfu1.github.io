---
layout: post
title: android在XML中画横线、竖线和虚线
author: lcfu1
original: 原创
---

## 一、画横线

```
<View
     android:layout_width="match_parent"
     android:layout_height="@dimen/border_line"
     android:background="#000000" />
```

## 二、画竖线

```
<View
     android:layout_width="1dp"
     android:layout_height="match_parent"
     android:background="#000000" />
```

## 三、画虚线

- 在drawable中新建一个dash_line.xml

```
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android" android:shape="line">
<stroke
    android:color="#000000"
    android:dashWidth="3dp"
    android:dashGap="5dp"/>
    <!--width：线条的高度
    color：颜色
    dashWidth：破折线的宽度
    dashGap：破折线间空隙的宽度
    如果这里设置了width，xml中android:layout_height的值必须比它大。不设置就默认为0
    -->
</shape>
```

- 在布局文件中使用

```
    <View
        android:layout_width="match_parent"
        android:layout_height="2dp"
        android:layerType="software"
        android:background="@drawable/dash_line"/>
```
