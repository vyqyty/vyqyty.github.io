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
## 2. Thử chạy tập lệnh Python

Python cung cấp 1 IDE cho bạn. Nếu test các bạn có thể dùng luôn IDE này. ngoài ra các bạn có thể dùng các IDE khác có hỗ trợ Python như Pycharm, Visual Code, ... để viết code nhanh hơn. Bản thân mình thì đang dùng Visual Code. :)
```
print("hello, world!")
```
Và đây là kết quả ( * trên command prompt):
```
$ python hello.py
hello, world!
```
## 3. Các kiểu dữ liệu phổ biến trong Python

**Ngôn ngữ lập trình Python** có hỗ trợ cho tất cả các **kiểu dữ liệu cơ bản** và cũng có kiểu dữ liệu kết hợp rất mạnh.

### 3.1. Số nguyên: integers
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

### 3.5. Tuple

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

### 3.7. Set

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

### 3.8. Boolean

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

## 4. Tìm hiểu về Biến trong lập trình Python

Bạn chưa được học về biến trong Python nhưng bạn học lập trình Python thì đây là kiến thức căn bản không thể thiếu.
Bây giờ, chúng ta sẽ xem xét kỹ hơn về biến trong Python.
Trong Python, biến không có kiểu (hay không cần khai báo kiểu dữ liệu).
Chúng chỉ là tên giữ chỗ đó và có thể giữ bất kỳ giá trị với bất kỳ kiểu dữ liệu nào, hãy xem ví dụ sau:
```
x = 5
print(x)
x = 'hello'
print(x)
```
Chạy chương trình, ta nhận được kết quả:
```
5
hello
```
Note: Nếu bạn làm như thế trong Java thì lỗi sấp mặt rồi.
Điều quan trọng là bạn có thể nhận thấy sự khác biệt giữa các biến và chuỗi.
Thông thường người mới học lập trình sẽ hay bị nhầm lãn.
Hãy thử xem bạn có thể nhận ra lỗi nào trong ví dụ sau không?
```
name = "hello"
print("name")
```

## 5. Tìm hiểu về Hàm trong lập trình Python
Hàm - hay còn gọi là function.
Trong Python, có nhiều hàm dựng sẵn (built-in functions). Ví dụ, print một hàm được tích hợp sẵn được sử dụng phổ biến nhất.
```
print('hello')
print('hello', 1, 2, 3)
```
Chạy chương trình, ta có kết quả:
```
hello
hello 1 2 3
```
Chúng ta cũng đã thấy hàm len ở phần trước. Hàm len được sử dụng để tính chiều dài của một chuỗi, list hoặc các tập hợp khác.
```
print(len("hello"))
print(len(['a', 'b', 'c']))
```
Chạy chương trình, ta nhận được kết quả:
```
5
3
```
Một điều quan trọng về Python là nó không cho phép các hoạt động trên các kiểu dữ liệu không tương thích.
Ví dụ, bạn làm như thế này:
```
print(5 + "2")
```
Bạn sẽ nhận được thông báo lỗi tương tự thế này:
```
Traceback (most recent call last):
File "c:/Users/Admin/Desktop/Hello.py", line1, in <module>
print(5 + "2")
TypeError: unsupported operand type(s) for +: 'int' and 'str'
```
Đó là bởi vì không thể cộng số với chuỗi.
Chúng ta cần chuyển đổi 5 thành một chuỗi hoặc "2" thành một số.
Để làm điều này, chúng ta có hàm dựng sẵn là int sẽ chuyển đổi một chuỗi thành một số và hàm str sẽ chuyển đổi bất kỳ giá trị nào thành một chuỗi.
Ví dụ như thế này:
```
int('2')
```
Bây giờ, chúng ta làm lại ví dụ ở bên trên:
```
print(5 + int('2'))
print(str(5) + "2")
```
Khi chạy chương trình, ta có kết quả:
```
7
52
```
Vì cộng chuỗi với chuỗi nên chúng ta có chuỗi 52

## 6. Tạo hàm tùy chỉnh trong Python

