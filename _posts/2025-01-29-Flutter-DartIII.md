---
layout: post
title:  "Flutter"
date:   2025-01-29
author: Easyfun
categories: Flutter
tags: [documentation,sample]
image: flutterbird
---

## 泛型(Generics)

可以用泛型來確定特定的東西放到指定的地方。

{% highlight dart %}

List items = [];
items.add('money');
items.add(111);

{% endhighlight %}

這樣寫法靈活，但裡面的內容會變得不好管理。

使用泛型後，會變得清楚可控:

{% highlight dart %}

List<String> items = [];
items.add('money');  // 可以放
items.add(111); // 會報錯

{% endhighlight %}

### 泛型基本概念

泛型可以清楚操作的是什麼類型的列表，但除了規範類型外，它還能幫助避免重複撰寫程式碼。透過泛型，可以用同一段程式碼處理不同的型別，讓程式設計更高效。

泛型通常用單個大寫字母表示，如T、E、K、V:


{% highlight dart %}

class Box<T> {
  T value;
  Box(this.value);
}

var intBox = Box<int>(42);
var stringBox = Box<String>('Hello');

{% endhighlight %}

### 泛型函式

除了類別可以使用泛型外，函式也可以使用:

{% highlight dart %}

T firstElement<T>(List<T> list) {
  return list[0];
}

var first = firsrtElement<int>([1, 2, 3]);

{% endhighlight %}

### 泛型集合

當需要同時規範兩個類別，可用集合來表示，一次規範兩種類別。

{% highlight dart %}

T firstElement<T>(List<T> list) {

{% endhighlight %}

### 類型約束

使用extends關鍵字限制泛型類型，可以看到限制T只能是繼承自num的類別。例如int或者double，就無法使用String等其他非繼承自num的子類別。

{% highlight dart %}

class NumberBox<T extends num> {
  T value;

  NumberBox(this.value);
}

{% endhighlight %}

### 泛型的好處

1.程式碼重用:一個泛型類別或函式可以用於多種類型

2.類型安全:編譯時類型檢查可補獲錯誤

3.性能優化:泛型可以生成更高效的程式碼

### 類型推斷

Dart通常可推斷泛型的類型，如果是不同的類Dart會推斷為Object。

{% highlight dart %}

var names = ['Mike', 'Easy']; // Dart會推斷names的類型為List<String>
var names = ['1', 123];       // Dart會推斷names的類型為List<Object>

{% endhighlight %}

範例:


{% highlight dart %}

void printList<T>(list<T> list) {
  for (var item in list) {
    print(item);
  }
}

printList<int>([1, 2, 3]);
printList<String>(['a', 'b', 'c']);

{% endhighlight %}


