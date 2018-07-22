---
layout: post
title:  "파이썬 자료형-리스트편"
subtitle: 리스트를 활용해보자
categories: python
tags: structure
comments: true
---

* edwith 강좌를 바탕으로 정리한 내용입니다.

## Collection

Collection 은 수집, 모음 이라는 뜻입니다. 그렇다면 Python에서 Collection이라는 뜻은 무엇일까요? 여러 개의 값들의 수집할 수 있는 자료 구조를 말합니다. 리스트, 딕셔너리, 튜플이 collection에 해당합니다.  

우리가 알고 있는 변수와 collection 과의 차이에 대해 간단히 살펴보도록 하겠습니다.

#### 변수일 경우  

![스크린샷 2018-07-21 오후 4.26.08](https://i.imgur.com/7IblUOt.png)

```Python
a = 2
print(a)
a = 3
print(a)
```

#### 리스트일 경우 (collection)  

![스크린샷 2018-07-21 오후 4.27.16](https://i.imgur.com/x6Ol4Mj.png)  

```Python
list = [0]
print(list)
list.append(1)
print(list)
```  

값을 단순히 수집하는것 이외에도 collection을 이용하면 훨씬 더 다양한 방법으로 데이터를 처리할 수 있습니다. 오늘은 collection 중 리스트에 대해 알아보고 활용할 수 있는 다양한 방법들에 대해 살펴보도록 하겠습니다.

## 1. List

### 리스트의 특징  
리스트는 collection의 일종으로 , 다음과 같은 특징을 가지고 있습니다.

1. 리스트 상수는 대괄호로 둘러싸여 있고, 리스트 원소는 반점으로 구분됨

![스크린샷 2018-07-21 오후 4.41.32](https://i.imgur.com/MNfJHfJ.png)  

2. 리스트는 파이썬의 어떤 객체도 원소로 넣을 수 있음 (다른 컬렉션도 가능)

![스크린샷 2018-07-21 오후 4.58.48](https://i.imgur.com/nvyV6O1.png)

3. 빈 리스트 생성 가능
![스크린샷 2018-07-21 오후 5.04.26](https://i.imgur.com/RD5V5na.png)  


### 리스트의 내부

list은 데이터를 여러값을 저장할 수 있지만, 저장하고 나서 활용하는게 더 중요하겠죠? list안에 저장된 여러 값들을 가져오는 방법에 대해 알아보겠습니다.

- 리스트는 위치가 정해져있고 **순서를** 가지고 있습니다.
- 우리는 그 순서를 **인덱스(index)라고** 합니다.
- 인덱스를 이용해 리스트의 원소를 하나하나 가져올 수 있습니다.
- 인덱스는 0부터 시작하며, 원소 갯수 만큼 순차적으로 증가합니다.

![스크린샷 2018-07-22 오후 1.20.34](https://i.imgur.com/FTjr7J2.png)

### 리스트와 문자열의 차이 : list are Mutable

문자열도 리스트와 마찬가지로 인덱스를 가져와서 문자 하나씩 읽을 수 있습니다.

![스크린샷 2018-07-22 오후 1.42.38](https://i.imgur.com/LAXuGqD.png)  

문자열과 리스트의 차이점은 리스트는 각 원소의 값을 변경할 수 있지만, 문자열은 인덱스를 이용해 문자를 변경할 수 없습니다.

- 문자열은 변경 불가 : immutable
	- 변경하려면 새로운 문자열을 만들어야함  

  ![스크린샷 2018-07-22 오후 1.48.26](https://i.imgur.com/vXltkwY.png)  

- 리스트는 변경 가능 : mutable
	- 인덱스 연산자를 사용하여 리스트 요소를 변경 가능  

  ![스크린샷 2018-07-22 오후 1.50.08](https://i.imgur.com/LvGThSF.png)  


## 2. List 활용

리스트는 파이썬 내장함수와 리스트 메소드를 이용해서 다양하게 활용할 수 있습니다.

### len 함수 : 리스트의 원소갯수 알아내기
- 리스트를 매개 변수로 받아서 리스트의 원소 개수를 반환
- len()는 아무 집합이나 시퀀스를 받아 원소의 갯수를 반환

![스크린샷 2018-07-22 오후 2.41.30](https://i.imgur.com/szAYhnf.png)  

```python
greet = 'Hello Bon'
print(len(greet))

x = [1,2,'joe',99]
print(len(x))
```

### range 함수 : 인덱스 생성하기

- range() 함수는 0 부터 ~ 매개변수-1값 까지의 숫자리스트를 반환합니다.

![스크린샷 2018-07-22 오후 3.01.55](https://i.imgur.com/3XscvX1.png)  

```python
print(range(4))

friends = ['Joseph','Glenn','Sally']
print(len(friends))
print(range(len(friends)
))
```

- for문 , len 함수와 함께 인덱스루프로 자주 사용됩니다.

![스크린샷 2018-07-22 오후 3.14.50](https://i.imgur.com/bRuY8cb.png)  

```Python
for friend in friends :
	print('Happy new year:', friend)

for i in range(len(friends)):
	friend = friends[i]
	print('Happy new year:',friend)
```

### "+" : 리스트 연결하기

- 기존에 존재하는 두 리스트를 더하여 새로운 리스트를 생성할 때 사용합니다.
- 마치 줄을 잇는 것 처럼 연결해줍니다.  

![스크린샷 2018-07-22 오후 3.20.33](https://i.imgur.com/hjGHrgS.png)

```python
a = [1,2,3]
b = [4,5,6]
c = a+b
print(c)
print(a)
```

### ":" : 리스트 자르기   

- range함수와 마찬가지로 괄호 안의 두번째 숫자 -1 까지만 포함합니다.
- : 앞과 뒤가 공백일때는 처음부터 끝까지 포함합니다.

![스크린샷 2018-07-22 오후 3.28.35](https://i.imgur.com/qsHa93r.png)  


```python
t = [9,41,12,3,74,15]
t[1:3]
t[:4]
t[3:]
t[:]
```

### 리스트 메서드 활용하기

- 리스트메서드 확인하기  

![스크린샷 2018-07-22 오후 3.39.11](https://i.imgur.com/usQJFBd.png)  

```python
# 빈리스트 생성방법
x = []
type(x)
dir(x)
```

- append : 리스트를 생성
- count : 특정한 요소가 리스트 내에 몇 개 있는지 알려줌
- extend : 리스트 끝에 원소를 추가
- index : 리스트의 특정원소를 찾아 위치값을 반환
- insert : 리스트 중간에 입력
- pop : 리스트에서 마지막원소를 꺼냄
- remove : 리스트의 원소를 삭제
- reverse : 리스트 원소 배열순서를 뒤집음
- sort : 값에 따라 원소를 정렬


### append : 리스트 만들기  

- 빈 리스트를 만들고 원소를 추가할 수 있습니다.
- 리스트 안은 순서가 유지되고 새 원소는 리스트 끝에 더해집니다.

![스크린샷 2018-07-22 오후 3.43.30](https://i.imgur.com/xSvJrTO.png)  

```python
stuff = []
stuff.append('book')
stuff.append(99)
print(stuff)

stuff.append('cookie')
print(stuff)
```

### in , not in : 리스트 원소 탐색

- 파이썬에서는 특정원소가 리스트에 있는지 확인할 수 있는 2가지 연산자를 제공합니다.
- True, False를 반환하는 논리연산자입니다.

![스크린샷 2018-07-22 오후 3.49.07](https://i.imgur.com/OyLiw2X.png)

```python
some = [1,9,21,10,16]
print(9 in some)
print(15 in some)
print(20 not in some)
```

### sort : 리스트 정렬

- 순서를 바꾸기 위해 별도의 행동을 하지 않는 한 아이템의 순수를 유지합니다.
- 리스트는 원소 정렬이 가능합니다.
- sort 메소드는 '스스로를 정렬'하는 기능입니다.

![스크린샷 2018-07-22 오후 3.56.28](https://i.imgur.com/Inj7Zhd.png)  

```python
friends = ['b','a','c']

friends.sort()
print(friends)

friends.sort(reverse=True)
print(friends)
```

### 기타 내장함수

- 리스트를 매개변수로 받는 내장함수는 여러가지 있습니다.

![스크린샷 2018-07-22 오후 4.03.43](https://i.imgur.com/6VAULoC.png)  

```python
nums = [3,41,12,9,74,15]
print(len(nums))
print(max(nums))
print(min(nums))
print(sum(nums))
print(sum(nums)/len(nums))
```

- 평균과 갯수를 세리는 루프 예시

루프 예시 시나리오
1. 숫자를 연속으로 입력받는다.
2. 입력이 끝났다면 done을 입력한다.
3. 입력된 숫자의 평균값이 나온다.

![스크린샷 2018-07-22 오후 7.02.37](https://i.imgur.com/G0qjW3m.png)  

**코드 작성 시나리오 1**  

1. False 일때 까지 반복하는 루프문 생성
2. 숫자 입력 받기
3. done 을 입력받으면 반복문 끝내기
4. 입력받은 숫자는 문자열이니까 float형태로 변환하기
5. 입력받은 숫자들의 합계를 total에 저장하기
6. 입력받은 숫자들의 갯수를 count에 저장하기
7. 합계/갯수 를 average에 저장하기
8. average 값 출력하기

![스크린샷 2018-07-22 오후 7.22.32](https://i.imgur.com/kf5Mvob.png)  

```python
total = 0
count = 0
while True:
	inp = input('Enter a number:')
	if inp == 'done' : break
	value = float(inp)
	total = total + value
	count = count +1

average = total/count
print('Average:', average)
```

- 리스트를 이용한 루프 예시

**코드 작성 시나리오 2**

1. 입력된 숫자를 보관할 리스트 생성
2. False일 때까지 반복하는 반복문 생성
3. 숫자 입력 받기
4. 'done'을 입력받으면 반복문 끝내기
5. 입력받은 문자열을 float으로 변환
6. 리스트에 입력값 추가
7. (리스트 합계) / (리스트의 원소갯수)로 평균구하기
8. average값 출력하기


![스크린샷 2018-07-22 오후 7.33.03](https://i.imgur.com/nkzXTyk.png)  

```python
numlist = list()
while True:
	inp = input('Enter a number:')
	if inp == 'done' : break
	value = float(inp)
	numlist.append(value)

average = sum(numlist)/len(numlist)
print('Average:', average)
```

- 두 가지의 방법 중 어떤 방법이 더 효율적일까요?
	- 데이터가 10억개일 때 두번째 방법은 10억개의 데이터를 모두 메모리에 저장하고 있어야합니다.
	- 하지만 첫 번째 방법은 반복해서 계산하기 때문에 메모리를 많이 차지하지 않습니다.


## 최고의 친구들 : 문자열과 리스트
- split 함수는 문자열을 작게 나누고 문자열로 구성된 리스트를 생성합니다.
- 특정 단어에 접근하거나 모든 단어에 대해 루프를 실행할 수 있습니다.

![스크린샷 2018-07-22 오후 7.51.38](https://i.imgur.com/aSlcg2z.png)  

```python
abc = 'With three words'
# 공백으로 문자열을 나누고 리스트를 생성
stuff = abc.split()
print(stuff)
print(len(stuff))
print(stuff[0])

for w in stuff:
	print(w)
```

- 구획 문자를 별도로 설정하지 않으면, 여러 칸의 공백도 하나의 구획문자로 여겨집니다.
- 문장을 나눌 때 어떤 구획 문자를 사용할 지 정할 수 있습니다.  

![스크린샷 2018-07-22 오후 8.01.34](https://i.imgur.com/JcC6ctR.png)  


```python
line = 'A lot.      of space'
etc = line.split()
print(etc)

# 구획문자 지정
line = 'first;second;third'
thing = line.split()
print(thing)
print(len(thing))

thing = line.split(';')
print(thing)
print(len(thing))
```

- 예시 : mbox-short.txt 파일을 읽고 , 메일이 온 요일과 메일 호스트를 판별하는 프로그래밍을 해봅시다.

[mbox-short.txt](https://www.py4e.com/code3/mbox-short.txt) 파일을 다음과 같은 내용이 담겨있습니다.

**코드 작성 시나리오**
1. 개행문자 제거하기
2. From으로 시작하는 문장찾기
3. 공백으로 문자열 나누기
4. 요일정보 가져오기
5. 메일 호스트 가져오기

![스크린샷 2018-07-22 오후 8.13.53](https://i.imgur.com/YT1mlQd.png)  

![스크린샷 2018-07-22 오후 8.32.00](https://i.imgur.com/9LVW21x.png)  

```python
fhand = open('mbox-short.txt')
for line in fhand:
	# 1.개행문자 공백제거
	line = line.rstrip()
	# 2.From 으로 시작하는 문장가져오기
	if not line.startswith('From:'):continue
	# 3.가져온 문장에서 요일부분 추출
	words = line.split()
	print(words[2])

	# 4.메일호스트 추출하기
	email = words[1]
	pieces = email.split('@')
	print(pieces[1])
```
