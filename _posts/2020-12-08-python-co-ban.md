---
title: Python Cơ Bản
date: 2020-12-08
categories: [Python]
tags: []
math: true
---
## Cài đặt Python
Các bạn vào trang https://www.python.org/downloads/windows/ chọn phiên bản OS và Python và cài đặt.

## 1. Thử chạy trình thông dịch Python
Python đi kèm với một trình thông dịch tương tác. Khi bạn gõ python trong shell hoặc command prompt, trình thông dịch python sẽ hoạt động với một dấu nhắc >>> và chờ lệnh của bạn.
```
$ python
Python 3.7.4 (v3.7.4:e09359112e, Jul  8 2019, 14:54:52)
[Clang 6.0 (clang-600.0.57)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```
Bây giờ bạn có thể gõ bất kỳ biểu thức python hợp lệ tại dấu nhắc lệnh này. Python sẽ đọc biểu thức bạn vừa gõ, đánh giá nó và trả lại kết quả.
Ví dụ:
```
>>> 42
42
>>> 4 + 2
6
```
# 2. Thử chạy tập lệnh Python
Python cung cấp 1 IDE cho bạn. Nếu test các bạn có thể dùng luôn IDE này. ngoài ra các bạn có thể dùng các IDE khác có hỗ trợ Python như Pycharm, Visual Code, ... để viết code nhanh hơn. Bản thân mình thì đang dùng Visual Code. :)
```
print("hello, world!")
```
Và đây là kết quả ( * trên command prompt):
```
$ python hello.py
hello, world!
```
# 3. Các kiểu dữ liệu phổ biến trong Python
**Ngôn ngữ lập trình Python** có hỗ trợ cho tất cả các **kiểu dữ liệu cơ bản** và cũng có kiểu dữ liệu kết hợp rất mạnh.
### 3.1. số nguyên: integers
```
print(1 + 2)
```
Chạy chương trình thì chúng ta có kết quả:
```
3
```
Python cũng rất giỏi trong việc xử lý số rất lớn.
Ví dụ: Chúng ta hãy thử tính 2^1000.
```
print(2**1000)
```
Kết quả là một con số khá lớn :)

### 3.2. Số dấu phẩy động: float
```
print(1.2 + 2.3)
```
Chạy chương trình ta có kết quả:
```
3.5
```
### 3.3. Chuỗi: String
```
print("hello world")
print('hello world')
```
Chạy chương trình, ta có kết quả:
```
hello world
hello world
```
Chuỗi có thể được đặt trong dấu ngoặc đơn '' hoặc dấu ngoặc kép "". Cả hai đều giống hệt nhau.
Trong Python, các chuỗi rất linh hoạt và rất dễ dàng để làm việc với chúng.
```
print('hello' + 'world')
print("hello" * 3)
print("=" * 10)
```
Chạy chương trình, ta có kết quả:
```
helloworld
hellohellohello
==========
```
Hàm len tích hợp (built-in function) được sử dụng để tìm độ dài của chuỗi.
```
print(len('helloworld'))
```
Chạy chương trình, ta có kết quả:
```
10
```
Python cũng hỗ trợ viết các chuỗi trên nhiều dòng. Chúng được đặt trong ba dấu ngoặc kép hoặc ba dấu ngoặc đơn, như ví dụ sau:
```
text = """Đây là một chuỗi nhiều dòng.
Dòng thứ 2
Dòng thứ 3
và nó có thể chứa đoạn text "Trong dấu nháy" như thế này.
"""
print(text)
```
Chạy chương trình Python trên ta nhận được kết quả:
```
Đây là một chuỗi nhiều dòng.
Dòng thứ 2
Dòng thứ 3
và nó có thể chứa đoạn text "Trong dấu nháy" như thế này.
```
Python cũng hỗ trợ các lệnh tắt. \n là thông báo một dòng mới, \t là thông báo 1 tab ...
Ví dụ:
```
print("a\nb\nc")
```
Kết quả khi chạy chương trình nhận được là:
```
a
b
c
```
### 3.4. List
Python có kiểu dữ liệu dạng danh sách (được gọi là List). 
List là một trong những loại dữ liệu hữu ích nhất của Python.
```
# Khai báo một List
x = ["a", "b", "c"]
# In ra x
print(x)
# In ra độ dài của x
print(len(x))
# Truy cập phần tử thứ 2
print(x[1])
```
Chạy chương trình trên, ta nhận được kết quả:
```
['a', 'b', 'c']
3
b
```
Để khai báo một List trong Python, chúng ta sử dụng ngoặc vuông [].
### 3.5 Tuple
Python cũng có một kiểu dữ liệu khác gọi là tuple để biểu diễn các bản ghi với chiều rộng cố định.
Tuples hành xử giống như List, nhưng chúng là bất biến.
```
# Khai báo một tuple
point = (2, 3)
# In ra tuple
print(point)
```
Chạy chương trình, ta nhận được kết quả:
```
(2, 3)
```
Khi khai báo một tuple, bạn có thể bỏ qua dấu ngoặc đơn, như thế này.
```
# Khai báo một tuple không có ngoặc đơn
point = 2, 3
```
Bạn cũng có thể gán một tuple với nhiều giá trị cùng một lúc:
```
# Khai báo một tuple
yellow = (255, 255, 0)
# Gán tuple với nhiêu giá trị
r, g, b = yellow
# In ra các giá trị
print(r, g, b)
```
Chạy chương trình ta nhận được kết quả:
```
255 255 0
```
### 3.6. Dictionary
Python có kiểu dữ liệu dictionary để biểu diễn dữ liệu theo các cặp name : value
```
# Khai báo một dictionary
person = {"name": "hello", "email": "hello@hello"}
# In ra giá trị của name
print(person['name'])
# In ra giá trị của email
print(person['email'])
```
Chạy chương trình, chúng ta nhận được kết quả là:
```
hello
hello@hello
```
### 3.6 Set
Thêm nữa, Python cũng có một kiểu dữ liệu gọi là set. Một set là một tập hợp các phần tử không có thứ tự và duy nhất.
```
# Khai báo một set
x = {1, 2, 3, 2, 1}
# In set
print(x)
```
Chạy chương trình, chúng ta nhận được kết quả:
```
{1, 2, 3}
```
### 3.7 Boolean
Python có kiểu boolean. Nó có hai giá trị đặc biệt True và False để đại diện cho Đúng và Sai.
```
# Khai báo một biến boolean
x = True
# In x
print(x)
```
Kết quả nhận được là:
```
True
```
Lưu ý: Trong python thì True và False sẽ viết hoa chữ cái đầu, sẽ hơi khác so với các ngôn ngữ khác như Java, PHP.
Cuối cùng, Python có một kiểu dữ liệu đặc biệt gọi là None để đại diện cho không có gì.
```
# None: Kiểu dữ liệu đặc biệt trong Python
x = None
print(x)
```
Bây giờ bạn đã biết hầu hết các cấu trúc dữ liệu phổ biến của Python.
