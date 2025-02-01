---
layout: post
title:  "Dart Records"
date:   2025-01-30
author: Easyfun
categories: Flutter
tags: [documentation,sample]
image: flutterbird
---

## 紀錄(Records)

Records提供了輕量且靈活的方式來組合多個值，無需繁瑣的類別定義。

### 基本概念

1.Records是匿名的、不可變的複合類型

2.允許將多個值捆綁再一起，類似輕量級的Class

語法:

1.使用圓括號()來建立Records

2.可以包含位置參數和命名參數

{% highlight dart %}

var person = ('John', age: 30);  // John是位置參數

{% endhighlight %}

存取參數:

1.使用.$1、.$2等存取位置參數

2.使用.fieldName存取命名參數

{% highlight dart %}

print(person.$1);  // 輸出John
print(person.age); // 輸出30

{% endhighlight %}

類型註解:

可為record指定類型

{% highlight dart %}

(String, {int age}) typePerson = ('Mike', age: 30))

{% endhighlight %}

### 用途

當需要函式返回都個相關的值時，Record特別有用。像在獲取用戶基本資訊的場景中，可以同時返回姓名和年齡:

{% highlight dart %}

(String, int) getPersonInfo() {
  return ('Mike', 30);
}
var (name, age) = getPersonInfo();

{% endhighlight %}

### 相等性

兩個records有相同的結構和值，則被視為相等:

{% highlight dart %}

var record1 = (1, 2);

var record2 = (1, 2);

print(record1 == record2); // true

{% endhighlight %}


