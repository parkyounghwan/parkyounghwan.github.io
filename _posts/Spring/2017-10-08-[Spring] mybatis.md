---
layout: post
title:  "[Spring]-mybatis"
date:   2017-10-08 
categories: Spring
comments: false
---
**----------사전지식-----------**

**  
**

***ORM(Object Relational Mapping)**

- 관계형 데이터베이스에서 조회한 데이터를 Java 객체로 변환하여 리턴해주고, Java 객체를 관계형 데이터베이스에 저장해 주는 라이브러리 혹은 기술.

- Object : 객체지향 언어의 객체 / Relational : 관계형 데이터베이스(Relational Database) / Mapping : 객체와 관계형 데이터를 서로 변환.

- Java ORM 기술로 유명한 것은 mybatis, Hibernate, JPA 가 있다.

  


  


***JPA(Java Persistence API)**

- API 표준의 이름.

- JPA 표준 규격대로 만들어진 제품 중에서 유명한 것이 Hibernate 오픈소스 라이브러리.

- Spring JPA에 Hibernate 라이브러리가 포함.

  


  


*분류





*분류



*분류

ORM

 mybatis

JPA , Hibernate 

  


  


*비교

mybatis

JPA

 SQL 명령으로 구현(소스 코드 양 많음)

 SQL 명령어 필요 없음(소스 코드 양 적음)

 관계형 데이터베이스에 한정

 관계형 데이터베이스가 아니라도 적용 가능 

 객체 구조로 변환이 용이

고급 JPA 기능을 공부 해야함 

 DBMS 교체시 소스코드 수정

DBMS에 상관 없이 작동 

  


  


**------------------------------**

  


1. mybatis  


  


1) mybatis mapper  


  


*구조

- DB table에 대한 SELECT/UPDATE/DELETE 명령들을 mybatis mapper에 구현한다.

- DB table 1개당 mybatis mapper 1개 구현.

  


mapper XML 

mapper Java Interface 

DB table에 대한 조회, 삽입, 수정, 삭제 SQL 명령어 작성. 

SQL 명령어 호출을 휘한 Java 메소드 선언 

 ex) StudentMapper.xml (Student 테이블 가정)

ex) StudentMapper.java 

  


*구현  


- mapper 메소드(SQL명령어)를 호출하기 위한 Java 메소드를 Java Interface에 선언하기만 하면 된다.

- Java 메소드를 구현 할 필요는 없다. (mybatis spring이 자동으로 구현)

  


ex) StudentMapper Java Interface만 만들면 된다. 이 인터페이스를 구현(Implements)한 Java 클래스를 구현할 필요 없다.

  


