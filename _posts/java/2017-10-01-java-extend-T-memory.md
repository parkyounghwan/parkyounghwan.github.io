---
layout: post
title:  "상속과 T 메모리"
date:   2017-10-01 
categories: Java
comments: false
---
**1. 하위 클래스의 인스턴스가 생성될 때 상위 클래스의 인스턴스도 함께 생성된다.**

- 하위 클래스형 객체 참조 변수를 생성해도 상위 클래스의 인스턴스(속성, 메소드)도 생긴다.  


  


* 클래스 다이어그램으로 상속 구조를 표현

  
 ⓒ inhertance03.Animal 

   ⊙ name: String

   ● showName(): void

  

 ⓒ inhertance03.Animal 

 ⊙ name: String

 ● showName(): void

 ↑  


 ⓒ inhertance03.Penguin

 ⊙ habitat: String

 ● showHabitat(): void

  


*Driver 클래스(main이 작동하는 클래스를 Driver 클래스라고 부른다.)

![](https://t1.daumcdn.net/cfile/tistory/995B463359D0C8D327)

- **pororo** 객체를 생성하면 메모리에 Animal 클래스의 인스턴스도 생성된다.

  


* T메모리 (Static, Stack, Heap)

Static

 java.lang / Animal(name: String | showName(): void) / Penguin(habitat: String | showHabitat() :void)

   Stack

Heap  main() 스텍 프레임( pororo □ | args □ ) 

  **→** :Penguin(habitat : null | showHabitat()) / :Animal(name : null | showName())



Static

 java.lang / Animal(name: String | showName(): void) / Penguin(habitat: String | showHabitat() :void)

 Stack

 main() 스텍 프레임( pororo □ | args □ ) 

 **→** :Penguin(habitat : null | showHabitat()) / :Animal(name : null | showName())

**- pororo 객체가 가리키는 대상은 Penguin 이다. "근데 Animal도 생긴다." 가 하고 싶은 말이다.**

  


  


* Animal 형 객체 참조 변수, **pingo**를 생성했다.

![](https://t1.daumcdn.net/cfile/tistory/99864D3359D0CF6732)

  


**- 상위 클래스(Animal) 타입의 객체 참조 변수를 사용하여 하위 클래스(Penguin)의 생성자로 초기화 한다.**

**  
**Stack

 Heap 

  pingo 

  :Penguin(habitat : null | showHabitat()) / → :Animal(name : null | showName())

  

Stack

Heap 

pingo 

 :Penguin(habitat : null | showHabitat()) / → :Animal(name : null | showName())

- pingo가 가리키는 건 Animal

  


