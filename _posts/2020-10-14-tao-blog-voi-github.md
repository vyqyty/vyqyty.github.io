---
title: Tạo blog với github
date: 2020-10-14
categories: [Blog]
tags: [Other]
math: true
---
Jekyll là một phần mềm được viết trên Ruby giúp tạo ra các website tĩnh. Nó không có nhiều khả năng như WordPress, hơi khó sử dụng với người mới nhưng với việc tạo các website cá nhân, blog, trang tài liệu thì khả năng sinh web tĩnh cho phép nó đạt hiệu suất vượt trội. Bạn có thể tùy biến đủ kiểu với website của mình và lưu trữ nó trên chính Github - dịch vụ lưu trữ mã nguồn một cách hoàn toàn miễn phí. Một ưu điểm nữa là web tĩnh sẽ cho phép website của bạn miễn nhiễm với các mã độc, sự tấn công của hacker chúng ta thường thấy trên các CMS như WordPress.

## Tại sao sử dụng Github Pages để lưu trữ website cá nhân
Github là dịch vụ lưu trữ mà nguồn quen thuộc với các bạn lập trình viên. Github cũng cung cấp dịch vụ Github Pages cho phép bạn lưu trữ các website của dự án, website cá nhân và tổ chức trên chính Github. Ưu điểm của việc sử dụng Github lưu trữ website cá nhân là:
* Nó hoàn toàn miễn phí. Nó đã giúp tôi tiết kiệm được hơn 1 triệu đồng (tôi phải sử dụng để thuê hosting WordPress bên Namecheap mỗi năm). Bạn có thể sử dụng tên miền miễn phí dạng <tên tk github>.github.io, tuy nhiên cũng có thể dùng luôn các tên miền bạn sở hữu như vietanhdev.com
* Hỗ trợ Jekyll. Jekyll là phần mềm tạo các website tĩnh từ các file Markdown hoặc html. Thông thường bạn cần biên dịch tất cả các file sang mã html trước rồi mới upload lên các máy chủ lưu trữ. Nhưng với Github, điều đó là không cần thiết. Bạn có thể chỉnh sửa các bài viết, các trang của website sử dụng Jekyll và commit lên Github, vậy là xong.
* Khá quen thuộc với các lập trình viên. Nếu bạn là một lập trình viên thì việc commit code lên Github là một việc khá quen thuộc rồi. Làm website, viết blog theo cách đó chắc chắn sẽ làm bạn thấy thoải mái.

## OK. Tiến hành làm website bằng Jekyll nào

```
Level cơ bản sử dụng Github Pages để lưu trữ website và theme Beautiful Jekyll để tạo website cá nhân với Jekyll.
```

Trước tiên chúng ta hãy tìm một theme (giao diện) cơ bản để bắt đầu với Website nhé. Có rất nhiều theme tôi thấy rất ok tại jekyllthemes.org hoặc themes.jekyllrc.org. Tuy nhiên với Level cơ bản sử dụng Github Pages, chúng ta sẽ bắt đầu với một theme đơn giản, nhưng cá nhân tôi thấy là rất tốt để tạo một website cá nhân : Beautiful Jekyll của Dean Attali.

**Fun fact:** Website hiện tại của Việt Anh sử dụng theme này.

* Để sử dụng theme này với Github Pages, trước tiên bạn cần đăng kí một tài khoản Github. Github thì khá quen thuộc với lập trình viên rồi. Bạn nên lập luôn một cái để sử dụng cho nhiều mục đích khác sau này. Lưu ý là Username Github của bạn sẽ quyết định địa chỉ website cá nhân được lưu trữ trên Github. Ví dụ Username của Việt Anh là vietanhdev.com thì tên miền mặc định cho website được Github cấp là vietanhdev.github.io.
* Tiếp theo bạn nên làm quen với ngôn ngữ sử dụng chủ yếu để viết nội dung cho Jekyll Website là Markdown. Ngôn ngữ này cũng được sử dụng khá phổ biến trong Github để viết các file README.Md - giới thiệu chung cho mỗi dự án nguồn mở trên Github. Bạn có thể học Markdown tại www.markdowntutorial.com (tiếng Anh) hoặc Hướng dẫn sử dụng Markdown tại đây.

