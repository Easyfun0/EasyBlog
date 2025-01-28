---
layout: post
title:  Ruby initialize
date:   2024-02-20
author: Easyfun
categories: Ruby
featured-img: cloud
---

### 實體初始化

#### self呼叫相同實體上的其他方法

當需要在相同物件的initialize方法中，呼叫name=和salary=等屬性寫入器方法。讓我們得以在設定@name和@salary等實體變數前，執行寫入器方法的驗證碼。但這樣會無法運作:

    def initialize(name = "Anonymous", salary = 0.0)
      name =  name
      salary = salary
    end
    
    # @name和@salary的值會是nil



