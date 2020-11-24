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

[Html1]<https://github.com/vyqyty/vyqyty.github.io/blob/master/assets/ecom-django-html-1.md>

**product.html**

[Html2]<https://github.com/vyqyty/vyqyty.github.io/blob/master/assets/ecom-django-html-2.md>

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

[nguồn]<https://minhng.info/tutorials/hoc-django-trong-1-ngay.html>
