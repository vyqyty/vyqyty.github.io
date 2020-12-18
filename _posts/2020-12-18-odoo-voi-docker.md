---
title: Odoo với docker
date: 2020-12-18
categories: [Other]
tags: []
math: true
---
# Odoo với docker

## Chuẩn bị

* Server đã được cài đặt Ubuntu (server/desktop phiên bản 18.04 - link download)
* File docker-compose.yml (tham khảo ở https://github.com/trobz/docker-odoo-run.git)

## Tiến hành cài đặt bằng terminal.

## Cài đặt một số thư viện

* sudo apt update
* sudo apt install apt-transport-https ca-certificates curl software-properties-common git -y

## Cài đặt docker

* sudo apt update
* curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
* sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
* sudo apt install docker-ce -y

## Kiểm tra thông tin docker đã cài thành công

* sudo systemctl status docker

![](https://raw.githubusercontent.com/vyqyty/vyqyty.github.io/master/assets/img/uploads/docker1.png)

## Cài đặt docker-compose (phiên bản mới nhất ở thời điểm viêt bài 1.25.0-rc2 released on Aug 7)

* sudo curl -L https://github.com/docker/compose/releases/download/1.25.0-rc2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
* sudo chmod +x /usr/local/bin/docker-compose

## Khởi chạy Odoo

* git clone https://github.com/trobz/docker-odoo-run.git -b 13.0
* cd docker-odoo-run
* sudo docker-compose up -d
* sudo chmod 777 -R odoo odoo-web-data
* sudo docker restart o13-web

## Truy cập vào URL (IP:8069 - địa chỉ IP chính là địa chỉ IP của Ubuntu server)

![](https://raw.githubusercontent.com/vyqyty/vyqyty.github.io/master/assets/img/uploads/docker2.png)

## Ghi chú: 

### Stop|Start|Restart docker:

* sudo docker o13-web stop|start|restart

### View logs:

* cd docker-odoo-run
* tail -fn 500 odoo/odoo-server.log

### Một số lưu ý trong bài:

* 13.0: tên git branch
* o13-web: tên container trong docker được định nghĩa ở đây

