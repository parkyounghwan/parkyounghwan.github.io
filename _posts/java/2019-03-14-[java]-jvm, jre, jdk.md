---
layout: post
comment: false
categories: java
---

> JVM, JRE, JDK 의 용어와 역할에 대해 알아보자.  

### JVM
---
__용어__  
* JVM, 'Java Virtual Machine' 의 약자이며, 국문으로는 `자바 가상 머신`.  

__역할__  
* 자바 소스코드로 만들어지는 Binary 파일(~.class)을 실행한다.  
* Binary 파일을 실행한다.  
> Binary 코드 읽기(Load) -> Binary 코드 검증 -> Binary 코드 실행  
* 실행 환경(Runtime Environment)의 규격을 제공한다. (라이브러리 및 기타 파일 제공, 어떠한 장비에서건 구동이 되기 위해 환경을 구축)

__특징__  
* 플렛폼에 의존적, 사용자가 구동하는 OS 마다, JVM 이 다르다. (JVM 설치 할 때, OS에 맞게 다운로드)
* 단, 컴파일 된 Binary 코드는 어떤 JVM 에서도 동작 가능.  

*Java 자체는 플랫폼에 독립적*  

### JRE
---
__용어__  
* JRE, 'Java Runtime Environment' 의 약자이며, 국문으로는 `자바 실행 환경`.  

__역할__
* JVM 이 자바 프로그램을 동작시킬 때 필요한 라이브러리 파일들과 기타 파일들을 가지고 있다.
* 물리적으로 존재하는 JVM 을 구현하는 역할.

__특징__
* JRE 는 JVM 의 실행 환경을 구현했다고 할 수 있다.
* JRE = 라이브러리 + 기타 파일 + 'JVM'  

### JDK
---
__용어__  
* JDK, 'Java Development Kit'의 약자이며, 국문으로는 `자바 개발 도구`.  

__역할__  
* JRE + 개발을 위해 필요한 도구(javac, java 등) 을 포함.