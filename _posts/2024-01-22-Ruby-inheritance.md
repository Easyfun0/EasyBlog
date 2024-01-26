---
layout: post
title:  Ruby inheritance
date:   2024-01-22
author: Easyfun
categories: Ruby
featured-img: sunset
---

## 繼承

Ruby也跟其他物件導向一樣，有著繼承(inheritance)的概念，可以讓類別從另一個類別繼承方法。

繼承可把常用的方法移往單一類別，而不必在多個類似的類別中重複定義方法，可以讓其他類別繼承該類別。具有常用方法的類別稱為超類別(superclass)或稱為父類別，繼承這些方法的類別稱為子類別(subclass)。

![alt text]({{ site.baseurl }}/assets/img/inher.png "Profile Picture"){:.profile}

這邊有Car,Truck,Motocycle等類別具有若干共同的實體方法和屬性，每個類別用於代表一種類型的種類。這邊建立一個新的類別，將該類別取名為Vehicle，並把用的方法和屬性移往該處。這樣Vehicle類別稱為三個類別的父類別。而Car,Truck,Motocycle則稱為Vehicle的子類別。

在Ruby中，子類別不會繼承實體變數;他們所繼承的是用於建立這些變數的屬性存取器方法(attribute accessor method)。

#### 定義父類別

為了消除Car,Truck.Motorcycle等類別中重複的方法，把共享的方法和屬性移往Vehicle類別。Car,Truck.Motorcycle皆為Vehicle的子類別，繼承了Vehicle的方法。

{% highlight ruby %}

class Vehicle

  attr_accessor :odometer
  attr_accessor :gas_used

  def accelerate
    puts "Floor"
  end

  def sound_horn
    puts "Beep"
  end

  def strre 
    puts "Turn"
  end

  def mileage
    return @odometer / @gas_used
  end

end

{% endhighlight %}

#### 定義子類別

子類別定義就像一般類別的定義。

Ruby使用小於(<)符號是因為子類別是父類別的一個子集合。

    class Car < Vehicle
    end

    class Truck < Vehicle
    end

    class Motorcycle < Vehicle
    end

只要把Car,Truck,Motorcycle定義成子類別，他們就會繼承Vehicle的所有屬性和實體方法。即使子類別本身不包含任何程式碼，所建立的任何實體將可獲得父類別的所有功能。

    truck = Truck.new
    truck.accelerate
    truck.steer

    car = Car.new
    car.odometer = 11432
    car.gas_used = 366

    puts "HIII"
    puts car.mileage

現在Car,Truck,Motorcycle類別皆具有相同的功能，但沒有重複的程式碼。

#### 添加方法到子類別

現在要添加新的方法，但避免影響到他類別，所以不能更改到父類別，所以要把新的屬性定義在要加的子類別上。

{% highlight ruby %}

class Truck < Vehicle

  attr_accessor :cargo

  def load_bed(contents)
    puts "Securing #{contents} in the truck"
    @cargo = contents
  end

end

{% endhighlight %}

我們可以建立新的實體，然後承載和存取。

    truck = Truck.new
    truck.load_bed("259")
    puts "The truck is carrying #{truck.cargo}"

#### 實體變數屬於物件，非類別

定義於父類別的實體變數會由子類別所繼承

![alt text]({{ site.baseurl }}/assets/img/veh.png "Profile Picture"){:.profile}

Car會從Vehicle繼承@odometer和@gas_used等實體變數。所有的Ruby皆具有名為instance_variables的方法，對物件呼叫該方法，能看到物件具有哪些實體變數。

    car = Car.new
    puts "car.instance_variables"

這樣輸出會沒有輸出，是因為car尚未具有任何實體變數，等到物件的實體方法，才會在物件上建立實體變數。這邊呼叫odometer和gas_used等屬性寫入器方法:

    car.odometer = 22914
    car.gas_used = 728
    puts car.instance_variables

所以Car類別不會繼承@odometer和@gas_used等實體變數...而是繼承ometer= 和gas_used= 等實體方法，並使用這些方法來建立實體變數。

假設有一個不符合規定的父類別，他使用@storage實體變數來為他的name=和name存取器方法保存值，有一個子類別使用相同的變數名稱，@storage來為他的salary=和salary 存取器方法保存值。

{% highlight ruby %}

class Person

  def name = (new_value)
    @storage = new_value
  end

  def name 
    @storage
  end
end

class Employee < Person

  def salary = (new_value)
    @storage = new_value
  end

  def salary
    @storage
  end

end

{% endhighlight %}

當我們實際使用Employee子類別的時候，只要我們對salary屬性賦值，就會覆寫name屬性，因為他們使用了相同的實體變數。

    employee = Employee.new
    employee.name = "Easy fun"
    employee.salary = 89000
    puts employee.name

確保總是使用與你的屬性存取器名稱一致的合理變數名稱。

#### 覆寫方法

如果父類別的行為並非子類別需要的，繼承功能為你提供了另一個有用的機制:方法覆寫(override)。這個機制讓你得以使用子類別專用的方法來取代從父類別繼承來的方法。

