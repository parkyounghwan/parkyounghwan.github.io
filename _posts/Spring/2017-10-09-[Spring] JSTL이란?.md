---
layout: post
title:  "[Spring]-JSTL이란?"
date:   2017-10-09 
categories: Spring
comments: false
---
***JSTL이란?**  


- JSP 표준 라이브러리(JSP Standard Tag Library)의 약어이다.  


- 라이브러리는 여러 프로그램이 공통으로 사용하는 코드를 모아 놓은 코드의 집합이다.

- JSTL이란 자주 사용 될 수 있는 커스텀 태그들을 모아서 표준으로 모아놓은 태그 라이브러리다.

- 스크립틀릿, 표현식을 사용하는 것 보다 훨씬 간결한 문법 구조를 지원한다.

  


- JSTL은 5가지의 태그를 지원한다.

라이브러리

기능 

접두어 

URL 식별자 

 core(코어)

변수지원, 흐름 제어, URL처리 

c 

http://java.sun.com/jsp/jstl/core

 XML

XML 코어, 흐름 제어, XML 변환 

x 

http://java.sun.com/jsp/jstl/xml

 국제화(포매팅)

지역, 메시지 형식, 숫자 및 날짜 형식 

fmt 

http://java.sun.com/jsp/jstl/fmt 

데이터베이스

SQL 

sql 

http://java.sun.com/jsp/jstl/sql 

함수 

콜렉션 처리, String 처리 

fn 

http://java.sun.com/jsp/jstl/functions

  


  


***JSTL로 할 수 있는 일**

1) 간단한 프로그램 로직의 구사. (자바의 변수 선언, if문, for문 등에 해당하는 로직)

2) 다른 JSP page 호출. ( <:redirect>, <c:import> )

3) 날짜, 시간, 숫자의 포맷.

4) JSP 페이지 하나를 가지고 여러 가지 언어의 웹 페이지 생성.

5) 데이터베이스로의 입력, 수정, 삭제, 조회.

6) XML 문서의 처리.

7) 문자열을 처리하는 함수 호출.

  


  


*코어(core) tag  


 기능

태그명 

기능 설명 

변수 지원 

**set**

jsp에서 사용될 변수를 설정. 

**remove**

설정한 변수를 제거. 

흐름 제어 

**if **

조건에 따라 내부코드를 수행. 

** choose**

다중 조건을 처리할 때 사용. 

** forEach**

Collection의 각 항목을 처리할 때 사용. 

**forTokens **

구분자로 분리된 각각의 토큰을 처리할 때 사용. 

 URL 처리

** import**

URL을 사용하여 다른 자원의 결과를 삽입. 

** redirect**

지정한 경로로 이동. 

** url **

URL을 재작성. 

기타 태그

**catch **

예외 처리에 사용. 

**out **

jspWrite에 내용에 알맞게 처리 후 출력. 

  


  


***사용 예**

**  
**

- jsp 혹은 html 파일 상단에 아래 태그 삽입.

<%@ taglib prefix="c" uri="<http://java.sun.com/jsp/jstl/core>" %>

= prefix -> 접두어 **c **로 시작.

= uri -> URL 식별자.

  


  


- "접두어: 태그명" 으로 사용한다.

<c:set var="num1">

  


