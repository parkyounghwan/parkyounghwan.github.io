---
layout: post
title: "[Programmers - 웹 백엔드 강의] 1 주차 리뷰"
date:   2019-09-04
categories: Spring
comments: false
---

* JdbcTemplate, 주입 받는 법
* DTO 와 벨리데이션 그리고 메시지 처리
* 메시지를 일일이 정의하지 않고, 코드 형식으로 정리
* 람다 처리
* Repository
* 인터페이스 처리
* @Test - @Order(?)
* Web 서비스 아키텍쳐
* Spring Security 기반 인증&인가 처리
* 로컬 스토리지

<br/>

## JdbcTemplate, 주입 받는 법

*

## 인터페이스 처리

* Service 와 Repository 를 분리.
* 습관적으로 인터페이스 기반으로 하라.

## 람다 처리

* JdbcTemplate 을 람다로 처리 PreparedStatement 가 functionalInterfase 이기 때문에

<br/>

## Web 서비스 아키텍쳐

* REST API - 10년 동안 표준처럼 여겨지면서, 레퍼런스가 많이 쌓였다.

* 3-Tier 아키텍처

  1. 프레젠테이션 레이어 - 사용자와의 접점 제공 (HTML5, JS, CSS)

  2. 애플리케이션 레이어 - 트랜잭션 처리를 위한 비즈니스 로직 제공 (Java, .NET, C#, Python, C++)

  3. 데이터 레이어 - 데이터를 저장하고 조회하는 기능 제공 (MySQL, Oracle, PostgreSQL, ...)

  * 레이어 간에 구분이 잘 되어있으면, 개별 개층을 개선할 수 있다.
  * 잘 구성된 '3-Tier' 아키텍처라면, 사용자가 계속 증가하고 있는 서비스라면, 'Application Layer' 를 수평 확장을 통해서 감당할 수 있다.
  * 특정 'Application Layer' 에서 문제가 생긴다면?

* Session

  * 톰켓 기반 이라면, Session 기능을 사용한다.
  * 장애가 발생한 서버의 사람들은 다시 로그인 해야 한다.
  * 인증 정보를 잃는다.
  * HTTP 프로토콜은 어떠한 것도 저장하지 않는다.
  * Session Cluster - Redis (세션을 잃지 않기 위해) WAS에 있지 않고 세션 레퍼지터리에서 가져옴
  * Session Cluster 에서 장애가 난다면 전체 서버에 영향을 미칠 수 있음
  * 대규모 장애 방지를 위해 여러개 사용
  * Session Cluster 를 극복하기 위해 JWT 를 사용했다.
  * HTTP 는 근본적으로 무상태 프로토콜 이지만 로그인은 어떤 서비스에서든 사용하기 때문에 상태를 남길 수 밖에 없다.
  * JSON 하나로 사용자 정보를 충분하게 가지고 있다.
  * 위변조가 쉽기 때문에, 변조되지 않았다는 접두를 가지고 있다.
  * **사용자에 민감한 정보를 JWT 에 절대 담으면 안된다.** (email, password) 

## Spring Security 기반 인증&인가 처리

* Session Cluster 는 시스템의 메모리를 사용하는 것.
* 백엔드 시스템의 메모리 사용량이 늘어난다.
* 사용자가 많아지면 Session Cluster 에서 사용되는 메모리가 어마어마해진다.
* JWT 같은 무상태 기반 인증 처리가 훨씬 빠르다. (BUT, 항상 좋은 것은 아니다 - 인하우스 기반이라면)
* 우리 서비스는 페이스북 처럼 사용자가 많은 처리를 하기 때문에 JWT 가 적합하다.

<br/>

* 주요개념.
* ThreadLocal 저장소 개념 꼭 공부해보기.
* 'Authentication Manager' + 'Access Decision Manager'
* Filter Class 를 잘 알고 있고, 커스텀 할 수 있어야 하는데 클래스가 많아서 익히기가 어렵다는 말이다.

## 인증 & 인가 처리

