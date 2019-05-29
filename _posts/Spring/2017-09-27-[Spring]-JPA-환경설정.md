---
layout: post
title:  "[Spring]-JPA-환경설정"
date:   2017-09-27 
categories: Spring
comments: false
---
  p.p1 {margin: 0.0px 0.0px 0.0px 0.0px; font: 17.0px Monaco; color: #3933ff} span.s1 {color: #000000}  

Database > Table name, Field name <--JPA--> Java > class name, property name

  


JPA : 양방향 변환해 주는 ORM 기술 중 하나

  


  


spring.jpa.hibernate.naming.physical-strategy=org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardlmpl

  


studentNo -> studentNo(설정)

studentNo -> student\_no(default)  


  


*JPA에서 default를 snake case로 주어서 camel case로 바꿔 주는 코드.

  


*Bug 잡자

1) 테스트 코드 / jUnit

2) 코드 리뷰

3) logging(컴파일 시 콘솔창에 뜨는 막 지나가는 것)

  


loggin.level.org.hibernate.SQL=DEBUG //SQL관련 log message를 보겠다

     <span style="font-size: 10pt;"> p.p1 {margin: 0.0px 0.0px 0.0px 0.0px; font: 17.0px Monaco} span.s1 {text-decoration: underline} span.s2 {color: #3933ff} </span>  

loggin.level.org.hibernate.type.descriptor.sql.BasicBinder=TRACE //console 창에서

  


*spring data(sub project) - JPA(moduel), JDBC(moduel)

  


  


  


