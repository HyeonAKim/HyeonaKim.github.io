---
layout: post
title:  "파이썬 자료형-파일편"
subtitle: 파일을 탐색하자
categories: python
tags: structure
comments: true
---

* edwith 강좌를 바탕으로 정리한 내용입니다.

오랜만에 포스팅을 하네요! :)
그 동안 게으름을 피운것도 있고, 하고 싶은 내용이 너무 많다 보니까 이것도 저것도 해야하는데 언제 다하지? 제자리에서 고민한 시간이 많았습니다. 그러다 결국엔 초심으로 돌아와서 차근차근 정리해보자라는 마음이 들어서 다시 마음을 잡고 글을 쓰고 있습니다. (자기반성)

오늘은 파이썬 자료형-파일편 입니다. 지난 [파일 읽고쓰기](https://hyeonakim.github.io/python/2018/04/22/python-structure-4/) 라는 포스팅에서 파일을 읽고, 쓰고, 닫고 하는 간단한 방법에 대해 알아보았습니다. 이번에는 조금 더 응용할 수 있는 방법들에 대해 알아보도록 하겠습니다.


## 1. 파일 열기

우선, 파일안에 있는 글들을 보기 위해서는 파일을 열어야 합니다.
파이썬에서는 open()함수를 사용해서 파일을 엽니다.

```python
fhand = open('mbox.txt','r')
```
![스크린샷 2018-06-24 오후 10.11.33](https://i.imgur.com/4DNirKj.png)  

open 인자는 파일명, 모드가 있습니다.
파일명은 어떤 파일을 읽을지를 정해주는 역할을 합니다. [예제 파일](https://www.py4e.com/code3/mbox.txt)
모드는 파일로 어떤 작업을 할 것인지를 알려줍니다.

open 함수로 파일을 열면 **fhand** 변수에 어떤 정보들이 들어가게 됩니다.
어떤 정보가 들어가는 것일까요? 파일에서 읽어온 글들이 저장되어 있을까요? 한번 확인해보도록 하겠습니다.

```python
print(fhand)
```
![스크린샷 2018-06-24 오후 10.14.11](https://i.imgur.com/MnoWtXO.png)  

확인해보니 파일에서 읽어온 정보가 들어 있지 않습니다. 그럼 어떤 정보일까요? 한 번 살펴보니 파일명, 모드, 인코딩 정보가 있네요. 사실 이 안에는 컴퓨터가 어느 문장을 읽고 있는지에 대한 내용도 들어 있습니다.

파일에 대한 정보를 가지고 있다고 해서 우리는 fhand를 **핸들** 이라고 합니다. 마치 자동차 핸들처럼 파일이 지금 어떻게 해야하는지를 알려주는 역할을 합니다.

핸들의 변수명은 꼭 fhand가 아니여도 됩니다. 마음대로 정하셔도 됩니다. :)

### open()사용

![스크린샷 2018-06-24 오후 10.11.33](https://i.imgur.com/GpOl2hQ.png)  

- 핸들 = open(파일명, 모드)
- 핸들 : 파일을 조작하는데 쓰는 핸들을 반환함
- 파일명 : 파일명을 뜻하는 문자열 혹은, 파일 경로
- 모드 : 매개변수를 넣는 것은 선택사항이며 파일을 읽으려면 'r'을, 파일에 쓰려면 'w'를 입력

## 2. 파일 읽기

파일을 열었으니 한번 읽어 볼까요? 파일을 읽기 전에 개행문자에 대해 먼저 살펴보도록 하겠습니다.

### 개행문자
파일을 읽을 때는 눈에 보이지 않지만 컴퓨터는 읽을 수 있는 문자가 있습니다. 그게 바로 **개행문자** 라는 특수한 문자입니다.
개행문자는 각 줄이 끝날때 이를 알리는 역할을 합니다. 우리는 이를 줄바꿈문자라고도 부릅니다.

![스크린샷 2018-06-24 오후 10.20.03](https://i.imgur.com/WgZanJh.png)  

문자열에서는 '\n'으로 표현하기도 합니다.
여기서 개행문자는 2글자가 아니고 1글자 입니다 :)


다시 돌아가서 파일을 읽어보도록 할까요?
for 문을 이용해서 파일의 문장을 한줄 씩 읽을 수 있습니다.
이때 for 문에 들어갈 변수는 **파일핸들** 입니다.
파일핸들은 일종의 문자열의 시퀀스로 볼 수 있습니다. 문자열이 파일핸들에 담기는 것은 아니지만, 파일의 문장 위치를 가진 일련의 집합입니다.

```python
xfile = open('mbox.txt') # 파일을 열고

for cheese in xfile:  # for문으로 파일핸들을 하나씩 가져오자!
	print(cheese)				# 가져온 문장을 출력하자!
```
![스크린샷 2018-06-24 오후 10.27.56](https://i.imgur.com/FuwNKZ7.png)  

파일핸들에는 문자열이 들어 있지는 않지만, 파일핸들변수를 하나씩 가져와 cheese라는 변수에 담고 출력하면 문장이 나옵니다!
신기하네요!! 파이썬 매직!


### 파일의 줄 세기
파일 안에 있는 문장의 수를 한번 세려볼까요?
차근차근 한단계씩 진행해보도록 하겠습니다.

1. 파일을 읽기 모드로 열기
2. for문을 이용하여 각 줄을 읽기
3. 한 줄 읽을때 마다 1씩 count 하기


```python
fhand = open('mbox.txt')
count = 0
for line in fhand:
	count = count+1

print('Line Count:', count)

```
![스크린샷 2018-06-24 오후 10.48.28](https://i.imgur.com/oWrnpLX.png)

### 파일 전체를 읽기
답답하게 꼭 한 문장씩 읽어야 하냐구요? 물론 한번에 다 읽어 올 수 도 있습니다! 하지만! 파일의 용량이 클 경우에는 주의해서 사용해야 합니다.

```python
fhand = open('mbox-short.txt')
inp = fhand.read()
print(len(inp))
print(inp[:20])

```
![스크린샷 2018-06-24 오후 10.51.36](https://i.imgur.com/oJC3DFM.png)  

## 3. 파일 내용 탐색_1
모든 문장을 보는 것은 용량이 너무 클땐 컴퓨터가 힘들고, 한 문장씩 다 보려니 정신적으로 너무 힘듭니다.
그러니 파일에서 특정 단어로 시작하는 문장만 보도록 하겠습니다.

1. 파일을 연다
2. for 문으로 한줄씩 읽는다.
3. 문장이 'From'으로 시작하는 지 확인한다.
4. 'From'으로 시작한다면 그 문장을 출력한다.

```python
fhand = open('mbox-short.txt')
for line in fhand :
	if line.startswith('From:'):
		print(line)
```
![스크린샷 2018-06-24 오후 10.57.54](https://i.imgur.com/4PBtUu6.png)

음.. 그런데 말입니다. 줄과 줄 사이의 빈줄은 왜 나오는 걸까요?
그것은! 문장의 끝에는 개행문자가 있고, print에서 개행문자를 추가로 더하기 때문에 2번 줄바꿈이 되기 때문입니다.  

![스크린샷 2018-06-24 오후 10.59.24](https://i.imgur.com/hUoNrjL.png)  

각 문장에 있는 개행문자를 제거해보록하겠습니다.
1. 파일을 연다.
2. for 문으로 한줄씩 읽는다.
3. 문장의 오른쪽 끝에 위치한 개행문자를 제거한다.
4. 문장이 'From'으로 시작하는지 확인한다.
5. 'From'으로 시작한다면 그 문장을 출력한다.

```python
fhand = open('mbox-short.txt')
for line in fhand:
	line = line.rstrip()
	if line.startswith('From:'):
		print(line)
```
![스크린샷 2018-06-24 오후 11.03.33](https://i.imgur.com/ZSglscZ.png)

조금 다른 방법으로도 from 으로 시작하는 문장을 찾을 수 있습니다. continue를 이용하는 방법입니다. 한 문장씩 읽고 from 으로 시작하지 않으면 넘어가는 거죠.

1. 파일을 연다.
2. for문으로 한 줄씩 읽는다.
3. 문장의 오른쪽 끝에 위치한 개행문자를 제거한다.
4. 문장이 'From'으로 시작하지 않는다면
5. 다음 문장으로 넘어간다.
6. 그렇지 않으면(존재하면) 출력한다.

```python
fhand = open('mbox-short.txt')
for line in fhand:
	line = line.rstrip()
	if not line.startswith('From:'):
		continue
	print(line)
```
![스크린샷 2018-06-24 오후 11.17.51](https://i.imgur.com/FguBnyV.png)  

## 4. 파일 내용 탐색_2
시작하는 단어 말고 특정단어가 들어 있는 문장을 찾고 싶을 땐 어떻게 할까요? in 함수를 써서 구현할 수 있습니다.

1. 파일을 연다.
2. for문으로 한 줄씩 읽는다.
3. 문장의 오른쪽 끝에 위치한 개행문자를 제거한다.
4. 문장에 '@uct.ac.za' 가 존재하지 않으면
5. 다음 문장으로 넘어간다.
6. 그렇지 않으면(존재하면) 출력한다.

```python
fhand = open('mbox-short.txt')
for line in fhand:
	line = line.rstrip()
	if not '@uct.ac.za' in line:
		continue
	print(line)
```
![스크린샷 2018-06-24 오후 11.20.30](https://i.imgur.com/vz1JWwA.png)  

## 5. 파일 내용 탐색 업그레이드
화려하진 않지만 조금 탐색하는 코드를 꾸며볼까요?
읽고자 하는 파일명과 특정단어를 입력하면
파일을 열어 특정단어로 시작하는 문장이 얼마나 있는지 확인하는 코드를 작성해 보겠습니다.

1. 파일명을 입력받는다.
2. 특정단어를 입력받는다.
3. 파일을 연다.
4. 문장을 세릴 준비를 한다.
5. 파일의 문장을 한 줄씩 읽는다.
6. 특정 단어로 문장이 시작하면
7. 1씩 더한다.
8. 모든 문장을 읽으면 이 파일에는  특정단어로 시작하는 문장이 몇줄입니다. 라고 알려준다.

```python
fname = input('Enter the file name: ')
fw= input('Enter the word: ')
fhand = open(fname)
count =0
for line in fhand:
	if line.startswith(fw):
		count = count +1
print ('There were', count,' ' , fw, ' lines in', fname)

```
![스크린샷 2018-06-24 오후 11.26.44](https://i.imgur.com/6b3tQnM.png)  

만약 입력된 파일명이 존재 하지 않거나 잘못 입력할 경우에는 파이썬 오류가 발생하게 됩니다. 이럴 경우에는 예외처리를 해서 오류가 나도 조금 더 자연스럽게? 넘어가 봅시다.

1. 파일명을 입력받는다.
2. 만약 파일을 열때 오류가 나면
3. 파일을 찾을 수 없다고 출력하고
4. 프로그램을 종료한다.
5. 파일을 열때 오류가 나지 않으면 문장을 세릴 준비를 한다.
7. 파일에서 문장을 한 줄씩 가져온다.
8. 특정문자로 시작하는 문장이라면
9. 1씩 더한다.
10. 문장을 다 읽으면 이 파일에는 특정단어로 시작하는 문장이 몇 줄입니다. 라고 알려준다.


```python
fname = input('Enter the file name: ')
try :
	fhand = open(fname)
except:
	print('File cannot be opened:', fname)
	quit()
count = 0
for line in fhand :
	if line.startswith('Subject'):
		count = count+1
print('There were', count, 'subject lines in', fname)
```
![스크린샷 2018-06-24 오후 11.35.13](https://i.imgur.com/XflkwSj.png)
