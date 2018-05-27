---
layout: post
title:  "파이썬 자료형-문자열편"
subtitle: 문자열 탐색하자
categories: python
tags: structure
comments: true
---
- edwith 강좌를 바탕으로 정리한 내용입니다.

오늘 포스팅은 **파이썬자료형-문자열편** 입니다.
파이썬에 관한 [첫번째 포스팅](https://hyeonakim.github.io/python/2018/03/05/python-structure-1)에서 문자열의 표현과 저장방식에 대해 아주 간략하게 언급했었습니다.
이번 포스팅에서는 문자열에 대해 조금 더 깊게 알아보고, 문자열을 탐색하는 방법들과 응용예시에 대해 이야기하려 합니다.

## 1. 문자열 자료형이란, 읽기와 변환
파이썬에서 문자열은 '' ,"", ''' ''' 로 표현이 가능합니다.
```python
str1 = "Hello"
str2 = 'hello'
str3 = '123'
print(str1)
print(str2)
print(str3)

type(str3)
```
![스크린샷 2018-05-27 오후 9.33.26](https://i.imgur.com/zG6NDdm.png)

위와 같이 '',"" 로 표현한 숫자도 모두 문자열로 인식을 하게 됩니다.  
또한 input()함수로 입력을 받게되는 모든 문자와 숫자도 문자열로 인식하기때문에 숫자연산을 할 경우에는 숫자형으로 타입을 변환해야합니다.

```python
str_num = input("Enter : ")

print(type(str_num))
```
![스크린샷 2018-05-27 오후 9.37.51](https://i.imgur.com/JZlMyM3.png)

```python
str_num = input("Enter : ")

print(type(str_num))

# str을 int로 변환해서 연산하기
sum = int(str_num) + 1

print(sum)
```
![스크린샷 2018-05-27 오후 9.40.17](https://i.imgur.com/QxDLGoO.png)

## 2. 문자열 파악
문자열이 변수에 저장될 때에는 리스트와 비슷하게 인덱스가 매겨져서 저장이 됩니다. 다시말해 한 글자씩 문자가 저장이 되고 우리는 한 글자씩 분석할 수 있습니다.  
문자열을 확인하는 방법은 다음과 같습니다.
```python
str1 = "Hello"
print(str1[0])
print(str1[1])
print(str1[2])
print(str1[3])
print(str1[4])

# 문자열의 범위를 벗어날 경우에는 에러가 발생합니다.
print(str1[5])

```
![스크린샷 2018-05-27 오후 9.46.18](https://i.imgur.com/29YLtsN.png)

우리가 프로그래밍을 하다보면 항상 문자열의 길이를 알 수 없습니다. 그때는 len()함수를 사용하면 문자열의 길이를 파악할 수 있습니다. **인덱스는 항상 0 부터 시작합니다. 잊지마세요**

```python
str1 = "Hello"

len(str1)
```
![스크린샷 2018-05-27 오후 9.49.39](https://i.imgur.com/lnubULr.png)


## 3. 루프를 이용한 문자열 탐색
문자열이라는게 단어가 될 수도 있고, 문장이 될 수도 있고, 문서가 될 수도 있습니다. 이처럼 문자열이 길어지거나, 길이가 일정하지 않을 때 루프문을 이용해서 쉽게 처리할 수 있습니다.

### while문을 이용한 문자열 탐색
`while문, 반복 변수, len함수`를 이용해서 문자열에 있는 문자를 확인하는 코딩을 해보겠습니다.
```python
# 체리를 입력합니다.
fruit = 'cherry'
# 반복변수의 초기값을 설정합니다.
index = 0

# 반복변수가 문자열의 길이의 수보다 작을때 까지 반복문이 실행 됩니다.
while index < len(fruit):
    # letter변수에 한글자씩 담습니다.
    letter = fruit[index]
    # 반복변수  index와 letter에 담긴 글자를 출력합니다.
    print(index,letter)
    # 반복변수를 변경해줍니다.
    index = index + 1
```

![스크린샷 2018-05-27 오후 9.59.37](https://i.imgur.com/NlsKW9A.png)

### for문을 이용한 문자열 탐색
이번에는  for문을 이용해서 한글자씩 출력해보겠습니다.
```python
fruit = 'cherry'

for letter in fruit:
    print(letter)
```
![스크린샷 2018-05-27 오후 10.02.47](https://i.imgur.com/xsR0fgz.png)

while문에 비해서 for문이 굉장히 코드가 깔끔합니다. 그 이유는 `in`의 역할 덕분인데요. `in`을 사용함으로써 `반복변수`를 따로 만들지 않아도 되고 `len`함수를 따로 사용하지 않아도 문자열의 길이를 알아서 파악해주기 때문이죠. :) 매우 좋죠?

## 4. 문자열 탐색 방법
이제까지 문자열의 입력, 구조에 대해 살펴보았다면 문자열을 탐색할 수 있는 다양한 방법에 대해 알아보도록 하겠습니다.

### 1. 문자열 슬라이싱
문자열의 특정범위를 슬라이싱할때는 문자열의 인덱스의 범위를 정의하면 됩니다. 이 경우에서는 문자열의 끝 범위를 넘어가도 에러가 발생하지 않습니다. 코드로 살펴보도록 하겠습니다.  

```python
str = "Hello"

print(str[0:2])
# 문자열의 범위를 넘어가도 에러가 발생하지 않습니다.
print(str[0:6])
# 문자열의 길이를 알 수 없는 경우에는 인덱스를 지정하지 않아도 됩니다.
print(str[0:])

```
![스크린샷 2018-05-27 오후 10.13.01](https://i.imgur.com/HCBxK1X.png)

### 2. 문자열 병합
문자열을 연결할때에는 `+` 로 병합할 수 있습니다. 처음에 살펴 보았듯이 `+` 뒤에 숫자가 올 경우에 에러가 발생하니 , 문자열을 숫자로 변경하거나 숫자를 문자열로 타입을 변환해야합니다.

```python
str = "Hello"


print(str+'  everybody')
print(str+' 1')
# 에러 발생
print(str+1)

```
![스크린샷 2018-05-27 오후 10.17.39](https://i.imgur.com/qrsKMm5.png)  

### 3. 특정문자 있나 없나 확인하기
문자열 안에 특정문자가 있는지 없는지 `in`을 사용해서 확인할 수 있습니다. `in`은 앞에서 for문과 함께 사용하였는데, 여기에서는 논리연산자의 역할을 합니다.  

```python
fruit = 'cherry'

'r' in fruit
```
![스크린샷 2018-05-27 오후 10.25.24](https://i.imgur.com/oGPfdGG.png)

if문을 활용해서 특정문자의 존재를 조금 더 부드럽게? 나타내 볼 수 있습니다.  

```python
fruit = 'cherry'

if 'r' in fruit :
    # 찾았다!
    print ('Found it!')

```
![스크린샷 2018-05-27 오후 10.27.38](https://i.imgur.com/ELh4qPj.png)

### 4. 문자열 라이브러리
앞서 대충 지나쳤던, 문자열의 타입을 다시 한번 확인해보겠습니다.  
```python
string = 'Hello'
print(type(string))
```
![스크린샷 2018-05-27 오후 10.39.54](https://i.imgur.com/wmIaUwj.png)

출력결과를 다시보면 `<class 'str'>`이라고 적혀있습니다. str이라는 파이썬 기본 내장클래스라는 뜻입니다. 이 내장클래스에는 다양한 멤버메소드가 있습니다. 멤버메소드들은 특정기능을 하는 함수라고 볼 수 있습니다.

멤버메소드를 이용할 때에는 `문자열변수.메소드()`의 형식으로 사용합니다.
```python
string = 'Hello'

# 문자열변수.메소드()
string.find('H')
```  
![스크린샷 2018-05-27 오후 10.44.53](https://i.imgur.com/u0Zbh7z.png)  

#### 문자열 method 확인
str 클래스의 멤버메소들이 어떤것이 있는지 알아보도록 하고 그 중 자주 사용하는 메소드에 대해 간략히 소개하도록 하겠습니다.  

```python
#멤버메소드 종류 확인하기
print(dir(str))
```  

![스크린샷 2018-05-27 오후 10.48.02](https://i.imgur.com/4zExpaP.png)  

#### 1) 문자열 위치 찾기 : find()
`find()`함수는 문자열에서 특정문자열의 첫번째 인덱스위치를 알려줍니다. 만약 문자열이 존재 하지 않을 경우에는 '-1'을 반환합니다.  
```python
str1 = 'Hello'
print(str1.find('e'))
print(str1.find('w'))
```
![스크린샷 2018-05-27 오후 10.52.11](https://i.imgur.com/hmvhyFL.png)  

#### 2) 대소문자로 변경하기 : upper(),lower()
`upper()`와 `lower()` 함수는 문자열을 대문자 혹은 소문자로 변경해줍니다. 이때 대상문자열을 복사해서 변경하기 때문에 대상문자열은 변경되지 않습니다.  

```python
str1 = 'Hello'

print(str1.upper())
print(str1.lower())
```
![스크린샷 2018-05-27 오후 10.55.06](https://i.imgur.com/hDBDqOs.png)

#### 3) 찾아바꾸기 : replace()
`replace()`함수는 대상문자열에서 특정문자를 찾아서 바꿔줍니다.  
```python

str1 = 'Hello Hyuna'
# 찾는 문자, 변경할 문자
print(str1.replace('Hyuna', 'MJ'))

# 대상문자열은 바뀌지 않습니다.
print(str1)
```
![스크린샷 2018-05-27 오후 10.58.51](https://i.imgur.com/7teTr9m.png)

#### 4) 공백제거하기 : lstrip(), rstrip(), strip()  
 `lstrip()`은 문자열의 왼쪽 끝의 공백을 제거하며, `rstrip()`은 문자열의 오른쪽 끝의 공백을 제거해줍니다. `strip()`은 문자열의 양쪽 끝의 공백을 제거합니다.  

```python
str1 = '    Hello  '
print(str1)
# 왼쪽 공백 제거
print(str1.lstrip())
# 오른쪽 공백 제거
print(str1.rstrip())
# 양쪽 공백 제거
print(str1.strip())
```
![스크린샷 2018-05-27 오후 11.03.54](https://i.imgur.com/yHZg3uz.png)  

#### 5) 처음시작하는 단어 확인하기: startwith()
`startwith()`함수는 문자열에서 특정문자로 시작하는지 여부를 확인할 수 있는 함수 입니다. 대소문자를 구별하니 주의해서 사용해야 합니다.

```python
str1 = 'Hello Hyuna'
print(str1.startswith('H'))
print(str1.startswith('h'))
```
![스크린샷 2018-05-27 오후 11.07.34](https://i.imgur.com/zGsMWTP.png)

## 5. 문자열 탐색 응용
앞서 포스팅에서 다룬 내용을 가지고 문자열 탐색응용을 하고 포스팅을 마무리하려합니다.  

`안녕하세요. 저는 몽망이입니다. 제 메일은 abc@gmail.com 입니다.`

위의 문자에서 이메일주소(@)뒤의 주소를 찾아보도록 합시다.

```python
data = '안녕하세요. 저는 몽망이입니다. 제 메일은 abc@gmail.com 입니다.'
# @의 위치를 찾습니다.
atpos = data.find('@')
print(atpos)

# @ 다음에 나오는 공백위치를 찾습니다.
sppos = data.find(' ',atpos)
print(sppos)

# @위치에서 부터 공백위치까지 슬라이싱합니다.
host = data[atpos+1 :sppos]
print(host)
```
![스크린샷 2018-05-27 오후 11.15.38](https://i.imgur.com/LMJhrFD.png)
