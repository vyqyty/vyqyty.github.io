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
OK, 1 thư mục ecom vừa mới được tạo ra :D.
![Alt text](https://vyqyty.github.io/assets/img/uploads/2020/09/django_ecom_1_create_app_ecom.png)
Thêm app vừa tạo vào django_ecom/settings.py
```
INSTALLED_APPS = [
    'ecom.apps.EcomConfig',
    #... config còn lại giữa nguyên.
]
```
## 3. Thiết kế và tạo model
