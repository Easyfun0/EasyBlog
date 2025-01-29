---
layout: post
title:  "Flutter function"
date:   2025-01-28
author: Easyfun
categories: Flutter
tags: [documentation,sample]
image: flutter.png
---

## 函式(Function)

Dart對函式處理很靈活，允許將其它數據類型一樣進行賦值、傳遞和返回，大幅強化其表達能力和靈活性。

### 函式宣告

{% highlight dart %}

int add(int a, int b) {
  return a + b;
}
// 也可用箭頭函式跟JS一樣
int multiply(int a, int b) => a * b;

{% endhighlight %}

### 可選參數

Dart支持可選的位置參數和命名參數，就是不一定要滿足全部函式所需的參數，可選擇性的填寫:

{% highlight dart %}

// 可選的位置參數
String great (String name, [String? greeting]) {
  greeting ??= 'HIIII';   // 如果greeting為null，使用預設值
  return '$greeting, $name!';
}

// 可選的命名參數，在使用上必須填上參數名稱
void printPerson({required String name, int? age}) {
  print('Name: $name');
  if (age != null) {
    print('Age: $age');
  }
}

// 使用
print(greet('Mike'));  // 輸出: HIIII, Mike!
print(greet('Mike', 'Hi'));  // 輸出: HI, Mike!
printPerson(name: 'Easy'); // 輸出: Name: Easy
printPerson(name: 'Easyfun0', age: 30); //輸出: Name: Easyfun0 和 Age: 30

{% endhighlight %}


### 函式作為變數傳遞

變數通常只用來儲存數據(例如整數、字串等)，在Dart中，函式也可被視為一個「值」，並可像數據一樣傳遞。也意味著可將函式作為參數傳遞給其他函式，甚至可以將函數賦值給變數，靈活地控制程式碼執行流程。

{% highlight dart %}

var sayHello = (String name) => 'Hello, $name!';
print(sayHello('Mike')); // 輸出: Hello, Mike!

{% endhighlight %}

