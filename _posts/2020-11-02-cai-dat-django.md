---
title: Cài đặt Django
date: 2020-11-02
categories: [Django]
tags: [Other]
math: true
---
Django là một web framework miễn phí mã nguồn mở được viết bằng Python. Trong bài viết này mình dựng server Dev trên Ubuntu 20.04. đã có sẵn Python3.8. Cài đặt Django qua Virtual Environment.
1. Kiểm tra Python
```
python3 --version
```
```
Output
Python 3.8.5
```
2. Cài đặt Pip
```
sudo apt install python3-pip
```
3. Cài Virtual Environment
```
sudo apt install python3-venv
```
4. Tạo thư mục cho dự án
```
mkdir ~/newproject
cd ~/newproject
```
5. Tạo môi trường ảo
```
python3.8 -m venv my_env
```
6. Kích hoạt môi trường ảo
```
source my_env/bin/activate
```
Sau khi kích hoạt thành công môi trường ảo sẽ hiển thik
```
(my_env)username@hostname:~/newproject$
```
7. Trong mối trường ảo cài đặt django
```
(my_env) $ pip install django
```
kiểm tra django
```
(my_env) $ django-admin --version
```
```
Output
3.8.1
```
8. Tạo dự án Django của bạn
```
(my_env) $ django-admin startproject djangoproject .
```
9. Cập nhập vào csdl(Tôi để mặc định là SQL lite của Django)
```
(my_env) $ python manage.py migrate
```
```
Output
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying admin.0003_logentry_add_action_flag_choices... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying sessions.0001_initial... OK
```
10. Tạo Administrator để có thể sử dụng giao diện quản trị
```
(my_env) $ python manage.py createsuperuser
```
11. Sửa ALLOWED_HOSTS trong Django setting 
```
(my_env) $ vim ~/django-test/djangoproject/settings.py
```
```
~/django-test/djangoproject/settings.py
...
ALLOWED_HOSTS = ['your_server_ip_or_domain', 'your_second_ip_or_domain', '*', . . .]
```
12. Kiểm tra server DEV
```
(my_env) $ sudo ufw allow 8000
```
Khởi động server Django
```
(my_env) $ python manage.py runserver your_server_ip:8000
```
kiểm tra trên trình duyệt
```
http://your_server_ip:8000
```
13. Để rời môi trường ảo
```
(my_env) $ deactivate
```
