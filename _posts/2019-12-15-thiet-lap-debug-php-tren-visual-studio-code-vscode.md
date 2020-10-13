---
id: 147
title: Thiết lập debug php trên Visual Studio Code (VSCode)
date: 2019-12-15T13:56:16+07:00
author: Ime Share
excerpt: Xdebug là thư viện được viết ra để hỗ trợ việc tìm ra lỗi trong ứng dụng viết bằng PHP một cách hiệu quả hơn.
layout: post
permalink: /thiet-lap-debug-php-tren-visual-studio-code-vscode/
post_views_count:
  - "434"
categories: [Orther]
tags: [VSCode]
---
**Xdebug** là thư viện được viết ra để hỗ trợ việc tìm ra lỗi trong ứng dụng viết bằng PHP một cách hiệu quả hơn. Các công cụ hỗ trợ tìm ra lỗi của ứng dụng như Xdebug được gọi là debugger, đặc biệt **Xdebug** cho phép kết nối đến các IDE (như Visual Studio Code, Sublime Text, PHPStorm &#8230;) để gỡ rối mã PHP, lúc này từ IDE có thể thực hiện việc đặt các breakpoint (điểm dừng mã để trích xuất, xem các thông tin &#8230;) cũng như các thao tác Debug như : Step Into, Step Over, Restart &#8230;

**Bước 1.** Cài đặt **Xdebug:**   
&#8211; Download file DLL đúng phiên bản PHP đang cài đặt tại đây <https://xdebug.org/download>  
&#8211; Copy file DLL vừa download vào thư mục **C:\xampp\php\ext\**

**Bước 2.** Thêm cấu hình Xdebug vào php.ini (\xampp\php\php.ini)

```
[XDebug] 
zend_extension=C:\xampp\php\ext\php_xdebug-xxx.dll 
xdebug.remote_enable = 1 
xdebug.remote_autostart = 1

```

php_xdebug-xxx.dll: là file vừa download ở bước 1

Sử dụng phpinfo() hoặc vào CMD gõ php -v để xem Xdebug đã cấu hình chưa.

**Bước 3.** Cài đặt PHP Debug Extension trong VS Code

Link: <https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-debug>  
[<img class="aligncenter wp-image-653 size-full" src="https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug.jpg" alt="" width="1070" height="323" srcset="https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug.jpg 1070w, https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug-300x91.jpg 300w, https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug-1024x309.jpg 1024w, https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug-768x232.jpg 768w, https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug-150x45.jpg 150w" sizes="(max-width: 1070px) 100vw, 1070px" />](https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug.jpg)

**Bước 4.** Add config cho project PHP và sử dụng

&#8211; Chọn hình cọn bọ và bấm vào chỗ bánh xe để add config cho project cần debug -> sau khi add xong sẽ tạo ra 1 file **launch.json** giống như hình dưới

[<img class="aligncenter wp-image-656 size-full" src="https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug2.jpg" alt="" width="1178" height="496" srcset="https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug2.jpg 1178w, https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug2-300x126.jpg 300w, https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug2-1024x431.jpg 1024w, https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug2-768x323.jpg 768w, https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug2-150x63.jpg 150w" sizes="(max-width: 1178px) 100vw, 1178px" />](https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug2.jpg)

&#8211; Bây giờ có thể đặt breakpoint và bấm vào nút mũi tên xanh để bắt đầu debug.

[<img class="wp-image-655 size-full aligncenter" src="https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug3.jpg" alt="" width="1090" height="377" srcset="https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug3.jpg 1090w, https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug3-300x104.jpg 300w, https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug3-1024x354.jpg 1024w, https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug3-768x266.jpg 768w, https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug3-150x52.jpg 150w" sizes="(max-width: 1090px) 100vw, 1090px" />](https://anhkevin.github.io/assets/img/uploads/2019/10/Xdebug3.jpg)