---
layout: post
title:  "[Spring]-JPA"
date:   2017-09-25 
categories: Spring
comments: false
---
ORM

 1. JPA

- 표준

- 자바에서 데이터를 저장하는데 쓰는 API를 정해놓은 것.

- 제품 : hibernate

  


 2. mybatis

- 제품

- spring mybatis (별도의 프로젝트), spring 에서 표준 sub 프로젝트를 지정하지 않았다. mybatis 팀에서 만든 프로젝트

  


spring sub project. (스프링 표준)

1. Spring Web MVC

2. Spring Data

- JDBC

- JPA (@Autowired, **repository** spring 에서 만들어 준다)

 *패키지 명을 보면 알 수 있다.

import org.springframework.data.**jpa**.repository.JpaRepository;

  


  


REST API

- 클라이언트의 URL 요청에 대해서 JSON 형태의 데이터를 출력하는 서버의 메소드.

  


**(JavaScript) 클라이언트 <---(JSON 데이터)---> (RESP API) 서버**

**  
**

- JS로 MVC 구현. //React, angular

- JSON 데이터를 서버로 변환 시켜주는 것. **Jackson 라이브러리**

  


- URL에 동사를 사용하지 않는다.

* http://localhost:8080/studentServer/api/student/3

 Request Method가 select 면 조회, insert 면 삽입, delete면 삭제, set 이면 수정.

  


* @PathVariable 상대경로가 유지된다.

  


- foreign key 설정 부분 외우기

@ManyToOne

@JoinColumn(name = "departmentId")

Department department; //foreign key 대상 되는 table명

  


-Eager Loading, Lazy Loading

1) Eager : 처음부터 열심히

2) Lazy : 가급적 미루고 미루다 필요할 때만

  


-JPA repository

*Spring Data 프로젝트의 기능이다.

  


1) 기본 메소드(findAll, remove 등등)

  


2) Query creation

  


3) JPQL (JPA Query Language)

검색 조건이 많을 때 매소드 이름이 길어지는 것을 방지(데이터베이스 쿼리 검색 조건 늘어날 때)

