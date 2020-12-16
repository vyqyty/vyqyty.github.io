---
title: Hướng dẫn Backup và Restore Postgres Database
date: 2020-12-16
categories: [SQL]
tags: []
math: true
---
# 1. Cách backup dữ liệu Postgres ra file text
## Backup
```
pg_dump -U john -h localhost -W -a -d mydb -f backup.sql
```

Các tham số:

* -U username
* -h domain, địa chỉ host
* -p port của Postgres service
* -W yêu cầu nhập password
* -a data-only chỉ xuất data
* -s schema-only chỉ xuất cấu trúc bảng
* -d tên database muốn backup
* -f tên file để lưu trữ

## Restore

Khi backup bằng file text thì phải import bằng psql:
```
psql -U john -h localhost -W -d mydb -1 -f backup.sql
```

Các tham số tương đối giống pg_dump, chỉ có 1 chút khác biệt:

* -f tên file lưu trữ để import vào
* -1 chạy từng lệnh 1

# 2. Cách backup dữ liệu Postgres ra file nén

Bạn có thể sử dụng custom format của Postgres để giúp tiết kiệm dung lượng lưu trữ cũng như tăng tốc restore (import)

## Backup
```
pg_dump -U john -h localhost -W -a -d mydb -Fc -Z9 -f backup.psql
```

Các tham số:

* -U username
* -h domain, địa chỉ host
* -p port của Postgres service
* -W yêu cầu nhập password
* -a data-only chỉ xuất data
* -s schema-only chỉ xuất cấu trúc bảng
* -d tên database muốn backup
* -f tên file để lưu trữ
* -Fc: tham số -F cho phép chọn kiểu lưu trữ (c:custom, d:directory, t:tar, p:plain_text), ta dùng c
* -Z9: tham số -Z cho phép tùy chọn cấp độ nén từ 0-9

## Restore

Khi backup bằng file nén thì phải import bằng pg_restore.
```
pg_restore -U john -h localhost -W -j 8 -d mydb backup.psql
```

Các tham số tương đối giống pgsql và pg_dump ở trên, chỉ có 1 chút khác biệt:

* Chỉ đặt tên tên file ở cuối lệnh, ko dùng tham số -f
* -j số lượng job chạy song song đồng thời. ở đây ta dùng 8. Hữu ích khi import file lớn
 
# 3. So sánh giữa cách sử dụng file text và file nén
Có thể tóm gọn như sau:

* File text: dump nhanh, kích thướng lớn, restore lâu,
* File nén: dump lâu hơn, kích thước nhở, restore nhanh (với tham số -j)

Nguồn (http://webfaver.com/database/huong-dan-backup-va-restore-postgres-database.html)
