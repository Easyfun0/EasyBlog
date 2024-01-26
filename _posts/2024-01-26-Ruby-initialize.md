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