Giống như cách gán một giá trị cho một biến, một đoạn logic cũng có thể được liên kết với một tên bằng cách định nghĩa nó là một hàm.
Ví dụ hàm tùy chỉnh trong Python:
```
# Khai báo một hàm tính bình phương
def square(x):
    return x * x
# In ra bình phương của 5
print(square(5))
```
Chạy chương trình, ta nhận được kết quả:
```
25
```
Trong đó:
từ khóa def để định nghĩa một hàm
square là tên hàm (tùy bạn đặt)
x là tham số của hàm
Phần thân của hàm được thụt lề (bằng tab). Thụt lề cũng là để cách phân nhóm các câu lệnh Python.
Các hàm trong Python có thể được sử dụng trong bất kỳ biểu thức nào:
```
print(square(2) + square(3))
print(square(square(3)))
```
Chạy chương trình ta có kết quả là:
```
13
81
```
Các hàm hiện có cũng có thể được sử dụng để tạo ra các hàm mới.
```
# Tạo hàm mới sử dụng hàm hiện có
def sum_of_squares(x, y):
    return square(x) + square(y)
# Tính tổng bình phương của 2 và 3
print(sum_of_squares(2, 3))
```
Chạy chương trình ta có kết quả:
```
13
```
Các hàm trong Python cũng giống như các giá trị khác, chúng có thể được gán, được chuyển dưới dạng đối số cho các hàm khác.
Ví dụ gán hàm cho biến:
```
# Gán hàm square cho biến f
f = square
# Tính bình phương của 4
f(4)
```
Chạy chương trình, ta có kết quả:
```
16
```
Ví dụ truyền hàm dưới dạng tham số:
```
# Ví dụ truyền hàm dưới dạng tham số
def fxy(f, x, y):
    return f(x) + f(y)
# Sử dụng thử hàm vừa tạo
print(fxy(square, 2, 3))
```
Chạy chương trình, ta có kết quả là:
```
13
```
Điều quan trọng là bạn phải hiểu được phạm vi của các biến được sử dụng trong các hàm.
Hãy nhìn vào một ví dụ.
```
# Khai báo, khởi tạo 2 biến x và y
x = 0
y = 0

# Khai báo hàm incr
def incr(x):
    y = x + 1
    return y
# Thử sử dụng hàm vừa tạo
print(incr(5))
# In ra giá trị của biến x, y
print(x, y)
```
Chạy chương trình, chúng ta có kết quả:
```
6
0 0
```
Điều này xảy ra vì các biến được gán trong một hàm, bao gồm các đối số được gọi là các biến cục bộ của hàm (local variables).
Các biến được định nghĩa ở cấp cao nhất được gọi là biến toàn cục (global variables).
Nếu bạn thay đổi giá trị của x và y bên trong hàm incr thì nó cũng sẽ không ảnh hưởng những giá trị của biến toàn cục, x và y.
Nhưng, bên trong hàm, chúng ta lại có thể sử dụng các giá trị của các biến toàn cục:
```
# Khai báo một biến toàn cục
pi = 3.14
# Tạo một hàm tính chu vi hình tròn
def area(r):
    # Sử dụng biến toàn cục trong hàm
    return pi * r * r
# Thử sử dụng hàm vừa tạo để tính toán
print(area(5))
```
Chạy chương trình, ta có kết quả:
```
78.5
```
Khi Python thấy việc sử dụng một biến không được định nghĩa trong phạm vi cục bộ, nó sẽ cố gắng tìm một biến toàn cục có tên đó.
Nếu có, nó có thể sử dụng
Tuy nhiên, bạn phải khai báo rõ ràng một biến là global để có thể sửa đổi nó.
```
# Khai báo một biến toàn cục
numcalls = 0
# Tạo một hàm tính bình phương
# Sử dụng biến toàn cục để đếm số lần hàm
# vừa tạo được sử dụng
def square(x):
    global numcalls
    numcalls = numcalls + 1
    return x * x
print(square(2))
print(square(5))
print(numcalls)
```
Như bạn đã thấy, chúng ta thực thi 2 lần hàm square. Vậy theo như hàm vừa tạo, chúng ta kỳ vọng numcalls lúc này sẽ có giá trị là 2 đúng không?
Chạy chương trình, ta có kết quả:
```
25
2
```
