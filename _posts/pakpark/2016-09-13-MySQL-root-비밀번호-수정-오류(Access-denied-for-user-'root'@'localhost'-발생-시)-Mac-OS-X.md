---
layout: post
title:  "MySQL-root-비밀번호-수정-오류(Access-denied-for-user-'root'@'localhost'-발생-시)-Mac-OS-X"
date:   2016-09-13 
categories: pakpark
comments: false
---
-Mac OS X 환경에서 MySQL을 설치하여 접속 할 때 흔히 발생하는 에러 메시지가 있다.

  


**ERROR 1045 (28000): access denied for user 'root'@localhost**

**  
**

-간단한 해결책으로 옵션을 통해 비밀번호를 입력하여 해결하는 방법도 있다.  


  


**sudo ./mysql -p<password>**

**  
**

-비밀번호가 일치하는 경우 접속되겠으나, 틀린 경우 다음과 같은 메시지로 변경된다.

**  
**

**ERROR 1045 (28000): access denied for user 'root'@localhost (using password:YES)**

**  
**

-분명히 맞는데 접속이 안되는 경우. 이런 경우에 새로운 패스워드를 지정하여 접속해야 한다.

**  
**

**  
**

**  
**

**-MySQL 비밀번호 재설정**

**  
**

**  
**

-우선 MySQL을 중단시킨다. 하단 주소로 들어가서 OS에 맞는 명령어 입력. 주소 잘 보고 입력하도록.

<https://coolestguidesontheplanet.com/start-stop-mysql-from-the-command-line-terminal-osx-linux/>

  


-그리고

 **sudo /usr/local/mysql/bin/mysqld\_safe --skip-grant-tables  **

를 통해 잠시 동안 패스워드 없이 동작하도록 조정.  


  


-또 다른 터미널을 열어서 다음 명령어를 수행하여 접속한다.

**sudo /usr/local/mysql/bin/mysql -u root**

**  
**

-그리고 비밀번호 변경  


**UPDATE mysql.user SET password=PASSWORD(여기에 새로운 비밀번호 입력 괄호 포함) WHERE user='root';**

**  
**

**  
**

**password 칼럼이 없다고 뜬다.**

  


  


-아이러니 하게도 버전에 따라 password 칼럼이 존재하지 않는 경우가 있다.

따라서 새로운 해결 방법이 필요하다.

  


-우선 mysql에 접속하여

**use mysql;**  


명령어를 통해 데이터베이스를 선택한 후 다음 명령어를 실행한다.

  


**UPDATE user set authentication\_string=password(새로운 비밀번호 입력) WHERE user='root';**  


**  
**

**  
**

