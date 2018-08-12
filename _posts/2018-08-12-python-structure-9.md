---
layout: post
title:  "파이썬 자료형-딕션너리편"
subtitle: 빈도수를 세려보자.
categories: python
tags: structure
comments: true
---

* edwith 강좌를 바탕으로 정리한 내용입니다.

## 1. 딕셔너리의 정의와 특징
### "컬렉션"이란?
- 여러개의 값을 하나의 변수에 담을 수 있음
- 변수 안에 공간을 여러개 가짐
- 변수 안에 서로 다른 공간을 찾는 방법이 있음

### "컬렉션"이 아닌 것은?
- 대부분의 변수는 한 값만을 가짐
- 변수에 새값을 대입하면 이전값이 덮어씌어짐

```python
x =2
x =4
print(x)
```

### 컬렉션의 종류
- 리스트 : 순서를 유지하는 값들의 선형 컬렉션
	- 프링글스 같음
- 딕셔너리 : 고유의 라벨을 갖고 있는 값을 넣은 가방
	- 순서라는 것이 없음
	- 마치 라벨을 붙이는 것과 같음
	- 지갑과 캐리어와 같음
	- 안에 던져 넣고 이거줘이거줘 ! 소리치는 것

### 딕셔너리
- 파이썬의 가장 강력한 데이터 컬렉션
- 파이썬에서 빠르게 데이터베이스 같은 연산을 가능하게 함
- 연관 : 키와 값사이의 연결 > 엄청난 성능
- 다른 언어에서는 다른 이름으로 불림
	- Associative Array(연관배열) : Perl / PHP
	- Properties or Map or HashMap(속성, 맵, 해쉬맵) - java
	- Property Bag(속성 가방) -C# .NET

- 리스트는 리스트안에서 원소의 위치를 기반으로 인덱스를 매김
- 딕셔너리는 가방과 같아, 순서가 없음
- 따라서 딕셔너리에 넣는 대상은 "조회태그"를 달아 인덱스를 매김

```python
purse = dict()
purse['Money'] = 12
purse['candy'] = 3
purse['tissues'] = 75
print(purse)
print(purse['candy']) # 캔디 달라고 소리침

purse['candy'] = purse['candy']+2
print(purse)
```

### 리스트와 딕셔너리의 비교
- 둘다 원소를 추가하거나 삭제할 수 있음
- 차이는 인덱싱에서 난다.
	- 리스트에서 인덱싱은 위치를 나타냄
	- 딕셔너리에서 인덱싱은 키값을 나타냄
- 딕셔너리는 값을 찾기 위해 숫자 대신 키를 사용하는 것만 빼면 리스트와 동일

```python
# 리스트일 경우 : 키를 우리가 정하지 않음
lst = list()
lst.append(21)
lst.append(183)
print(lst)
lst[0] = 23
print(lst)

# 딕셔너리인 경우 : 키는 문자열도 가능하며, 우리가 지정할 수 있음
ddd = dict()
ddd['age'] = 21
ddd['course'] = 182
print(ddd)
ddd['age'] = 23
print(ddd)
```

### 딕셔너리 표현 (상수)

- 딕셔너리는 중괄호로 표현하며 키:값 쌍 목록을 가짐
- 사이가 비어있는 중괄호로 빈 딕셔너리를 만들 수 있음

```python
jjj = {'chunk':1, 'fred':42, 'jan':100}
print(jjj)
ooo = {} # emty dictionary
print(ooo)
```

## 2. 딕셔너리 응용
문제 :  

빈도수를 세리자! 데이터를 한번에 다 볼 수 없으니 하나씩 보고 세릴것!
어떤 이름이 가장 많이 나왔는지 볼 것.

- 이름을 보고 몇 번 나왔는지 적기
- 새로운 이름을 보면 목록에 이름을 추가하고 작대기 표시해서 추가해 나간다.
- 그리고 빈도수를 봐서 가장 큰 것을 고름.

### 가장 많이 나온 이름 찾기
- 대상이 얼마나 자주 보이는 지를 카운팅

```python
ccc = dict()
ccc['csev'] = 1
ccc['cwen'] = 1
print(ccc)

ccc['cwen'] = ccc['cwen']+1
print(ccc)
```

### 딕셔너리 Traceback 에러
- 딕셔너리에 없는 키를 참조하는 것은 오류를 발생
- in 연산자를 사용하여 키가 딕셔너리에 있는지 확인 가능

```python
ccc = dict()
print(ccc['csev'])
'csev' in ccc
```

### 새로운 이름을 보는 경우
- 새로운 이름을 보게되면, 딕셔너리에 새 원소로 집어 넣고,
- 두 번째 혹은 그 이상 본 이름은, 해당하는 이름에 1을 더함

```python
counts = dict()
names = ['csev','cwen','csev','zqian','cwen']

for name in names:
	if name not in counts:
		counts[name] = 1
	else:
		counts[name] = counts[name]+1

print(counts)
```

### 딕셔너리 메소드 : get
- 키가 이미 딕셔너리에 있는지 확인하고
- 키가 없다면 기본값으로 설정하는 확인 패턴 많이 사용 > get()이라는 메소드가 존재

```python
if name in counts:
	x = counts[name]
else:
	x = 0

x = counts.get(name,0)
```

- get을 이용해서 숫자세기

```python
counts = dict()
names = ['csev','cwen','csev','zqian','cwen']
for name in names:
	counts[name] = counts.get(name,0)+1 # get(key_name, default값)
print(counts)
```

### 텍스트에서 단어 수 세기
```python
counts = dict()
line = input('Enter a line of test:')
words = line.split()

print('words:', words)
print('Counting..')

for word in words:
	count[word] = counts.get(word,0)+1

print('Counts', counts)
```
한 줄의 텍스트를 받고 단어로 나눈 다음, 단어의 수를 세리는 방법

### 유한루프와 딕셔너리
- 딕셔너리 안에 저장되는 순서가 없다고 해도,
- for 문을 작성하여 딕셔너리의 모든 원소를 돌 수 있음

```python
counts = {'chunk':1, 'fred':42, 'jan': 100}

for key in counts:
	print(key, counts[key])
```

### 키와 값 목록 검색
- 딕셔너리에서 키나 값이나 아이템의 목록을 얻을 수 있음

```python
jjj = {'chunk':1, 'fred':42, 'jan': 100}

print(list(jjj))
print(jjj.keys())
print(jjj.values())
print(jjj.items()) # 튜플로 받음
# 약간의 복잡한 형태로 값을 줌 # 다음 시간에 튜블을 배움
```

### 두개의 반복변수!
- 두개의 반복변수를 사용하여 딕셔너리의 키-값 쌍을 반복해서 다룸
- 매번 반복할 때, 첫번째 변수는 키, 두 번째 변수는 키에 대응하는 값을 나타냄

```python
jjj ={'chunk':1, 'fred':42, 'jan': 100}

for aaa,bbb in jjj.items():
	print(aaa,bbb)
```

- 파일내의 단어의 갯수를 파악해보자

```python
name = input('Enter file:')
handle = open(name)

# 단어의 갯수를 세리는 딕셔너리 생성
counts = dict()
for line in handel:
	words = line.split()
	for word in words:
		counts[word] = counts.get(word,0) +1

# 가장 많이 나오는 딕셔너리 찾기
bigcount = None
bigword = None

for word, count in counts.items():
	if bigcount is None or count > bigcount :
		bigword = word
		bigcount = count

print(bigword, bigcount)
```
