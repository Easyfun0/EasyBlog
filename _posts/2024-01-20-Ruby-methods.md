
---
layout: post
title:  "Ruby"
date:   2024-01-16
author: Easyfun
categories: Ruby
tags: [documentation,sample]
image: railway.png
---

### Ruby的方法和類別

使用Ruby來建立類別(class)-新物件的模板。

使用實體變數(instanec variable)來定義物件，以及使用實體方法(instance method)來定義物件能做的事。

#### 定義方法

在Ruby中，定義方法方式:

{% highlight ruby %}

def print_sum(arg1, arg2)
  print arg1 + arg2
end

{% endhighlight %}

要呼叫包含引數的方法，將需要為方法定義加入參數(parameter)。參數將會出現在方法名稱之後的圓括號裡(如果沒有參數，則應該省略圓括號)，方法呼叫上的每個引數將會被存入方法定義中相對應的參數。

{% highlight ruby %}

def hello
  puts "Hello"
end

def bye
  puts "bye"
end

{% endhighlight %}

也可以把方法參數先寫出來

{% highlight ruby %}

def hello(Mike)
  puts "Hello #{Mike}"
end

{% endhighlight %}

#### 呼叫所定義的方法

{% highlight ruby %}

def hello(Mike)
  puts "Hello #{Mike}"
end

hello

{% endhighlight %}

跟JS一樣直接呼叫方法名稱即可。

#### 方法名稱

方法名稱可以是一或多個小寫單字，單字間以底線符號隔開。

名稱以問號(?)或驚嘆號(!)結尾的方法也是有效的，甚至是等號(=)結尾也是可行。

#### 參數

如果需要把資料傳入你的方法，可以在方法名稱之後加上一或多個參數，參數之間以逗號隔開。在方法本體中可以把參數當成變數來存取。

{% highlight ruby %}

def print_sum(length, width)
  print length * width
end

{% endhighlight %}

#### 可選參數

參數變成可選用(make the parameter optional)可以在方法宣告中提供預設值。

{% highlight ruby %}

def order_drink(flavor, size = "medium", quantity = 1)
  if quantity == 1
    plural = "cola"
  else
    plural = "colas"
  end
  puts "#{quantity} #{size} #{flavor} #{plural}, here u are"
end

{% endhighlight %}

要是想要改變預設值，只要在引數指定你要的值就行了，如果對預設值感到滿意也可跳過該引數。

{% highlight ruby %}

order_drink("orange")
order_drink("soda", "small", 2)
order_drink("apple", "large")

{% endhighlight %}

可選參數必須出現在你打算賦值的任何其他參數之後，如果把需要賦值的參數擺到可選參數後，將無法省略可選參數。

{% highlight ruby %}

def order_drink(flavor, size = "medium", quantity)
  ....
end
order_dring("apple")

{% endhighlight %}

可以在可選參數宣告時賦值

{% highlight ruby %}

def for_drink( drink = "cola")
  puts "I like #{drink} for lunch"
  puts "It's good!!"
end
#不用再為drink賦值。

for_drink
for_drink("coffee")

{% endhighlight %}

#### 回傳值

Ruby的回傳值(return value)，就是「方法」回傳給「方法呼叫者」的值，使用return關鍵字，方法可以把一個值回傳給他的呼叫者。


{% highlight ruby %}

def mileage(miles_driven, gas_used)
  return miles_driven / gas_used
end

#可以用同一個方法來計算

trip_mileage = mileage(400, 12)

puts "I got #{trip_mile}"

lifetime_mileage = mileage(11432, 366)
puts "This car averages #{lifetime_mileage}"

{% endhighlight %}

#### 隱式回傳值

回傳值的方法，也可以不用使用return。在一個方法中，最後一個運算式的求值結果會自動成為該方法的回傳值。所以mileage可以被改寫成不使用return。

#### 提早從方法返回

return會導致方法結束執行，因此在其後的程式碼將不會被執行。

假如我這邊給的值是(0, 0)的話，任何值除以0會產生錯誤。

所以可以先測試值是否為0，來解決此問題;如果值為0，方法就提早返回。

{% highlight ruby %}

def mileage(miles_driven, gas_used)
  if gas_used == 0
    return 0.0
  end
  miles_driven / gas_used
end

{% endhighlight %}

#### 設計一個類別

使用物件的好處是，物件會把一組資料以及運算這些資料的方法擺在同一個地方。

建立物件前，需要先定義類別，類別是建立物件的藍圖，使用一個類別來建立物件，類別描述了該物件所知道的事，以及所能做的工作。

![alt text]({{ site.baseurl }}/assets/img/class.png "Profile Picture"){:.profile}

🐠 一個物件所知道的事情，稱為:實體變數

