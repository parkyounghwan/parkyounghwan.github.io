---
layout: post
title: "[PRG - 웹 백엔드 개발 스터디(1)] 오리엔테이션"
date:   2019-08-28
categories: Spring
comments: false
---

* 코드리뷰
* 스터디 소개
* 스프링 주요 프로젝트
* Spring Framework
* 토비의 스프링 (초난감 DAO)
* 제어의 역전 (IoC)
* 스프링 부트 시작하기
* 미션 소개
* 사전과제 리뷰
* Q&A

<br/>

## 코드리뷰

* 일단은 작성하고 작성하며, 톤앤 매너를 맞춰 간다.

<br/>

## 스터디 소개

* 페이스북 클론 서비스 (회원가입, 로그인, 포스트 작성, 좋아요, 댓글)
* UI 코드는 제공이 되고, 백엔드 코드를 작성한다.
* 주차 마다 베이스 코드가 제공이 된다.
* 1주차 : maven 설정 / 프로젝트 생성
* 2추자 : 제공 된 Base Code 를 바탕으로 코딩
* 3주차 : API / Swagger
* 4주차 : 사진 / AWS / 다시 보이기
* 5주차 : 이벤트(도메인) / 스프링 이벤트 시스템 / 웹 Notification

<br/>

## 스프링 주요 프로젝트

* Spring Boot / Spring Framework / Spring Security / ...
* 여러 프로젝트들이 SPRING 으로 제공 되고 있다.
* 우리는 Spring Framework 에 집중해서 본다.

<br/>

## Spring Framework

* Spring Framework 를 위주로 공부한다.
* JDBC Template 사용
* 의존성 주십
* 스프링의 선언적 트랜잭션 관리를 포함한 AOP

<br/>

## 토비의 스프링 (초난감 DAO)

* 클래스는 한가지 일만 한다.

<br/>

## 제어의 역전

* 스프링이 IoC 인 것은 아니다.
* 외부에서 생성한 오브젝트를 주입 받는다.
* 스프링을 사용하지 않더라도, 어떤 팩토리를 만들어서 A Class 가 B Class 를 사용할 수 있게 할 수 있다.
* 스프링을 하면 위 작업을 편하게 할 수 있다.
* Context Class 를 구현해서 직접 빈 관리를 할 수 있다.
* 프레임 워크에 의해서 전체적인 구조가 만들어져 있고, **우리 코드를 끼워 넣는다.**
* 프레임워크가 우리 코드를 사용한다.
* 라이브러리는 우리가 코드에 사용한다.
* 어플리케이션 컨텍스트에 의해 관리되는 것이 빈이다.

<br/>

## 스프링 부트 시작하기

* 스프링 프로젝트를 빠르게 개발하고 시작하는데 도움을 준다.
* SpringApplication 을 통한 손쉬운 실행
* Auto Configuration
* 쉬운 외부 환경 설정 - 'properties', 'yaml', 'command line 설정'
* embeded tomcat  으로 서버를 띄우는 기능 ('.jar' 파일 실행, not '.war')
* Docker 기반으로 말아서 빠르게 빌드하고 수평 확장이 용이하다.
* Spring Boot Starter : pom 프로젝트로 주요 'dependency' 의 묶음 / spring-boot-starter-web 의 디펜던시
* 'spring-boot-maven-plugin' 역할 : jar 파일 실행(?)
* 'SpringApplication.run()' 메서드를 통해서, was(임베디드 tomcat) 가 실행

<br/>

## 미션소개

* 스프링 부트 프로젝트 만들기.
* User Entity 에 해당하는 다음 기능을 만들어 보세요.
* HTTP 요청을 처리하는 컨트롤러에 대한 테스트를 작성하세요.
  * HTTP GET api/user/{param} - JSON 형태로 반환 (H2 DB 에서 읽어서) / 시간이 있으면 전체 조회
  * POST api/user/join - H2 DB 에 저장 / 요청에 대한 DTO를 만들어보세요
* HTTP 요청을 처리하는 컨트롤러에 대한 테스트를 작성하세요
  * Moking 을 하는 방법을 고민해 보는게 좋을 것 같다.
  * 실제 DB를 사용하지 않고 메모리상에서 처리가 되도록

<br/>

## 사전과제 리뷰

* Entity 만들기
  * Builder 패턴
  * final 키워드
  * Hash & Equals Override
  * 생성자 고민해서 만들기
  * Optional
* RESTful API
  * https://slides.com/eungjun/rest#/
* 코드리뷰
  * 임박해서 올리면, 피드백이 얼마 없어진다.
  * 빨리 올리면 코드리뷰 빨리 받아볼 수 있다.

<br/>

## Q&A

* 이직 or 커리어 관련 질문
* 'slack' or 'live session' 으로 계속 질문
* 해외 취업에 대한 설명 (Harry)