{% highlight ruby %}

class Motorcycle < Vehicle

  def steer
    puts "Turn right"
  end

end

{% endhighlight %}

我們呼叫一個Motorcycle實體的steer方法，所用到的是經過覆寫的方法，我們所用到的是Motorcycle類別中所定義的steer方法，而非從Vehicle繼承來的方法。

但我們呼叫一個Motocycle實體的任何其他方法，所用到的是繼承來的方法。

    motorcycle.accelerate

如果Ruby看到呼叫端所要求的方法定義於子類別，他將會呼叫該方法並停在該處。

但如果沒有在子類別找到該方法，Ruby將會到父類別中尋找該方法，然後再到父類別的父類別中...以此類推，沿著繼承鏈往上尋找。

![alt text]({{ site.baseurl }}/assets/img/over.png "Profile Picture"){:.profile}

如果需要改程式，可以在Vehicle類別中進行，所做的改變會自動傳播到子類別;就是每個子類別都會得到更新的好處。如果一個子類別需要特殊的行為，直接覆寫從父類別繼承來的方法就可。

#### super關鍵字

使用super關鍵字時會導致父類別中同名被呼叫。

{% highlight ruby %}

class Person

  def greeting
    puts "Hello"
  end

end

class Friend < Person

  def greeting
    super
    puts "Nice to meet u"
  end

Friend.new.greeting

end

{% endhighlight %}

我們呼叫子類別上這個進行複寫的方法，將看到super關鍵字如同在呼叫父類別上遭覆寫的方法。

super關鍵字就是一個普通的方法呼叫。

{% highlight ruby %}

class Person

  def greeting
    puts "Hello"
  end

end

class Friend < Person

  def greeting
    basic_greeting = super
    "#{basic_greeting} Nice to meet u"
  end

end

puts Friend.new.greeting

{% endhighlight %}

super也可以傳引數給他，而這些引數將會傳給父類別的方法。

{% highlight ruby %}

class Person

  def greeting_by_name(name)
    "Hello, #{name}!"
  end

end

class Friend < Person

  def greeting_by_name(name)
    basic_greeting = super(name)
    "#{basic_greeting} Nice to meet u"
  end

end

puts Friend.new.greeting_by_name("Easy")

{% endhighlight %}

super不同於一般的方法呼叫:如果未傳遞引述給他，Ruby會自動把你傳遞給子類別方法的引數拿來呼叫父類別方法。

{% highlight ruby %}

class Person

  def greeting_by_name(name)
    "Hello, #{name}!"
  end

end

class Friend < Person

  def greeting_by_name(name)
    basic_greeting = super
    "#{basic_greeting} Nice to meet u"
  end

end

puts Friend.new.greeting_by_name("Easy")

{% endhighlight %}

super與super()不一樣，super以進行覆寫的方法。super()是在呼叫遭覆寫的方法時未傳入引數，即使覆寫的方法有收到引數。

#### 使用super的子類別

可以把方法中重複的程式碼代換成呼叫super，以便利用父類別之方法所提供的功能。


{% highlight ruby %}

class Armadillo < Animal

  def move(destination)
    puts "#{@name} unrolls"
    super(destination)
  end

end

#或是

class Armadillo < Animal

  def move(destination)
    puts "#{@name} unrolls"
    super
  end
#自動傳遞，當被呼叫傳入的引數
end

dillon = Armadillo.new
dillon.name = "Easy"
dillon.move("burrow")

{% endhighlight %}

### Object類別

#### Ruby物件皆會繼承Object類別

如果沒有為所定義的類別指定父類別，Ruby會自動替該類別設置名為Object的父類別。

即使有為你的類別指定父類別，該父類別也可能繼承Object。幾乎每一個Ruby物件不是直接就是間接，以Object為父類別。

Ruby這樣是因為Object類別為幾乎所有的Ruby物件定義了所需要的許多有用方法:

🌏 to_s:把物件轉換成字串。

🌏 inspect: 把物件轉換成除錯字串。

🌏 class: 告訴你一個物件是哪一個類別的實體。

🌏 methods:告訴你一個物件具有哪些實體方法。

🌏 instance_variables:列出一個物件的實體變數清單。

Ruby物件從Object類別繼承了許多做為基礎工具方法。

#### 覆寫繼承來的方法

把Dog類別的父類別指定為Animal類別。因為沒有為Animal指定為父類別，Ruby會把Object類別指定為他的父類別。

要是Aniaml實體會從Object類別繼承to_s方法。Dog實體會從Animal繼承to_s。當把Dog物件傳遞給puts或print，他的to_s方法會被呼叫，以便把他轉換成一個字串。

{% highlight ruby %}

class Dog < Animal

  def to_s
    puts "#{@name} the dog, age #{@age}"
  end

end

mike = Dog.new
mike.name = "Easy"
mike.age = 4

phil = Dog.new
phil.name = "Rex"
phil.age = 2

puts mike.to_s, phil.to_s

{% endhighlight %}

甚至可以改成

    puts mike, phil


