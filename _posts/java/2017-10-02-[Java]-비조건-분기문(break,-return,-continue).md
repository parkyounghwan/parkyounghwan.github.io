---
layout: post
title:  "[Java]-비조건-분기문(break,-return,-continue)"
date:   2017-10-02 
categories: Java
comments: false
---
[네이버 백과]

  


*분기문

- **절차 분기문**(procedure branching statement)

원시 프로그램 중에 쓰여진 순서에 따르지 않고 다음의 실행문이 아닌 다른 문에 제어의 명시적인 이행을 일으키는 문.

  


- **무조건 분기문**(unconditional branch statement)

프로그램의 순차적 수행 순서에서 이탈하여 지정된 곳으로 무조건 분기를 지시하는 문장.

  


  


  


  


[위키]

-**조건 분기문 **

구문의 덩어리르 어떤 조건이 만족하는 경우에만 실행하게 할 수 있다. 그렇지 않으면, 그 구문의 덩어리를 실행하지 않고 그 다음부터 실행한다. => 조건문

  


-**비조건 분기문**

실행 순서를 프로그램의 다른 부분으로 옮기는 것이다. 여러 언어에서 제공하는 GOTO문, 서브프로그램, 프로시저, 호출문들이 비조건 분기분이다.

  


  


＃종합해 보면 **분기문**이라는 말이 우리가 알고 있는 조건문, 반복문을 통칭하는 의미 인것 같고, 내가 알고 싶은 '반복문을 탈출(?) 하는 방법'은 **비조건 분기문 **이라는 용어가 적합해 보인다.

  


  


  


  


[Oracle - Java documentation]  


**Branching Statements**

**  
**

**-**The *break *Statement

The break statement has two forms: labeled and unlabeled. (뭐 break문에 두 가지 폼이 있다는 것 같다.)

뒤에 해석을 덧붙이자면 언라벨드(라벨=명명) 형식은 *switch*나 *for, while, do-while *에서 쓰는 거랑 같다.

  


![](https://t1.daumcdn.net/cfile/tistory/9908EF3359D1D62A02)

* Oracle - java documentation의 코드를 가져왔다.

* 배열에서 원하는 값을 찾아내는 간단한 코드이다.

  


  


  


  


  


  


  


  


  


* for문 안에 if문이 있고 우리의 *break* 가 보인다.

* searchfor에 해당하는 값을 찾으면 for문을 종료한다.

* 알다시피이며 새로울게 없당.

  


  


  


  


  


  


  


  


  


  


  


문제는 라벨드된 놈인데, 코드 한번 보자.

(이건 이차원 배열에서 원하는 값을 찾는거다. 위랑 비슷해서 탐색하는 부분만 가져왔다.)

![](https://t1.daumcdn.net/cfile/tistory/9982DF3359D1D7B908)

  


  


* 이 줄의 위풍당당한 *search: *가 보이는가?

  


  


  


  


* ***break search; ***

** *이게 라벨드다(Labeled)

  


  


  


  


  


  


  


  


아래 Oracle -java documention 의 설명이다.

![](https://t1.daumcdn.net/cfile/tistory/9911D33359D1D8E81C)

  


안보이는데 걍 *break *만나면 for문 끝난다는 뜻이다.

  


※결론 쓰든 안쓰든 for문 끝남, 전달해주는 값 없고, for문 끝나면 for문 다음 명령어 수행.

*근데 라벨드는 쓰임을 좀 더 확인해 볼만은 하다.  


  


  


  


*이 부분은 넘겨도 된다. 걍 내가 새롭게 알게된 사실이다.

![](https://t1.daumcdn.net/cfile/tistory/990EC33359D1E10F24)![](https://t1.daumcdn.net/cfile/tistory/9985C23359D1E1A41B)

  


  


*for문은 조건문을 무조건 다 돈다.

*라벨해 놓아도 순차가 남아있으면 for문 돈다.

  


  


  


  


**-**The *continue *Statement

![](https://t1.daumcdn.net/cfile/tistory/99D32B3359D1E56F06)

(반복문을 스킵한다)  


  


![](https://t1.daumcdn.net/cfile/tistory/99FE563359D1E72E04)

  


  


  


  


  


  


* 좀 추상적인데 코드를 보면 문자열을 검색하다가 p가 아니면 for문 안의 *continue *밑의 명령어를 생략한다는 뜻이다.

  


  


*즉 p를 만나면 numPs++를 실행한다는 뜻.

  


  


*결과: Found 9 p's in the string.

  


  


*이 친구도 라벨드가 있다.(다음에 설명한다 머리아프다)

  


  


  


-The *result *Statement

https://docs.oracle.com/javase/tutorial/java/nutsandbolts/branch.html

