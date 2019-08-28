---
layout: post
title: "서블릿 컨테이너"
date:   2019-08-23
categories: Spring
comments: false
---

* Spring Boot 실행 순서

> https://minwan1.github.io/2018/11/21/2018-11-21-jsp-springboot-동작과정/
>
> 

## 서블릿 컨테이너 (Servlet Container)

* 웹 어플리케이션 서버 중에서 HTTP 요청을 받아 처리하는 기초 역할.
* 대부분의 웹 프레임워크가 제공하는 기능은 서블릿 컨테이너 위에서 동작하는 **서블릿, 필터, 이벤트 리스너** 등을 적절하게 구현한 것.
* 따라서, 사용자가 웹 프레임워크로 작성한 웹 어플리케이션은 결국 서블릿 컨테이너 위에서 동작한다.
* **아파치 톰켓(Apache Tomcat), 제티(Jetty)** 등이 서블릿 컨테이너.

<br/>

## 서블릿 구현

서블릿 컨테이너에 의해 프로그램이 실행되기 위해서는 표준 즉, Servlet interface 를 구현해줘야 한다.

<br/>

**사용자 정의 서블릿** 은 서블릿 컨테이너 내에 등록 된 후 서블릿 컨테이너에 의해 생성, 호출, 소멸이 이루어 진다.

<br/>

서블릿 컨테이너는 서블릿의 생명주기에 따라 서블릿의 상태를 변경하면서 서블릿 인터페이스에 정의 된 각 메서드를 불러준다.

<br/>

**HTTP프로토콜** 로 전달된 메시지는 서블릿 컨테이너에서 해석되고 재조합되어 웹 프로그래머가 작성한 서블릿으로 전달되는 과정을 거친다.

<br/>

## 서블릿

서블릿 프로그램을 개발 할 때, 반드시 구현해야 하는 메서드를 선언하고 있는 인터페이스이다. 이 표준을 구현해야 서블릿 컨테이너가 해당 서블릿을 실행 할 수 있다.

### GenericServlet

* 클라이언트 - 서버 환경에서 서버 단의 애플리케이션으로서 필요한 기능을 구현한 추상 클래스.
* 'service()' 메서드를 제외 한 모든 메서드를 재정의하여 적절한 기능으로 구현.
* 애플리케이션의 프로토콜에 따라 메서드 재정의 구문을 적용.

### HttpServlet 

일반적으로 서블릿 이라 하면, 거의 대부분 HttpServlet 을 상속 받은 서블릿을 의미.

* HttpServlet 은 GenericServlet 을 상속 받음
* GenericServlet 의 유일한 추상 메서드인 service 를 HTTP 프로토콜 요청 메서드에 적합하게 재구현
* GET, POST, DELETE, PUT, HEAD, TRAC 을 처리하는 메소드가 모두 정의 되어있음

<br/>

## 서블릿 실행 순서

서블릿의 실행 순서는 개발자가 관리하는 게 아니라, 서블릿 컨테이너가 관리 한다. 

* 서블릿에 의해 사용자가 정의한 서블릿 객체가 생성되고 호출되고 사라진다

**개발자가 아닌 프로그램에 의해 객체들이 관리되는 것을 IoC(Inversion of Control) 이라고 한다.**

#### 서블릿 컨테이너의 생명주기

#### <img width="752" alt="스크린샷 2019-08-23 오후 6 58 22" src="https://user-images.githubusercontent.com/20623970/63585173-7bf8f880-c5d9-11e9-9b99-8b1062f2fb78.png">

* 최초 요청인지 판단
* init 메소드는 해당 사용자 서블릿이 최초 생성되고 바로 호출되는 메서드
* service 메소드는 최초의 요청이든 2번째 요청이든 계속 호출되는 메서드

<br/>

## Spring boot 와 Servlet

Spring boot 는 내부적으로 내장 톰켓을 가지고 있다.

* Spring boot 가 실행되면서, 내부적으로 내장 톰켓 즉, 서블릿 컨테이너가 실행
* 스프링 부트에서 사용자 정의 프로그램을 구현한 프로그램인 서블릿은 DispatcherServlet
* Spring boot 에서 DispatcherServlet 이 FrontController 역할

<br/>

* DispatcherServlet 상속 구조

<img width="191" alt="스크린샷 2019-08-23 오후 7 06 25" src="https://user-images.githubusercontent.com/20623970/63585184-82877000-c5d9-11e9-87c4-237ab9fe30e2.png">