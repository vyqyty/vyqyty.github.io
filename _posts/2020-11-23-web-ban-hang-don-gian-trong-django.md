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
