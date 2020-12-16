---
title: Quy Trình Restore Postgres Database
date: 2020-12-16
categories: [SQL]
tags: []
math: true
---
1. Vào quyền quản trị Posgress : sudo su posgres

2. psql

3. SELECT pg_terminate_backend(pg_stat_activity.procpid) FROM pg_stat_activity WHERE pg_stat_activity.datname = 'TARGET_DB' AND procpid <> pg_backend_pid(); 

(TARGET_DB là database định drop) 

4. Xóa một database: drop databse DATABASENAME;

5. create database "thuy" encoding='utf8'; (Nếu cần phân biệt hoa thường của Database thì cho vào dầu ").

6. alter database "thuy"  owner to odoo; (Set quyền cho user sử dụng để chạy OpenERP Server thông thường là openerp).

(Ấn ctr+d sau đó  gõ cd ~ để dump và restore)

7. pg_dump -F t -f “thuy”  “demo”;

8. pg_restore -F t -d “thuy” “thuy”;

(Hoặc pg_restore --dbname=thuy --verbose /home/dtthuy/db.dump.gz;)

9. Show list database

* \list or \l: list all databases
* \dt: list all tables in the current database
* Note: Sử dụng 4 lõi để restore

(pg_restore  -j 4 --dbname=thuy --verbose /home/dtthuy/db.dump.gz;)
