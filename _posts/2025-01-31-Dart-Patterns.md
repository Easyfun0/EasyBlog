---
layout: post
title:  "Dart Patterns"
date:   2025-01-31
author: Easyfun
categories: Flutter
tags: [documentation,sample]
image: flutterbird
---

## Patterns

在Dart3.0才有的特性Patterns，可用於匹配、解構和處理複雜的數據結構。

### Patters三大核心

1.數據解構(Destructuring)

將複雜的數據結構拆解成簡單的變數:

{% highlight dart %}

// 基礎解構:從陣列中提取數據
var nums = [1, 2, 3];
var [first, second, third] = nums;
print('第一個是$first');  // 輸出: 第一個是 1

// 對象解構: 從Map中提取數據
var person = {'name':'Easyfun', 'age': 30);  
var ('name': name, 'age': age} = person;
print('$name 今年 $age 歲'); // 輸出:Easyfun今年30歲

// 複雜結構解構

var data = {'user': {'profile': {'name': 'EJ', 'age': 30}}};
var {'user': {'profile': {'name': userName}}} = data;
print('用戶名: $userName'); // 輸出:用戶名: EJ

{% endhighlight %}

2.模式匹配(Pattern Matching)

用於檢查數據是否符合特定結構，並根據結構執行不同操作:

{% highlight dart %}

void processData(dynamic data) {
  switch (data) {
    // 匹配值陣列結構
    case [int x, int y];
      print('這是一個座標: ($x,$y)');

    // 匹配Map結構
    case {'name': String name, 'age': int age}:
      print('這是人:$name, $age歲');

    // 匹配數值範圍
    case int n when n > 0 && n < 100;
      print('這是一個1-99的數字:$n');

    default;
      print('未知類型');
  }
}

// 使用範例
processData([10, 20]);   // 這是一座標:(10, 20)

// 輸出:這是人: Easy, 30歲
processData({'name': 'Easy', 'age': 30});
processData(70);   // 這是一個1-99的數字: 70

{% endhighlight %}

3.數據轉換(Data Transformation)

在處理數據時進行過濾或轉換:

{% highlight dart %}

// 過濾列表中的偶數
var nums = [1, 2, 3, 4, 5, 6];
var evenNum = [
  for (var n in num)
  if (n.isEven) n
];
print(evenNum);  // 輸出:[2, 4, 6]

// 轉換數據結構

var users = [
  {
    'name': 'Mike',
    'scores': [100, 90, 80]
  },
  {
    'name': 'Easyfun',
    'scores': [90, 80 ,100]
  }
];

var transformedData = [
  for (var ('name': name, 'scores': scores as List<int>) in users)
  {
    'student': name,
    'average': scores.isEmpty
    ? 0
    : scores.fold<num>(0, (a, b) => a + b) / scores.length
  }
];

print(transformedData);
// 輸出: [{student: Mike, average: 90.0}, {student: Easyfun, average: 92.0}]

{% endhighlight %}

### 實用的Pattern類型

1. 變數模式(Variable Pattern)

{% highlight dart %}
// 基本的模式，用於任何值
var [a, b] = [1, 2];  // a = 1, b = 2

{% endhighlight %}

2. 列表模式(List Pattern)

{% highlight dart %}
// 匹配固定長度列表
var [x, y, z] = [1, 2, 3];

// 使用...匹配剩餘元素
var [first, second, ...rest] = [1, 2, 3, 4, 5];
print(rest); //輸出:[3, 4, 5]

// 可以跳過某些元素
var [a, ..., c] = [1, 2, 3]; // a = 1, c = 3

{% endhighlight %}

3. Map模式(Map Pattern)

{% highlight dart %}
// 基本Map匹配
var {'name': name, 'age': age} = {'name': 'EJ', 'age': 30};
print(name); // EJ
print(age); // 30

// 只提取需要的字段

var {'name': username} = {'name': 'EJ', 'age': 30, 'city': 'Tai'};
print(userName); // EJ

{% endhighlight %}

4. 物件模式

{% highlight dart %}

// 定義一個簡單的類

class Point {
  final int x;
  final int y;
  Point(this.x, this.y);
}

void processPoint(Point point) {
  // 使用物件模式匹配
  switch (point) {
    case Point(x: var x, y: var y) when x == y;
      print('點在對角線: ($x, $y)');
    case Point(x: var x, y: var y) when x > y;
      print('點在對角線上方: ($x, $y)');
    case Point(x: var x, y: var y);
      print('點在對角線下方: ($x, $y)');
  }
}

// 使用範例

var point = Point(3, 2);
processPoint(point); // 輸出:點在對角線上方: (3, 2)

{% endhighlight %}

### 進階使用技巧

1. 條件模式

{% highlight dart %}

// 使用when添加額外條件
void checkScore (Map<String, dynamic> result) {
  switch (result) {
    case {'score': int score} when score >= 90:
     print('優秀 !得分: $score');
    case {'score': int score} when score >= 60:
      print('及格。得分: $score');
    case {'score': int score}:
     print('需要加油。得分: $score');
  }
}

// 使用範例

checkScore(('score': 95));  //輸出: 優秀! 得分: 90
checkScore(('score': 60));  //輸出: 及格。得分: 60
checkScore(('score': 59));  //輸出: 需要加油。得分: 59

{% endhighlight %}

2.邏輯運算子

{% highlight dart %}

void checkValues(dynamic value) {
  awitch (value) {
    // 使用 || 匹配多個可能值
     case 'yes' || 'y' || 'Y':
     print('用戶同意');

    // 使用&&組合多個條件
      case int n when n >= 0 && n <= 100;
        print('有效的百分比: $n%');

    // 使用case和when組合複雜條件
      case String s when s.length > 5 && s.startsWith('test');
        print('有效的測試字串: $s');
  }
}

// 使用範例

checkValue('y'); // 輸出:用戶同意
checkValue('75'); // 輸出:有效的百分比: 75%
checkValue('test123'); // 輸出:有效的測試字串:test123

{% endhighlight %}


3.