🐠 一個物件所能做的方法，稱為:實體方法

類別的一個實體(instance)就是使用該類別所建立的一個物件，你只需要攥寫一個類別，但你可以使用該類別建立許多實體。

實體(instance)是物件(object)的另一種說法。

實體變數(instance variable)就是屬一個物件的變數。實體變數組成了該物件所知道的事情。代表了物件的狀態(資料)，就類別的每一個實體而言，可以具有不同的值。

實體方法(instance method)就是一個物件可供直接呼叫的方法，實體方法組成了該物件所能做的工作。可以存取物件的實體變數，以及根據這些變數的值來改變他們的行為。

#### 類別與物件有何區別

類別是物件的藍圖，會告訴Ruby如何建立特定資料型態的物件，物件具有實體變數和實體方法，但變數和方法是類別的一部分。

**若類別是餅乾模型，那麼物件就是由它所做成的餅乾。**

就類別的方法中所用到的實體變數而言，類別的每一個實體可以具有自己的值。舉例:只會定義Dog類別一次，在Dog類別的方法中，將會指定Dog實體一次，而Dog實體應該具有name和age等實體變數。但是每個Dog物件將會有自己的名字(name)和年齡(age)，不同於其他的Dog實體。

![alt text]({{ site.baseurl }}/assets/img/class_dog.png "Profile Picture"){:.profile}


這是一個Dog類別:

{% highlight ruby %}

class Dog

  def talk
    puts "woo"
  end 

  def move(destination)
    puts "Running to #{destination}"
  end

end
{% endhighlight %}

先使用class關鍵字來一個新類別的定義，後面跟著我們的新類別的名稱。

在類別的定義中，可以包含方法的定義，我們在此處所定義的任何方法將會成為類別之實體上的實體方法。

最後在用end關鍵字來結束類別的定義。

#### 建立新的實體(物件)

如果我們呼叫一個類別的new方法，他將會傳回此類別的一個新實體，接著我們可以把該實體賦值給一個變數，或是對他進行我們需要做的事。

    fido = Dog.new
    rex = Dog.new

我們擁有了類別的一或多個實體，我們就可以呼叫他們的實體方法。我們是以相同的方式來呼叫物件的任何方法:我們會用點號為「方法的接收者」只應一個實體。

    fido.talk
    rex.move("food good")



#### 使用物件導向的做法

可以採取物件導向的做法解決問題，不再需要建立一個大型的方法來包含所有類型;可以透過類別來表示每一種類型的東西，在為每一個類別放入小型的方法，其中定義了該東西類型持有的行為。

{% highlight ruby %}

class Bird

  def talk
    puts "choo"
  end 

  def move(destination)
    puts "Flying to #{destination}"
  end

end

class Cat

  def talk
    puts "mew"
  end 

  def move(destination)
    puts "Running to #{destination}"
  end

end

class Dog

  def talk
    puts "woo"
  end 

  def move(destination)
    puts "Running to #{destination}"
  end

end
{% endhighlight %}

#### 為新的類別建立實體

定義好類別後，可以為它建立新的實體(以類別為基礎的新物件)以及呼叫他們的方法。

在Ruby中，用於為類別建立實體的程式碼與用於宣告類別的程式碼可以存在於同一個檔案中，在較大型的應用程式中，可能不會想以這方式來組織，但在簡單的開發可以把建立實體的程式碼放在類別宣告的下面。

{% highlight ruby %}

class Bird

  def talk
    puts "choo"
  end 

  def move(destination)
    puts "Flying to #{destination}"
  end

end

class Cat

  def talk
    puts "mew"
  end 

  def move(destination)
    puts "Running to #{destination}"
  end

end

class Dog

  def talk
    puts "woo"
  end 

  def move(destination)
    puts "Running to #{destination}"
  end

end

bird = Bird.new
dog = Dog.new
cat = Cat.new
#為我們的類別建立新的實體


bird.move("Cage")
dog.talk
bird.talk
cat.move("house")
#呼叫實體的方法

{% endhighlight %}

![alt text]({{ site.baseurl }}/assets/img/class_group.png "Profile Picture"){:.profile}

以上圖為例，類別的實體具有兩個實體方法:talk和move。

我們可以把name參數加入talk和move方法。


    dog = Dog.new
    dog_name = "Mike"
    cat = Cat.new
    cat_name = "Phil"

使用實體變數來保存物件裡的資料。這是物件導向設計的好處，把資料和處理資料的方法放在同一個地方，這樣就不用傳遞那麼多引數給我們的實體方法。


#### 區域變數存活到方法結束為止

區域變數(local variable)，是有效範圍被侷限在當前作用域的變數，只要當前作用域結束，區域變數便不復存在。

{% highlight ruby %}

