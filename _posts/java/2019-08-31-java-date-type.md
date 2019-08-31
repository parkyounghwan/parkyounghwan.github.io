---
layout: post
title: "Java, Date Type"
date:   2019-08-31
categories: Java
comments: false
---

* [Java 의 날짜와 시간 API](https://d2.naver.com/helloworld/645609)
* LocalDateTime

<br/>

## Java 의 날짜와 시간 API

Java 의 기본 SDK 에서 날짜와 시간을 다루는 'Date' 클래스와 'Calendar' 클래스가 있다. 하지만, 사용기 불편하다.

다행히, JDK 8에서는 개선된 날짜와 시간 API가 제공된다.

### 불변 객체가 아니다.

Java 의 기본 날짜, 시간 클래스는 불변 객체가 아니다.

Calendar 클래스는 set 메서드를 호출하여 날짜를 지정하고, 다시 같은 객체에 set(int, int) 를 호출해서 수행한 날짜 연산 결과 저장.

Date 클래스도 값을 바꿀 수 있는 set 메서드가 존재.

<br/>

## LocalDateTime

* Java 8 에서 추가 됨.