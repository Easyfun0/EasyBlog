---
layout: post
title:  Ruby initialize
date:   2024-01-26
author: Easyfun
categories: Ruby
featured-img: cloud
---

### 實體初始化

#### Ruby的Integer

我們對於Integer類別的實體進行運算，Ruby會向下捨入到最接近的整數

    50000/365*14

解果會是1904

會向下取整是因為Integer的實體無法儲存帶小數的數值，僅用於存取整數。

#### Ruby的Float運算

當一個Integer實體除以另一個Integer的結果。

    50000/365

結果是136，但應該是136.9863。我們可以透過讓數值包含小數點來達成。

    50000.0/365.0

會是136.986301369863

被除數與除數不必皆為Float;只要有一個運算元是Float，Ruby會回傳一個Float給你。

    50000.0/365

加法和乘法也是如此，但在除法要確保至少有一個運算元是Float。

#### 格式化

Ruby提供了格式化format方法。

例如要取到小數第二位，就會先格式化。

{% highlight ruby %}

result = format("%0.2f", 3.14159265)
puts result

{% endhighlight %}

format兩功能:

1. 格式序列

2. 格式序列寬度

#### 格式序列

format的第一個引數用於格式化輸出，大部分內容會以原樣出現在輸出裡，其中的%將被視為格式序列(format sequence)的開頭，其所構成的字串將會被特定格式的值所取代，其餘引數則是這些格式序列的值。

        puts format("the %s cost %i cents each","shirts", 23)
        puts format("That will be $%f please", 0.23 * 5)

#### 格式序列型態

百分比符號之後的字母用於指定我們所預期的各種型態的值，常見的有:

🌴 %s 字串 

🌴 %i 整數

🌴 %f 浮點小樹

#### 格式序列寬度

格式序列中，可以在百分比符號之後指定最小寬度，如果該格式序列之引數的寬度小於最小寬度，他將會被填充空格，直至達到最小寬度。

        puts format("%12s | %s", "Product", "Cost")
        puts "-" * 30

        puts format("%12s | %2i", "cola", 10)
        puts format("%12s | %2i", "tea", 14)
        puts format("%12s | %2i", "juice", 8)

整個數字的最小寬度包括小數。如果有指定，較短的數字將會被填充空格，直至達到此寬度，如果省略不會有任何空格被加入。

小數點之後的寬度是要顯示最大位數，如果所給定的是較精確的數字，他將會被(向下或向上)捨入到所指定的小數位數。

#### 浮點數的格式序列寬度

當我們在處理浮點數時，格式序列寬度讓我們得以指定小數點之前後之後所要顯示的位數。

寬度值的範例:

        def test_format(format_string)
            print "Testing '#{format_string}':"
            puts format(format_string, 12.3456)
        end

        test_format "%7.3f"
        test_format "%7.2f"
        test_format "%7.1f"
        test_format "%.1f"
        test_format "%.2f"

最後一個，"%.2f"可以把任何精準的浮點數捨入到小數第二位。

#### nil

Ruby具有一個特殊值，nil代表沒有，也就是沒有值，跟JS的null一樣。nil代表沒有並不是什麼都沒有，就像是在Ruby中任何其他東西一樣，是一個物件，並具有自己的類別。

確實有東西在，那為啥在輸出時會沒有看到呢？

因為來自NilClass的實體方法to_s總是傳回一個空字串。

#### "/"方法

大多數的數學運算符都被當作成方法，Ruby在看到這樣的運算式:

        6 + 2

會把它轉換成物件6之上一個名為+的方法，並以+右邊的物件作為引數。

儘管Integer和Float等類別有定義這些運算符方法，但NilClass卻沒有。

        puts nil./(365.0)

        // 錯誤: undefined method '/' for nil:NicClass

nill並未定義你在其他Ruby物件上所看到的大多數實體方法。

#### initialize方法

當我們呼叫類別之實體上的方法，存取他裡面的實體變數時，卻得到nil。

因為當建立一個實體的時候，該實體處在無效的狀態，除非對實體變數賦值，否則呼叫時會引發錯誤。所以當建立實體的時候要對他的方法賦值，就可以避免產生錯誤。

新物件被建立後，Ruby會呼叫該物件上的initialize方法。 

當新增initialize方法，他將會在任何其他實體呼叫之前為新的實體。


        def initialize
            @name = "Anonymous"
            @salary = 0.0
        end

#### initialize的引數

initialize方法現在會把@name的預設值設定為"Anonymous"以及把@salary的預設值設定為0。

傳遞給new方法的任何引數都會被傳遞給initialize。

        class MyClass
            def initialize(my_param)
                puts "Goy a parmeter from 'new': #{my_param}"
            end
        end

        MyClass.new("hello")

透過此功能，我們可以讓Employee.new的呼叫者為name和salary設定該有的初始值。我們只需要為initialize添加name和salary等參數，以及使用它們來設定@name和@salary等實體變數。

        def initialize(name, salary)
            @name = name
            @salary = salary
        end

可以經由Employee.new的引數來設定@name和@salary

        employee = Employee.new("Mike", 5000)
        employee.print_pay_stub

但是如果沒有傳遞任何引數給new，就沒有引數會被傳遞給initialize。要是呼叫Ruby方法的時候沒有提供正確數目的引數也會發生同樣的錯誤。

#### 為ininialize使用可選參數

如果我們以initialize方法來為實體變數設定預設值，就無法指定自己的值。

        def initialize
            @name = "Anonymous"
            @salary = 0.0
        end

如果不能為initialize添加參數，我們就必須為name和salary賦值，不能依靠預設值。

        def initialize(name, salary)
            @name = name
            #使用name參數來設定@name實體變數
            @salary = salary
            #使用salary參數來設定@salary實體變數
        end

initialize是一個普通方法，可以使用普通方法的功能。宣告參數時可以指定預設值，如果忽略參數，則會得到預設值，因此可以把那些參數賦值給實體變數。

        def initialize(name = "Anonymous", salary = 0.0)
            @name = name
            @salary = salary
        end

#### initialize驗證

屬性寫入器方法，name=，可以避免把空字串指定給employee:

        mike = Employee.new
        mike.name = ""

        錯誤:in `name`: Name can't be blank!

還可以確保不會為salary設定賦值:

        easy = Employee.new
        easy.salary = -2356

當initialize方法直接對@name和@salary等實體變數賦值，所以無效的資料可以藉此繞過驗證程序。

        employee = Employee.new("", -200)
        employee.print_pay
        #這樣印出來程式沒錯，但值是負值

