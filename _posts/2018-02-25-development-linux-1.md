---
layout: post
title:  "CentOS 7 그룹, 사용자 생성, 권한"
subtitle:   
categories: development
tags: linux
comments: true
---

지난 프로젝트에서는 플랫폼 담당자분께서 계정 관리를 해주셨어요. 옆에서 어떻게 하시나 지켜보려고 했지만, 빛과 같은 속도로 계정을 생성하시기에 .. 놓쳐버렸죠.. 이렇게 평생 놓치나 했는데..

리알못인 저에게 얼마지나지 않아 생성할 기회가 왔습니다.

	생각보다 간단했습니다.

그래서 저와 같이 막연한 두려움이 있는 사람들을 위해 간단하게 정리 해보았습니다.

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=2 orderedList=false} -->
<!-- code_chunk_output -->

* [1. 사용자 계정 생성 목적](#1-사용자-계정-생성-목적)
* [2. 사용자 계정 관리 방법](#2-사용자-계정-관리-방법)
* [3. 그룹 생성 및 관리](#3-그룹-생성-및-관리)
* [4. 사용자 생성 및 관리](#4-사용자-생성-및-관리)
* [5. 폴더 및 파일 소유권](#5-폴더-및-파일-소유권)
* [참고](#참고)

<!-- /code_chunk_output -->

## 1. 사용자 계정 생성 목적
----------

저 같은 경우는 사용자 계정을 생성하는 목적이 크게 2가지가 있습니다.  

### 첫번째 DB2 사용
**DB2는 `OS 계정 = DB 계정` 입니다.**  
그래서 db2를 사용하려면 사용자계정을 생성해야합니다.


### 두번째는 **권한 관리**
데이터 분석만 하는것이 아니라 분석시스템을 구축하는 것 또한 저의 업무입니다. 서버관리 차원에서 권한 관리가 필수입니다.

## 2. 사용자 계정 관리 방법
-----

사용자계정이 한개 두개이면 권한 관리를 하나씩 잘하면 됩니다.  
문제는 사용자계정이 계속 늘어나게 될 때입니다.  
계정이 10개가 넘어가면.. 관리하기 너무 귀찮..

그래서 각 사용자를 **그룹화** 하고 그룹별로 관리를 하면 그나마 수월하게 할 수 있습니다.
그럼 그룹을 생성해보죠!

## 3. 그룹 생성 및 관리
-----

* 그룹생성.
* 그룹변경.
* 그룹삭제.
* 그룹관리.

### 3.1 그룹 생성


#### 그룹생성

- 명령어  
**groupadd** : group을 추가합니다.

```
# 그룹 생성 방법
groupadd [그룹명]

# 그룹 확인
groups
	#또는
cat /etc/group
```
500번 이후의 GID(Group Identifier) 가 자동으로 생성됩니다. (1~499번은 시스템GID이기 때문입니다.)

#### 그룹옵션
- 명령어  
**-g [GID]** : 그룹 GID를 지정합니다.


```
# GID지정 그룹생성
groupadd -g [GID] [그룹명]
```

**등록된 마지막 GID를 확인하고 그 다음 번호로 지정해야 합니다.**

### 3.2 그룹변경

#### 그룹명
- 명령어
**groupmod -n** : 그룹명 변경

````
##그룹명 변경
groupmod -n [변경후 그룹명] [변경전 그룹명]
````

#### 그룹 GID 변경
-명령어
**groupmod -g** : 그룹GID 변경

```
##그룹GID 변경
groupmod -g [변경후 GID] [변경전 GID]

```

### 3.3 그룹삭제

- 명령어
**groupdel** : 그룹 삭제

```
## 그룹삭제
groupdel [그룹명]
```

### 3.4 그룹관리


#### 그룹패스워드 설정
* 명령어  
**gpasswd** : 그룹 패스워드를 설정합니다.

```
## 패스워드 설정방법
gpasswd [그룹명]
```

#### 그룹패스워드 제거
* 명령어  
**gpasswd -r** : 그룹패스워드를 삭제합니다.

```
## 그룹패스워드 삭제
```
#### 그룹 사용 금지 설정
* 명령어.   
**gpasswd -R** : 그룹 사용을 금지합니다.

```
## 그룹 사용 금지
gpasswd -R [그룹명]
```

#### 그룹 사용자 추가
* 명령어   
**gpasswd -a** : 그룹에 사용자를 추가합니다.  

```
## 그룹 사용자 추가
gpasswd -a [사용자명] [그룹명]
```
#### 그룹 관리 사용자 지정
* 명령어   
**gpasswd -A** : 그룹에 관리사용자를 지정합니다.   

```
## 그릅 관리자 지정
gpasswd -A [사용자명] [그룹명]
```

#### 그룹 사용자 삭제
* 명령어   
**gpasswd -d** : 그룹에서 사용자를 삭제합니다.

```
##그룹 사용자 삭제
gpasswd -d [사용자명] [그룹명]
```

#### 그룹 사용자 초기화
* 명령어   
**gpasswd -M** : 그룹 사용자를 초기화하고 사용자를 추가합니다.

```
## 그룹 사용자 초기화
gpasswd -M [사용자명] [그룹명]
```


## 4. 사용자 생성 및 관리
----
그룹을 만들었으니, 사용자를 생성하면서 그룹도 같이 설정해보죠.  

* 사용자 생성
* 사용자 변경
* 사용자 삭제
* 사용자 관리

### 4.1 사용자 생성


* 명령어  
**useradd** : user을 추가합니다.

```
# 사용자 생성 방법
useradd -g [그룹명] [user명]

# 사용자의 UID 지정
useradd -u [UID] [user명]

# 사용자의 설명 추가
useradd -c [설명] [user명]

# 비밀번호 설정
passwd [user명]
```

### 4.2 사용자 변경


* 명령어  
**usermod** : 사용자를 변경합니다.  

```
# 사용자 설명 수정
usermod -c [설명] [user명]

# 사용자 디렉토리 변경
usermod -d [디렉토리] [user명]

```

### 4.3 사용자 삭제


* 명령어  
**userdel** : 사용자를 삭제합니다.

```
#사용자 계정 삭제
userdel [user명]

#사용자 디렉토리 및 계정 삭제
userdel -r [user명]
```
### 4.4 사용자 관리
---

* 명령어  
**cat /etc/passwd** : 사용자를 확인합니다.


## 5. 폴더 및 파일 소유권
----
옆에 친구가 나의 프로젝트 파일을 실수로 지우면 .. 상상만해도 끔직하네요.   
싸우지 않기 위해 각 사용자별로 폴더에 소유권을 줘서 다른 사용자나 그룹에서 변경하지 못하도록 해봅시다.

사용자별로 권한을 줄 수 도 있고,   
그룹별로 권한을 줄 수 도 있습니다.

* 명령어  
**chown** : change own 소유를 변경합니다.

```
# 사용자별로 권한주기
chown [사용자명] [파일명]
chown [사용자명] [디렉토리]
# 디렉토리의 하위 디렉토리까지 변경
chown [사용자명] -R [디렉토리]

# 그룹별로 권한주기
chown :[그룹명] [파일명]
chown :[그룹명] [디렉토리]
chown :[그룹명] -R [디렉토리]

# 사용자, 그룹별 권한주기
chown [사용자명]:[그룹명]
chown [사용자명]:[그룹명] [파일명]
chown [사용자명]:[그룹명] [디렉토리]
chown [사용자명]:[그룹명] -R [디렉토리]

```

## 참고
https://conory.com/blog/14446