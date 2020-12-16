---
title: Python - Sự khác nhau giữa Junior và Senior
date: 2020-12-16
categories: [Python]
tags: []
math: true
---
## 1. Lặp các phần tử trong list đồng thời lấy index

**Junior**
```
x = ['a', 'b', 'c']
counter = 0
for e in x:
    print('%d: %s' % (counter, e))
    counter += 1
```
**Senior**
```
x = ['a', 'b', 'c']
for i, e in enumerate(x):
    print('%d: %s' % (i, e))
```
Output:
```
0: a
1: b
2: c
```

## 2. Lặp các phần tử trong tử điển đồng thời lấy key và value

**Junior**
```
d = {'a': 10, 'b': 20, 'c': 30}
for k in d.keys():
    print('%s: %d' % (k, d[k]))
```
**Senior 1**
```
d = {'a': 10, 'b': 20, 'c': 30}
for k, v in d.items():
    print('%s: %d' % (k, v))
```
**Senior 2**
```
d = {'a': 10, 'b': 20, 'c': 30}
for i, (k, v) in enumerate(d.items()):
    print('%d. %s: %d' % (i, k, v))
```
Output:
```
c: 30
b: 20
a: 10
```
```
c: 30
b: 20
a: 10
```
```
1. c: 30
2. b: 20
3. a: 10
```

# 3. Lặp từng cặp phần tử trong 2 danh sách (dùng zip)
**Junior**
```
m = [0, 1, 2]
n = ['a', 'b', 'c']

counter = 0
for i in range(len(m)):
    print('%d. %d <-> %s' % (i, m[i], n[i]))
    counter += 1

print('\n')
``` 
**Senior**
```
m = [0, 1, 2]
n = ['a', 'b', 'c']

for i, (mx, nx) in enumerate(zip(m, n)):
    print('%d. %d <-> %s' % (i, mx, nx))
```
Output:
```
0. 0 <-> a
1. 1 <-> b
2. 2 <-> c
```
## 4. Thay đổi mỗi phần tử trong danh sách (dùng list comprehensive)
**Junior**
```
p = [1, 2, 3]
for k in range(len(p)):
    p[k] *= 2
print(p)
    
print('\n')
```
**Senior (list comprehensive)**
```
p = [1, 2, 3]
p = [e*2 for e in p]
print(p)
```
Output:
```
[2, 4, 6]
```

## 5. Lọc phần tử trong danh sách (dùng list comprehensive)
**Junior**
```
list_input = [1, 2, 3, 4]
list_output = []
for element in list_input:
    if element % 2 == 0:
        list_output.append(element)
print(list_output)
    
print('\n')
```
**Senior (list comprehensive)**
```
list_input = [1, 2, 3, 4]
list_output = [e for e in list_input if e % 2 == 0]
print(list_output)
```
Output:
```
[2, 4]
```

## 6. "Ternary" trong Python
**Junior**
```
x = 10
if x > 5:
    x = 5
else:
    pass    # do nothing
print(x)

print('\n')
```
**Senior (ternary)**
```
x = 10
x = 5 if x > 5 else x
print(x)
```
Output:
```
5
```

## 7. Gọi hàm với tham số dạng danh sách (list) hoặc từ điển (dict)
```
def foo(key, value):
    print('key: %s | value: %s' % (str(key), str(value)))
```
**Junior**
```
foo(1, 'a')
foo(2, 'b')
foo(3, 'c')
foo(4, 'd')
foo(5, 'e')
foo(6, 'f')
foo(7, 'g')
```
**Senior 1**
```
params = [(1, 'a'), (2, 'b'), (3, 'c'), (4, 'd'), (5, 'e'), (6, 'f'), (7, 'g')]
for p in params:
    foo(*p)         # params passing by list / tuple: *p
``` 
**Senior 2**
```
params = [
    {'key': 1, 'value': 'a'},
    {'key': 2, 'value': 'b'},
    {'key': 3, 'value': 'c'},
    {'key': 4, 'value': 'd'},
    {'key': 5, 'value': 'e'},
    {'key': 6, 'value': 'f'},
    {'key': 7, 'value': 'g'}
]
for p in params:
    foo(**p)        # params passing by dictionary: **p
```
Output:
```
key: 1 | value: a
key: 2 | value: b
key: 3 | value: c
key: 4 | value: d
key: 5 | value: e
key: 6 | value: f
key: 7 | value: g
```

## 8. Gọi hàm động trong Python
```
def foo(key, value):
    print('foo key: %s | foo value: %s' % (str(key), str(value)))
    
def bar(key, value):
    print('bar key: %s | bar value: %s' % (str(key), str(value)))

func = 'bar'    # 'foo' or 'bar'
params = [(1, 'a'), (2, 'b'), (3, 'c'), (4, 'd'), (5, 'e'), (6, 'f'), (7, 'g')]
```
**Junior: does not know how to call "func" function multiple times with the given params. :((.**
**Senior: just uses "eval" to get function pointer and call it with the given params. :)).**
```
func_pointer = eval(func)
for p in params:
    func_pointer(*p)
```
Output:
```
bar key: 1 | bar value: a
bar key: 2 | bar value: b
bar key: 3 | bar value: c
bar key: 4 | bar value: d
bar key: 5 | bar value: e
bar key: 6 | bar value: f
bar key: 7 | bar value: g
```

## 9. Kiểm tra động thuộc tính trong đối tượng (dùng hasattr, getattr, setattr)
**Senior says:**
```
class Senior():
    def __init__(self):
        pass
    
    def set_dynamic_field(self, field, value):
        setattr(self, field, value)
            
    def get_dynamic_field(self, field):
        if not hasattr(self, field):
            return None
        return getattr(self, field)

s = Senior()
s.set_dynamic_field('name', 'minhng.info')
print(s.name)
```
**Junior: what the f*ck?? I'm done.**
Output:

## 10. Dùng hàm dựng sẵn trong Python (min, max, sum, sorted, …)
```
x = [4, 3, 6, 8, 10, 72]
```
**Junior: it's easy. Let me calculate sum, min, max by using "for" loop :D.**
```
sum_val = 0
for v in x:
    sum_val += v
    
min_val = x[0]
for v in x:
    min_val = v if v < min_val else min_val     # junior: haha, I'm using "ternary" :D.
    
max_val = x[0]
for v in x:
    max_val = v if v > max_val else max_val
    
print('sum: %d' % sum_val)
print('min: %d' % min_val)
print('max: %d' % max_val)
```
**Senior: what are you doing? See it.**
```
print('sum: %d' % sum(x))
print('min: %d' % min(x))
print('max: %d' % max(x))
```
**Junior: ...**
Output:
```
sum: 103
min: 3
max: 72
```
Nguồn minhng.info