### Bắt đầu với theme Beautiful Jekyll nào.

Mang Beautiful Jekyll về làm trang web của bạn

* Đăng nhập Github.

* Truy cập trang mã nguồn Beautiful Jekyll trên Github: https://github.com/daattali/beautiful-jekyll.

* Fork (tạo một bản sao) mã nguồn Beautifull Jekyll về tài khoản Github của mình bằng cách ấn nút Fork ở góc trên bên phải của trang mã nguồn.

* Đổi tên repository vừa Fork thành dạng <username>.github.io , trong đó <username> là tên đăng nhập Github của bạn.

* Chỉnh sửa file _config.yml để tạo các thiết lập ban đầu cho website của bạn. Mở file đó lên thì các dòng có # ở đầu là các dòng comment hướng dẫn bạn chỉnh sửa file cấu hình đó. Sau khi sửa xong các file ở Github, bạn ấn Commit changes để lưu lại thay đổi. Đối với website chạy bằng Jekyll thì mỗi lần bạn sửa một file nào đấy là Github sẽ tự động dịch lại toàn bộ mã nguồn website của bạn sang định dạng khả dụng cho một trang web.

* Sau khi bạn chỉnh sửa xong thiết lập về đường dẫn (phần url trong file _config.yml), hãy truy cập <username>.github.io để xem trang web của bạn đã tạo thành công chưa.
 
Mô tả các bước của tôi khá tổng quát, có thể các bạn chưa hình dung được. Và thêm nữa, trăm nghe không bằng một thấy, trăm đọc không bằng xem thực hành. Tôi xin phép được trích hình ảnh hướng dẫn cài theme Beautiful Jekyll của tác giả Dean Attali để các bạn hình dung được:

![alt](https://aicurious.io/posts/xay-dung-website-voi-jekyll/install-steps.gif)

**Kinh nghiệm**: Nếu website của bạn build bị lỗi ở chỗ nào đó thì Github sẽ gửi thông báo về email của bạn. Hãy mở nó lên và kiểm tra xem có vấn đề gì xảy ra nhé. Nếu lỗi nằm ở file cấu hình _config.yml (được viết bằng ngôn ngữ YAML) thì bạn hãy sử dụng công cụ tại http://codebeautify.org/yaml-validator - Copy toàn bộ nội dung file _config.yml vào đó và kiểm tra lỗi nhé.

### Cấu trúc thư mục Jekyll

Bạn vào trang Github chứa mã nguồn Beautiful Jekyll mình vừa Fork về sẽ thấy một loạt thư mục, tập tin với chức năng khác nhau bạn cần nắm để từng bước làm chủ website của mình.

* Một số file ở thư mục gốc cần chú ý:
    * _config.yml : File cấu hình của Jekyll. Bạn cần quẩy file này tưng bừng lên để nắm được cách tùy chỉnh trang Jekyll của mình.
    * index.html : Đây là mã nguồn của trang chủ. Bên trong ngoài mã HTML còn có YAML, Liquid templating.
    * aboutme.md : trang giới thiệu về bản thân bạn trên website. Tôi nghĩ bạn nên bắt đầu chỉnh sửa file này trước.
* Các thư mục cần chú ý cho người mới:
    * _posts : chứa các bài viết trên trang của bạn.
    * _layouts : các cấu trúc trang sửa dụng trong các trang, các bài viết trên blog của bạn.
    * css, js : chứa các tập tin css, js tùy biến giao diện và làm website của bạn trở nên sinh động hơn.

### Cách viết một bài viết (xây dựng một trang) trong Jekyll

Bạn có thể tạo trang, viết blog bằng Markdown, HTML, các mã Liquid templating, tuy nhiên có vài điểm cần lưu ý về cấu trúc:

* Tên bài viết nên đặt theo kiểu yyyy-mm-dd-ten-bai-viet.md. ví dụ : 2016-09-13-xay-dung-website-voi-jekyll.md.

* Đầu mỗi file bài viết (trang) sẽ có các mã YAML chứa thông tin bài viết (trang) đó. Mã này được viết giữa hai dòng chứa ba gạch nối (-).
