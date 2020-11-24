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

```html\
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>Ecom</title>
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
        <link href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css" rel="stylesheet" integrity="sha384-wvfXpqpZZVQGK6TAh5PVlGOfQNHSoD2xbE+QkPxCAFlNEevoEH3Sl0sibVcOQVnN" crossorigin="anonymous">
        <link href="https://maxcdn.bootstrapcdn.com/bootswatch/3.3.7/cosmo/bootstrap.min.css" rel="stylesheet" integrity="sha384-h21C2fcDk/eFsW9sC9h0dhokq5pDinLNklTKoxIZRUn3+hvmgQSffLLQ4G4l2eEr" crossorigin="anonymous">
    </head>
    
    <script defer src="https://code.jquery.com/jquery-3.2.1.min.js" integrity="sha256-hwg4gsxgFZhOsEEamdOYGBf13FyQuiTwlAQgxVSNgt4=" crossorigin="anonymous"></script>
    <script defer src="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.7/js/bootstrap.min.js"></script>

    <body>
        
        <nav class="navbar navbar-default navbar-expand-sm" style="background-color: #212121;">
          <div class="container-fluid">
            <div class="navbar-header">
              <a class="navbar-brand" href="/">Django Ecom</a>
            </div>
            <div class="collapse navbar-collapse" id="navbar-items">
            <ul class="nav navbar-nav">   
            </ul>    
            <ul class="nav navbar-nav navbar-right">
                <li><span class="navbar-brand slogan">Welcome to Django</span></li>
                <li>
                      <form class="navbar-form navbar-left" role="search">
                        <div class="form-group">
                          <input type="text" class="form-control" placeholder="Search">
                        </div>
                        <button type="submit" class="btn btn-default">Submit</button>
                      </form>
                </li>
            </ul>
            </div>
          </div>
        </nav>
        
        <div class="container">
        <div id="categories-tab">
            <ul class="nav nav-tabs">
            {% for type in type_objs %}
                {% if forloop.first %}
                    <li class="h4 active">
                        <a id="tab-{{ type.name | slugify }}" href="#{{ type.name | slugify }}" data-toggle="tab" aria-expanded="true">
                            <i class="fa fa-folder-o" aria-hidden="true"></i> &nbsp;
                            {{ type.name }}
                        </a>
                    </li>
                {% else %}
                    <li class="h4">
                        <a id="tab-{{ type.name | slugify }}" href="#{{ type.name | slugify }}" data-toggle="tab" aria-expanded="false">
                            <i class="fa fa-folder-o" aria-hidden="true"></i> &nbsp;
                            {{ type.name }}
                        </a>
                    </li>
                {% endif %}        
            {% endfor %}                
            </ul>
            <div id="product-in-category" class="tab-content">
            {% for type in type_objs %}
                {% if forloop.first %}
                    <div class="tab-pane fade active in" id="{{ type.name | slugify }}">
                {% else %}
                    <div class="tab-pane fade" id="{{ type.name | slugify }}"> 
                {% endif %}                        
                    </div>        
            {% endfor %}
            </div>
        </div>
        </div>
    </<body>
</html>
```
