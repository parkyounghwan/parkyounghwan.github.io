---
layout: post
title:  "[MySQL]-ONLY_FULL_GROUP_BY-에러로-시작된-SQL-모드"
date:   2018-10-17 
categories: MySQL
comments: false
---
*** SQL 모드**

**: **MySQL이 어떤 SQL syntax 를 지원하고 있는지 그리고 데이터의 유효성을 검사하는 방법은 무엇이 있는지를 가리키는 것이다.

: 이것은 MySQL을 서로 다른 환경에서 사용하는 것을 손쉽게 만들어 주며 다른 데이터 베이스 서버와 함께 MySQL 을 사용하는 것이 가능하도록 만들어 준다.

  


Q. 내가 직면한 문제는 **ONLY\_FULL\_GROUP\_BY** 이 에러를 받고, SET 을 통해 @@GLOBAL.sql\_mode 를 변경해 줬는데., 코드상에서는 적용이되는데 MySQL WORKBENCH에서 쿼리를 했을 때 동일한 동작을 하지 않은 점에서 시작된다.

  


## MySQL 버젼 마다 sql\_mode 가 다르기 때문에 사용하는 환경에 맞춰 모드를 설정해 줘야한다. 모드 설정에 따라 쿼리가 달라질 수가 있다.

나의 경우 GROUP BY 절에 칼럼만 적었더니 ONLY\_FULL\_GROUP\_BY 에러가 발생하였고, MySQL 버전이 올라감에 따라, GROUP BY 시에 어떤 TABLE의 COLUMN 기준으로 그루핑을 할 것인지 명시해 주는 과정이 필수적으로 들어가야 했기 때문이다.

  


A. 결론부터 말하자면, @@SESSION까지 바꿔 줬더니 동작했다는 것. 그렇다면 **GLOBAL은 뭐고 SESSION은 무엇인가.**

**  
**

**  
**

**  
**

*** 서버는 두 가지 종류의 시스템 변수를 관리한다.**

**:** GLOBAL 변수는 서버의 전반적인 동작에 영향을 준다.

: SESSION 변수는 개별 클라이언트 연결에 대한 서버 동작에만 영향을 준다.

: 시스템 변수는GLOBAL 과 SESSION 값을 모두 가질 수 있다.

  


**좀 더**

**:** 서버를 구동하면, 서버는 모든 GLOBAL 변수를 자신의 디폴트 값으로 초기화 시킨다.

**: **서버는 연결된 각각의 클라이언트에 대한 SESSION 변수 셋을 관리하기도 한다. 

: 클라이언트의 SESSION 변수는 연결되는 시점에 대응되는 GLOBAL 변수의 현재 값으로 초기화 된다.

=> 예를 들어, 클라이언트의 SQL 모드는 SESSION sql\_mode 값의 제어를 받는데, 이것은 클라이언트가 접속될 때 GLOBAL sql\_mode 값으로 초기화 된다.

  