class Dog

  def make_up_name
    name = "Mike"
  end 

  def talk
    puts "#{name} says Bark"
  end

end

dog = Dog.new
dog.make_up_name
dog.talk

{% endhighlight %}

以此範例，這Dog類別他具有一個額外的方法，make_up_name。當我們呼叫他會保存名字，以稍後供talk方法取用。

但要事先呼叫talk，這邊就會報錯，指出name變數並不存在。

雖然上面已經定義過name變數，但是在不同的區域(local)變數，區域變數的有效範圍侷限在建立他們的方法中，上面雖然有定義過但是他方法結束name便離開了作用域，name變數便不存在。

#### 只要實體存在實體變數就存在

物件可以把資料存入實體變數(instance varaibale);被繫結到物件實體的變數。被寫入實體變數的資料，與物件共存，只有當物件被移除，資料才會從記憶體中移除。

實體變數看起來像一個普通變數，且依循相同的命名慣例。語法上的差別是，他的開頭多了一個@符號。

:::info
my_variable 區域變數
:::

:::warning
@my_variable 實體變數
:::

上面範例改用實體變數，這樣呼叫talk方法就不會錯誤了。

{% highlight ruby %}

class Dog

  def make_up_name
    @name = "Mike"
  end 

  def talk
    puts "#{@name} says Bark"
  end

end

dog = Dog.new
dog.make_up_name
dog.talk

{% endhighlight %}

#### 封裝

現在我們可以使用實體變數來保存名字和年齡，但是方法只允許使用固定的值(當程式執行時，無法改變他們)

Ruby不允許我們從類別的外面直接存取實體變數，是為了防止其他程式和類別隨意修改你的實體變數。

#### 屬性存取器方法

可以建立存取器方法(accessor method)，他會為你把值寫入實體變數以及從實體變數把值讀回來。一但透過存取器方法來存取你的資料，就能擴充這些方法，讓他們來驗證你的資料拒絕任何錯誤的值。

Ruby具有兩種存取器方法: **屬性寫入器**(attriute writer)以及**屬性閱讀器**(attribute reader)。

{% highlight ruby %}

class MyClass

  def my_attribute = (new_value)
    @my_attribute = new_value
  end

  def my_attribute
    @my_attribute
  end

end

{% endhighlight %}


「屬性」是關於物件的一段資料，屬性寫入器方法可以設定實體變數，而屬性閱讀器方法則可以取回實體變數的值。

屬性閱讀器方法便是一個例子，可用於回傳@my_attribute的當前值。

如同「閱讀器」(reader)方法，屬性「寫入器」(writer)方法也是一個普通的方法，之所以稱作(attribute)方法，他的主要用途是更新實體變數的值。

    my_instance.my_attribute = "a value"

也可以用=號的方法做為屬性寫入器，**my_instance**是呼叫方法，**("a value")**是方法的引數。

#### 使用存取器方法

來更新Dog類別的方法，讓我們能夠讀取和寫入@name和@age等實體變數。

{% highlight ruby %}

class Dog

  def name = (new_value)
    @name = new_value
  end 

  def name
    @name
  end

  def age = (new_value)
    @age = new_value
  end

  def age
    @age
  end

  def report_age
    puts "#{name} is #{@age} years old"
  end

  fido = Dog.new
  fido.name = "Mike"
  fido.age = 2
  rex = Dog.new
  rex.name = "Phil"
  rex.age = 3
  fido.report_age
  rex.report_age
  
end

{% endhighlight %}

這樣可以從Dog類別之外(間接)設定和使用@name和@age等實體變數。

因為常需要為屬性建立這兩個存取器方法，Ruby提供了簡寫-attr_writer、attr_reader和attr_accessor。在類別定義中呼叫這三個做法，將會自動為你定義新的存取器方法:

![alt text]({{ site.baseurl }}/assets/img/attr.png "Profile Picture"){:.profile}

這三個方法都可以指定多個引數，想要定義的存取器不只一個，可以指定多個引數。

用這方法來改寫上面範例:

{% highlight ruby %}

class Dog

  attr_accessor :name, :age

  def report_age
    puts "#{name} is #{@age} years old"
  end
  
end

{% endhighlight %}


#### 符號

Ruby符號(symbol)由一串字符所構成，如同一個字串。:name和:age都是符號，與字串不同的是，符號的值不能改變，讓符號在Ruby中適合用於參用(refer to)名稱不會改變任何東西。

#### raise方法

使用raise方法時，if述句就不用else來接。如果所傳入的是無效值，raise述句會被執行，程式會終止。

{% highlight ruby %}

class Dog

  attr_accessor :name, :age

  def name = (value)
    if value == ""
      raise "Name is back"
    end
    @name = value
  end

{% endhighlight %}

