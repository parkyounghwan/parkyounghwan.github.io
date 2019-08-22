---
layout: post
title: "static import"
date:   2019-08-23
categories: Java
comments: false
---

* 테스트 코드에서 'import static' 편하게 넣는 방법

<br/>

## 'Import static'

'import static' 으로 시작하는 static import 는 주로 유틸리티 성 메소드에 사용하는 스태틱 메소드나 스태틱 상수 값 등을 사용할 때 적용하기 좋다.

* 자바 프로젝트에서 static method 가 가장 활발히 사용되는 곳은 테스트 코드
* Unit 4.x 는 3.x까지와 다르게 super class 를 상속하지 않고 테스트 클래스를 작성
* 테스트 클래스가 별도의 상속 구조를 가지거나 테스트 할 대상을 상속해서 테스트 클래스를 만드는 기법을 사용하기 좋음
* 상속을 하지 않아, 'TestCase' 와 같은 super class 에 정의 되어있는 'assertEquals()' 따위를 바로 사용할 수 가 없음
* 'assertXXX()' 는 독립적으로 실행되는 유틸리티성 메소드 -> 스태틱 메소드로 만들어 적용하기 적절한 대상

<br/>

IDE 에서 편리한 타입 검색, 자동 import 등의 기능이 스태틱 메소드에는 기본적으로 적용되지 않는다는 것. 프로젝트에서 사용하는 타입 정보의 경우 미리 다 읽어들여서 몇 글자만 넣어도 빠르게 찾도록 만들어두었지만, 메소드 레벨까지 모두 기원하는 것은 큰 부담이다.

<br/>

### 그래서

static import 를 편하게 추가할 수 있도록 'Favorites' 라는 기능을 제공한다. 코드에서 자주 사용하는 스태틱 메소드를 가진 타입을 미리 'Favorites' 에 등록해두면 해당 스태틱 메소드도 자동 검색/완성 기능의 대상이 된다.

<br/>

### 근데

내가 쓴 **IntelliJ** 에서 쓴 방법은 _'method()'_ 까지 입력하고 **'alt + enter'** 를 누르고 Matcher 클래스의 메소드를 사용하는 것이었다.