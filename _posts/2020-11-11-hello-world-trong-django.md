---
title: Hello world trong Django
date: 2020-11-11
categories: [Django]
tags: [Other]
math: true
---
Để tạo 1 app tên là home trong django ta chạy như sau:
python3.8 manage.py startapp home
Cấu trúc của app vừa tạo sẽ như thế này:
```
home/
├── admin.py
├── __init__.py
├── migrations
│   └── __init__.py
├── models.py
├── tests.py
└── views.py
```
Trong cấu trúc trên ta chỉ quan tâm nhiều nhất là models.py và views.py. Ngoài ra chúng ta cần tạo thêm 2 đối tượng quan trọng nữa là url config cho app và template.
Url config cho app sẽ nằm trong file urls.py:
```
touch urls.py
```
Template sẽ nằm trong folder template
```
mkdir templates
```
# Tạo 1 trang "hello world" trong Django

Để tạo 1 trang hello world trong django chúng ta cần các bước sau:
1. Template html chứa nội dung "hello world".
2. View dùng để render template
3. Url cho view

## Bước 1: Tạo template:
Vào thư mục gốc của dự án, sau đó:

```
vim home/templates/home/index.html
```
Với nội dung:

```
Hello world
```

Sau đó khai báo đường dẫn folder chứa template vừa mới khai báo bằng cách cập nhật file settings.py. Tìm đến phần TEMPLATES:

Sửa
```
...
 'DIRS': [],
...
```
Thành
```
...
'DIRS': [
           os.path.join(BASE_DIR, 'home', 'templates'),
       ],
...
```

## Bước 2: Tạo view để render template
```
vim /home/views.py
```
với nội dung
```
from django.shortcuts import render


def index(request):
   return render(
       request,
       'home/index.html'
   )
```

## Bước 3: Config url cho view mới:
Cập nhật file urls.py trong home:
```
rom django.conf.urls import patterns, url

urlpatterns = patterns(
   '',
   url(
       r'^$',
       'home.views.index',
       name='index'),
)
```
Khai báo file urls.py của app home vào home/urls.py:
'''
from django.conf.urls import patterns, include, url


urlpatterns = patterns(
   '',
   url(
       r'^',
       include('home.urls', namespace='home')),
)
'''
