---
layout: post
title:  "Eclipe-와-MySQL-연결하기-(JDBC이용)"
date:   2016-08-31 
categories: pakpark
comments: false
---
1. 기본 베이스 깔아 놓기.  


  


  


- <http://www.mysql.com/downloads/connector/j/> 여기 site 들어가서 

  


![](https://t1.daumcdn.net/cfile/tistory/2648723757C651F011)

- 'Platform Independent (Architecture Independent), ZIP Archive' 이 파일 다운로드 받는다.

- 아무데나 받아도 되고, 압축 풀면

  


![](https://t1.daumcdn.net/cfile/tistory/24725E3457C6527B15)

- 이렇게 나오는데 우리가 필요한 건 'mysql-connector-java-5.1.39-bin.jar' 일단 필요한지만 알고 이어간다.

  


  


  


2. MySQL 연결할 java 프로젝트 만들기.  


  


  


- 가볍게 java 프로젝트 만들듯이 만들어 준다. 

  


![](https://t1.daumcdn.net/cfile/tistory/2758E43F57C653741E)

  


* JPA Project로 만들어 주었다.

  


- 프로젝트 명도 가볍게 만들어 주자.

  


![](https://t1.daumcdn.net/cfile/tistory/2567753F57C6537513)

* 'TestMysql' 이라고 만들었다. 다른건 안 건드렸다.  


  


- 프로젝트 폴더 안에 'src' 폴더에 'Java Project' 만들어 준다.

  


![](https://t1.daumcdn.net/cfile/tistory/231B1E4557C654961B)

- 'src' 폴더 클릭하고 우클릭   


  


![](https://t1.daumcdn.net/cfile/tistory/2111DC4557C6549720)

- 'Java Project' 선택하고 넘어가기(Next)

  


![](https://t1.daumcdn.net/cfile/tistory/250ED34557C6549721)

- 프로젝트 이름 'jdbcTest'라고 가볍게 정해주고 피니쉬(Finish)  


  


  


3. java 코드 입력하기.  


  


*각주는 본인이 알아보기 위해 달아놓은 것이라 따로 안달아도 된다.

  


- 위 코드에서 'con =' 이 부분에서 'root'는 ID 입력란이고 "park"은 비밀번호 입력란이다. 

- 접근하려는 데이터베이스의 ID와 PW를 입력하면 된다.

  


*바로 import로 가지말고 MySQL 연결해야한다.

  


  


4. SQL연결  


  


- sql은 앞에서 해왔던 것 처럼 'mysql/bin' 이 존재하는 폴더까지 접근한다.

- 나는 이미 bin 폴더에 접근해 있어서 바로 명령어로 접근했다.

- 데이터베이스 뭐 있는지도 확인해보았다.

  


![](https://t1.daumcdn.net/cfile/tistory/2469294557C65DCE08)

  


  


5. 결과화면

  


![](https://t1.daumcdn.net/cfile/tistory/2306744C57C65E3730)

  


-끝  


