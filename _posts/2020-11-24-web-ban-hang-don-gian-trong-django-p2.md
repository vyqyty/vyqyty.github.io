---
title: Web bán hàng trong Django Phần 2
date: 2020-11-24
categories: [Django]
tags: [Other]
math: true
---

## 5. Viết giao diện sản phẩm
Bắt đầu đụng đến phần "View" trong mô hình MVC thôi :D.

**ecom/views.py**
```
# -*- coding: utf-8 -*-
from __future__ import unicode_literals

from django.http import Http404
from django.shortcuts import render
from .models import Type, Product

# Create your views here.
def index(request):
    type_objs = Type.objects.filter(active__exact=True)
    context = {
        'type_objs': type_objs,
    }
    return render(request, "ecom/type.html", context)
    
def product(request, product_id):
    try:
        product = Product.objects.get(id=product_id)
    except Product.DoesNotExist:
        raise Http404("Product does not exist")
    return render(request, 'ecom/product.html', {'product': product})
    
```

* Trang chủ sẽ show toàn bộ loại sản phẩm và sử dụng template "ecom/type.html".
* Trang sản phẩm (chi tiết) sẽ show thông tin chi tiết của sản phẩm và sử dụng template "ecom/product.html".

OK, vậy ta tiếp tục tạo 2 template html tương ứng:

* django_ecom/ecom/templates/ecom/type.html
* django_ecom/ecom/templates/ecom/product.html

![Alt text](https://vyqyty.github.io/assets/img/uploads/2020/09/django_ecom_3_templates.png)

Chôm template html có sẵn ở đâu đó (hoặc tự viết :v) rồi nhét 1 số đoạn code render thông tin sản phẩm (type / product) vào là được.

**type.html**

{@github: https://github.com/vyqyty/vyqyty.github.io/blob/master/assets/ecom-django-html-1.md}
