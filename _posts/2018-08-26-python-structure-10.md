---
layout: post
title:  "파이썬 자료형-튜플편"
subtitle: 리스트와 튜플의 차이
categories: python
tags: structure
comments: true
---

* edwith 강좌를 바탕으로 정리한 내용입니다.

## 1. 튜플과 리스트
- 튜플은 리스트와 비슷한 기능을 하는 시퀀스 임
- 0부터 시작하는 인덱스에 항목을 저장
- 리스트와 튜플의 차이점
	1. 소괄호를 사용함
	2. 튜플은 저장된 내용을 변경할 수 없음

```python
x = ('Glenn', 'Sally', 'Joseph')
print(x[2])

y = (1, 9, 2)
print(y)
print(max(y))

for iter in y:
    print(iter)
```

```python

# 1
# 리스트일 경우 각 원소의 값을 변경할 수 있음.
x = [9, 8, 7]
print('변경 전 :', x)

x[2] = 6
print('변경 후 :', x)

# 2
# 문자열일 경우 원소의 값을 변경할 수 없음.
y = 'ABC'
y[2] = 'D'
print('문자열: ', y) #TypeError: 'str' object does not support item assignment

# 3
# 튜플일 경우 원소의 값을 변경할 수 없음.
z = (5, 4, 2)
z[2] = 0 # TypeError: 'tuple' object does not support item assign

```
왜 수정할 수 없는 것일까 ?  
효용성 때문임, 수정하지 않고 접근하지 않도록 만듬.

그래서 당연히 리스트에서 되는 것들 중에 튜플에서 불가능한 것들이 존재한다.
- 튜플이 할 수 없는 것은?
리스트와 튜플의 내장함수를 보면 튜플은 count, index 만 가능한 것을 볼수 있다

```python
# 1
# 튜플의 메소드 확인
x = (2, 3, 1)
print(dir(x))

"""
['__add__', '__class__', '__contains__', '__delattr__', '__dir__',
'__doc__', '__eq__', '__format__', '__ge__', '__getattribute__',
'__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__',
'__init_subclass__', '__iter__', '__le__', '__len__', '__lt__',
'__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__',
'__repr__', '__rmul__', '__setattr__', '__sizeof__', '__str__',
'__subclasshook__', 'count', 'index']
"""

# 2
# 리스트의 메소드 확인
y = [1, 2, 3]
print(dir(y))

"""
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__'
, '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__'
, '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__',
'__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mul__',
'__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__',
 '__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__',
  'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove',
  'reverse', 'sort']
"""
```


## 2. 튜플의 장점
그럼 언제 튜플을 사용하는게 좋을까?
튜플을 사용하기 좋을때는 임시로 변수를 사용할때!
리스트는 조금 더 복잡한 일을 할때 사용!

- 튜플을 수정 가능하지 않게 저장하기 때문에 리스트와 비교하여 메모리 사용량과 성능측면에서 훨씬 단순하고 효과적
- 임시변수를 선언할 때는 리스트보다는 튜플을 쓰는 것이 좋음

## 3. 튜플 선언
- 튜플은 좌변에 놓는 것으로 선언한다.
- 괄호는 생략이 가능함.

```python
# 튜블의 선언 방법
(x, y) = (4, 'fred')
print(y)   # fred

a, b = 99, 98
print(a)  # 99
```

## 4. 튜플과 딕셔너리
- 딕셔너리의 items()메소드는 (키,값)를 튜플의 형태로 리턴한다.

```python
# 1
# 딕셔너리 생성
d = dict()
d['csev'] = 2
d['cwen'] = 4

# 2
# item 메소드 호출
for (k,v) in d.items():
	print(k,v)

tups = d.items()
print(tups)
```

## 5. 튜플의 비교
튜플에서는 다른 시퀀스와의 비교 연산이 가능하다.
첫번째 요소가 조건에 만족하면 뒤에는 비교 자체를 하지 않음.  
첫번째 요소가 조건에 만족하지 않을 경우는 다음으로 넘어가서 다시 조건을 확인.

```python
# 튜플의 원소비교
print((0, 1, 2) < (0, 1, 2)) # 모든 요소를 만족 하지 않음 False
print((0, 1, 200000) < (0, 3, 4)) # 두번째 요소를 만족함 True
```

## 6. 튜플, 딕셔너리, 리스트를 활용한 정렬

- sorting
	- 딕셔너리를 정렬하기 위해 튜플로 이루어진 리스트를 사용할 수 있음
	- items() 메소드를 통해 키와 값을 얻은 후 sorted()메소드로 딕셔너리를 정렬하면 됨

```python
# sorted 를 활용한 딕셔너리 정렬
d = {'b': 10, 'a': 1, 'c': 22}
print(d.items())  # dict_items([('b', 10), ('a', 1), ('c', 22)])
print(sorted(d.items()))  # sorted 함수를 사용하면 키를 기준으로 정렬되어 출력됨 (오름차순)
                          # [('a', 1), ('b', 10), ('c', 22)]
```

- sorted()함수는 무엇일까?
	- 내장된 sorted는 시퀀스를 인자로 받아 정렬된 시퀀스를 리턴함.
	- 활용도가 높고 편리함.

- 키가 아니고 값을 이용한 정렬은 어떻게할까?
	- (키,값) 형태의 튜플로 이루어진 리스트를 만들면 값을 기준으로 정렬이 가능함.
	- for 반복문을 사용하여서 튜플로 이루어진 리스트를 만들어 보자.

```python
# 1
# 딕셔너리 생성
c = {'b': 10, 'a': 1, 'c': 22}

# 2
# 리스트로 변경
tmp = list()
for k, v in c.items():
    tmp.append((v, k))
print(tmp)

# 3
# 값을 기준으로 정렬
tmp = sorted(tmp, reverse=True)
print(tmp)
```

## 7. 튜플 응용예제

- 가장 많이 쓰이는 단어 열개 찾기
테스트 자료 : [remeo.txt](https://www.py4e.com/code3/romeo.txt)

```python
# 1
# 입력데이터 처리
fhand = open('romeo.txt')

# 2
# 소문자변경 > 단어분리 > 단어갯수 세리기
counts = dict()
for line in fhand:
    line = line.lower()
    words = line.split()
    for word in words:
        counts[word] = counts.get(word, 0) + 1

# 3
# 값을 기준으로 정렬 : 리스트를 만들어 정렬
lst = list()
for key, val in list(counts.items()):
    lst.append((val, key))

lst.sort(reverse=True)

# 4
# 가장 많이 나온 단어 10개 출력
for key, val in lst[:10]:
    print(key, val)
```

- 튜플로 리스트가 만들어지고 정렬됨.

```python
# 1
# 입력데이터 처리
fhand = open('romeo.txt')

# 2
# 소문자변경 > 단어분리 > 단어갯수 세리기
counts = dict()
for line in fhand:
    line = line.lower()
    words = line.split()
    for word in words:
        counts[word] = counts.get(word, 0) + 1

# 3
# 리스트를 생성하지 않고 가장 많이 나온 단어 10개 출력
for key, val in sorted(((v, k) for k, v in counts.items()), reverse=True)[:10]:
    print(key, val)
```

- 다른 변수에 저장하지 않고 바로 정렬되서 나올 수 있는 방법.
- 돌아가는 내부구조를 파악하고 사용해야 잘 활용할 수 있음.
