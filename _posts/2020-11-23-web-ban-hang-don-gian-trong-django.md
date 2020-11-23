---
title: Web bán hàng trong Django
date: 2020-11-23
categories: [Django]
tags: [Other]
math: true
---
## 1. Tạo project
Tạo project django_ecom
```
django-admin startproject django_ecom
```
![Alt text](https://vyqyty.github.io/assets/img/uploads/2020/09/django_ecom_0_create_project.png)

Có 1 số file quan trọng cần chú ý:

* **settings.py**

    * DEBUG: bật / tắt chế độ Debug.
    * ALLOWED_HOSTS: nếu báo lỗi liên quan đến ALLOWED_HOSTS thì thêm địa chỉ vào list này.
    * INSTALLED_APPS: 1 project có thể có nhiều app, còn 1 app có thể thuộc nhiều project. Khi mình thêm 1 app mới thì cần cập nhật danh sách này.
    * DATABASES: đặc tả Database Engine mình muốn dùng: SQLite (mặc định), Postgres, Mysql, …

* **urls.py**
 
    * Đóng vai trò routing, đặc tả với địa chỉ nào thì sẽ thực thi hàm nào ở backend.

* **manage.py**
 
    * Đóng vai trò giống như 1 CLI để tạo app, migrate kiến trúc database, …

Không cần sửa file nào hết, chạy thử server trên local xem sao bằng 2 lệnh (nhớ cd vào thư mục django_ecom đã nhé):
```
$ python manage.py migrate
$ python manage.py runserver
```
## 2. Tạo App
Tạo app tên ecom
```
python manage.py startapp ecom
```
OK, 1 thư mục ecom vừa mới được tạo ra.

![Alt text](https://vyqyty.github.io/assets/img/uploads/2020/09/django_ecom_1_create_app_ecom.png)

Thêm app vừa tạo vào django_ecom/settings.py
```
INSTALLED_APPS = [
    'ecom.apps.EcomConfig',
    #... config còn lại giữa nguyên.
]
```
## 3. Thiết kế và tạo model

Django hỗ trợ ORM (Object-relational mapping), nói 1 cách dễ hiểu, là 1 class hướng đối tượng sẽ được map thành 1 bảng trong database, 1 object / instance (thực thể của 1 class) sẽ được map thành 1 record (1 dòng) của bảng trong database.

Lợi ích của ORM:

* Tránh viết các câu lệnh truy vấn SQL dài dòng.
* Code cực kì gọn, đẹp, dễ sử dụng và dễ hiểu.

Ta sẽ thiết kế 1 model đơn giản có:

* Type model gồm có 2 fields:
   * Name: tên loại sản phẩm.
   * Active: nếu type không active sẽ không được show ra.
* Product model bao gồm các thông tin cơ bản:
   * Type ID: khóa ngoại đến Type (Many2one).
   * Name: tên sản phẩm.
   * Price: giá cả.
   * Quantity: số lượng sản phẩm.
   * Image: ảnh sản phẩm (1 ảnh).
   * Description: mô tả sản phẩm (nhiều dòng).
   
**ecom/models.py**
```
# -*- coding: utf-8 -*-
from __future__ import unicode_literals

from django.db import models
from django.conf import settings
import django.utils.safestring as safestring

# Create your models here.
class Type(models.Model):
    name = models.CharField(max_length=200)
    active = models.BooleanField("Is Active", default=True)
    
    def __str__(self):
        return self.name


class Product(models.Model):
    type_id = models.ForeignKey(Type, on_delete=models.CASCADE)
    name = models.CharField("Product Name", max_length=200)
    price = models.IntegerField("Price", default=0)
    quantity = models.IntegerField("Quantity", default=0)
    image = models.ImageField(upload_to='uploads/%Y/%m/%d/')
    description = models.TextField("Description")
    
    def image_tag(self):
        if self.image:
            return safestring.mark_safe('<img src="%s%s" width="150" height="150" />' % (settings.MEDIA_URL, self.image))
        else:
            return ""

    image_tag.short_description = 'Image'
    image_tag.allow_tags = True
    
    def __str__(self):
        return self.name
```

Vì mình cho phép người dùng up ảnh sản phẩm và hiển thị ra, do đó phải chỉnh sửa settings 1 chút.

**django_ecom/settings.py**

```
MEDIA_URL = '/media/'
MEDIA_ROOT = (
    os.path.join(BASE_DIR)
)
```

Đồng thời ta phải chỉnh lại urls

**django_ecom/urls.py**

```
from django.conf.urls import url
from django.contrib import admin
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    url(r'^admin/', admin.site.urls),
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

Tiến hành migrate database thôi :v

```
$ python manage.py makemigrations ecom
# sau khi chạy sẽ tao ra file: ecom/migrations/0001_initial.py
# nếu ta chỉnh sửa cấu trúc của database thì lần makemigrations tới sẽ tạo ra file dạng: 0002_....py

$ python manage.py sqlmigrate ecom 0001
# 0001 chính là phần prefix của file: 0001_initial.py
# Lần tiếp theo thì ta cần sqlmigrate 0002 (tăng dần)

$ python manage.py migrate
# apply toàn bộ thay đổi vào web

# Hoặc ta dùng 1 câu lệnh duy nhất:
$ python manage.py makemigrations <app_name> && python manage.py migrate
ví dụ:
$ python manage.py makemigrations ecom && python manage.py migrate
```

Lưu ý:

* ecom: tên app <=> app_name
* 0001: version cấu trúc mình muốn migrate (tăng dần)
**Quan trọng**: ta phải đăng ký các model vừa tạo cho Admin Site biết, như vậy khi ta vào giao diện quản lý sẽ thấy được các model này để thao tác (thêm, sửa, xóa).

**ecom/admin.py**
```
# -*- coding: utf-8 -*-
from __future__ import unicode_literals

from django.contrib import admin
from .models import Type, Product

class TypeModelAdmin(admin.ModelAdmin):
    list_filter = ('active',)
    list_display = ('name', 'active', )

class ProductModelAdmin(admin.ModelAdmin):
    readonly_fields = ('image_tag',)    
    list_display = ('name', 'price', 'quantity', 'description')

admin.site.register(Type, TypeModelAdmin)
admin.site.register(Product, ProductModelAdmin)
```

Với đoạn code trên ta cũng đã customize lại ModelAdmin mặc định:

* Cho phép lọc theo field active trong list view của "Type".
* Hiển thị 2 cột "name" và "active" của "Type".
* Hiển thị ảnh từ file ảnh do người dùng upload là readonly.
* Hiển thị 4 cột "name", "price", "quantity", "description" của "Product"

Mình cùng qua bước tiếp theo để xem thành quả nhé!

## 4. Vào giao diện Admin xem model vừa tạo
```
python manage.py createsuperuser

# tạo tài khoản admin, các bạn có thể điền tùy thích. Lưu ý là thông tin password không được giống / gần giống Username và Email. Nếu không nó sẽ không cho tạo :v.
Username (leave blank to use 'ubuntu'): admin
Email address: admin@admin.com
Password: djangoecom
Password (again): djangoecom
```
Sau đó vào localhost:8000/admin đăng nhập bằng account vừa tạo.

Ố lala, ta có giao diện có thể thêm, sửa, xóa loại và sản phẩm.

![Alt text](https://vyqyty.github.io/assets/img/uploads/2020/09/django_ecom_2_type_model.png)

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

```
<!DOCTYPE html>
<html lang="vi">
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
                        <p>
                        <div class="row post-grid">
                            {% for product in type.product_set.all %}
                                {% if product.quantity > 0 %}
                                <div class="col-sm-4">
                                    <div class="row">
                                        <div class="col-xs-12">
                                            <a href="{% url 'product' product.id %}"><img src="/media/{{ product.image }}" /></a>
                                        </div>
                                    </div>
                                    <p>
                                        <p>
                                        <span><i class="fa fa-dollar" aria-hidden="true"></i>&nbsp; {{product.price}}</span>
                                        &nbsp; &nbsp; 
                                        <span><i class="fa fa-cart-plus" aria-hidden="true"></i>&nbsp; {{product.quantity}}</span>
                                        <a href="{% url 'product' product.id %}"><h4>{{ product.name }}</h4>        </a>    
                                    </p>
                                </div>
                                {% endif %}
                            {% endfor %}
                        </div>
                    </div>        
            {% endfor %}
            </div>
        </div>
        </div>
    </<body>
</html>
```
```
<!DOCTYPE html>
<html lang="vi">
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
        <div class="col-sm-8">
            <div class="row">
                <div class="col-xs-6">
                    <a href="{% url 'product' product.id %}"><img src="/media/{{ product.image }}" /></a>
                </div>
                <div class="col-xs-3">
                    <b>Product Name</b><br/>
                    <b>Price</b><br/>
                    <b>Quantity</b><br/>
                    <b>Description</b><br/>
                </div>
                <div class="col-xs-3">
                    {{product.name}}<br/>
                    ${{product.price}}<br/>
                    {{product.quantity}}<br/>
                    {{product.description}}<br/>
                </div>
            </div>
        </div>
        <div class="col-sm-4">
        </div>
        </div>
    </<body>
</html>
```

Mình sẽ dựa vào cú pháp Template của Django để viết các file template trên (chỗ lặp các object bằng for ... in ).

**urls.py**

```
from django.conf.urls import url
from django.contrib import admin
from django.conf import settings
from django.conf.urls.static import static

from ecom import views

urlpatterns = [
    url(r'^$', views.index, name='index'),
    url(r'^admin/', admin.site.urls),
    url(r'^product/(?P<product_id>[0-9]+)/$', views.product, name='product'),
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

* from ecom import views: import views.py của app ecom.
* Đặc tả trang chủ: '/' sẽ gọi hàm index() trong views.
* Đặc tả trang chi tiết sản phẩm: '/product/product_id' sẽ gọi hàm product() trong views.

Cuối cùng ta sẽ có giao diện web bán hàng khá chuẩn :D.

**localhost:8000**
![Alt text](https://vyqyty.github.io/assets/img/uploads/2020/09/django_ecom_4_web_1.png)
![Alt text](https://vyqyty.github.io/assets/img/uploads/2020/09/django_ecom_5_web_2.png)

Như vậy chúng ta đã kết thúc 1 ngày học Django viết bằng Python rồi đó. Có vẻ như mọi thứ khá ổn để ta bắt tay vào viết những trang web lớn hơn.

Tổng kết lại, điểm "ngon" của Django:

* ORM.
* Mô hình MVC phân chia khá rõ ràng.
* Vô số tài liệu hướng dẫn từ Django.
* Template khá mạnh, gần giống với ngôn ngữ markdown (rất phổ biến).
* Django Admin cung cấp sẵn các chức năng thêm, sửa, xóa ở CMS (có thể customize).

nguồn https://minhng.info/tutorials/hoc-django-trong-1-ngay.html
