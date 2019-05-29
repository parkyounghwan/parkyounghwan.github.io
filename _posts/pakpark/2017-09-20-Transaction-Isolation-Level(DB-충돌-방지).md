---
layout: post
title:  "Transaction-Isolation-Level(DB-충돌-방지)"
date:   2017-09-20 
categories: pakpark
comments: false
---
*

수강 신청 프로그램 작성시 SELECT를 30명에 한해서 진행하고 INSERT를 하게 한다.

많은 접속 인원이 동시에 진행할 경우 30명을 초과하는 경우가 발생한다.

와이?

*

  


SELECT와 INSERT 실행 사이에 들어오는 사용자가 있을 수 있기 때문에

  


REPEATABLE READ : TRANSCATION이 수행 되는 동안 읽기를 막는다.

SERIALIZABLE : TRANSACTION 수행 동안 미래에 발생할 INSERT 또한 막는다.

  


**LOCK (공유 데이터 보호)**

-읽기 락 vs 쓰기 락

  


1. 범위

 

1) 읽기 락

  


2) 쓰기 락 

쓰기 락 진행 중에는 읽기 락 거부, 대기 상태

  


  


-Read Uncommitted

읽기 락을 전혀 하지 않으며, 빠르다.

  


-Dirty read

쓰기 락이 걸려 있는 데이터도 읽을 수 있다.

  


-Non-repeatable read

트렌젝션 도중, 읽기 락이 풀려있어 변동이 있을 수 있다.

  


###시작

첫번째 조회 : 3

진행 중~

두번째 조회 : 4 //두번째 읽었을 때 달라져 있을 수 있다.

###종료

  


-Repeatable Read

내가 읽는 것을 다른 놈들이 못 건든다.

  


ex. 은행 잔액, 은행 거래 시

  


###Transaction

if( 잔액 > 10만원) {

~ // 이 부분에서 끼어드는 것을 방지한다.

 잔액 = 잔액 - 10만원;

}

  


*한계

내가 한번 읽은 것에 대한 락이 걸린다. 아직 읽지 않은 것에 대해서는 락이 걸리지 않는다.

  


ex. 수강 신청

if( count < 30 ) { //record(count)가 계속 바뀌는데 내가 읽은 count에 대해서만 락이 걸리므로 count 변경 되는 타이밍에 개입이 가능해짐.

insert 수강;

}

  


해결 = 락 범위를 넓힌다.

  


